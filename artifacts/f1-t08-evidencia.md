# Evidência F1-T08 — Demonstração, histórico e baseline

**Task:** F1-T08  
**SPEC:** SPEC-1-004 — Primeiro período controlado, histórico e baseline  
**Pré-condição:** F1-T07 aceita pela Champion em 2026-09-15  
**Preview:** `https://financeiro-telecuidar-91e6d--preview.goskip.app`  
**Versão Skip final:** 0.0.20 (`1211cfc`)  
**Migration:** `0006_periodo_historico_baseline` aplicada

## Implementação

- Painel `Demonstração F1-T08 · histórico e baseline` adicionado ao preview.
- Endpoint autenticado de histórico do período: abertura, conferência, criação, correção, reprocessamento e rollback, com antes/depois, ator, correlação e horário.
- Endpoint autenticado de reprocessamento idempotente: registra o evento sem criar itens ou lançamentos duplicados.
- Coleção `periodo_baselines` para registrar tipo (`medido`/`estimativa`), métrica, unidade, resultado, fonte, método e observações.
- Validação: resultado do tipo `estimativa` exige o marcador `[ESTIMATIVA]`; não há meta ou alvo automático.
- Correções de compatibilidade do runtime PocketBase: removido spread incompatível no hook de reprocessamento e corrigida a referência do array de eventos no histórico.

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

## QA e segurança

- QA oficial Skip 0.0.20 (`1211cfc`): setup, análise estática, build, integrações e testes — todos OK.
- Migration 0006 aplicada.
- Os erros encontrados no primeiro smoke foram corrigidos e revalidados após novo deploy.
- Nenhum PDF foi baixado ou aberto; nenhum dado real foi ingerido ou alterado.
- A fixture atual é sintética e permanece disponível no preview para o teste humano; deve ser removida com o botão `Rollback do recorte` após a validação.
- Não publicar nem iniciar F2 nesta task.

## Roteiro de teste humano

1. Abrir o preview e entrar com seu acesso.
2. Conferir o painel `Demonstração F1-T08 · histórico e baseline`: período `2026-08`, 4 itens, 3 conferidos, 1 pendência e 3 rastreáveis.
3. Abrir o histórico do `Papel de Parede` e confirmar eventos `Criacao` e `Correcao`, com antes/depois, ator, correlação e horário.
4. No painel de demonstração, clicar `Reprocessar sem duplicar`; esperar mensagem de sucesso com zero novos itens e zero novos lançamentos.
5. Conferir o cartão do baseline com marcador `[ESTIMATIVA]`, unidade, fonte e método.
6. Clicar `Rollback do recorte` no painel B-107 e confirmar a remoção de 4 itens e 3 lançamentos sintéticos.

**Resultado esperado:** todos os passos funcionam sem erro, sem duplicar lançamentos e sem alterar dados reais.  
**Falha:** qualquer erro HTTP, ausência de antes/depois, criação de novo lançamento no reprocessamento, baseline sem `[ESTIMATIVA]` ou resíduos após rollback.

## Estado de parada

Implementação e verificações automatizáveis concluídas. A F1-T08 aguarda teste humano da Champion; não concluir nem iniciar outra task antes da confirmação.
