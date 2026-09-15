# Evidência F1-T08 — Demonstração, histórico e baseline

**Task:** F1-T08  
**SPEC:** SPEC-1-004 — Primeiro período controlado, histórico e baseline  
**Pré-condição:** F1-T07 aceita pela Champion em 2026-09-15  
**Preview:** `https://financeiro-telecuidar-91e6d--preview.goskip.app`  
**Versão Skip implementada:** 0.0.20 (`1211cfc`)  
**Correção de ambiente:** 0.0.21 (`027719e`)  
**Migration:** `0006_periodo_historico_baseline` aplicada

## Implementação

- Painel `Demonstração F1-T08 · histórico e baseline` adicionado ao preview.
- Endpoint autenticado de histórico do período: abertura, conferência, criação, correção, reprocessamento e rollback, com antes/depois, ator, correlação e horário.
- Endpoint autenticado de reprocessamento idempotente: registra o evento sem criar itens ou lançamentos duplicados.
- Coleção `periodo_baselines` para registrar tipo (`medido`/`estimativa`), métrica, unidade, resultado, fonte, método e observações.
- Validação: resultado do tipo `estimativa` exige o marcador `[ESTIMATIVA]`; não há meta ou alvo automático.
- Correção de ambiente: limpeza autenticada e idempotente das três fixtures legadas da F1-T04, protegida por allowlist de IDs e metadados.

## Critérios e provas automatizadas

### CA-1-023 — correção, reprocessamento, histórico e não duplicidade

**PASSOU.** Smoke autenticado com fixture sintética B-107:

- Histórico do período: HTTP 200.
- Resumo: 4 itens, 3 conferidos, 1 pendência, 3 lançamentos rastreáveis, total válido de R$ 2.383,99.
- Correção do `Papel de Parede`: HTTP 200; histórico do lançamento: HTTP 200 com `Criacao` e `Correcao`, antes/depois, ator, correlação e horários.
- Reprocessamento: 3 chamadas HTTP 200; cada uma informou 4 itens existentes, 3 lançamentos existentes, `novos_itens=0` e `novos_lancamentos=0`.
- Histórico final: 3 eventos de `Reprocessamento`, sem duplicação dos 3 lançamentos rastreáveis.

### CA-1-024 — demonstração e baseline

**PASSOU no automatizado.**

- Painel visual exibe resumo do período, histórico detalhado e formulário de baseline.
- Baseline registrado: HTTP 201, tipo `estimativa`, resultado `[ESTIMATIVA] sem medição prévia`, fonte e método explícitos, sem meta inventada.
- Repetição do mesmo baseline: HTTP 200 idempotente, sem novo registro.
- Histórico final retornou HTTP 200 com o baseline persistido.

### Limpeza do ambiente sintético

**PASSOU.**

- Antes: exatamente os três lançamentos legados F1-T04 identificados por ID, descrição, data, valor, referência documental e tipo.
- Limpeza restrita: HTTP 200, removeu exatamente os IDs `d3irl8lgoz0vjc7`, `y8qisnzjjaqnte3` e `00v5e6vlern16rb`.
- Segunda chamada: HTTP 200 idempotente, `removidos=0`, `ausentes=3`.
- Após a limpeza: listagem de lançamentos sem registros; nenhum lançamento fora da allowlist foi tocado.
- Histórico do período B-107: HTTP 200, status `rollback`, sem itens, sem pendências e sem total válido.

## QA e segurança

- QA oficial Skip 0.0.20 (`1211cfc`): setup, análise estática, build, integrações e testes — todos OK.
- QA da correção Skip 0.0.21 (`027719e`): setup, análise estática, build, integrações e testes — todos OK.
- Migration 0006 aplicada.
- Nenhum PDF foi baixado ou aberto; nenhum dado real foi ingerido ou alterado.
- A causa e a correção estão registradas em `06_notas/debug/debug-2026-09-15-f1-t08-fixtures-legadas.md`.
- A fixture B-107 continua sintética; após novo teste humano, usar `Rollback do recorte` para removê-la caso seja reaberta.
- Não publicar nem iniciar F2 nesta task.

## Roteiro de novo teste humano

1. Abrir o preview e entrar com seu acesso.
2. Confirmar que a lista `Lançamentos registrados` não exibe mais os três lançamentos legados da F1-T04.
3. Se o recorte B-107 estiver aberto no ambiente, conferir o painel de demonstração: histórico, baseline `[ESTIMATIVA]` e reprocessamento sem duplicidade.
4. Confirmar que nenhum registro real ou lançamento fora das três fixtures foi removido.
5. Se o B-107 tiver sido reaberto para a validação, executar `Rollback do recorte` ao final.

**Resultado esperado:** os três lançamentos legados não aparecem mais; nenhum dado real é afetado; histórico, baseline, reprocessamento e rollback continuam funcionando.

## Estado de parada

A correção foi implementada e verificada. A F1-T08 aguarda novo teste humano da Champion; não concluir nem iniciar outra task antes da confirmação.
