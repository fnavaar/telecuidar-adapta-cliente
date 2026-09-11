# AP-2026-09-11-1717 — Enforcement runtime ausente no baseline

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: F1-T02 / SPEC-1-001
- Sinal: o Skip operacional está no template inicial e não possui mecanismo runtime de gate para recusar ingestão sem política ou fora da allowlist.
- Evidência: projeto Skip 57934 sem migrations, somente coleção auth `users`, lista de arquivos sem implementação de gate/integração e sonda contratual com `runtime_enforcement: NOT_AVAILABLE`.
- Regra reutilizável: não tratar uma sonda contratual em memória como prova de enforcement; exigir um ponto real de entrada e uma recusa observável antes de marcar o critério como aprovado.
- Quando aplicar: em tasks que precisam provar bloqueio, validação, permissão ou recusa no sistema.
- Quando não aplicar: quando a task exigir apenas documentação declarativa e não afirmar comportamento runtime.
- Confiança: alta — a limitação foi observada no baseline e a prova contratual foi explicitamente separada do runtime.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
