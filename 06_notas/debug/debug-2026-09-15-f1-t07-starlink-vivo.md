# Debug Summary
**Task e problema:** F1-T07 — o item 3 misturou Internet Starlink e Internet Vivo.

**Reprodução:** o formulário/backend tratavam o cenário divergente como um objeto único com `valor_planilha=339`, `valor_sistema=99,99` e uma referência `FATURA VIVO.pdf`.

**Causa raiz:** dois lançamentos independentes foram modelados como uma divergência sistema×planilha. A fonte confirma Starlink R$339,00 e Vivo R$99,99 como despesas distintas, cada uma com sua fatura.

**Correção:** bloqueada antes de alterar o produto. É necessário definir qual lançamento será o terceiro cenário divergente, ou aceitar um recorte com quatro itens (completo, sem documento, Starlink completo e Vivo completo) e escolher separadamente uma divergência real.

**Verificação automática:** fontes autorizadas reconsultadas; extrato registra Vivo R$99,99; planilha de detalhamento registra Internet Starlink R$339,00 com referência `NF 010898811 - STALINK`; metadados da pasta listam `FATURA VIVO.pdf` e `NF 010898811 - STALINK.pdf` em locais distintos. Nenhum PDF foi baixado ou aberto.

**Gate atual:** bloqueada por dúvida de recorte para o terceiro cenário B-107.
