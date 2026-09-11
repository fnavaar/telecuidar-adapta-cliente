# AP-2026-09-11-1838 — Revalidação de estados antes do fechamento documental

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: F1-T03 / SPEC-1-002
- Sinal: após o aceite humano, referências antigas de estado (`CANDIDATO`, aceite pendente e dúvida bloqueante) permaneceram em artefatos da mesma task e foram detectadas pela revalidação independente antes do fechamento.
- Evidência: `anexos/catalogo-executavel-f1-t03.md`, `anexos/F-regras-financeiras.md` e `anexos/relatorio-diff-catalogo-anexo-e.md`; prova de revalidação pré-fechamento identificou os estados obsoletos.
- Regra reutilizável: antes de concluir uma task documental, varrer todos os artefatos e referências de gate/status para garantir que decisões aceitas estejam refletidas de forma consistente, sem estados obsoletos.
- Quando aplicar: em toda conclusão de task com aceite humano que altere bloqueios, decisões ou status documentais.
- Quando não aplicar: não alterar o histórico do changelog nem reinterpretar requisitos; corrigir somente referências de estado comprovadamente desatualizadas.
- Confiança: alta — a inconsistência foi detectada por verificação independente e corrigida antes do fechamento.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto
