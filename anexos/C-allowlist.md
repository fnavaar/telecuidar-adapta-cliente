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

## Recorte confirmado

- **Dentro:** a pasta identificada pelo ID acima. Atualmente não há arquivos dentro dela.
- **Fora:** qualquer arquivo ou pasta que não esteja dentro da pasta allowlist `TESTE` será ignorado e não processado.
- **Subpastas:** a regra de fora da allowlist também se aplica a itens que não estejam dentro do recorte autorizado; não há subpastas visíveis nesta validação.
- **Regra de segurança aplicada nesta etapa:** nenhum item foi lido, copiado, ingerido ou alterado.
