# Estado atual — Adapta Cliente

- task_id: F1-T04
- task_anterior: F1-T03 concluída em 2026-09-11
- champion: Daniela
- spec: 04_fase-atual/specs/spec-1-002-modelo-lancamentos.md
- etapa: em_correcao
- autorizacao_implementacao: confirmada em 2026-09-11T18:58:00-03:00 — “sim”
- teste_humano: pendente — após correção automática, Daniela deverá testar aporte, saída, incompleto, correção e repetição no preview
- verificacao_automatica: falhou no smoke test — pipeline QA passou, migration aplicada e autenticação funcionou, mas criação sintética retornou `pendencia_validacao: cannot be blank` e nenhum lançamento foi persistido
- aprendizado: pendente
- ultima_acao: causa raiz identificada: campo booleano `pendencia_validacao` foi criado como obrigatório; PocketBase rejeita o valor normal `false` como blank
- proxima_acao: aplicar migration reversível 0002 para tornar `pendencia_validacao` opcional e repetir smoke test, RED, GREEN e REGRESSÃO
- atualizado_em: 2026-09-11T19:00:00-03:00
