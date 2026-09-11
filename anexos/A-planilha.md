# Anexo A — Planilha recebida

- **Task/SPEC:** F1-T01 / SPEC-1-001
- **Status:** recebido e inventariado; aceite humano da Champion registrado; pacote ainda sujeito à verificação final dos anexos.
- **Nome do arquivo:** `CUSTEIO_NOVO.xlsx`
- **Origem:** arquivo anexado pelo cliente MAX Soluções LTDA no canal do projeto em 2026-09-11.
- **Tamanho observado:** 39.741 bytes.
- **SHA-256:** `50b3dfd912d12d1de231aa43f4d7280730e0a16fcb39ef5c3e68222e9ed0166d`
- **MD5 apenas para conferência operacional:** `cd673474ff2fe093d619e920e7c009b1`.
- **Cópia do arquivo original:** não incluída neste repositório; o arquivo original permanece no ambiente de recebimento.
- **Uso nesta task:** inventário estrutural e amostra; nenhum dado foi ingerido no Skip Cloud.

## Abas observadas

| Aba | Dimensão observada | Estrutura identificada |
|---|---:|---|
| `CUSTEIO` | `B2:I182` | Tabela de lançamentos; 178 linhas de dados observadas; cabeçalho em `B3:I3`. |
| `DESPESA OPERACIONAL` | `B2:F33` | Quadros por período e responsável; cabeçalho inicial em `B3:F3`. |
| `INVESTIMENTO|ATIVO IMOLIZADO` | `B2:F46` | Quadros por período e responsável; cabeçalho inicial em `B3:F3`. O nome foi preservado exatamente como observado. |
| `DADOS` | `A1:B17` | Dicionário de campos e valores padrão; cabeçalho em `A1:B1`. |
| `PAINEL` | `A1:E17` | Estrutura de indicadores; cabeçalho em `A1:E1`. Não foi interpretado como dashboard implementado. |

## Colunas observadas em `CUSTEIO`

1. `Data Vencimento`
2. `Classificação`
3. `Descrição`
4. `Valor`
5. `Forma de Pagamento`
6. `Parcelamento`
7. `Status Pagamento`
8. `Responsável Pagamento`

## Aceite e pendências

- A Champion Daniela foi confirmada pelo cliente.
- A própria planilha foi confirmada como amostra representativa.
- Pendências estruturais foram preservadas sem correção: `P-1-001`, `P-1-002` e `P-1-003`, detalhadas no Anexo E.
- Nenhum dado foi descartado.
