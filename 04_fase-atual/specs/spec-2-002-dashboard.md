# SPEC-2-002 — Dashboard e prestação visual do período

**Fase:** 2  
**Status:** planejada  
**Dono:** Ethos; validação da Champion Daniela  
**Origem no escopo:** RQ-05 (dashboard → F2); AC-004/DH-03 (prestação compreensível); §5 Fase 2; EV-F1-03/04/07  
**Degrau da solução:** construção mínima sobre a consolidação da SPEC-2-001 — o dashboard visualiza o que a consolidação calcula; não recalcula nada.

## Contexto e decisões fechadas

- **Estado atual:** a F1 entregou painel de demonstração do período com histórico e baseline `[ESTIMATIVA]` (F1-T08, Skip 0.0.21); não existe dashboard de prestação por participante/classificação.
- **Estado desejado:** dashboard do período com tabela, gráfico e explicação simples, consumindo exclusivamente a consolidação da SPEC-2-001.
- **Decisões já fechadas:** pendências nunca em gráfico de valores (bloco separado, EV-F1-03); proveniência visível (EV-F1-04); UI/UX simples e compreensível (AC-004/DH-03 — prestação que Daniela explica aos diretores); telas não pressupõem papéis da F3 (EV-F1-07); dados reais somente após política/allowlist vigentes.
- **Bloqueios:** B-203 (formato final da prestação visual — tabela/gráfico/explicação — não validado pela Champion; sem aceite de formato, o dashboard entrega tabela consolidada + gráfico mínimo e o formato segue para conferência humana da task).

## Resultado observável

No preview, a Champion abre o dashboard do período controlado: tabela consolidada, gráfico de aportes/saídas por participante e explicação simples do período — todos os números rastreáveis à consolidação e desta aos lançamentos.

## Limites e dependências

- **Inclui:** dashboard do período (tabela, gráfico, explicação); leitura exclusiva da consolidação; conferência humana antes de disponibilizar.
- **Fora de escopo:** acesso dos diretores (F3, DH-04/G-04); multi-período e histórico comparativo; exportação automática; alertas/notificações; chatbot (F4).
- **Entradas e pré-condições:** SPEC-2-001 aceita (consolidação provada); período B-107 carregado; B-203 resolvido ou formato mínimo declarado.
- **Saídas/artefatos:** telas de dashboard no Skip autorizado; evidência no repo.
- **Atores e permissões mínimas:** Champion Daniela; nenhum papel novo.
- **Superfícies afetadas:** telas do projeto Skip; nenhuma rota de escrita.
- **Risco e plano B:** gráfico distorcer leitura (ex.: pendência aparentando valor) → prova negativa obrigatória; formato rejeitado → tabela consolidada permanece como entrega mínima.
- **Rollback:** telas são leitura — remoção reversível; consolidação intacta.

## Dados e integrações

| Origem/destino | Fonte de verdade | Campos/contrato | Autenticação/permissão | Timeout/retry/idempotência | Tratamento de erro |
|---|---|---|---|---|---|
| Consolidação (SPEC-2-001) | rotas server-side de agregação | totais, pendências, proveniência | sessão do preview | leitura pura | erro → tela de erro sem números parciais |

| Regra de negócio | Condição | Ação/resultado | Exceção | Fonte |
|---|---|---|---|---|
| RN-207 | dashboard | exibe somente números da consolidação; nenhuma fórmula própria | nenhuma | SPEC-2-001 |
| RN-208 | pendência no dashboard | bloco separado (contagem+valor); nunca em gráfico de valores | nenhuma | EV-F1-03 |
| RN-209 | proveniência | rótulo visível em tabela e gráfico | nenhuma | EV-F1-04 |
| RN-210 | explicação simples | texto gerado dos dados consolidados, sem adjetivo não derivável | nenhuma | AC-004/DH-03 |
| RN-211 | conferência humana | dashboard só é "prestação oficial" após conferência registrada da Champion | nenhuma | critério global 3 |

## Fluxo e regras

