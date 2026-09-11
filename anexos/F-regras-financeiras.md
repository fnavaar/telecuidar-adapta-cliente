# Anexo F — Regras financeiras e exemplos — F1-T03

- **Task/SPEC:** F1-T03 / SPEC-1-002
- **Status:** DRAFT COM DECISÕES RECEBIDAS — B-105 bloqueado por uma dúvida de compatibilidade com a RN-112; não criar modelo ou migration.
- **Responsável pela revisão:** Daniela.
- **Cadência:** revisão mensal, até o dia 10.
- **Fonte estrutural:** Anexo E da F1-T01.
- **Fonte das regras de comportamento:** SPEC-1-002, RN-110 a RN-114 e decisões recebidas do cliente em 2026-09-11.
- **Uso de dados:** exemplos abaixo são sintéticos/estruturais; nenhum lançamento real foi copiado.

## Decisões recebidas da Champion

| Tema | Decisão registrada | Estado |
|---|---|---|
| Campos obrigatórios | `Data Vencimento`, `Classificação`, `Descrição`, `Valor`, `Forma de Pagamento`, `Parcelamento`, `Status do Pagamento`, `Responsável Pagamento` — para aporte e saída | Recebida; deve ser aplicada sem default |
| Campo obrigatório ausente | Recusar o lançamento | Recebida |
| Chave de repetição | Mesma `Descrição` com mesma `Data Vencimento` | Recebida; risco de colisão em operações legítimas iguais deve ser avaliado antes da implementação |
| Totais válidos | `Pago`, `Pendente` e `Em atraso` incluídos; `Cancelado` excluído | Recebida, mas conflitante com RN-112 para itens em pendência |
| Revisão | Daniela; revisão mensal; até o dia 10 | Recebida |

## Regras da SPEC incorporadas

| ID | Regra | Resultado exigido |
|---|---|---|
| RN-110 | Campo obrigatório ausente | Recusar o lançamento, conforme decisão recebida; nunca preencher default. |
| RN-111 | Saída sem participante | Não é lançamento válido. |
| RN-112 | Item em pendência | Fica fora dos totais válidos e permanece visível como pendência. |
| RN-113 | Correção | Preserva antes/depois, ator e horário em trilha append-only; não há update destrutivo. |
| RN-114 | Comando repetido | A combinação `Descrição + Data Vencimento` produz um único registro e um recibo idempotente, salvo decisão posterior que evite colisão legítima. |

## Exemplos de entrada → resultado

| Caso | Entrada sintética | Resultado esperado | Estado |
|---|---|---|---|
| Aporte completo | Os oito campos obrigatórios preenchidos; participante e referência documental presentes | Registrar como lançamento rastreável, conforme catálogo aprovado | Definido; aceite B-105 bloqueado pela dúvida de totais |
| Saída completa | Os oito campos obrigatórios preenchidos; participante e referência documental presentes | Registrar como saída válida e rastreável | Definido; aceite B-105 bloqueado pela dúvida de totais |
| Campo obrigatório ausente | Qualquer um dos oito campos vazio | Recusar o lançamento; não criar registro válido e não preencher default | Definido |
| Saída sem participante | Saída com participante ausente | Recusar como lançamento válido, conforme RN-111 | Definido pela SPEC |
| Item pendente | Registro com pendência de validação/fonte | Manter pendência visível, sem valor inventado; pela RN-112, fora dos totais válidos | Conflita com a decisão de incluir o status `Pendente` nos totais |
| Correção | Registro original e correção posterior do mesmo lançamento | Manter antes/depois, ator e horário; nenhum update destrutivo | Definido pela SPEC |
| Repetição | Mesma `Descrição` e `Data Vencimento` enviadas novamente | Um registro e recibo idempotente, sem duplicidade | Definido; risco de colisão precisa ser aceito ou ajustado |

## DÚVIDA bloqueante — totais e pendências

A decisão recebida informa que o status `Pendente` entra nos totais válidos. A RN-112 da SPEC informa que um **item em pendência** fica fora dos totais válidos. Sem uma distinção explícita, `Pendente` pode significar tanto o status operacional da coluna quanto uma pendência de validação.

- **Decisão recebida:** `Pendente` entra nos totais válidos.
- **RN-112:** item em pendência fica fora dos totais válidos.
- **Não inferido:** se o status `Pendente` é diferente de uma pendência de validação.
- **B-105:** permanece aberto até a Champion escolher a interpretação.

## Regra de segurança

Até a resolução da dúvida e o aceite final do Anexo F:

- nenhum cálculo financeiro novo será criado;
- nenhum modelo ou migration será criado;
- nenhum dado real será usado;
- nenhuma lacuna receberá default;
- B-105 permanece aberto.
