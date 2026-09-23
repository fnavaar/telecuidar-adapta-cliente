# Roteiro B-204 — Conferência humana da prestação F2

**Projeto:** MAX Soluções / Telecuidar  
**Task:** F2-T04 — Formalizar roteiro de conferência (B-204)  
**SPEC:** SPEC-2-003 — Explicação rastreável e conferência humana da prestação  
**Dona da conferência:** Champion Daniela  
**Apoio:** Consultor / Ethos  
**Status do roteiro:** padrão F1-T08 formalizado; aceite específico da Champion pendente  
**Data de formalização:** 2026-09-23

## 1. Objetivo e regra de oficialização

Este roteiro formaliza a conferência humana da prestação do período controlado. A prestação só pode ser considerada **oficial** depois que a Champion registrar aceite explícito no registro de conferência correspondente.

A conferência verifica a prestação apresentada pelo Skip, não cria ou corrige números silenciosamente. Qualquer divergência deve ser registrada como pendência com causa, evidência, dono e próximo passo.

O roteiro reutiliza o padrão comprovado na F1-T08 — conferência de totais, pendências, proveniência, rastreio, explicação, histórico e reprocessamento — e o aplica ao dashboard F2-T03.

## 2. Escopo e limites

### Incluído

- consolidação F2-T02 do período `2026-08`;
- dashboard F2-T03;
- tabela por participante/classificação;
- gráfico mínimo de aportes e saídas;
- explicação textual do período;
- pendências fora do gráfico e dos totais;
- proveniência dos números;
- rastreio de números até lançamentos e histórico;
- aceite ou reprovação do formato B-203;
- registro de pendências com causa.

### Fora deste roteiro

- importação ou conciliação de OFX;
- alteração de lançamentos, histórico, planilha ou Drive;
- correção silenciosa de valores;
- criação de centros de custo ou datas efetivas por inferência;
- acesso de diretores/RBAC da F3;
- envio automático, exportação, multi-período ou chatbot;
- aprovação da Fase 3.

## 3. Pré-condições

Antes de iniciar, registrar:

- F2-T01 aceita, com B-201/B-202 definidos;
- F2-T02 aceita, com consolidação somente leitura provada;
- F2-T03 aceita tecnicamente, com dashboard disponível;
- período e fronteira conferidos:
  - competência histórica: `2026-08`;
  - fonte: `08.AGOSTO`;
  - fronteira: boletos e contas a pagar identificadas;
- sessão autenticada da Champion no Preview;
- nenhum dado real novo necessário para a conferência;
- fixture sintética identificada, quando usada, com limpeza própria;
- captura/evidência da versão conferida anexada ao registro.

Se uma pré-condição faltar, não registrar aceite como se a conferência tivesse ocorrido.

## 4. Registro da conferência

Usar um registro com os seguintes campos:

```text
B-204 ID:
Data/hora:
Champion:
Consultor/apoio:
Preview/versão:
Período:
Fonte/fronteira:
Tipo de conferência: sintética controlada | real autorizada
Resultado: ACEITO | ACEITO COM PENDÊNCIAS | REPROVADO
Observações:
Pendências vinculadas:
Evidências/capturas:
```

O registro deve preservar a resposta literal ou trecho inequívoco do aceite da Champion. “Parece correto”, silêncio ou resposta sem resultado não fecham o roteiro.

## 5. Passos operacionais

### Passo 1 — Abrir o período e confirmar a identidade

1. Entrar no Preview autenticado.
2. Abrir a seção `Consolidação F2-T02` e o `Dashboard F2-T03`.
3. Confirmar competência, fonte, fronteira e status exibidos.
4. Confirmar que a tela informa leitura derivada da consolidação e não alteração da Fase 1.

**Evidência:** captura do cabeçalho do período e da versão/sessão conferida.

### Passo 2 — Conferir a tabela contra a consolidação

1. Conferir a quantidade de grupos exibidos.
2. Para cada linha, conferir:
   - participante;
   - classificação;
   - aporte;
   - saída;
   - quantidade de lançamentos;
   - proveniência.
