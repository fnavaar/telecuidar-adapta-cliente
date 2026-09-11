# Anexo F — Regras financeiras e exemplos — F1-T03

- **Task/SPEC:** F1-T03 / SPEC-1-002
- **Status:** DRAFT COM DECISÕES REGISTRADAS — aguardando revisão e aceite humano da Champion Daniela; B-105 ainda não fechado.
- **Responsável pela revisão:** Daniela.
- **Cadência:** revisão mensal, até o dia 10.
- **Fonte estrutural:** Anexo E da F1-T01.
- **Fonte das regras de comportamento:** SPEC-1-002, RN-110 a RN-114 e decisões recebidas do cliente em 2026-09-11.
- **Uso de dados:** exemplos abaixo são sintéticos/estruturais; nenhum lançamento real foi copiado.

## Decisões recebidas da Champion/cliente

| Tema | Decisão registrada | Estado |
|---|---|---|
| Campos obrigatórios | `Data Vencimento`, `Classificação`, `Descrição`, `Valor`, `Forma de Pagamento`, `Parcelamento`, `Status do Pagamento`, `Responsável Pagamento` — para aporte e saída | Recebida; deve ser aplicada sem default |
| Campo obrigatório ausente | Recusar o lançamento | Recebida |
| Chave de repetição | Mesma `Descrição` com mesma `Data Vencimento` | Recebida; produz um único registro e recibo idempotente |
| Totais válidos | Os status operacionais `Pago`, `Pendente` e `Em atraso` entram; `Cancelado` fica fora | Recebida e compatibilizada com RN-112 pela distinção abaixo; aceite final pendente |
| Revisão | Daniela; revisão mensal; até o dia 10 | Recebida |

## Distinção entre status operacional e pendência de validação

A decisão recebida estabelece duas condições diferentes:

1. **`Status Pagamento = Pendente`** é um status operacional do lançamento e **entra nos totais válidos**.
2. **Pendência de validação** é uma condição de controle distinta do status operacional. Um item com pendência de validação permanece visível como pendência e **fica fora dos totais válidos**, conforme RN-112, mesmo que seu status operacional seja `Pendente`.

A distinção acima resolve a dúvida registrada anteriormente sem alterar a RN-112.

## Regras da SPEC incorporadas

| ID | Regra | Resultado exigido |
|---|---|---|
| RN-110 | Campo obrigatório ausente | Recusar o lançamento, conforme decisão recebida; nunca preencher default. |
| RN-111 | Saída sem participante | Não é lançamento válido. |
| RN-112 | Item em pendência de validação | Fica fora dos totais válidos e permanece visível como pendência. O status operacional `Pendente`, quando não houver pendência de validação, continua incluído nos totais. |
| RN-113 | Correção | Preserva antes/depois, ator e horário em trilha append-only; não há update destrutivo. |
| RN-114 | Comando repetido | A combinação `Descrição + Data Vencimento` produz um único registro e um recibo idempotente. |

## Exemplos de entrada → resultado

| Caso | Entrada sintética | Resultado esperado | Estado |
|---|---|---|---|
| Aporte completo | Os oito campos obrigatórios preenchidos; participante e referência documental presentes | Registrar como lançamento rastreável, conforme catálogo aprovado | Definido; aceite B-105 pendente |
| Saída completa | Os oito campos obrigatórios preenchidos; participante e referência documental presentes | Registrar como saída válida e rastreável | Definido; aceite B-105 pendente |
| Status operacional `Pendente` | Lançamento válido, com `Status Pagamento = Pendente` e sem pendência de validação | Permanece visível e entra nos totais válidos | Definido pela decisão recebida |
| Campo obrigatório ausente | Qualquer um dos oito campos vazio | Recusar o lançamento; não criar registro válido e não preencher default | Definido |
| Saída sem participante | Saída com participante ausente | Recusar como lançamento válido, conforme RN-111 | Definido pela SPEC |
| Pendência de validação | Registro com pendência de validação/fonte, distinta do status operacional `Pendente` | Manter pendência visível, sem valor inventado e fora dos totais válidos | Definido pela RN-112 e pela distinção recebida |
| Correção | Registro original e correção posterior do mesmo lançamento | Manter antes/depois, ator e horário; nenhum update destrutivo | Definido pela SPEC |
| Repetição | Mesma `Descrição` e `Data Vencimento` enviadas novamente | Um registro e recibo idempotente, sem duplicidade | Definido pela decisão recebida e RN-114 |

## Aceite pendente

- O catálogo candidato precisa ser revisado e aceito pela Champion para fechar B-104.
- Este Anexo F precisa ser revisado e aceito pela Champion para fechar B-105.
- A confirmação da distinção entre `Pendente` operacional e pendência de validação resolve a dúvida de requisito, mas não substitui o aceite humano final da task.

## Regra de segurança

Até o aceite final do catálogo e do Anexo F:

- nenhum cálculo financeiro novo será criado;
- nenhum modelo ou migration será criado;
- nenhum dado real será usado;
- nenhuma lacuna receberá default;
- B-105 permanece aberto.
