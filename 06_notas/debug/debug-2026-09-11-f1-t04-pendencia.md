# Debug Summary — F1-T04 — 2026-09-11

- **Sintoma inicial:** criação sintética retornou `pendencia_validacao: cannot be blank`; nenhum lançamento foi persistido.
- **Causa raiz confirmada:** o campo booleano `pendencia_validacao` foi criado como obrigatório; no PocketBase, o valor normal `false` foi tratado como blank.
- **Correção aplicada:** migration reversível `0002_fix_pendencia_validacao.js` tornou o campo opcional; a validação server-side continua exigindo booleano.
- **Evidência da primeira correção:** versão Skip 0.0.6; QA oficial passou em setup, análise estática, build, integrações e testes.
- **Regressão comprovada no preview:** autenticação; criação de Aporte; total válido; repetição com recibo idempotente; Saída com pendência de validação fora do total.
- **Submissão append-only:** o formulário nativo estava válido; a reprodução direta do submit acionou `POST /backend/v1/lancamentos/y8qisnzjjaqnte3/corrigir` com HTTP 200 e atualizou a lista. A causa da ausência anterior no log foi o método de clique automatizado não disparar o submit React, não uma falha do endpoint.
- **Histórico comprovado:** painel exibiu `Criacao` em 2026-09-11 19:10:57 e `Correcao` em 2026-09-11 19:17:01, ambos com ator e correlação; o evento de correção preservou `antes.descricao = Fixture aporte F1-T04` e `depois.descricao = Fixture aporte F1-T04 corrigido`.
- **Estado:** correção automática passou; F1-T04 aguarda teste humano da Daniela.
