# Estado atual — Adapta Cliente

- task_id: F1-T08
- champion: Daniela
- spec: 04_fase-atual/specs/spec-1-004-periodo-baseline.md
- etapa: aguardando_teste_humano
- autorizacao_implementacao: confirmada em 2026-09-15T14:57:00-03:00 — “Sim, implementar F1-T08 conforme este plano”
- teste_humano: pendente — novo teste deve confirmar ausência das três fixtures legadas F1-T04 e preservar histórico, baseline, reprocessamento e rollback do B-107
- verificacao_automatica: passou — QA Skip 0.0.21 (`027719e`) completo; limpeza allowlisted removeu exatamente 3 IDs legados F1-T04; segunda chamada idempotente; B-107 sem resíduos
- aprendizado: capturado:06_notas/aprendizado-continuo/AP-2026-09-15-1537-isolar-fixtures-por-task.md
- ultima_acao: debug concluído; causa confirmada como fixtures legadas F1-T04 sem rotina própria de limpeza; correção restrita implementada e verificada
- proxima_acao: novo teste humano de Daniela no preview e confirmação explícita do resultado
- atualizado_em: 2026-09-15T15:37:07-03:00
