# Evidência F1-T08 — Demonstração, histórico e baseline

**Task:** F1-T08  
**SPEC:** SPEC-1-004 — Primeiro período controlado, histórico e baseline  
**Pré-condição:** F1-T07 aceita pela Champion em 2026-09-15  
**Preview:** `https://financeiro-telecuidar-91e6d--preview.goskip.app`  
**Versão Skip implementada:** 0.0.20 (`1211cfc`)  
**Correção de ambiente:** 0.0.21 (`027719e`)  
**Migration:** `0006_periodo_historico_baseline` aplicada

## Aceites humanos

- Teste humano inicial: os critérios funcionaram, mas foram reportados três lançamentos legados remanescentes.
- Correção testada e confirmada pela Champion em 2026-09-15: **“confirmado”**.

## Implementação

- Painel `Demonstração F1-T08 · histórico e baseline` adicionado ao preview.
- Endpoint autenticado de histórico do período: abertura, conferência, criação, correção, reprocessamento e rollback, com antes/depois, ator, correlação e horário.
- Endpoint autenticado de reprocessamento idempotente: registra o evento sem criar itens ou lançamentos duplicados.
- Coleção `periodo_baselines` para registrar tipo (`medido`/`estimativa`), métrica, unidade, resultado, fonte, método e observações.
- Validação: resultado do tipo `estimativa` exige o marcador `[ESTIMATIVA]`; não há meta ou alvo automático.
- Correção de ambiente: limpeza autenticada e idempotente das três fixtures legadas da F1-T04, protegida por allowlist de IDs e metadados.

## Critérios e provas automatizadas

### CA-1-023 — correção, reprocessamento, histórico e não duplicidade

**PASSOU.** Revalidação final com fixture sintética B-107:

- Histórico do período: HTTP 200.
- Resumo: 4 itens, 3 conferidos, 1 pendência, 3 lançamentos rastreáveis, total válido de R$ 2.383,99.
- Correção do `Papel de Parede`: HTTP 200; histórico do lançamento: HTTP 200 com `Criacao` e `Correcao`, antes/depois, ator, correlação e horários.
- Reprocessamento: duas chamadas HTTP 200; cada uma informou 4 itens existentes, 3 lançamentos existentes, `novos_itens=0` e `novos_lancamentos=0`.
- Histórico final preservou os eventos de reprocessamento sem duplicação dos lançamentos.

### CA-1-024 — demonstração e baseline

**PASSOU.**

- Painel visual exibiu resumo do período, histórico detalhado e formulário de baseline.
- Baseline persistido como `estimativa`, resultado `[ESTIMATIVA] sem medição prévia`, com fonte, método e sem meta inventada.
- Repetição do baseline permaneceu idempotente.
- A Champion confirmou o funcionamento no teste humano.

### Limpeza do ambiente sintético

**PASSOU.**

- As três fixtures legadas F1-T04 foram identificadas por allowlist e removidas na versão 0.0.21; repetição da limpeza foi idempotente.
- Após a revalidação final do B-107, rollback HTTP 200 removeu 4 itens e 3 lançamentos sintéticos.
- Consulta final autenticada: listagem de lançamentos HTTP 200 com `total=0`; histórico do período HTTP 200 em `rollback`, sem itens e sem total válido.
- Nenhum lançamento fora da allowlist foi tocado.

## QA e segurança

- QA oficial Skip 0.0.20 (`1211cfc`): setup, análise estática, build, integrações e testes — todos OK.
- QA da correção Skip 0.0.21 (`027719e`): setup, análise estática, build, integrações e testes — todos OK.
- Migrations 0001–0006 aplicadas.
- Nenhum PDF foi baixado ou aberto; nenhum dado real foi ingerido ou alterado.
- A causa e a correção estão registradas em `06_notas/debug/debug-2026-09-15-f1-t08-fixtures-legadas.md`.
- Secret-pattern scan da evidência e do Debug Summary: limpo.
- Fase 2 não foi iniciada nem publicada.

## Estado de fechamento

F1-T08 concluída após teste humano confirmado e revalidação independente final. A Fase 1 tem 8/8 tasks concluídas e aguarda validação do consultor; não iniciar F2 automaticamente.