3. Comparar cada valor da tabela com o valor correspondente retornado pela consolidação F2-T02.
4. Não recalcular ou ajustar o valor na tela.

**Resultado esperado no B-107 sintético:**

- Francisco Figueiredo × Investimento/Ativo Imobilizado: saída R$ 1.945,00, 1 lançamento;
- Geraldo Tadeu × Despesa Operacional: saída R$ 438,99, 2 lançamentos;
- saídas válidas totais: R$ 2.383,99;
- aportes: R$ 0,00 no recorte.

### Passo 3 — Conferir o gráfico

1. Confirmar que o gráfico representa somente grupos válidos da consolidação.
2. Confirmar que as séries exibidas são aportes e saídas.
3. Confirmar que os rótulos correspondem aos participantes/classificações da tabela.
4. Confirmar que a proveniência está visível no contexto/tooltip/legenda do gráfico.
5. Procurar a pendência `Adapta` no gráfico.

**Resultado esperado:** `Adapta` não aparece no gráfico de valores. Ela deve aparecer somente no bloco de pendências.

### Passo 4 — Conferir a explicação rastreável

Para cada frase da explicação, identificar o número de origem:

| Afirmação | Número de origem | Rastreio esperado |
|---|---|---|
| Período e quantidade de lançamentos válidos | competência e `lancamentos_validos` | consolidação → período/lancamentos |
| Total de aportes | `resumo.aportes` | consolidação → lançamentos do tipo Aporte |
| Total de saídas | `resumo.saidas` | consolidação → lançamentos válidos do tipo Saída |
| Quantidade/valor de pendências | `resumo.pendencias` | consolidação → itens pendentes |
| Saldo bancário indisponível | `saldo_bancario` + B-201 | bloqueio nomeado; não calcular a partir de lançamentos |

A frase deve ser descritiva e derivável. Adjetivo, meta, comparação ou conclusão financeira que não tenha número de origem deve ser tratado como divergência.

### Passo 5 — Conferir pendências

1. Confirmar a contagem e o valor do bloco de pendências.
2. Confirmar que cada pendência tem descrição, valor, motivo, origem e proveniência.
3. Confirmar que a pendência não entra em total válido, saldo ou gráfico.
4. No B-107 sintético, confirmar:
   - `Adapta`;
   - valor R$ 5.833,33;
   - documento ausente;
   - status pendente;
   - origem `periodo_itens`.

### Passo 6 — Conferir proveniência

Conferir que cada número exibido traz uma etiqueta de proveniência:

- `real`, se houver fonte real autorizada;
- `sintetico`, para o B-107 controlado;
- `estimado`, quando o número for explicitamente estimativa;
- `indisponivel`, quando o insumo necessário não existir.

No B-107 sintético, os números devem indicar `sintetico · B-107 / 08.AGOSTO`. O saldo bancário deve permanecer `Indisponível`, com B-201 nomeado.

### Passo 7 — Rastrear um número até o lançamento

1. Escolher pelo menos um grupo da tabela.
2. Abrir a origem/lançamento correspondente.
3. Conferir ID, descrição, valor, participante, classificação e referência documental.
4. Abrir o histórico do lançamento quando disponível.
5. Confirmar `Criacao` e, se houver correção, `Correcao` com antes/depois, ator e correlação.
6. Confirmar que a prestação usa o valor corrente e não recalcula o histórico.

### Passo 8 — Conferir o estado vazio e os bloqueios

Quando o período não tiver itens ativos, confirmar:

- `Dashboard vazio`/consolidação vazia explícita;
- nenhum número parcial ou zero inventado;
- B-201/B-202 exibidos como indisponibilidades nomeadas;
- ausência de grupos, gráfico de valores e explicação numérica parcial.

### Passo 9 — Registrar resultado

Escolher exatamente um resultado:

- **ACEITO:** todos os passos passaram; prestação pode ser considerada oficial para o escopo definido;
- **ACEITO COM PENDÊNCIAS:** divergências não impeditivas foram registradas com causa, dono e prazo/condição;
- **REPROVADO:** existe afirmação não derivável, divergência de total, pendência plotada como valor, proveniência ausente ou rastreio quebrado.

