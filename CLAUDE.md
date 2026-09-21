# Operação do agente — Telecuidar

**Repo do cliente:** https://github.com/fnavaar/telecuidar-adapta-cliente

## Objetivo
Apoiar a construção do núcleo financeiro que substituirá a planilha dinâmica e integrará a pasta financeira do cliente, com rastreabilidade e conferência humana.

## Protocolo
- Fase atual: 2 — Consolidação e prestação visual.
- Única task elegível: F2-T01 (fechar insumos B-201/B-202 com a Champion). F2-T02..T05 bloqueadas por dependência.
- Não invente campo, fórmula, estado, permissão ou dado.
- Uma task por vez; análise e autorização precedem execução; teste humano precede conclusão.
- Invariantes da F2: pendência de validação fora de totais/gráficos (RN-112/202/208); proveniência real/sintético/estimado em todo número (RN-204/209/215); agregação só sobre lançamentos atômicos (RN-201); valor corrente + trilha, sem recálculo (RN-203); fixtures isoladas com limpeza própria (RN-206); fallback B-106 preservado; RBAC/diretores na F3.
- Dados reais: nenhum dado real novo é exigido pela F2; provas usam o período B-107 (competência 2026-08) e fixtures sintéticas isoladas.
- Ação externa exige confirmação imediata.
