# Anexo F — Regras financeiras e exemplos — F1-T03

- **Task/SPEC:** F1-T03 / SPEC-1-002
- **Status:** APROVADO pela Champion Daniela em 2026-09-11; B-105 fechado.
- **Responsável pela revisão:** Daniela.
- **Cadência:** revisão mensal, até o dia 10.
- **Fonte estrutural:** Anexo E da F1-T01.
- **Fonte das regras de comportamento:** SPEC-1-002, RN-110 a RN-114 e decisões recebidas do cliente em 2026-09-11.
- **Uso de dados:** exemplos abaixo são sintéticos/estruturais; nenhum lançamento real foi copiado.

## Decisões recebidas e aceitas pela Champion

| Tema | Decisão registrada | Estado |
|---|---|---|
| Campos obrigatórios | `Data Vencimento`, `Classificação`, `Descrição`, `Valor`, `Forma de Pagamento`, `Parcelamento`, `Status do Pagamento`, `Responsável Pagamento` — para aporte e saída | Aceita; deve ser aplicada sem default |
| Campo obrigatório ausente | Recusar o lançamento | Aceita |
| Chave de repetição | Mesma `Descrição` com mesma `Data Vencimento` | Aceita; produz um único registro e recibo idempotente |
| Totais válidos | Os status operacionais `Pago`, `Pendente` e `Em atraso` entram; `Cancelado` fica fora | Aceita e compatibilizada com RN-112 pela distinção abaixo |
| Revisão | Daniela; revisão mensal; até o dia 10 | Aceita |

## Distinção entre status operacional e pendência de validação

A decisão aceita estabelece duas condições diferentes:

1. **`Status Pagamento = Pendente`** é um status operacional do lançamento e **entra nos totais válidos**.
2. **Pendência de validação** é uma condição de controle distinta do status operacional. Um item com pendência de validação permanece visível como pendência e **fica fora dos totais válidos**, conforme RN-112, mesmo que seu status operacional seja `Pendente`.

A distinção acima resolve a dúvida registrada anteriormente sem alterar a RN-112.

## Regras da SPEC incorporadas

| ID | Regra | Resultado exigido |
|---|---|---|
| RN-110 | Campo obrigatório ausente | Recusar o lançamento, conforme decisão aceita; nunca preencher default. |
| RN-111 | Saída sem participante | Não é lançamento válido. |
| RN-112 | Item em pendência de validação | Fica fora dos totais válidos e permanece visível como pendência. O status operacional `Pendente`, quando não houver pendência de validação, continua incluído nos totais. |
| RN-113 | Correção | Preserva antes/depois, ator e horário em trilha append-only; não há update destrutivo. |
| RN-114 | Comando repetido | A combinação `Descrição + Data Vencimento` produz um único registro e um recibo idempotente. |

## Exemplos de entrada → resultado

| Caso | Entrada sintética | Resultado esperado | Estado |
|---|---|---|---|
| Aporte completo | Os oito campos obrigatórios preenchidos; participante e referência documental presentes | Registrar como lançamento rastreável, conforme catálogo aprovado | Aceito |
| Saída completa | Os oito campos obrigatórios preenchidos; participante e referência documental presentes | Registrar como saída válida e rastreável | Aceito |
| Status operacional `Pendente` | Lançamento válido, com `Status Pagamento = Pendente` e sem pendência de validação | Permanece visível e entra nos totais válidos | Aceito |
| Campo obrigatório ausente | Qualquer um dos oito campos vazio | Recusar o lançamento; não criar registro válido e não preencher default | Aceito |
| Saída sem participante | Saída com participante ausente | Recusar como lançamento válido, conforme RN-111 | Aceito pela SPEC |
| Pendência de validação | Registro com pendência de validação/fonte, distinta do status operacional `Pendente` | Manter pendência visível, sem valor inventado e fora dos totais válidos | Aceito pela RN-112 |
| Correção | Registro original e correção posterior do mesmo lançamento | Manter antes/depois, ator e horário; nenhum update destrutivo | Aceito pela SPEC |
| Repetição | Mesma `Descrição` e `Data Vencimento` enviadas novamente | Um registro e recibo idempotente, sem duplicidade | Aceito pela decisão e RN-114 |

## Aceite humano

Daniela revisou e aceitou o catálogo e este Anexo F em mensagem do projeto em 2026-09-11. Com esse aceite, CA-1-007 e CA-1-008 estão atendidos; B-104 e B-105 estão fechados.

## Regra de segurança

Durante e após esta task:

- nenhum cálculo financeiro novo foi criado nesta task;
- nenhum modelo ou migration foi criado nesta task;
- nenhum dado real foi usado;
- nenhuma lacuna recebeu default;
- a implementação da F1-T04 continua condicionada ao seu próprio ciclo de análise, autorização e testes.
