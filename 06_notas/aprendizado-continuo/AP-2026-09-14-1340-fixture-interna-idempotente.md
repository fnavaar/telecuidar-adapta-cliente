# AP-2026-09-14-1340 — Fixture interna com fingerprint e rollback idempotente

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: F1-T06 / SPEC-1-003
- Sinal: fixture documental interna, identificada por `source_id`/`source_ref` e fingerprint determinística, permitiu três reprocessamentos, confirmação humana única, preservação após falha e rollback que removeu candidato, vínculo e lançamento sintéticos sem deixar resíduos.
- Evidência: `artifacts/f1-t06-evidencia.md`; smoke autenticado independente no preview em 2026-09-14; migration `0003_create_documento_vinculos` e QA Skip 0.0.7.
- Regra reutilizável: para provas de integração documental sem fonte externa disponível, usar fixture interna com fingerprint única, confirmação humana obrigatória, estados explícitos e rollback idempotente; nunca criar arquivo real apenas para testar o pipeline.
- Quando aplicar: em spikes e testes de integração em que a fonte externa está vazia, indisponível ou proibida para dados reais; manter a fixture isolada por lote e limpar ao final.
- Quando não aplicar: não usar fixture interna para declarar que OAuth, timeout, revogação ou leitura de conteúdo real foram provados; esses cenários exigem evidência específica.
- Confiança: alta — padrão exercitado no preview, com três reprocessamentos, confirmação repetida, falha pós-confirmação e rollback verificado com zero resíduos.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
