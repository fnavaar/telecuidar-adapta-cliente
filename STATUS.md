# STATUS — Telecuidar / MAX Soluções

- **Fase:** 1 — núcleo financeiro e rastreabilidade.
- **Progresso:** 7/8 tasks concluídas (87,5%).
- **Task ativa:** F1-T08 — demonstrar o período, histórico e registrar baseline.
- **Situação:** debug da F1-T08 concluído na versão Skip 0.0.21; três fixtures legadas da F1-T04 foram removidas por allowlist; aguardando novo teste humano da Champion. F1-T08 não está concluída e nenhuma task seguinte foi iniciada.
- **Champion:** Daniela.
- **F1-T08:** painel de demonstração, histórico do período, correção/reprocessamento idempotente e baseline medido/estimativa; migration `0006_periodo_historico_baseline` aplicada.
- **Correção de ambiente:** rota autenticada `/backend/v1/lancamentos/limpar-fixtures-f1-t04`, com validação de ID, descrição, data, valor, referência e tipo; removeu exatamente 3 fixtures legadas e repetição foi idempotente.
- **QA:** Skip 0.0.21 (`027719e`) passou em setup, análise estática, build, integrações e testes.
- **Revalidação anterior preservada:** histórico HTTP 200; correção com antes/depois; três reprocessamentos HTTP 200 com zero novos itens/lançamentos; baseline `[ESTIMATIVA]` persistido e idempotente.
- **Evidência:** `artifacts/f1-t08-evidencia.md`; Debug Summary `06_notas/debug/debug-2026-09-15-f1-t08-fixtures-legadas.md`.
- **Segurança:** limpeza limitada às três fixtures sintéticas identificadas; nenhum dado real, PDF, token, segredo ou credencial foi acessado ou alterado.
- **Próxima ação:** Daniela deve testar novamente o preview e confirmar que os três lançamentos legados não aparecem mais, preservando os critérios da F1-T08; não concluir a task sem esse aceite.
