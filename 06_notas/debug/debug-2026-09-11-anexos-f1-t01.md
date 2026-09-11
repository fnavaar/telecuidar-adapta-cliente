# Debug Summary — F1-T01

**Task e problema:** F1-T01 / fechamento reprovado inicialmente porque os anexos A–E exigidos pela SPEC-1-001 não existiam no repositório; após a primeira correção, P-1-004 e P-1-005 permaneciam sem definição.

**Reprodução:** inspeção da árvore do repositório identificou inicialmente a ausência dos cinco anexos. Após sua criação, a leitura de `anexos/C-allowlist.md` e `anexos/D-politica.md` mostrou as lacunas explícitas de retenção e de tratamento de itens fora da allowlist.

**Causa raiz:** os insumos haviam sido validados na conversa e no estado, mas não tinham sido materializados inicialmente como artefatos versionados; depois, duas regras de governança ainda dependiam de decisão da Champion.

**Correção:** criados e depois atualizados os anexos A–E. A Champion confirmou retenção indefinida e determinou que arquivos fora da pasta allowlist `TESTE` sejam ignorados e não processados. As regras foram registradas nos Anexos C e D, sem alterar a planilha original, sem criar cópia e sem descartar dados.

**Verificação automática:** os cinco anexos existem no repositório; CA-1-001 a CA-1-005 estão documentados; o hash e o catálogo estrutural da planilha estão registrados; B-102 está fechado; B-103 está documentado com acesso, armazenamento, uso, retenção indefinida e proibição de descarte; pendências P-1-001, P-1-002 e P-1-003 permanecem visíveis; nenhum arquivo financeiro original foi incluído; nenhuma migration ou coleção de negócio foi criada no Skip; nenhum dado foi ingerido ou descartado.

**Gate resolvido:** a Champion confirmou às 17:00 “tudo correto, testado e aprovado”. A verificação final confirmou P-1-004/P-1-005 fechadas no Anexo E, CA-1-001..005 demonstrados e zero ingestão. F1-T01 concluída; F1-T02 liberada apenas como elegível, sem autorização de execução.
