# STATUS — Telecuidar / MAX Soluções

- **Fase:** 1 — núcleo financeiro e rastreabilidade.
- **Progresso:** 3/8 tasks concluídas (37,5%).
- **Task ativa:** F1-T04 — construir e provar lançamentos controlados no Skip.
- **Situação:** análise concluída; aguardando esclarecimento de dúvida material antes da autorização de implementação.
- **Champion:** Daniela.
- **Pré-condições:** F1-T03 aceita; B-104 e B-105 fechados; B-108 confirmado no projeto Skip 57934.
- **Baseline Skip:** versão 0.0.4, preview disponível, produção não publicada, nenhuma migration registrada e somente coleção `users`; alteração pendente em `.skip.config.json` foi preservada e não tocada.
- **Baseline funcional:** preview atual ainda é a sonda F1-T02; os quatro cenários sintéticos passaram; não há formulário, lista, coleção financeira, persistência ou histórico de lançamentos.
- **DÚVIDA bloqueante F1-T04:** a SPEC exige associar participante e referência documental, e exercitar aporte e saída, mas os anexos aceitos não definem seus tipos, valores permitidos, forma de armazenamento nem o campo/enum que distingue aporte de saída. Não criar defaults ou inferências.
- **Escopo planejado após esclarecimento:** migration reversível; coleção/coleções mínimas derivadas somente das decisões aprovadas; validação server-side; trilha append-only para correção; idempotência por `Descrição + Data Vencimento`; UI mínima de formulário/lista; fixtures sintéticas; sem dashboard F2, integração Drive, dados reais ou publicação de produção.
- **Próxima ação:** esclarecer a DÚVIDA de requisito; depois, em nova mensagem, autorizar explicitamente a implementação do plano.
