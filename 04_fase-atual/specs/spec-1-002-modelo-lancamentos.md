# SPEC-1-002 — Modelo mínimo e lançamentos controlados

**Fase:** 1  
**Status:** bloqueada por SPEC-1-001  
**Dono:** Ethos; validação da Champion  
**Origem:** RQ-02/RQ-03; AC-002/AC-003; G-02  
**Degrau:** construção mínima no Skip/SkipCloud — stack decidida, modelo derivado somente dos anexos aceitos.

## Contexto e decisões fechadas

O sistema substitui a planilha como superfície operacional. Campos, classificações, estados e fórmulas não são definidos nesta SPEC em abstrato: entram por anexos versionados da SPEC-1-001 e por um contrato de regras aprovado pela Champion.

**Bloqueios:** B-101/102/103 fechados; **B-104 catálogo aprovado**; **B-105 regras financeiras com exemplos aprovados**, sob responsabilidade da Champion e com prazo/cadência registrados; **B-108 projeto Skip identificado, acessível e autorizado**. Sem B-104/B-108 não há migration/modelo; sem B-105 não há total ou saldo.

## Resultado observável

No preview, a Champion registra um aporte e uma saída controlados conforme o catálogo aprovado, associa participante e referência documental, deixa um caso incompleto como pendência e corrige um lançamento preservando histórico.

## Limites e dependências

- **Inclui:** catálogo versionado; participantes; lançamentos; validação; pendência; correção append-only; lista mínima do período.
- **Fora:** dashboard/gráficos F2, integração Drive (SPEC-1-003), diretores/RBAC F3, IA F4.
- **Dados:** primeiro usar fixtures estruturais sem conteúdo real; dados reais somente após B-103 e autorização da task.
- **Superfícies:** modelo/migrations, rotas server-side, formulários e lista no projeto Skip autorizado.
- **Rollback:** migration reversível; correção nunca apaga histórico.

## Contratos e regras

| Contrato | Fonte | Obrigação | Falha |
|---|---|---|---|
| Catálogo | Anexo E aceito | igualdade item a item | divergência bloqueia deploy |
| Regras | Anexo F aceito | exemplos de entrada→resultado | regra ausente bloqueia cálculo |
| Lançamento | catálogo | campos mínimos declarados pela Champion | ausente vira recusa/pendência conforme Anexo F |

| Regra | Condição | Resultado |
|---|---|---|
| RN-110 | campo obrigatório ausente | recusa ou pendência, exatamente conforme Anexo F |
| RN-111 | saída sem participante | não entra como válida |
| RN-112 | pendência | fora de totais válidos |
| RN-113 | correção | antes/depois, ator e horário append-only |
| RN-114 | comando repetido | mesma chave idempotente, sem duplicidade |

## Fluxo e erros

1. Validar anexos e gerar contrato executável do catálogo.
2. Formalizar Anexo F com exemplos reais e aceite.
3. Criar modelo e migrations reversíveis.
4. Criar rotas server-side e UI mínima.
5. Exercitar aporte, saída, incompleto, correção e repetição.
6. Champion testa no preview.

| Cenário | Esperado | Recuperação |
|---|---|---|
| Completo | lançamento válido e rastreável | — |
| Incompleto | pendência/recusa sem default inventado | completar fonte |
| Repetido | um registro | retornar recibo idempotente |
| Regra ausente | cálculo indisponível | manter B-105 |

## Critérios de aceite

- [ ] **CA-1-007:** modelo contém exatamente o catálogo aprovado, com diff automatizado limpo.
- [ ] **CA-1-008:** Anexo F contém regras e exemplos entrada→resultado aceitos pela Champion.
- [ ] **CA-1-009:** aporte e saída válidos são registrados com participante e referência.
- [ ] **CA-1-010:** incompleto nunca recebe default inventado e não entra em total válido.
- [ ] **CA-1-011:** correção preserva antes/depois, ator e horário sem update destrutivo.
- [ ] **CA-1-012:** repetição da mesma chave produz um registro e recibo idempotente.

## TDD da SPEC

| Etapa | Prova | Ação | Esperado | Evidência |
|---|---|---|---|---|
| RED | catálogo divergente; saída sem participante | testes de contrato/rota | falham | relatório RED |
| GREEN | aporte/saída completos | suíte + preview | CA-007, CA-009 e CA-010 passam; CA-008 é gate de insumo (Anexo F aceito), conferido antes do GREEN, não teste de suíte | logs/capturas |
| REGRESSÃO | correção e repetição | testes de histórico/idempotência | CA-011/012 passam | trilha/recibo |

**Fixtures:** geradas do esquema aprovado, anonimizadas; fixture real apenas após política.
**Ponto de parada:** UI mínima aceita; não construir dashboard F2.

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
| F1-T03 | Formalizar catálogo e regras financeiras com exemplos | Champion + Consultor | SPEC-1-002 | CA-1-007..008 | Diff catálogo×Anexo E + aceite do Anexo F | Relatório de diff, Anexo F, responsável/prazo e aceite da Champion | F1-T02 aceita; B-104; B-108; Champion disponível | BLOQUEADA por F1-T02/B-104/B-108 |
| F1-T04 | Construir e provar lançamentos controlados no Skip | Ethos | SPEC-1-002 | CA-1-009..012 | GREEN aporte/saída/incompleto + REGRESSÃO correção/idempotência | Testes executados, capturas do preview, trilha append-only e recibo idempotente | F1-T03 aceita; B-105 fechado; projeto Skip autorizado | BLOQUEADA por F1-T03/B-105 |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
