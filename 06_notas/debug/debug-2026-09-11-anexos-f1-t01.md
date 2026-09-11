# Debug Summary — F1-T01

**Task e problema:** F1-T01 / fechamento reprovado porque os anexos A–E exigidos pela SPEC-1-001 não existiam no repositório.

**Reprodução:** inspeção da árvore do repositório após o aceite humano; não havia diretório `anexos/` nem os cinco arquivos nomeados na seção “Saídas” da SPEC.

**Causa raiz:** os insumos haviam sido validados na conversa e no estado, mas não tinham sido materializados como artefatos versionados no handoff operacional.

**Correção:** criados `anexos/A-planilha.md`, `B-amostra.md`, `C-allowlist.md`, `D-politica.md` e `E-catalogo-observado.md`, com hash, inventário estrutural, pasta allowlist, política confirmada e pendências explícitas. Também foi preservada a referência da pasta vazia como backup, sem cópia ou descarte.

**Verificação automática:** artefatos criados dentro do recorte da SPEC; conteúdo limitado a metadados, estrutura, regras confirmadas e pendências; nenhum arquivo financeiro original foi incluído no repositório; nenhuma migration ou coleção de negócio foi criada no Skip; nenhum dado foi ingerido ou descartado.

**Pendências que impedem o fechamento:** `P-1-004` (retenção não definida) e `P-1-005` (recorte fora da pasta não confirmado). A task deve retornar ao teste/aceite humano após essas pendências serem resolvidas ou formalmente aceitas pela Champion.
