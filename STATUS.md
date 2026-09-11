# STATUS — Telecuidar / MAX Soluções

- **Fase:** 1 — núcleo financeiro e rastreabilidade.
- **Progresso:** 5/8 tasks concluídas (62,5%).
- **Task ativa:** F1-T06 — vincular documentos com deduplicação, pendência e recuperação.
- **Situação:** análise concluída; decisões da fixture e do destino registradas; aguardando autorização explícita para implementar.
- **Champion:** Daniela.
- **Pré-condições confirmadas:** F1-T04 concluída; F1-T05 concluída; B-106 fechado; nenhum dado real ingerido.
- **Decisões da prova:** fixture sintética será interna no Skip, sem criar arquivo na pasta `TESTE`; o vínculo apontará para um novo lançamento sintético.
- **Baseline Skip:** versão 0.0.6; coleções `lancamentos` e `lancamento_eventos`; migrations 0001/0002 aplicadas; apenas `.skip.config.json` pendente; sem segredo de Drive.
- **Baseline da aplicação:** UI e API server-side cobrem autenticação, criação/listagem/correção/histórico de lançamentos; não existe coleção, endpoint ou tela de candidatos documentais/vínculos.
- **Plano fechado:** adaptador server-side restrito; coleção de candidatos/vínculos com `source_id`, `source_ref`, `fingerprint`, `observed_at` e status; confirmação humana explícita; pendência com motivo; idempotência por fingerprint; três reprocessamentos; falha/timeout/revogação em modo manual; rollback sem tocar no Drive; UI acessível para revisar candidatos.
- **Limites:** não ampliar allowlist; não ler conteúdo/OCR/IA; não confirmar automaticamente; não usar documento real; não marcar timeout/revogação como aprovados por inferência.
- **Próxima ação:** aguardar autorização explícita para implementar somente a F1-T06.
