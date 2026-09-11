# STATUS — Telecuidar / MAX Soluções

- **Fase:** 1 — núcleo financeiro e rastreabilidade.
- **Progresso:** 3/8 tasks concluídas (37,5%).
- **Task ativa:** F1-T04 — construir e provar lançamentos controlados no Skip.
- **Situação:** análise concluída; decisões de modelagem registradas; aguardando autorização explícita de implementação.
- **Champion:** Daniela.
- **Pré-condições:** F1-T03 aceita; B-104 e B-105 fechados; B-108 confirmado no projeto Skip 57934.
- **Baseline Skip:** versão 0.0.4, preview disponível, produção não publicada, nenhuma migration registrada e somente coleção `users`; alteração pendente em `.skip.config.json` foi preservada e não tocada.
- **Baseline funcional:** preview atual ainda é a sonda F1-T02; os quatro cenários sintéticos passaram; não há formulário, lista, coleção financeira, persistência ou histórico de lançamentos.
- **Decisões F1-T04 registradas:** `Responsável Pagamento` será reutilizado como participante, com `Antonio Jorge`, `Francisco Figueiredo` e `Geraldo Tadeu`; `Referência Documental` será texto obrigatório, sem baixar ou integrar o Drive nesta task; `Tipo de Lançamento` será campo obrigatório com os valores `Aporte` e `Saída`.
- **Plano após autorização:** criar migration reversível para a coleção mínima derivada do catálogo aprovado e das decisões registradas; incluir os oito campos do catálogo, `Referência Documental` e `Tipo de Lançamento`, sem campo participante adicional; validar obrigatoriedade, domínios, ausência sem default, saída sem participante, pendência de validação distinta do status operacional, correção append-only e idempotência por `Descrição + Data Vencimento`; criar rotas server-side e UI mínima de formulário/lista; usar somente fixtures sintéticas; executar RED, GREEN e REGRESSÃO; não criar dashboard F2, integração Drive, dados reais ou publicação de produção.
- **Riscos a verificar durante a execução:** preservar a alteração pendente em `.skip.config.json`; não expor registros por regra de acesso inadequada; não confundir `Pendente` operacional com pendência de validação; não alterar a planilha original; não criar valor, fórmula ou domínio não aprovado.
- **Próxima ação:** aguardar autorização explícita para implementar a F1-T04.
