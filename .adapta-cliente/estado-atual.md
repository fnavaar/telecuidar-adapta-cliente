# Estado atual — Adapta Cliente

- task_id: F1-T02
- task_anterior: F1-T01 concluída documentalmente em 2026-09-11
- champion: Daniela
- spec: 04_fase-atual/specs/spec-1-001-fontes-politica-allowlist.md
- etapa: em_correcao
- autorizacao_execucao: confirmada em 2026-09-11T17:12:00-03:00 — “pode”
- teste_humano_F1_T01: aprovado pela Champion em 2026-09-11T17:00:00-03:00 — “tudo correto, testado e aprovado”; correção e liberação confirmadas pelo Consultor às 16:57
- verificacao_F1_T01: aprovada — anexos A–E versionados; CA-1-001..005 demonstrados; B-101/B-102/B-103 fechados; P-1-001..003 preservadas; P-1-004/P-1-005 constam fechadas no Anexo E; zero ingestão e zero descarte
- verificacao_baseline_F1_T02: passou somente leitura — projeto Skip 57934 running, preview era template inicial; nenhuma migration e nenhuma coleção financeira antes da execução; somente coleção auth `users`; nenhum arquivo de aplicação para gate ou integração existente
- plano_F1_T02: provar CA-1-006 com RED (tentativa de avanço com política/allowlist ausente ou fora da allowlist recusada), GREEN (estado/export/log sanitizado comprova B-101..103 fechados e zero ingestão), regressão (repetir tentativa e confirmar que migrations/coleções/dados permanecem ausentes); criar apenas evidência documental/log sanitizado, sem migration, modelo, integração, dado real ou alteração da planilha/pasta
- riscos_F1_T02: não confundir inspeção de estado com ingestão; não testar com dados reais; não registrar segredos; cobertura parcial se o mecanismo de gate ainda não existir no runtime
- autorizacao_implementacao: confirmada em 2026-09-11T17:12:00-03:00 — “pode”
- teste_humano: pendente — preview ainda não expunha a sonda; nova UI de teste será disponibilizada antes do teste humano
- verificacao_automatica: passou parcialmente — hook QA e rota backend passaram; falta verificar a UI do preview chamando a rota real
- aprendizado: capturado:06_notas/aprendizado-continuo/AP-2026-09-11-1717-gate-runtime-ausente.md
- ultima_acao: diagnóstico do pedido do cliente; confirmado que o preview permanecia no template inicial e não expunha a rota server-side
- proxima_acao: criar painel de teste sintético no preview e verificar a chamada real ao backend
- atualizado_em: 2026-09-11T17:59:00-03:00
