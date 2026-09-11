# STATUS — Telecuidar / MAX Soluções

- **Fase:** 1 — núcleo financeiro e rastreabilidade.
- **Progresso:** 5/8 tasks concluídas (62,5%).
- **Task ativa:** F1-T06 — vincular documentos com deduplicação, pendência e recuperação.
- **Situação:** análise concluída; implementação bloqueada por dúvida de requisito. A pasta `TESTE` está vazia e não deve ser alterada.
- **Champion:** Daniela.
- **Pré-condições confirmadas:** F1-T04 concluída; F1-T05 concluída; B-106 fechado; nenhum dado real ingerido.
- **Baseline Skip:** versão 0.0.6; coleções `lancamentos` e `lancamento_eventos`; migrations 0001/0002 aplicadas; apenas `.skip.config.json` pendente; sem segredo de Drive.
- **Baseline da aplicação:** UI e API server-side cobrem autenticação, criação/listagem/correção/histórico de lançamentos; não existe coleção, endpoint ou tela de candidatos documentais/vínculos.
- **DÚVIDA bloqueante:** a SPEC exige fixture sintética na prova, mas não define se ela deve ser apenas um candidato interno, se deve ser vinculada a um lançamento sintético novo ou a um lançamento já existente. Não criar arquivo em `TESTE`, não usar documento real e não escolher silenciosamente.
- **Plano proposto após decisão:** adaptador server-side restrito; coleção de candidatos/vínculos com `source_id`, `source_ref`, `fingerprint`, `observed_at` e status; confirmação humana explícita; pendência com motivo; idempotência por fingerprint; três reprocessamentos; falha/timeout/revogação em modo manual; rollback sem tocar no Drive; UI acessível para revisar candidatos.
- **Riscos:** não ampliar allowlist; não ler conteúdo/OCR/IA; não confirmar automaticamente; não alterar o contrato dos lançamentos sem definir o destino do vínculo; não marcar timeout/revogação como aprovados por inferência.
- **Próxima ação:** cliente definir a fixture sintética e o destino do vínculo; depois a task volta a `aguardando_autorizacao` para autorização explícita da implementação.