1. Champion abre o dashboard do período no preview.
2. Tabela consolidada, gráfico e explicação carregam da consolidação (RN-207).
3. Pendências aparecem à parte (RN-208); proveniência visível (RN-209).
4. Champion confere e registra o aceite do formato (B-203/RN-211).

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | período 2026-08 | tabela+gráfico+explicação batem com a consolidação | divergência → bug, não ajuste |
| Limite | período vazio | dashboard vazio explícito | — |
| Prova negativa | pendência presente | pendência NÃO aparece no gráfico de valores | falha → reprova |
| Falha | consolidação indisponível | erro explícito; dashboard não renderiza números parciais | retry manual |

## Instruções de execução para o Ethos

1. **Ler antes de alterar:** SPEC-2-001, escopo §5 F2/AC-004/DH-03, delta-fase-2, B-203.
2. **Alterar somente:** telas de dashboard no Skip autorizado.
3. **Não alterar:** rotas de consolidação, lançamentos, regras, permissões, fases futuras.
4. **Executar nesta ordem:** B-203 → RED (prova negativa da pendência fora do gráfico) → GREEN → REGRESSÃO → conferência humana.
5. **Parar e pedir validação quando:** formato divergir do aceito; qualquer número não rastreável.
6. **Estado válido ao parar:** dashboard lê e não escreve; prestação oficial só após conferência registrada.

## Checklist de execução

- [ ] B-203 conferido ou formato mínimo declarado
- [ ] Prova negativa da pendência fora do gráfico executada
- [ ] Caminhos principal, limite e falha exercitados
- [ ] Varredura de segredos/dados fora do recorte limpa
- [ ] Conferência humana da Champion registrada

## Critérios de aceite

- [ ] **CA-2-007:** dashboard exibe tabela, gráfico e explicação do período consumindo exclusivamente a consolidação (nenhuma fórmula própria).
- [ ] **CA-2-008:** pendência de validação nunca aparece em gráfico de valores — bloco separado com contagem e valor.
- [ ] **CA-2-009:** todo número do dashboard tem proveniência visível e é rastreável até o lançamento.
- [ ] **CA-2-010:** explicação do período é derivada dos dados consolidados, sem adjetivo não derivável.
- [ ] **CA-2-011:** Champion confere o dashboard e registra aceite do formato (B-203) antes de qualquer disponibilização.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | dashboard inexistente; pendência somada/plotada como valor | abrir preview atual com pendência ativa | ausência/falha ligada a CA-2-007/008 | relatório RED |
| GREEN | dashboard do período B-107 | telas + comparar com consolidação | CA-2-007..010 passam | capturas + evidência |
| REGRESSÃO | reprocessamento e correção no período | repetir provas F1; conferir dashboard pós-correção | CA-2-009 sem regressão F1; aceite humano (CA-2-011) | trilha + registro do aceite |

**Fixtures:** período B-107 + fixtures sintéticas isoladas com limpeza própria; nenhum dado real novo.
**Caminhos de erro obrigatórios:** período vazio; consolidação indisponível; pendência ativa; formato rejeitado.
**Evidência exigida:** capturas do preview + registro do aceite da Champion no repo.

## Handoff e operação

- **Como demonstrar:** abrir dashboard do período, conferir tabela/gráfico/explicação, verificar pendências à parte, rastrear um número até o lançamento.
- **Como operar depois:** a prestação é oficial somente após conferência registrada da Champion.
- **Como monitorar:** divergência dashboard×consolidação é bug e vira pendência técnica.
- **Pendência conhecida:** acesso dos diretores e contas individuais ficam na F3.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| F2-T03 | Construir e provar o dashboard do período | Ethos | SPEC-2-002 | CA-2-007..011 | RED prova negativa + GREEN + conferência humana | Capturas, evidência, aceite do formato | F2-T02 aceita; B-203 | ☐ |

## Emendas

<!-- Append-only (D19): mudanças aprovadas depois da geração. A história não é reescrita. -->

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
