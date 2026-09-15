# Estado atual — Adapta Cliente

- task_id: F1-T08
- champion: Daniela
- spec: 04_fase-atual/specs/spec-1-004-periodo-baseline.md
- etapa: em_correcao
- autorizacao_implementacao: confirmada em 2026-09-15T14:57:00-03:00 — “Sim, implementar F1-T08 conforme este plano”
- teste_humano: pendente
- verificacao_automatica: falhou — versão 0.0.17 passou QA; smoke encontrou histórico HTTP 400 por referência inexistente e reprocessamento HTTP 400 por helper de spread incompatível; correção aplicada no código; versões 0.0.18/0.0.19 tiveram timeout de estabilidade do backend durante deploy; versão 0.0.18 respondeu histórico HTTP 200 após recuperação, mas reprocessamento ainda exigia nova observação de deploy
- aprendizado: capturado:06_notas/aprendizado-continuo/AP-2026-09-15-1315-separar-cobrancas-independentes.md
- ultima_acao: nova tentativa de deploy 0.0.19 para forçar atualização do hook de reprocessamento; integração falhou por HTTP 502 transitório no hook corte_gate_probe
- proxima_acao: aguardar recuperação do backend, confirmar que o hook corrigido está ativo e repetir reprocessamento idempotente, histórico e limpeza
- atualizado_em: 2026-09-15T15:02:00-03:00
