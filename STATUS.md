# STATUS — Telecuidar / MAX Soluções

- **Fase:** 1 — núcleo financeiro e rastreabilidade.
- **Progresso:** 6/8 tasks concluídas (75%).
- **Task ativa:** F1-T07 — definir e conferir o primeiro período controlado.
- **Situação:** B-107 recebido parcialmente; implementação bloqueada por conflito de amostra. Nenhuma metadata/listagem da nova pasta foi acessada.
- **Champion:** Daniela.
- **Decisões B-107 recebidas:** competência `2026-08`; fonte proposta = nova pasta Drive indicada pelo cliente, ID `1f03hUNACl6PENUI1NHV5p3YEv4opmLm6`; fronteira = boletos e contas a pagar identificadas; tratamento = destacar documentos que ficarão ausentes; amostra escolhida = 1 lançamento completo.
- **Emenda B-106 recebida:** incluir a nova pasta na allowlist, preservando escopo somente leitura, responsável Daniela, janela máxima de 30 minutos, orçamento R$ 0,00 e fallback manual idempotente. A emenda ainda não foi exercitada por metadata/listagem.
- **Conflito bloqueante:** SPEC-1-004 define fixture/recorte com 3 cenários — 1 completo, 1 sem documento e 1 divergente da planilha —, mas a decisão recebida seleciona apenas 1 lançamento completo. Não alterar a SPEC nem escolher silenciosamente.
- **Regras preservadas:** sem documento/participante = pendência; divergência sistema×planilha = pendência com causa; baseline não medido = `[ESTIMATIVA]`; período parcial rotulado parcial; planilha continua referência de conferência; nenhum dado real ingerido.
- **Segurança:** a nova pasta está fora da allowlist anteriormente aprovada; nenhum arquivo, conteúdo, metadata, token ou segredo foi acessado nesta rodada.
- **Próxima ação:** resolver se a amostra deve ser ampliada para os 3 cenários da SPEC ou se haverá emenda formal da SPEC/critério antes de qualquer acesso.
