# Debug Summary

**Task e problema:** F1-T08 — após o teste humano, três lançamentos iniciais permaneciam na lista, embora o roteiro da F1-T08 e o rollback do B-107 tivessem funcionado.

**Reprodução:** listagem autenticada de lançamentos retornou exatamente três registros: `Fixture saida pendente F1-T04` (ID `d3irl8lgoz0vjc7`), `Fixture aporte F1-T04 corrigido` (ID `y8qisnzjjaqnte3`), e `Buffet Inauguração` (ID `00v5e6vlern16rb`). Os três tinham referências sintéticas/legadas, datas de 2026-09-11 a 2026-09-13 e históricos antigos da F1-T04; não tinham vínculo com o período B-107.

**Causa raiz:** o rollback da F1-T06 removia a fixture documental e seus lançamentos vinculados, mas não havia uma limpeza explícita para os três lançamentos sintéticos criados nos testes iniciais da F1-T04. O rollback da F1-T08 corretamente limpava apenas o lote B-107, portanto não deveria removê-los.

**Correção:** criada a rota autenticada `/backend/v1/lancamentos/limpar-fixtures-f1-t04`, com allowlist fixa dos três IDs e validação simultânea de descrição, data, valor, referência documental e tipo de lançamento antes de qualquer exclusão; eventos históricos dos três IDs são removidos na mesma transação. Adicionado botão `Limpar fixtures legadas F1-T04` no painel F1-T08.

**Verificação automática:** QA Skip 0.0.21 (`027719e`) passou integralmente. A rota removeu exatamente 3 registros/IDs; segunda chamada HTTP 200 foi idempotente (`removidos=0`, `ausentes=3`); listagem posterior ficou sem lançamentos; histórico do período B-107 respondeu HTTP 200 em `rollback`, sem itens ou total válido.

**Gate atual:** correção aceita; F1-T08 concluída após confirmação humana.
