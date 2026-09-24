# Registro de conferência B-204 — 2026-08

- **B-204 ID:** B204-2026-08-20260924-1349
- **Data/hora:** 2026-09-24T13:49:56-03:00
- **Champion:** Daniela — conferência executada no Preview com autorização do proprietário
- **Consultor/apoio:** Ethos
- **Preview/versão:** `https://financeiro-telecuidar-91e6d--preview.goskip.app` · Skip 0.0.25 (`21a7adb`)
- **Período/fonte/fronteira:** `2026-08` · `08.AGOSTO` · boletos e contas a pagar identificadas
- **Tipo:** sintética controlada; nenhum OFX e nenhum dado real processado
- **Resultado preliminar:** **ACEITO**, pendente de confirmação humana final do resultado nesta task

## Pré-condições

- F2-T01 aceita com B-201/B-202 definidos.
- F2-T02 aceita e consolidação somente leitura disponível.
- F2-T03 aceita e dashboard disponível.
- B-204 aceito pela Champion em task anterior.
- Fixture B-107 aberta com quatro itens sintéticos e limpeza própria.

## Conferência executada

- **Tabela:** PASSOU — 2 grupos; Francisco Figueiredo × Investimento/Ativo Imobilizado = R$1.945,00 em 1 lançamento; Geraldo Tadeu × Despesa Operacional = R$438,99 em 2 lançamentos; total de saídas R$2.383,99; aportes R$0,00.
- **Gráfico:** PASSOU — gráfico renderizado sobre grupos válidos; `Adapta` não apareceu no DOM do gráfico.
- **Explicação:** PASSOU — frases derivadas do período, lançamentos válidos, aportes, saídas, pendências e saldo bancário indisponível/B-201; nenhum adjetivo ou número não derivável.
- **Pendências:** PASSOU — `Adapta`, R$5.833,33, documento ausente, origem `periodo_itens`, fora de total/saldo/gráfico.
- **Proveniência:** PASSOU — números sintéticos com `B-107 / 08.AGOSTO`; saldo bancário `Indisponível` com B-201.
- **Rastreio:** PASSOU — `Papel de Parede`, ID `gsdlxwf1f2xti3z`, referência `NF 1 - THAIS BARROS INTERIORES LTDA`; histórico HTTP 200 com evento `Criacao`, antes/depois e correlação `mpFgVnSWsse315y1`.
- **Divergências:** nenhuma; saída observada R$2.383,99 = saída esperada R$2.383,99; diferença R$0,00.
- **Erro/vazio:** PASSOU — período vazio exibiu `PERIODO_VAZIO` sem números inventados; falha simulada de leitura exibiu erro sem números parciais.

## Limpeza

- Rollback B-107 HTTP 200.
- 4 itens removidos.
- 3 lançamentos removidos.
- Consulta final: 0 lançamentos; período `rollback`; resumo nulo; `PERIODO_VAZIO`, B-201 e B-202 nomeados.
- Nenhum OFX, planilha ou Drive tocado.

## Aceite final

O resultado preliminar é `ACEITO` e aguarda a confirmação humana final da Champion nesta task. A prestação só será considerada oficial após esse aceite registrado.
