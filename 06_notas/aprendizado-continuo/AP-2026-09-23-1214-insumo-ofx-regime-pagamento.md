# AP-2026-09-23-1214 — Separar conciliação, alocação e regime temporal

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: F2-T01 / SPEC-2-001
- Sinal: a decisão da Champion separou explicitamente a fonte da movimentação (conciliação bancária por OFX), a natureza da movimentação (entradas/aportes e saídas/contas a pagar), a alocação (centro de custo) e o regime temporal (data efetiva do pagamento).
- Evidência: `06_notas/f2-t01-termo-insumos-b201-b202.md`; aceite humano “CORRETO” em 2026-09-23; revalidação independente do termo.
- Regra reutilizável: ao fechar insumos de consolidação, registrar separadamente fonte/transação, natureza, dimensão de alocação e regime temporal; não inferir identificação, centros de custo ou datas ausentes; manter essas ocorrências como pendências nomeadas.
- Quando aplicar: em qualquer consolidação financeira que combine extrato/OFX, lançamentos atômicos, alocação e agrupamento temporal.
- Quando não aplicar: quando a fonte contratual já definir explicitamente todos esses elementos e não houver decisão operacional nova.
- Confiança: alta — decisão explicitamente aceita pela Champion e verificada no termo versionado.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
