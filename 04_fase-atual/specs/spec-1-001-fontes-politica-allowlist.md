# SPEC-1-001 — Corte operacional, fontes, política e allowlist

**Fase:** 1  
**Status:** planejada  
**Dono:** Champion Daniela + Consultor  
**Origem:** RQ-01, RQ-03; RQ-09 como requisito transversal de nomenclatura/recorte; G-01/G-03  
**Degrau da solução:** contrato documental versionado — os insumos pertencem ao cliente e precisam ser recebidos antes da construção com dados reais.

## Contexto e decisões fechadas

- A planilha dinâmica da Champion é a fonte do modelo atual, mas ainda não foi anexada.
- A pasta financeira pertence ao cliente; a pasta específica ainda precisa ser registrada.
- A Champion definirá a política antes de qualquer ingestão real.
- **B-101:** planilha/amostra; **B-102:** allowlist; **B-103:** política. Nenhum bloqueia iniciar F1-T01, mas todos bloqueiam seu aceite e as tasks posteriores.

## Resultado observável

Um pacote de corte aceito pela Champion contendo: planilha e amostra com hash; inventário observável de abas/colunas/tipos sem inferência; ID/URL da pasta allowlist; política de dados; pendências nomeadas. Esse pacote destrava a construção sem ser confundido com o sistema final da Fase 1.

## Limites e dependências

- **Inclui:** solicitar, receber, validar, hashear, inventariar e obter aceite.
- **Fora:** modelar banco, integrar Drive, migrar histórico ou ingerir dado no Skip.
- **Saídas:** `anexos/A-planilha.md`, `B-amostra.md`, `C-allowlist.md`, `D-politica.md`, `E-catalogo-observado.md`; o Anexo F é produzido e aceito na SPEC-1-002, passo 2, sob responsabilidade da Champion.
- **Atores/permissões:** cliente fornece; Champion define/aceita; Consultor registra. Sem acesso automatizado.
- **Risco/plano B:** insumo incompleto mantém bloqueio aberto; nunca substituir por suposição.
- **Rollback:** nova versão invalida a anterior com motivo; nada é apagado.

## Dados e regras

| Origem | Fonte de verdade | Contrato | Erro |
|---|---|---|---|
| Cliente → Anexo A | arquivo enviado | hash, data, abas/colunas observadas | ilegível: solicitar novamente |
| Cliente → Anexo B | amostra enviada | tipo, origem, data, representatividade | tipo ausente: lacuna nomeada |
| Champion → Anexo C | confirmação escrita | ID/URL, recorte dentro/fora | pasta incerta: B-102 aberto |
| Champion → Anexo D | política aprovada | acesso, armazenamento, retenção, descarte, autorização | cláusula ausente: B-103 aberto |

| Regra | Condição | Resultado |
|---|---|---|
| RN-101 | item não observável | marcar `[NÃO OBSERVÁVEL]` |
| RN-102 | divergência fonte×relato | pendência P-1-NNN |
| RN-103 | política ou allowlist ausente | zero ingestão real |

## Fluxo e recuperação

1. Solicitar os quatro insumos com lista exata.
2. Receber sem copiar conteúdo sensível para artefatos de consultoria.
3. Calcular hashes e inventariar apenas estrutura necessária.
4. Registrar allowlist e política nas palavras da Champion.
5. Marcar lacunas e obter aceite item a item.
6. Fechar B-101/B-102/B-103 somente após o aceite humano.

| Cenário | Resultado esperado | Recuperação |
|---|---|---|
| Completo | cinco anexos aceitos | — |
| Amostra parcial | lacunas explícitas | solicitar complemento |
| Pasta/política incerta | bloqueio permanece | escalar à Champion |

## Critérios de aceite

- [ ] **CA-1-001:** planilha e amostra têm hash, data, origem e aceite da Champion.
- [ ] **CA-1-002:** catálogo observado aponta aba/coluna/célula ou marca `[NÃO OBSERVÁVEL]`.
- [ ] **CA-1-003:** allowlist registra ID/URL e limites dentro/fora confirmados pela Champion.
- [ ] **CA-1-004:** política registra acesso, armazenamento, retenção, descarte e autorização para uso.
- [ ] **CA-1-005:** divergências e tipos ausentes estão em pendências P-1-NNN, sem suposição.
- [ ] **CA-1-006:** inspeção do Skip/SkipCloud comprova zero ingestão real antes do aceite; se a inspeção estiver indisponível, usar export/estado do projeto mais declaração técnica registrada, marcar cobertura parcial e manter B-103 aberto.

## TDD da SPEC

| Etapa | Prova | Ação | Esperado | Evidência |
|---|---|---|---|---|
| RED | bloqueios abertos | inspecionar anexos | faltas identificadas | registro B-101..103 |
| GREEN | pacote completo | validar e obter aceite | CA-001..005 passam | anexos + aceite |
| REGRESSÃO | tentativa de avançar incompleto | executar gate | recusa e zero ingestão | CA-006 + log |

**Fixtures:** somente arquivos fornecidos pelo cliente; nenhuma fixture substitui a fonte nesta SPEC.
**Ponto de parada:** pacote aceito; não iniciar modelagem na mesma task.

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
| F1-T01 | Solicitar, receber e validar o pacote de fontes da Telecuidar | Consultor + Champion | SPEC-1-001 | CA-1-001..005 | RED dos bloqueios B-101..103 + GREEN dos anexos A–E | Anexos A–E com hashes, pendências P-1-NNN e aceites da Champion | Checks aprovados; canal com Champion | CONCLUÍDA — 2026-09-11 |
| F1-T02 | Provar o gate de zero ingestão e selar o corte operacional | Ethos + Consultor | SPEC-1-001 | CA-1-006 | REGRESSÃO: tentativa de avanço incompleto é recusada | Inspeção/export do estado do projeto e log sanitizado do gate | F1-T01 aceita; B-108 disponível para inspeção ou cobertura parcial registrada | ELEGÍVEL — aguarda autorização explícita |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
