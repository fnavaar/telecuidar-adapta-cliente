# Anexo E — Catálogo observado

- **Task/SPEC:** F1-T01 / SPEC-1-001
- **Fonte:** `CUSTEIO_NOVO.xlsx`
- **SHA-256 da fonte:** `50b3dfd912d12d1de231aa43f4d7280730e0a16fcb39ef5c3e68222e9ed0166d`
- **Método:** leitura somente estrutural; nenhum lançamento individual foi reproduzido neste anexo.

## `CUSTEIO`

- **Intervalo observado:** `B2:I182`.
- **Cabeçalho:** `B3:I3`.
- **Linhas de dados observadas:** 178.
- **Colunas:** `Data Vencimento`, `Classificação`, `Descrição`, `Valor`, `Forma de Pagamento`, `Parcelamento`, `Status Pagamento`, `Responsável Pagamento`.
- **Tipos observados:** data, texto e número, conforme a coluna; células vazias foram mantidas como lacunas.
- **Contagem estrutural por coluna:**
  - `Data Vencimento`: 170 datas; 8 vazios — `P-1-002`.
  - `Classificação`: 170 textos; 8 vazios.
  - `Descrição`: 177 textos; 1 vazio.
  - `Valor`: 178 números.
  - `Forma de Pagamento`: 163 textos; 15 vazios.
  - `Parcelamento`: 163 textos; 15 vazios.
  - `Status Pagamento`: 162 textos; 16 vazios.
  - `Responsável Pagamento`: 119 textos; 59 vazios — `P-1-003`.

## `DADOS`

- **Intervalo observado:** `A1:B17`.
- **Cabeçalho:** `Campo`, `Valor Padrão`.
- **Valores observados:**
  - Formas de pagamento: `Pagamento Imediato`, `Cartão de Crédito`.
  - Status: `Pago`, `Pendente`, `Em atraso`, `Cancelado`.
  - Classificações: `Despesa Operacional`, `Custo Serviço Prestado`, `Investimento/ Ativo Imobilizado`.
  - Responsáveis: `Antonio Jorge`, `Francisco Figueiredo`, `Geraldo Tadeu`.
- **Lacuna:** `Classificação - Opção 4` sem valor — `P-1-001`.

## `DESPESA OPERACIONAL`

- **Intervalo observado:** `B2:F33`.
- **Cabeçalho inicial:** `Período`, `Antonio Jorge`, `Francisco Figueiredo`, `Geraldo Tadeu`, `Total Geral`.
- **Estrutura observada:** quadros agregados por período e responsável; a semântica de cada fórmula não foi inferida.

## `INVESTIMENTO|ATIVO IMOLIZADO`

- **Intervalo observado:** `B2:F46`.
- **Cabeçalho inicial:** `Período`, `Antonio Jorge`, `Francisco Figueiredo`, `Geraldo Tadeu`, `Total Geral`.
- **Estrutura observada:** quadros agregados por período e responsável; o nome da aba foi preservado exatamente como observado; a semântica de cada fórmula não foi inferida.

## `PAINEL`

- **Intervalo observado:** `A1:E17`.
- **Cabeçalho observado:** `Indicador`, `Valor / Descricao`, `Cartão de crédito`, `Total`, `Participação no total`.
- **Estrutura:** área de indicadores observada; significado, fórmulas e preenchimento não foram inferidos nesta task.

## Pendências consolidadas

- `P-1-001`: valor ausente em `DADOS` para `Classificação - Opção 4`.
- `P-1-002`: 8 linhas de `CUSTEIO` sem `Data Vencimento`.
- `P-1-003`: 59 linhas de `CUSTEIO` sem `Responsável Pagamento`.
- `P-1-004` — **fechada em 2026-09-11:** retenção sem descarte até nova decisão explícita e versionada da Champion.
- `P-1-005` — **fechada em 2026-09-11:** itens e subpastas fora da allowlist são recusados por padrão; inclusão exige confirmação explícita e atualização do Anexo C.

Nenhuma pendência foi preenchida por suposição e nenhum dado foi descartado.
