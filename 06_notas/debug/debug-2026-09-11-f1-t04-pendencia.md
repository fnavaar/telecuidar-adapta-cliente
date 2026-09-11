# Debug Summary — F1-T04 — 2026-09-11

- **Sintoma inicial:** criação sintética retornou `pendencia_validacao: cannot be blank`; nenhum lançamento foi persistido.
- **Causa raiz confirmada:** o campo booleano `pendencia_validacao` foi criado como obrigatório; no PocketBase, o valor normal `false` foi tratado como blank.
- **Correção aplicada:** migration reversível `0002_fix_pendencia_validacao.js` tornou o campo opcional; a validação server-side continua exigindo booleano.
- **Evidência da correção:** versão Skip 0.0.6; QA oficial passou em setup, análise estática, build, integrações e testes.
- **Regressão comprovada no preview:** autenticação; criação de Aporte; total válido; repetição com recibo idempotente; Saída com pendência de validação fora do total.
- **Falha restante:** a submissão de correção append-only não produziu uma requisição observável ao endpoint `/backend/v1/lancamentos/{id}/corrigir`; CA-1-011 e histórico antes/depois permanecem abertos.
- **Estado:** F1-T04 permanece em correção; não está pronta para aceite humano nem conclusão.
