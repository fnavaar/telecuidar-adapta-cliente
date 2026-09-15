# AP-2026-09-15-1537 — Isolar fixtures sintéticas entre tasks

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: F1-T08 / SPEC-1-004
- Sinal: o rollback do B-107 removeu corretamente o lote atual, mas três lançamentos sintéticos antigos da F1-T04 permaneceram na lista porque não pertenciam ao período controlado.
- Evidência: `06_notas/debug/debug-2026-09-15-f1-t08-fixtures-legadas.md`; rota `limpar-fixtures-f1-t04`; smoke HTTP 200 removeu exatamente três IDs em allowlist e segunda chamada foi idempotente.
- Regra reutilizável: toda fixture sintética deve ter identificação persistente de task/lote e rotina de limpeza própria; rollback de um lote nunca deve inferir ou remover fixtures de outra task.
- Quando aplicar: ao criar testes sintéticos persistentes em ambiente compartilhado entre tasks.
- Quando não aplicar: para dados reais ou registros cuja origem não esteja confirmada por identificadores e metadados; nesses casos, bloquear a remoção.
- Confiança: alta — causa reproduzida, allowlist validada e limpeza reexecutada sem tocar registros fora do recorte.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
