# SPEC-2-003 — Explicação rastreável e conferência humana da prestação

**Fase:** 2  
**Status:** planejada  
**Dono:** Champion Daniela + Consultor; apoio Ethos  
**Origem no escopo:** §5 Fase 2 ("explicação rastreável e conferência humana"); AC-004/DH-03; critérios globais 3 e 4; EV-F1-04/05  
**Degrau da solução:** reuso da consolidação e do dashboard — a explicação é derivada dos dados consolidados; a conferência é roteiro operacional com registro, não nova construção.

## Contexto e decisões fechadas

- **Estado atual:** a F1 provou correção append-only com antes/depois, reprocessamento idempotente e conferência item a item contra a planilha (RN-131); o painel de demonstração da F1-T08 não gera explicação textual do período.
- **Estado desejado:** toda prestação exibida (consolidação e dashboard) tem explicação rastreável — cada afirmação deriva de números rastreáveis a lançamentos — e passa por conferência humana registrada da Champion antes de ser considerada oficial.
- **Decisões já fechadas:** explicação deriva somente de dados consolidados (RN-210); nenhum adjetivo não derivável; proveniência em tudo (EV-F1-04); valor corrente + trilha (EV-F1-05); IA não gera prestação (escopo §6 — decisão financeira/agente fora; a explicação é determinística, derivada dos dados).
- **Bloqueios:** B-204 (roteiro de conferência da prestação — passos e registro do aceite da Champion — não formalizado; sem ele, a conferência segue o padrão da F1-T08: roteiro executado + aceite registrado no chat e no repo).

## Resultado observável

A Champion executa a conferência da prestação do período controlado com roteiro registrado: verifica totais, pendências, proveniência, rastreio e explicação; registra o aceite (ou as pendências com causa) e a prestação passa a ser oficial para consumo futuro pelos diretores na F3.

## Limites e dependências

- **Inclui:** roteiro de conferência; registro do aceite/pendências; explicação rastreável verificada; fechamento documental da F2.
- **Fora de escopo:** envio automático a diretores; multi-período; migração integral; métricas/alvo (F4, G-05); chatbot.
- **Entradas e pré-condições:** SPEC-2-001 e SPEC-2-002 aceitas; período B-107; B-204 resolvido ou padrão F1-T08 declarado.
- **Saídas/artefatos:** roteiro + registro de conferência no repo; STATUS/changelog da F2 atualizados.
- **Atores e permissões mínimas:** Champion Daniela; consultor valida o fechamento documental.
- **Superfícies afetadas:** nenhum código novo obrigatório; roteiro/registro documentais.
- **Risco e plano B:** explicação afirmar algo não derivável → reprova na conferência; conferência reprovar → prestação não vira oficial e pendências ficam visíveis com causa.
- **Rollback:** documental; prestação não oficial não é publicada.

## Dados e integrações

| Regra de negócio | Condição | Ação/resultado | Exceção | Fonte |
|---|---|---|---|---|
| RN-212 | afirmação da explicação | cada afirmação cita o número consolidado de origem | nenhuma | §5 F2 |
| RN-213 | conferência humana | prestação oficial somente com aceite registrado | nenhuma | critério global 3 |
| RN-214 | divergência na conferência | pendência com causa; sem ajuste silencioso | nenhuma | RN-131 |
| RN-215 | proveniência na prestação oficial | rótulo real/sintético/estimado presente na prestação conferida | nenhuma | EV-F1-04 |

## Fluxo e regras

1. Champion abre consolidação e dashboard do período.
2. Executa o roteiro: totais, pendências à parte, proveniência, drill-down, explicação.
3. Registra aceite ou pendências com causa (RN-213/214).
4. Consultor valida o fechamento documental da F2 (gate de transição F2→F3).

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | prestação consistente | aceite registrado; prestação oficial | — |
| Limite | afirmação não derivável | reprova; correção da explicação | reexecutar conferência |
| Falha | divergência de totais | pendência com causa; prestação não oficial | resolver e reconferir |

## Instruções de execução para o Ethos

1. **Ler antes de alterar:** SPEC-2-001/002, roteiro F1-T08, critérios globais 3/4, B-204.
2. **Alterar somente:** roteiro e registro documentais da conferência.
3. **Não alterar:** dados, regras, telas já aceitas, permissões.
4. **Executar nesta ordem:** B-204 → roteiro → conferência → registro → fechamento.
5. **Parar e pedir validação quando:** qualquer afirmação não rastreável; aceite ambíguo.
6. **Estado válido ao parar:** prestação com proveniência e aceite registrados, ou pendências visíveis.

## Checklist de execução

- [ ] B-204 conferido ou padrão F1-T08 declarado
- [ ] Roteiro executado com registro
- [ ] Explicação verificada afirmação a afirmação
- [ ] Aceite/pendências registrados no repo
- [ ] STATUS/changelog da F2 atualizados

## Critérios de aceite

- [ ] **CA-2-012:** toda afirmação da explicação cita número consolidado rastreável a lançamento.
- [ ] **CA-2-013:** conferência humana da prestação registrada com aceite ou pendências com causa.
- [ ] **CA-2-014:** prestação oficial carrega proveniência (real/sintético/estimado) em todos os números.
- [ ] **CA-2-015:** divergência encontrada na conferência virou pendência com causa, sem ajuste silencioso.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | explicação atual sem rastreio afirmação→número | varrer explicações do dashboard | afirmações não rastreáveis expostas | relatório RED |
| GREEN | explicação rastreável + roteiro | executar conferência com a Champion | CA-2-012..014 passam | registro + capturas |
| REGRESSÃO | conferência com divergência induzida | inserir divergência conhecida em fixture isolada | CA-2-015: pendência com causa, sem ajuste silencioso | registro da pendência |

**Fixtures:** nenhuma nova; usa o período B-107 e fixtures isoladas existentes.
**Caminhos de erro obrigatórios:** afirmação não derivável; divergência de totais; aceite ambíguo.
**Evidência exigida:** roteiro + registro de conferência no repo; aceite humano da Champion.

## Handoff e operação

- **Como demonstrar:** executar o roteiro de conferência no preview com a Champion e registrar o resultado.
- **Como operar depois:** toda prestação de período novo repete o roteiro antes de oficial.
- **Como monitorar:** pendências de conferência ficam visíveis com causa e dono.
- **Pendência conhecida:** envio/consulta pelos diretores só após F3 (contas individuais, DH-04/G-04).

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| F2-T04 | Formalizar roteiro de conferência (B-204) | Champion + Consultor | SPEC-2-003 | CA-2-013 (gate de insumo) | B-204 registrado ou padrão F1-T08 declarado | Roteiro com aceite da Champion | F2-T03 aceita | ☐ |
| F2-T05 | Executar a conferência da prestação e fechar a F2 | Champion + Consultor | SPEC-2-003 | CA-2-012..015 | Conferência executada + registro | Roteiro executado, aceite/pendências, STATUS/changelog | F2-T04 aceita | ☐ |

## Emendas

<!-- Append-only (D19): mudanças aprovadas depois da geração. A história não é reescrita. -->

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
