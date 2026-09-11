# STATUS — Telecuidar / MAX Soluções

- **Fase:** 1 — núcleo financeiro e rastreabilidade.
- **Progresso:** 4/8 tasks concluídas (50%).
- **Task ativa:** F1-T05 — executar spike timeboxed do mecanismo de acesso à pasta.
- **Situação:** B-106 completo; aguardando autorização explícita para executar o spike. Nenhum acesso foi iniciado.
- **Champion:** Daniela.
- **Pré-condições confirmadas:** F1-T02 aceita; B-102/B-103/B-108 disponíveis; F1-T04 concluída.
- **Contrato B-106 aprovado:** OAuth2 com conta Google autorizada; escopo somente a pasta `TESTE` (`1S0vZYfRJl5VvlC3-uratZD4Dp0Jqr5Cl`), sem ampliação; Daniela fará alterações/revogação; responsável Daniela Serpa; janela máxima de 30 minutos; orçamento máximo de R$ 0,00.
- **Fallback manual idempotente aprovado:** diante de timeout, erro de permissão ou parada, não criar lançamento automaticamente; registrar `source_ref`, `fingerprint`, motivo e estado pendente quando disponíveis; reprocessamentos com a mesma referência/fingerprint não podem duplicar; reconciliação somente após confirmação humana.
- **RED planejado:** sem B-106, fora da allowlist ou credencial inválida deve resultar em recusa/nenhum item listado; esta prova só pode começar após autorização do spike.
- **Segurança:** nenhum arquivo do Drive foi baixado, lido, copiado, movido ou alterado; nenhum dado real foi ingerido; nenhuma credencial, segredo ou token foi compartilhado ou criado; produção não foi publicada.
- **Próxima ação:** autorizar explicitamente a execução do spike OAuth2 timeboxed; depois executar somente a F1-T05.
