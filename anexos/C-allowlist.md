# Anexo C — Allowlist e referência de backup

- **Task/SPEC:** F1-T01 / SPEC-1-001
- **Nome da pasta:** `TESTE`
- **ID da pasta:** `1S0vZYfRJl5VvlC3-uratZD4Dp0Jqr5Cl`
- **URL:** https://drive.google.com/drive/folders/1S0vZYfRJl5VvlC3-uratZD4Dp0Jqr5Cl?usp=drive_link
- **Tipo observado:** pasta do Google Drive (`application/vnd.google-apps.folder`).
- **Proprietária observada:** Daniela Serpa.
- **Estado observado:** não está na lixeira.
- **Conteúdo:** o cliente confirmou que a pasta não contém arquivos; a listagem somente leitura também retornou zero itens visíveis.
- **Função registrada:** referência de backup/allowlist para o projeto. Nenhuma cópia foi criada e nenhum arquivo foi baixado, movido ou alterado.

## Recorte

- **Dentro:** a pasta identificada pelo ID acima; atualmente não há arquivos dentro dela.
- **Fora:** qualquer item cujo ancestral não seja a pasta identificada acima é recusado por padrão; nova inclusão exige confirmação explícita da Champion e atualização versionada deste anexo.
- **Subpastas:** recusadas por padrão enquanto não forem adicionadas nominalmente à allowlist.
- **Regra de segurança:** negar por padrão fora da allowlist; nesta etapa nenhum item foi lido, copiado, ingerido ou alterado.
