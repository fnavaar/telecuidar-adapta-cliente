# Changelog

## 2026-09-23
- Daniela · Task F2-T01 concluída: CA-2-006 aprovado; B-201 registrado como conciliação bancária via OFX (entradas = aportes, saídas = contas a pagar, alocação por centro de custo, saldo conforme banco) e B-202 como data efetiva do pagamento; teste humano “CORRETO”; revalidação independente passou; nenhum OFX, código, migration ou dado real processado. F2-T02 é a próxima task elegível, ainda não iniciada.
- Daniela · Decisões B-201/B-202 recebidas no formulário da F2-T01: consolidação por conciliação bancária via OFX; entradas tratadas como aportes; saídas como contas a pagar; alocação por centro de custo; saldo conforme banco; regime temporal pela data efetiva do pagamento. Termo registrado em `06_notas/f2-t01-termo-insumos-b201-b202.md`; verificação documental passou; nenhum OFX, integração, código, migration ou dado real processado; F2-T01 aguarda teste humano.

## 2026-09-22
- Ethos · F2-T01 autorizada e executada até o gate de insumo: Anexo F, B-107 e fontes da Fase 1 foram inspecionados; B-201 continua sem fórmula aceita para consolidação/alocação por participante e classificação; B-202 continua sem regime temporal geral aceito entre competência e data de pagamento. DÚVIDA de requisito registrada; nenhum código, migration, ingestão ou alteração do Skip realizada; F2-T01 bloqueada e F2-T02..T05 permanecem bloqueadas.

## 2026-09-21
- Fase 1 encerrada com validação do consultor: check-fase-1 APROVADO (digest ativo `1ae1cd83a3753b3f03f6e2de52adbf9a21df3ba7e7a20fb2a26da1ebdcf4a27d`); F1 arquivada em `05_entregas/fase-1/` com README e closure manifest.
- Evoluções da F1 (EV-F1-01..09) decididas; delta-fase-2 aplicado às SPECs.
- Fase 2 liberada: SPEC-2-001 consolidação (CA-2-001..006), SPEC-2-002 dashboard (CA-2-007..011), SPEC-2-003 explicação rastreável/conferência (CA-2-012..015); tasks F2-T01..T05 lineares.
- Somente F2-T01 é elegível (insumos B-201/B-202 com a Champion); F2-T02..T05 bloqueadas por dependência.
- Manifesto do handoff atualizado para phase 2 com hashes das SPECs F2; nenhuma implementação ou dado real novo.
