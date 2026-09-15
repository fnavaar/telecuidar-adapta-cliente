# STATUS — Telecuidar / MAX Soluções

- **Fase:** 1 — núcleo financeiro e rastreabilidade.
- **Progresso:** 7/8 tasks concluídas (87,5%).
- **Task ativa:** F1-T08 — demonstrar o período, histórico e registrar baseline.
- **Situação:** implementação da F1-T08 concluída na versão Skip 0.0.20; aguardando teste humano da Champion. F1-T08 não está concluída e nenhuma task seguinte foi iniciada.
- **Champion:** Daniela.
- **F1-T07 concluída:** B-107 emendado, competência `2026-08`, fonte `08.AGOSTO`, fronteira `boletos e contas a pagar identificadas`; 4 itens independentes; Starlink R$339/fatura própria; Vivo R$99,99/fatura própria; Adapta pendente; Papel de Parede completo.
- **F1-T08 implementada:** painel de demonstração, histórico do período, correção/reprocessamento idempotente e registro de baseline medido/estimativa; migration `0006_periodo_historico_baseline` aplicada.
- **QA:** Skip 0.0.20 (`1211cfc`) passou em setup, análise estática, build, integrações e testes.
- **Revalidação automatizada:** histórico HTTP 200; resumo de 4 itens, 3 conferidos, 1 pendência e 3 lançamentos rastreáveis; correção com antes/depois; três reprocessamentos HTTP 200, cada um com zero novos itens e zero novos lançamentos; baseline `[ESTIMATIVA]` persistido e repetição idempotente.
- **Evidência:** `artifacts/f1-t08-evidencia.md`.
- **Fixture:** sintética, disponível no preview para validação humana; deve ser removida pelo botão `Rollback do recorte` após o teste.
- **Segurança:** nenhum PDF foi baixado ou aberto; nenhum dado real foi ingerido ou alterado; nenhum token, segredo ou credencial foi persistido.
- **Próxima ação:** Daniela deve testar o roteiro da F1-T08 no preview, confirmar o resultado e executar o rollback; não concluir a task sem esse aceite.
