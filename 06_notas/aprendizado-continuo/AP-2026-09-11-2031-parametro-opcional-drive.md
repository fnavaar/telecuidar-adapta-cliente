# AP-2026-09-11-2031 — Parâmetro opcional do conector Drive

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: F1-T05 / SPEC-1-003
- Sinal: o conector retornou HTTP 400 quando `includePermissionsForView` foi enviado vazio; a mesma consulta de metadados, com o valor suportado `published`, retornou HTTP 200 sem ampliar o escopo.
- Evidência: `artifacts/f1-t05-spike-evidencia.md`; logs sanitizados `log_NccetLWj8D6d` e `log_mKHaKqma-ysV`.
- Regra reutilizável: parâmetros opcionais de conectores devem ser omitidos ou preenchidos somente com valores aceitos pelo provedor; campo vazio não deve ser enviado como se fosse ausente.
- Quando aplicar: ao repetir chamadas Google Drive com `includePermissionsForView` ou parâmetros opcionais equivalentes; validar a resposta HTTP antes de interpretar a autorização.
- Quando não aplicar: não usar esse ajuste para ampliar escopo, buscar arquivos fora da allowlist ou substituir a verificação de permissões.
- Confiança: alta — houve falha observada e nova chamada controlada com o mesmo ID e escopo que passou.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
