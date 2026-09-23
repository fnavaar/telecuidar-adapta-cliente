# Evidência F2-T03 — Dashboard e prestação visual do período

**Task:** F2-T03  
**SPEC:** SPEC-2-002 — Dashboard e prestação visual do período  
**Preview:** `https://financeiro-telecuidar-91e6d--preview.goskip.app`  
**Versão final:** Skip 0.0.25 (`21a7adb`)  
**Dependência:** F2-T02 aceita no Skip 0.0.24 (`32d9b9e`)  
**Captura:** `artifacts/f2-t03-dashboard-prestacao.png`

## Implementação

- Componente `DashboardPanel` integrado após a consolidação F2-T02.
- Leitura exclusiva de `getConsolidacao()`; nenhuma rota nova, migration ou escrita criada.
- Tabela da prestação por participante/classificação.
- Gráfico mínimo de aportes e saídas usando somente grupos válidos da consolidação.
- Explicação textual derivada exclusivamente dos valores retornados pela consolidação.
- Pendências em bloco separado, sem serem plotadas como valores.
- Proveniência visível nos cartões, tabela, gráfico e pendências.
- Rastreabilidade da tabela até os lançamentos por origem/ID/referência.
- Estados explícitos de carregamento, erro sem números parciais e período vazio.
- Formato mínimo B-203 declarado; aceite visual da Champion permanece pendente (CA-2-011).

## QA oficial

- Skip 0.0.25 (`21a7adb`): setup, análise estática, build, integrações e testes — **todos OK**.
- Migrations `0001–0006` aplicadas e coleções F1 preservadas.
- Secret-pattern scan no repositório: sem resultados.
- Nenhuma alteração em rota de consolidação, lançamentos, permissões, planilha ou Drive.

## Provas automatizadas e smoke autenticado

### CA-2-007 — tabela, gráfico e explicação da consolidação

**PASSOU.** Com o B-107 sintético conferido, a captura e o DOM mostraram:

- seção `Tabela da prestação`;
- seção `Aportes e saídas por participante/classificação`;
- seção `Explicação do período`;
- 1 gráfico renderizado;
- tabela com Francisco Figueiredo × Investimento/Ativo Imobilizado e Geraldo Tadeu × Despesa Operacional;
- números vindos do endpoint da consolidação, sem fórmula paralela no dashboard.

### CA-2-008 — pendência fora do gráfico

**PASSOU.** `Adapta` e R$ 5.833,33 apareceram somente em `Pendências fora do gráfico e dos totais`. O DOM do gráfico não continha `Adapta`.

### CA-2-009 — proveniência e rastreabilidade

**PASSOU.** Proveniência `sintetico · B-107 / 08.AGOSTO` visível nos cartões, tabela, gráfico e pendência; origem da tabela expõe lançamentos, IDs e referências documentais.

### CA-2-010 — explicação derivada

**PASSOU.** A explicação exibiu somente fatos derivados:

- período `2026-08`;
- quantidade de lançamentos válidos;
- total de aportes;
- total de saídas;
- contagem/valor das pendências fora do gráfico;
- saldo bancário indisponível por OFX não carregado.

Nenhum adjetivo ou número não derivável foi introduzido.

### CA-2-011 — aceite humano/B-203

**PASSOU.** A Champion Daniela conferiu o dashboard no preview e respondeu `teste ok` em 2026-09-23, aprovando o formato mínimo B-203.

### Caminhos obrigatórios

- **Período vazio:** painel exibiu `Dashboard vazio` e não renderizou números parciais.
- **Consolidação indisponível:** falha simulada exibiu `Não foi possível carregar a consolidação; nenhum número parcial foi exibido.`
- **Pendência ativa:** `Adapta` permaneceu fora do gráfico.
- **Correção/reprocessamento:** após correção sintética do Papel de Parede para R$ 2.000,00, a consolidação e o dashboard acompanharam o valor corrente; histórico preservou `Criacao`/`Correcao`; reprocessamento da F2-T02 permaneceu idempotente.
- **Rollback:** HTTP 200 removeu 4 itens e 3 lançamentos; estado final teve 0 lançamentos e `PERIODO_VAZIO`.

## Resultado visual principal

No recorte canônico B-107, a prestação mostrou:

- aportes: R$ 0,00;
- saídas: R$ 2.383,99;
- lançamentos válidos: 3;
- pendências: 1 · R$ 5.833,33;
- saldo bancário: Indisponível;
- grupos: Francisco Figueiredo/R$ 1.945,00 e Geraldo Tadeu/R$ 438,99.

## Limites e segurança

- Nenhum dado real novo processado.
- Nenhum OFX importado.
- Nenhuma credencial, token ou segredo persistido.
- Nenhuma escrita sobre a consolidação ou lançamentos pela tela F2-T03.
- Fixture sintética B-107 limpa ao final.

## Estado de parada

A implementação, a automação e o aceite humano foram concluídos. Não iniciar F2-T04 automaticamente.
