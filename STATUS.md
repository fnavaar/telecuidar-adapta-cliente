# STATUS — Telecuidar / MAX Soluções

- **Fase:** 1 — núcleo financeiro e rastreabilidade.
- **Progresso:** 3/8 tasks concluídas (37,5%).
- **Task ativa:** F1-T04 — construir e provar lançamentos controlados no Skip.
- **Situação:** em correção; criação, idempotência e pendência de validação passaram; correção append-only ainda não comprovada.
- **Champion:** Daniela.
- **Implementação Skip:** versão 0.0.6; QA oficial passou em setup, análise estática, build, integrações e testes; migrations `0001_create_lancamentos` e `0002_fix_pendencia_validacao` aplicadas; coleções `lancamentos` e `lancamento_eventos` existentes.
- **Smoke test sintético:** conta criada; Aporte criado e incluído no total; repetição retornou recibo idempotente sem duplicar; Saída com pendência de validação ficou visível e fora do total válido.
- **Falha aberta:** a submissão de correção append-only ainda não gerou requisição observável em `/backend/v1/lancamentos/{id}/corrigir`; CA-1-011 e histórico antes/depois permanecem não verificados.
- **Causa corrigida:** `pendencia_validacao` booleano obrigatório rejeitava `false` como blank no PocketBase; migration 0002 tornou o campo opcional, mantendo a validação server-side.
- **Segurança:** somente fixtures sintéticas foram usadas; nenhum dado real, documento do Drive, segredo ou produção foi publicado; alteração preexistente em `.skip.config.json` foi preservada.
- **Próxima ação:** continuar o debug exclusivo da correção append-only; não concluir a task nem iniciar outra.
