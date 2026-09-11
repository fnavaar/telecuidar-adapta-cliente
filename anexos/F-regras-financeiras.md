# Anexo F — Regras financeiras e exemplos — F1-T03

- **Task/SPEC:** F1-T03 / SPEC-1-002
- **Status:** DRAFT — não aceito pela Champion; B-105 permanece aberto.
- **Responsável pelo aceite:** Daniela — Champion.
- **Fonte estrutural:** Anexo E da F1-T01.
- **Fonte das regras de comportamento:** SPEC-1-002, RN-110 a RN-114.
- **Uso de dados:** exemplos abaixo são sintéticos/estruturais; nenhum lançamento real foi copiado.

## Regras já fixadas pela SPEC

| ID | Regra | Resultado exigido |
|---|---|---|
| RN-110 | Campo obrigatório ausente | Recusa ou pendência exatamente conforme a decisão da Champion registrada neste Anexo F. O default automático é proibido. |
| RN-111 | Saída sem participante | Não é lançamento válido. |
| RN-112 | Item em pendência | Fica fora dos totais válidos e permanece visível como pendência. |
| RN-113 | Correção | Preserva antes/depois, ator e horário em trilha append-only; não há update destrutivo. |
| RN-114 | Comando repetido | A mesma chave idempotente produz um único registro e um recibo idempotente. |

## Exemplos de entrada → resultado para aceite

| Caso | Entrada sintética | Resultado esperado para aprovação | Estado |
|---|---|---|---|
| Aporte completo | Todos os campos obrigatórios do catálogo preenchidos; participante e referência documental presentes | Registrar como lançamento rastreável, conforme catálogo aprovado | Aguardando definição dos campos obrigatórios e aceite |
| Saída completa | Classificação e valor preenchidos; participante e referência documental presentes | Registrar como saída válida e rastreável | Aguardando aceite |
| Saída sem participante | Saída com participante ausente | Recusar como lançamento válido, conforme RN-111 | Regra da SPEC; aceite da Champion pendente |
| Campo obrigatório ausente | Um campo que a Champion declarar obrigatório está vazio | Escolher explicitamente `recusa` ou `pendência`; nunca preencher default | Decisão B-105 pendente |
| Item pendente | Registro incompleto ou sem fonte suficiente | Manter pendência visível, fora dos totais válidos, sem valor inventado | Regra da SPEC; mapping de status pendente |
| Correção | Registro original e correção posterior do mesmo lançamento | Manter antes/depois, ator e horário; nenhum update destrutivo | Regra da SPEC; aceite pendente |
| Repetição | Mesma chave idempotente enviada novamente | Um registro e recibo idempotente, sem duplicidade | Regra da SPEC; formato da chave pendente |

## Decisões necessárias da Champion para fechar B-105

1. Quais campos são obrigatórios em aporte e saída, separadamente?
2. Para cada campo obrigatório ausente, o resultado é `recusa` ou `pendência`?
3. Qual é a chave idempotente da repetição? A chave será fornecida pelo usuário, composta de campos, ou outro mecanismo aprovado?
4. Quais status/condições entram nos totais válidos? A regra de pendência da RN-112 deve ser aplicada a quais valores da coluna `Status Pagamento`?
5. Qual responsável, prazo e cadência revisarão o Anexo F depois de aprovado?
6. A Champion aprova os valores de domínio e os nomes exatamente como registrados no catálogo candidato?

## Regra de segurança

Até o aceite do Anexo F:

- nenhum cálculo financeiro novo será criado;
- nenhum modelo ou migration será criado;
- nenhum dado real será usado;
- nenhuma lacuna receberá default;
- B-105 permanece aberto.