Não usar “aceito” sem registrar a decisão e as evidências.

## 6. Matriz dos critérios da SPEC-2-003

| Critério | Prova no roteiro | Evidência mínima | Resultado binário |
|---|---|---|---|
| CA-2-012 | Passos 2, 4 e 7: cada frase e total são ligados à consolidação e ao lançamento | tabela de rastreio + captura/ID do lançamento | PASSOU se todas as afirmações têm origem; caso contrário REPROVADO |
| CA-2-013 | Passo 9: registro com Champion, data/hora, resultado e evidências | registro B-204 no repo/chat | PASSOU somente com aceite explícito ou pendências formalizadas |
| CA-2-014 | Passo 6: proveniência conferida em cartões, tabela, gráfico e pendências | captura do dashboard + observação de cada número | PASSOU se todos os números têm rótulo |
| CA-2-015 | Passos 2, 4, 5 e 9: divergência não é ajustada silenciosamente | registro da divergência com causa/dono/próximo passo | PASSOU se toda divergência vira pendência nomeada |

## 7. Tratamento de divergências e ambiguidades

### Divergência de total

- parar a conferência no item divergente;
- preservar o valor observado e a fonte;
- registrar a diferença e a causa conhecida/desconhecida;
- não editar lançamento, planilha ou dashboard para fazer coincidir;
- classificar como pendência e definir responsável pela reconferência.

### Afirmação não derivável

- marcar a frase como não rastreável;
- reprovar a explicação para fins de oficialização;
- não substituir por adjetivo ou estimativa;
- pedir correção documental/técnica e repetir a conferência.

### Aceite ambíguo

- não converter “ok?”, “parece certo” ou silêncio em aceite;
- solicitar resposta inequívoca: `ACEITO`, `ACEITO COM PENDÊNCIAS` ou `REPROVADO`;
- manter a prestação não oficial até a resposta explícita.

### Falha de leitura

- registrar erro e horário;
- não usar cache ou números anteriores;
- repetir manualmente após a disponibilidade;
- manter a prestação não oficial enquanto não houver leitura completa.

## 8. Registro-modelo de execução

```markdown
# Registro de conferência B-204 — <período>

- B-204 ID: <identificador>
- Data/hora: <ISO-8601>
- Champion: Daniela
- Consultor/apoio: <nome>
- Preview/versão: <URL e versão>
- Período/fonte/fronteira: <valores>
- Tipo: sintética controlada | real autorizada
- Tabela: PASSOU | FALHOU — <observação>
- Gráfico: PASSOU | FALHOU — <observação>
- Explicação: PASSOU | FALHOU — <observação>
- Pendências: PASSOU | FALHOU — <observação>
- Proveniência: PASSOU | FALHOU — <observação>
- Rastreio: PASSOU | FALHOU — <observação>
- Divergências: nenhuma | <lista com causa/dono>
- Resultado: ACEITO | ACEITO COM PENDÊNCIAS | REPROVADO
- Aceite literal da Champion: <trecho e data/hora>
- Evidências: <caminhos/links>
```

O registro de execução deve ser criado somente quando a Champion executar a conferência. Este roteiro, por si só, não constitui aceite da prestação.

## 9. Provas de segurança e integridade

- O roteiro não concede permissões nem cria integrações.
- Nenhum segredo, token, documento ou dado pessoal deve ser copiado para o registro.
- O registro deve usar IDs, valores e referências já visíveis no sistema, sem anexar conteúdo documental sensível.
- Fixtures sintéticas devem ser limpas após a prova, usando rollback/rotina autorizada.
- O roteiro não autoriza ingestão de dados reais.

## 10. Critério de parada

A F2-T04 só pode ser considerada concluída quando:

1. a Champion conferir e aceitar este roteiro ou declarar pendências com causa;
2. o registro de execução for anexado quando a conferência ocorrer;
3. CA-2-013 estiver sustentado por evidência explícita;
4. F2-T05 permanecer bloqueada até este aceite.

**Aceite do roteiro B-204:** pendente — aguardar conferência humana da Champion.
