# F2-T01 — Termo de insumos B-201/B-202

**Projeto:** MAX Soluções / Telecuidar  
**Task:** F2-T01 — Fechar insumos de consolidação (B-201/B-202) com a Champion  
**SPEC:** SPEC-2-001 — Consolidação por período, participante e classificação  
**Data do registro:** 2026-09-23  
**Fonte do aceite:** resposta da Champion no formulário de decisões da F2-T01: “Registrar decisões aprovadas”  
**Status do termo:** **ACEITO** pela Champion Daniela em 2026-09-23 — “CORRETO”

## Pré-condições confirmadas

- Fase 1 encerrada formalmente em 2026-09-21 com `check-fase-1 APROVADO` pelo consultor Navaar.
- Pacote da Fase 1 arquivado em `05_entregas/fase-1/`.
- Período controlado de referência: B-107, competência `2026-08`, com quatro itens do recorte emendado.
- Nenhum dado real novo é necessário para esta task.

## B-201 — fórmula operacional aprovada

A Champion aprovou que a consolidação financeira deve ser orientada por **conciliação bancária mediante exportação de arquivo OFX**, observando:

1. **Aportes:** são as entradas identificadas na conciliação bancária.
2. **Saídas:** são as contas a pagar identificadas na conciliação bancária.
3. **Alocação:** as despesas devem ser destinadas aos centros de custos correspondentes.
4. **Saldo:** deve refletir o saldo apurado no banco.

### Limites preservados

- Esta decisão define a fonte e a lógica operacional, mas não inventa percentuais, centros de custo, regras de identificação de transação, arquivos OFX, contas bancárias ou lançamentos.
- A consolidação deve manter rastreabilidade entre transação OFX, lançamento atômico, documento/referência e centro de custo quando disponíveis.
- Transação sem correspondência, centro de custo ou evidência suficiente deve permanecer como pendência nomeada; não pode ser alocada silenciosamente.
- A F2-T01 não baixou, importou ou processou arquivo OFX e não criou integração bancária.

## B-202 — regime temporal aprovado

- **Regime:** data efetiva do pagamento.
- **Regra:** a consolidação deve agrupar a movimentação pela data efetiva em que o pagamento ocorreu, conforme registrada na conciliação bancária/OFX.
- A competência `2026-08` do B-107 permanece como referência histórica do recorte da Fase 1; para a consolidação da Fase 2, o agrupamento temporal aprovado é a data efetiva do pagamento.
- Transação sem data efetiva válida deve ficar fora do agrupamento válido e aparecer como pendência nomeada; não receberá data por inferência.

## Invariantes da SPEC preservados

- Pendência de validação fora de total e saldo, com bloco separado e rastreável (RN-112/RN-202).
- Agregação somente sobre lançamentos atômicos válidos (RN-201).
- Valor corrente do lançamento e trilha append-only, sem recalcular histórico (RN-203).
- Proveniência em todos os números: real, sintético ou estimado (RN-204).
- Consolidação como leitura; nenhuma escrita sobre lançamentos nesta task.
- F2-T02 deverá detalhar o contrato de identificação OFX, mapeamento aos campos existentes, centros de custo e tratamento de pendências antes de qualquer implementação.

## Aceite

- **Champion:** Daniela — decisão recebida no formulário em 2026-09-23 e teste humano confirmado em 2026-09-23: “CORRETO”.
- **Verificação independente:** termo, SPEC, estado, Fase 1 arquivada, Skip e migrations revalidados; nenhum código, migration, ingestão ou alteração de produto foi realizado nesta task.
