# Evidência F2-T02 — Consolidação por período, participante e classificação

**Task:** F2-T02  
**SPEC:** SPEC-2-001 — Consolidação por período, participante e classificação  
**Preview:** `https://financeiro-telecuidar-91e6d--preview.goskip.app`  
**Versão final:** Skip 0.0.24 (`32d9b9e`)  
**Migrations preservadas:** 0001–0006  
**Coleções preservadas:** modelo F1; nenhuma coleção ou migration nova criada

## Implementação

- Rota autenticada `GET /backend/v1/periodos/consolidacao`.
- Painel autenticado `Consolidação F2-T02` integrado à página principal.
- Leitura somente sobre `periodo_itens` e `lancamentos`; nenhuma escrita sobre F1.
- Agrupamento por participante e classificação.
- Aportes e saídas separados pelo tipo de lançamento.
- Pendências fora de total e saldo, com valor, motivo, origem e proveniência.
- Drill-down de cada lançamento agrupado para histórico `Criacao`/`Correcao`.
- Proveniência visível nos números: `sintetico` para o recorte B-107 e `indisponivel` para saldo bancário sem OFX.
- Bloqueios B-201/B-202 exibidos sem inventar OFX, centro de custo ou data efetiva.
- Período vazio retorna consolidação explicitamente vazia, sem transformar ausência em zeros calculados.

## QA oficial

- QA inicial 0.0.22 (`d483072`): setup, análise estática, build e testes passaram; integração reprovou por escopo de funções auxiliares no hook PocketBase.
- Correção 0.0.23 (`87c622e`): funções auxiliares movidas para dentro do callback; QA completo passou.
- Correção de borda 0.0.24 (`32d9b9e`): período vazio explicitamente vazio; QA completo passou.
- Resultado final: setup, análise estática, build, integrações e testes — **todos OK**.
- Migrations 0001–0006 aplicadas; coleções F1 preservadas.

## Smoke autenticado e critérios

### CA-2-001 — período B-107 bate com a conferência

**PASSOU.** Conferência sintética de quatro itens:

- 3 lançamentos rastreáveis;
- 1 pendência documental (`Adapta`);
- total válido de saídas: **R$ 2.383,99**;
- aportes: R$ 0,00 no recorte.

### CA-2-002 — agregação atômica por participante/classificação

**PASSOU.** Dois grupos de saída foram exibidos:

- Francisco Figueiredo × Investimento/Ativo Imobilizado: R$ 1.945,00;
- Geraldo Tadeu × Despesa Operacional: R$ 438,99, composto por Starlink R$339,00 e Vivo R$99,99.

Starlink e Vivo permaneceram lançamentos independentes; nenhum agrupamento foi feito apenas por valor.

### CA-2-003 — pendência fora dos totais

**PASSOU.** Adapta apareceu no bloco separado de pendências por R$ 5.833,33, sem lançamento atômico e fora do total válido.

### CA-2-004 — proveniência

**PASSOU.** Todos os números exibidos carregaram proveniência `sintetico · B-107 / 08.AGOSTO`; saldo bancário foi `Indisponível` com proveniência `indisponivel · B-201`, sem cálculo inventado.

### CA-2-005 — drill-down e histórico

**PASSOU.** O lançamento Papel de Parede abriu histórico HTTP 200 com operações `Criacao` e `Correcao`, preservando antes/depois, ator e correlação.

### CA-2-006 — bloqueio nomeado quando o insumo bancário não existe

**PASSOU.** A consolidação exibiu `B-201-OFX`, `B-201-CENTRO-CUSTO` e `B-202-DATA-EFETIVA`, mantendo saldo bancário indisponível e sem inventar centro de custo ou data efetiva.

### Regressão e recuperação

**PASSOU.**

- Correção append-only do Papel de Parede HTTP 200.
- Dois reprocessamentos HTTP 200:
  - `novos_itens=0`;
  - `novos_lancamentos=0`.
- Histórico do período preservou os eventos de reprocessamento.
- Rollback HTTP 200 removeu 4 itens e 3 lançamentos sintéticos.
- Consulta final: 0 lançamentos e período em `rollback`.
- Consolidação final: bloco `PERIODO_VAZIO`, sem total calculado e com B-201/B-202 nomeados.

## Segurança e limites

- Nenhum OFX importado.
- Nenhum dado real processado.
- Nenhuma alteração na planilha ou no Drive.
- Nenhum lançamento/histórico da F1 alterado fora do recorte sintético B-107.
- Nenhuma credencial, token ou segredo persistido.
- Secret-pattern scan no repositório: **sem resultados**.
- Fixture B-107 limpa ao final.

## Limitação conhecida

O modelo F1 ainda não possui centro de custo, data efetiva bancária ou saldo OFX. A tela deixa esses itens indisponíveis e nomeados; não os infere. A integração/importação OFX não faz parte desta task.

## Estado de parada

Implementação e verificações automatizáveis concluídas. F2-T02 aguarda teste humano da Champion; não concluir nem iniciar F2-T03 antes da confirmação.
