# Catálogo executável candidato — F1-T03

- **Task/SPEC:** F1-T03 / SPEC-1-002
- **Fonte de verdade estrutural:** Anexo E da F1-T01 e `CUSTEIO_NOVO.xlsx`
- **SHA-256 da fonte:** `50b3dfd912d12d1de231aa43f4d7280730e0a16fcb39ef5c3e68222e9ed0166d`
- **Status:** CANDIDATO — catálogo aprovado em princípio pela Champion; B-104 aguarda fechamento conjunto com a resolução da dúvida do Anexo F.
- **Limite:** este catálogo formaliza somente o que foi observado e as obrigatoriedades explicitamente informadas; não cria campo, valor, fórmula, participante, referência documental ou chave além das decisões registradas.

## Campos de `CUSTEIO`

| Campo | Tipo observado | Valores/forma observados | Obrigatório | Regra executável | Fonte/pendência |
|---|---|---|---|---|---|
| `Data Vencimento` | Data | Datas; 8 células vazias observadas | Sim | Ausência recusa o lançamento; não preencher automaticamente | Anexo E; P-1-002 |
| `Classificação` | Texto | `Despesa Operacional`; `Custo Serviço Prestado`; `Investimento/ Ativo Imobilizado`; 8 vazios observados | Sim | Aceitar somente valores do catálogo aprovado; ausência recusa o lançamento; sem default | Anexo E; P-1-001 cobre opção vazia em DADOS |
| `Descrição` | Texto | Textos; 1 célula vazia observada | Sim | Ausência recusa o lançamento; nenhuma transformação ou inferência | Anexo E |
| `Valor` | Número | Números; 178 valores observados | Sim | Ausência recusa o lançamento; nenhuma fórmula ou arredondamento novo nesta task | Anexo E |
| `Forma de Pagamento` | Texto | `Pagamento Imediato`; `Cartão de Crédito`; vazios observados | Sim | Aceitar somente valores do catálogo aprovado; ausência recusa o lançamento; sem default | Anexo E |
| `Parcelamento` | Texto | Textos como `Não` e `Parcela 1 de N`; vazios observados | Sim | Ausência recusa o lançamento; preservar como recebido; sem cálculo novo | Anexo E |
| `Status Pagamento` | Texto | `Pago`; `Pendente`; `Em atraso`; `Cancelado`; vazios observados | Sim | Aceitar somente valores do catálogo aprovado; ausência recusa o lançamento; sem default | Anexo E |
| `Responsável Pagamento` | Texto | `Antonio Jorge`; `Francisco Figueiredo`; `Geraldo Tadeu`; 59 vazios observados | Sim | Ausência recusa o lançamento; não preencher responsável automaticamente | Anexo E; P-1-003 |

## Valores de domínio observados em `DADOS`

| Domínio | Valores observados | Situação |
|---|---|---|
| Forma de Pagamento | `Pagamento Imediato`; `Cartão de Crédito` | Igual ao Anexo E; decisão recebida |
| Status do Pagamento | `Pago`; `Pendente`; `Em atraso`; `Cancelado` | Igual ao Anexo E; regra de totais ainda tem dúvida sobre `Pendente` |
| Classificação | `Despesa Operacional`; `Custo Serviço Prestado`; `Investimento/ Ativo Imobilizado` | Igual ao Anexo E; opção 4 vazia preservada |
| Responsável Pagamento | `Antonio Jorge`; `Francisco Figueiredo`; `Geraldo Tadeu` | Igual ao Anexo E; vazios preservados |

## Regras de catálogo

1. Os oito campos de `CUSTEIO` são obrigatórios para aporte e saída.
2. Campo obrigatório ausente gera recusa do lançamento.
3. Nenhuma lacuna recebe default inventado.
4. Nenhum campo, valor ou fórmula ausente na fonte é acrescentado nesta task.
5. `P-1-001`, `P-1-002` e `P-1-003` permanecem visíveis.
6. A chave de repetição informada para idempotência é `Descrição + Data Vencimento`; sua aplicação será formalizada no Anexo F.
7. Este catálogo não autoriza migration, coleção financeira, rota de lançamento ou ingestão de dado real.
8. Divergência entre este catálogo e o Anexo E bloqueia o próximo deploy/modelo.
