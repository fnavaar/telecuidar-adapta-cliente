# SPEC-1-004 — Primeiro período controlado, histórico e baseline

**Fase:** 1  
**Status:** bloqueada por SPEC-1-002 e SPEC-1-003  
**Dono:** Champion Daniela + Consultor; apoio Ethos  
**Origem:** RQ-08; DH-05; G-05  
**Degrau:** reuso das entregas F1 + roteiro operacional — fecha o valor da fase sem criar dashboard F2.

## Contexto e decisões fechadas

O valor da F1 não é levantamento: é um período controlado demonstrável. O baseline mede o processo atual; não cria meta. A planilha continua como referência de conferência durante a F1.

**Bloqueios:** SPEC-1-002/003 aceitas; B-103 política; B-105 regras; B-107 período e fronteira escolhidos pela Champion.

## Resultado observável

A Champion demonstra no preview um período escolhido: aportes, saídas, participantes, referências, pendências e histórico de correção. A conferência com a planilha é registrada item a item e o baseline de tempo/esforço é documentado com fonte medida ou `[ESTIMATIVA]`.

## Limites e dependências

- **Inclui:** escolher fronteira, registrar amostra controlada, conferir, tratar pendências, demonstrar e medir baseline.
- **Fora:** migração integral, descomissionar planilha, dashboard/gráficos, meta/alvo e multi-período.
- **Dados:** somente o recorte aprovado no B-107 e sob a política.
- **Rollback:** lote reversível com histórico; anexos append-only.

## Regras

| Regra | Condição | Resultado |
|---|---|---|
| RN-130 | sem documento/participante | pendência explícita |
| RN-131 | divergência sistema×planilha | pendência + causa investigada, sem ajuste silencioso |
| RN-132 | baseline não medido | `[ESTIMATIVA]`, nunca métrica medida |
| RN-133 | período parcial | rotular parcial; não declarar completo |

## Fluxo e recuperação

1. Champion define período, fontes e fronteira.
2. Registrar lançamentos via sistema/integração.
3. Conferir item a item contra a planilha e regras aprovadas.
4. Resolver ou manter pendências visíveis.
5. Exercitar uma correção e reprocessamento.
6. Champion demonstra o roteiro.
7. Registrar baseline e aceite da Fase 1.

| Cenário | Esperado | Recuperação |
|---|---|---|
| Completo | período demonstrado e conferido | — |
| Documento ausente | pendência fora dos totais | obter/vincular depois |
| Divergência | causa registrada | emenda se regra errada |

## Critérios de aceite

- [ ] **CA-1-019:** período, fontes e fronteira estão registrados e aceitos antes do primeiro dado.
- [ ] **CA-1-020:** todos os itens do recorte têm lançamento rastreável ou pendência nomeada.
- [ ] **CA-1-021:** pendências ficam fora dos totais válidos e visíveis na demonstração.
- [ ] **CA-1-022:** conferência sistema×planilha existe item a item; divergências têm causa/estado.
- [ ] **CA-1-023:** uma correção e um reprocessamento preservam histórico e não duplicam.
- [ ] **CA-1-024:** Champion demonstra o período e baseline de tempo/esforço é registrado, medido ou `[ESTIMATIVA]`, sem meta inventada.

## TDD da SPEC

| Etapa | Prova | Ação | Esperado | Evidência |
|---|---|---|---|---|
| RED | B-107 aberto | tentar registrar lançamento fora do período/fronteira | recusa registrada | log da tentativa + estado de B-107 |
| GREEN | recorte registrado | conferir/demonstrar | CA-019..022 | planilha de conferência/capturas |
| REGRESSÃO | corrigir e reprocessar | repetir fluxo | CA-023/024 | trilha + baseline |

**Fixtures:** recorte sintético do B-107 (1 lançamento completo, 1 sem documento, 1 divergente da planilha); dado real somente após aceite de CA-1-019.

**Ponto de parada:** aceite humano da F1; não iniciar F2 sem `liberar-fase`.

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
| F1-T07 | Definir e conferir o primeiro período controlado | Champion + Consultor | SPEC-1-004 | CA-1-019..022 | RED fora de B-107 + GREEN recorte registrado e conferido item a item | Registro B-107, planilha de conferência, pendências e capturas | F1-T04/F1-T06 aceitas; B-103/B-105/B-107 | BLOQUEADA por F1-T04/F1-T06/B-107 |
| F1-T08 | Demonstrar o período, histórico e registrar baseline | Champion + Consultor | SPEC-1-004 | CA-1-023..024 | REGRESSÃO correção/reprocessamento + demonstração humana e baseline | Trilha antes/depois, prova sem duplicidade, roteiro gravado/ata e Anexo de baseline | F1-T07 aceita | BLOQUEADA por F1-T07 |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
