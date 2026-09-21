# SPEC-1-003 — Integração documental da pasta do cliente

**Fase:** 1  
**Status:** bloqueada por SPEC-1-001 e SPEC-1-002  
**Dono:** Ethos; autorização/validação da Champion  
**Origem:** RQ-01; G-03  
**Degrau:** mecanismo mínimo de leitura suportado pelo ambiente — escolhido somente após prova técnica; esta SPEC não presume API, OAuth ou conta de serviço específicos.

## Contexto e decisões fechadas

A pasta pertence ao cliente e é a entrada sistêmica. A F1 não captura correio/e-mail/WhatsApp, não edita arquivos e não usa IA para interpretar documentos.

**Bloqueios:** B-102 allowlist, B-103 política, B-106 mecanismo de acesso autorizado e provado no ambiente. Sem B-106, executar spike timeboxed com fixture sintética e parar; não conectar dado real.

## Resultado observável

Um documento autorizado na pasta registrada aparece como candidato no sistema; após confirmação humana, vincula-se a um lançamento com identificador e impressão digital; reprocessamento não duplica; ilegível vira pendência; falha do acesso mantém estado consistente.

## Limites e dependências

- **Inclui:** prova do mecanismo; leitura restrita; inventário incremental; impressão digital; vínculo após confirmação; dedupe; pendência; retry/fallback; rollback de lote.
- **Fora:** editar/mover arquivo, ampliar pasta, OCR/IA, captura dos canais e confirmação automática.
- **Permissão:** menor privilégio de leitura na pasta exata. Segredo, se houver, somente server-side/secret manager disponível.
- **Superfícies:** adaptador server-side, configuração secreta, coleções de referência e UI de candidatos.
- **Plano B:** registro manual idempotente com referência; reconciliação quando o acesso voltar.

## Contrato de integração

| Campo lógico | Origem | Uso |
|---|---|---|
| source_id | mecanismo autorizado | identidade externa |
| source_ref | pasta/arquivo | referência exibível sem segredo |
| fingerprint | bytes/metadados permitidos | idempotência |
| observed_at | sistema | auditoria |
| status | máquina de estados entregue e aprovada na prova B-106 antes do adaptador | candidato/pendência/vinculado/falha |

O mapeamento para campos reais do provedor é anexado após a prova B-106; o executor não escolhe silenciosamente.

| Regra | Condição | Resultado |
|---|---|---|
| RN-120 | fora da allowlist | acesso negado/não listado |
| RN-121 | fingerprint já processada | sem segundo lançamento |
| RN-122 | ilegível/incompleto | pendência com motivo |
| RN-123 | sem confirmação humana | nenhum lançamento válido |
| RN-124 | timeout/permissão revogada | falha registrada + modo manual |

## Fluxo e recuperação

1. Provar o mecanismo em ambiente de teste e registrar contrato/autorização. Antes de iniciar, registrar dono, janela de tempo e orçamento máximo do spike B-106; ao atingir qualquer limite sem prova, parar no modo manual idempotente.
2. Configurar menor privilégio e varrer segredos.
3. Listar somente a allowlist e criar candidatos.
4. Champion confirma ou marca pendência.
5. Reprocessar 3 vezes e comprovar idempotência.
6. Induzir timeout/revogação e exercer fallback/reconciliação.
7. Exercer rollback de lote sem tocar arquivos do cliente.

## Critérios de aceite

- [ ] **CA-1-013:** prova B-106 registra mecanismo, escopo, conta autorizadora, revogação e resultado; nenhuma capacidade é presumida.
- [ ] **CA-1-014:** item fora da allowlist não é listado nem processado.
- [ ] **CA-1-015:** documento confirmado vincula lançamento a source_id/source_ref/fingerprint.
- [ ] **CA-1-016:** três reprocessamentos produzem um único vínculo/lançamento.
- [ ] **CA-1-017:** ilegível/incompleto vira pendência com motivo, sem valor inventado.
- [ ] **CA-1-018:** timeout/revogação preserva confirmados, registra falha e reconcilia sem duplicidade.

## TDD da SPEC

| Etapa | Prova | Ação | Esperado | Evidência |
|---|---|---|---|---|
| RED | sem B-106 ou fora da allowlist | tentar listar com fixture sintética e credencial inválida | recusa/nenhum item listado | log sanitizado da tentativa |
| GREEN | candidato→confirmação→vínculo | fixture autorizada | CA-013..015 | captura/registro |
| REGRESSÃO | 3 reprocessamentos + falha | repetir/revogar/reconciliar | CA-016..018 | trilha |

**Fixtures:** sintéticas na prova; documento real só após política e autorização da task.
**Ponto de parada:** integração/fallback provados; nenhum arquivo do cliente alterado.

## Instruções de execução para o Ethos

1. **Ler antes de alterar:** escopo definitivo, matriz, esta SPEC e anexos/bloqueios citados.
2. **Alterar somente:** superfícies explicitamente incluídas nesta SPEC.
3. **Não alterar:** planilha original, outras fases, regras sem evidência, permissões ou conectores não aprovados.
4. **Executar nesta ordem:** pré-condições → RED → menor entrega GREEN → bordas/recuperação → REGRESSÃO → evidências.
5. **Parar e pedir validação quando:** surgir campo, fórmula, estado, permissão, acesso ou exceção não demonstrada.
6. **Estado válido ao parar:** nenhum dado real exposto, nenhuma regra inventada e bloqueios atualizados.

## Checklist de execução

- [ ] Pré-condições e bloqueios conferidos
- [ ] Caminhos principal, limite e falha exercitados
- [ ] Evidências anexadas
- [ ] Varredura de segredos e dados fora do recorte limpa
- [ ] Teste humano da Champion registrado

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| F1-T05 | Executar spike timeboxed do mecanismo de acesso à pasta | Ethos + Champion | SPEC-1-003 | CA-1-013..014 | RED sem B-106/fora allowlist + prova mínima no ambiente de teste | Contrato B-106 com dono/timebox/orçamento, log sanitizado e prova de recusa fora da allowlist | F1-T02 aceita; B-102/B-103/B-108; autorização da Champion | BLOQUEADA por F1-T02/B-102/B-103/B-108 |
| F1-T06 | Vincular documentos com deduplicação, pendência e recuperação | Ethos | SPEC-1-003 | CA-1-015..018 | GREEN candidato→vínculo + REGRESSÃO 3 reprocessamentos/timeout/reconciliação | Capturas, trilha, logs sanitizados, rollback de lote e teste humano | F1-T05 aceita; F1-T04 aceita; B-106 fechado | BLOQUEADA por F1-T04/F1-T05/B-106 |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
