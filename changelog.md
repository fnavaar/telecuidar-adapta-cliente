# Changelog

## 2026-09-23
- 2026-09-23 · Daniela · Task F2-T03 concluída: dashboard somente leitura no Skip 0.0.25 (`21a7adb`) aceito após teste humano “teste ok”; B-203/formato mínimo aceito; CA-2-007..011 revalidados independentemente; tabela, gráfico, explicação, proveniência, pendência fora do gráfico, erro/vazio e rollback limpo; evidência `artifacts/f2-t03-evidencia.md`; captura `artifacts/f2-t03-dashboard-prestacao.png`.
- 2026-09-23 · Daniela · Task F2-T02 concluída: consolidação somente leitura no Skip 0.0.24 (`32d9b9e`) aceita após teste humano “teste ok”; CA-2-001..006 revalidados independentemente, B-107 sintético conferido (R$2.383,99 em 3 lançamentos e 1 pendência), proveniência, drill-down, B-201/B-202, período vazio, reprocessamentos idempotentes e rollback limpo; evidência `artifacts/f2-t02-evidencia.md`.
- Ethos · F2-T02 implementada e verificada no Skip 0.0.24 (`32d9b9e`): rota autenticada e painel de consolidação somente leitura; CA-2-001..005 passaram com B-107 sintético (R$2.383,99 em 3 lançamentos, 1 pendência, proveniência e drill-down); correção/reprocessamento/rollback revalidados; período vazio sem zeros inventados; ambiente final limpo; aguarda teste humano.
- Ethos · ANÁLISE F2-T02 concluída: RED no preview confirmou ausência da consolidação; modelo F1/hook/telas inspecionados; plano de rota server-side e painel somente leitura sobre lançamentos atômicos, com proveniência, pendências e drill-down; lacunas de OFX, data efetiva e centro de custo não serão inventadas; Skip Cloud retornou 503 ao inventário de coleções/migrations; nenhum arquivo do Skip alterado; F2-T02 aguarda autorização explícita.
- Daniela · Task F2-T01 concluída: CA-2-006 aprovado; B-201 registrado como conciliação bancária via OFX (entradas = aportes, saídas = contas a pagar, alocação por centro de custo, saldo conforme banco) e B-202 como data efetiva do pagamento; teste humano “CORRETO”; revalidação independente passou; nenhum OFX, código, migration ou dado real processado.
- Daniela · Decisões B-201/B-202 recebidas no formulário da F2-T01: consolidação por conciliação bancária via OFX; entradas tratadas como aportes; saídas como contas a pagar; alocação por centro de custo; saldo conforme banco; regime temporal pela data efetiva do pagamento. Termo registrado em `06_notas/f2-t01-termo-insumos-b201-b202.md`; verificação documental passou; nenhum OFX, integração, código, migration ou dado real processado; F2-T01 aguarda teste humano.

## 2026-09-22
- Ethos · F2-T01 autorizada e executada até o gate de insumo: Anexo F, B-107 e fontes da Fase 1 foram inspecionados; B-201 continua sem fórmula aceita para consolidação/alocação por participante e classificação; B-202 continua sem regime temporal geral aceito entre competência e data de pagamento. DÚVIDA de requisito registrada; nenhum código, migration, ingestão ou alteração do Skip realizada; F2-T01 bloqueada e F2-T02..T05 permanecem bloqueadas.

## 2026-09-21
- Fase 1 encerrada com validação do consultor: check-fase-1 APROVADO (digest ativo `1ae1cd83a3753b3f03f6e2de52adbf9a21df3ba7e7a20fb2a26da1ebdcf4a27d`); F1 arquivada em `05_entregas/fase-1/` com README e closure manifest.
- Evoluções da F1 (EV-F1-01..09) decididas; delta-fase-2 aplicado às SPECs.
- Fase 2 liberada: SPEC-2-001 consolidação (CA-2-001..006), SPEC-2-002 dashboard (CA-2-007..011), SPEC-2-003 explicação rastreável/conferência (CA-2-012..015); tasks F2-T01..T05 lineares.
- Somente F2-T01 é elegível (insumos B-201/B-202 com a Champion); F2-T02..T05 bloqueadas por dependência.
- Manifesto do handoff atualizado para phase 2 com hashes das SPECs F2; nenhuma implementação ou dado real novo.
