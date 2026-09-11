# Catálogo executável candidato — F1-T03

- **Task/SPEC:** F1-T03 / SPEC-1-002
- **Fonte de verdade estrutural:** Anexo E da F1-T01 e `CUSTEIO_NOVO.xlsx`
- **SHA-256 da fonte:** `50b3dfd912d12d1de231aa43f4d7280730e0a16fcb39ef5c3e68222e9ed0166d`
- **Status:** DRAFT — aguarda aprovação da Champion para fechar B-104.
- **Limite:** este catálogo formaliza somente o que foi observado; não cria regra financeira, default, fórmula, participante ou chave de idempotência.

## Campos de `CUSTEIO`

| Campo | Tipo observado | Valores/forma observados | Obrigatório | Regra executável | Fonte/pendência |
|---|---|---|---|---|---|
| `Data Vencimento` | Data | Datas; 8 células vazias observadas | `[NÃO DEFINIDO]` | Não preencher automaticamente | Anexo E; P-1-002 |
| `Classificação` | Texto | `Despesa Operacional`; `Custo Serviço Prestado`; `Investimento/ Ativo Imobilizado`; 8 vazios observados | `[NÃO DEFINIDO]` | Aceitar somente valores do catálogo aprovado; vazio sem default | Anexo E; P-1-001 cobre opção vazia em DADOS |
| `Descrição` | Texto | Textos; 1 célula vazia observada | `[NÃO DEFINIDO]` | Nenhuma transformação ou inferência | Anexo E |
| `Valor` | Número | Números; 178 valores observados | `[NÃO DEFINIDO]` | Nenhuma fórmula ou arredondamento novo nesta task | Anexo E |
| `Forma de Pagamento` | Texto | `Pagamento Imediato`; `Cartão de Crédito`; vazios observados | `[NÃO DEFINIDO]` | Aceitar somente valores do catálogo aprovado; vazio sem default | Anexo E |
| `Parcelamento` | Texto | Textos como `Não` e `Parcela 1 de N`; vazios observados | `[NÃO DEFINIDO]` | Preservar como recebido; sem cálculo novo | Anexo E |
| `Status Pagamento` | Texto | `Pago`; `Pendente`; `Em atraso`; `Cancelado`; vazios observados | `[NÃO DEFINIDO]` | Aceitar somente valores do catálogo aprovado; vazio sem default | Anexo E |
| `Responsável Pagamento` | Texto | `Antonio Jorge`; `Francisco Figueiredo`; `Geraldo Tadeu`; 59 vazios observados | `[NÃO DEFINIDO]` | Não preencher responsável automaticamente | Anexo E; P-1-003 |

## Valores de domínio observados em `DADOS`

| Domínio | Valores observados | Situação |
|---|---|---|
| Forma de Pagamento | `Pagamento Imediato`; `Cartão de Crédito` | Igual ao Anexo E; aprovação B-104 pendente |
| Status do Pagamento | `Pago`; `Pendente`; `Em atraso`; `Cancelado` | Igual ao Anexo E; sem interpretação adicional |
| Classificação | `Despesa Operacional`; `Custo Serviço Prestado`; `Investimento/ Ativo Imobilizado` | Igual ao Anexo E; opção 4 vazia preservada |
| Responsável Pagamento | `Antonio Jorge`; `Francisco Figueiredo`; `Geraldo Tadeu` | Igual ao Anexo E; vazios preservados |

## Regras de catálogo

1. Nenhuma lacuna recebe default inventado.
2. Nenhum campo, valor ou fórmula ausente na fonte é acrescentado nesta task.
3. `P-1-001`, `P-1-002` e `P-1-003` permanecem visíveis.
4. Este catálogo não autoriza migration, coleção financeira, rota de lançamento ou ingestão de dado real.
5. Divergência entre este catálogo e o Anexo E bloqueia o próximo deploy/modelo.
