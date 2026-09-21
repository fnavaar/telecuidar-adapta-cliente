# SPEC-2-001 — Consolidação por período, participante e classificação

**Fase:** 2  
**Status:** planejada  
**Dono:** Ethos; validação da Champion Daniela  
**Origem no escopo:** RQ-04 (consolidação → F2); §5 Fase 2; EV-F1-01..05 (evoluções aceitas 21/09)  
**Degrau da solução:** reuso das entregas da F1 (lançamentos, catálogo, correção append-only, período B-107) — a consolidação agrega o que a F1 provou, sem novo modelo de origem.

## Contexto e decisões fechadas

- **Estado atual:** o Skip 0.0.21 tem lançamentos atômicos com participante, referência documental, tipo (Aporte/Saída), catálogo aprovado (Anexo E), correção append-only com antes/depois, idempotência provada e um período controlado demonstrado (competência 2026-08, 4 itens, B-107 emendado). Fonte: SPECs F1 + STATUS/changelog do repo (HEAD `9a21fbf`).
- **Estado desejado:** consolidação por período/participante/classificação com aporte, alocação, saldo e pendência, lendo valor corrente + trilha, sem recalcular histórico.
- **Decisões já fechadas:** agregação opera somente sobre lançamentos atômicos com referência documental própria (EV-F1-02); pendência de validação fora de total/saldo (RN-112, EV-F1-03); consolidação lê valor corrente e nunca recalcula histórico (EV-F1-05); todo número exibido carrega proveniência real × sintético × estimado (EV-F1-04); fórmulas e regime temporal vêm da fonte validada na F1 (Anexo F), sem invenção.
- **Bloqueios:** B-201 (fórmulas de consolidação/alocação do Anexo F não cobrem agregação por participante/classificação — insumo da Champion; sem ele, totais por participante ficam indisponíveis, não inventados); B-202 (regime temporal de consolidação — competência × data de pagamento — não declarado pela Champion; sem ele, agrupamento temporal segue o regime já usado no B-107 emendado, competência 2026-08, e mudança posterior exige decisão registrada).

## Resultado observável

No preview, a Champion seleciona o período controlado existente e visualiza a consolidação: aportes, saídas alocadas por participante e classificação, saldo do período e pendências como bloco separado — cada número com proveniência e rastreio aos lançamentos de origem.

## Limites e dependências

- **Inclui:** agregação por período/participante/classificação; aporte/alocação/saldo; pendência fora dos totais; proveniência em todo número; drill-down ao lançamento.
- **Fora de escopo:** dashboard/gráficos (SPEC-2-002); explicação textual rastreável (SPEC-2-003); contas individuais/RBAC dos diretores (F3); loops/agentes (F4); migração integral e descomissionamento da planilha.
- **Entradas e pré-condições:** F1 8/8 concluída (check-fase-1 APROVADO); Anexo F vigente; período B-107 emendado carregado; B-201/B-202 resolvidos ou com regime vigente declarado.
- **Saídas/artefatos:** rotas server-side de consolidação; evidência `artifacts/f2-t02-evidencia.md` (numeração conforme tasks).
- **Atores e permissões mínimas:** Champion Daniela (operação e conferência); sem novos papéis (RBAC é F3).
- **Superfícies afetadas:** projeto Skip autorizado (rotas server-side e telas de consolidação); nenhuma migration de origem além do modelo F1, exceto índices/visões de agregação reversíveis.
- **Risco e plano B:** divergência consolidação×planilha → pendência com causa, sem ajuste silencioso (RN-131); fórmula ausente → total indisponível com bloqueio nomeado, nunca zero inventado.
- **Rollback:** agregação é leitura — reversível por remoção das rotas/telas; nenhuma escrita sobre lançamentos.

## Dados e integrações

| Origem/destino | Fonte de verdade | Campos/contrato | Autenticação/permissão | Timeout/retry/idempotência | Tratamento de erro |
|---|---|---|---|---|---|
| Lançamentos F1 | coleções do Skip (modelo F1) | valor corrente, participante, classificação, tipo, competência, referência, pendência | sessão do preview; sem novos papéis | leitura pura; idempotente por natureza | erro de leitura → tela de erro sem números parciais |

| Regra de negócio | Condição | Ação/resultado | Exceção | Fonte |
|---|---|---|---|---|
| RN-201 | agregação por participante/classificação | soma somente lançamentos válidos atômicos | fórmula ausente (B-201) → valor indisponível + bloqueio nomeado | Anexo F + EV-F1-02 |
| RN-202 | pendência de validação | fora de total, saldo e agregação; bloco separado com contagem, valor e rastreio | nenhuma — invariante | RN-112/EV-F1-03 |
| RN-203 | correção existente no período | consolidação usa valor corrente; trilha acessível via drill-down | nenhuma — nunca recalcular histórico | EV-F1-05 |
| RN-204 | todo número exibido | rótulo de proveniência real/sintético/estimado | ingestão real não autorizada → tudo sintético/estimado | EV-F1-04 |
| RN-205 | regime temporal | agrupamento por competência (regime B-107 vigente) | mudança de regime → decisão registrada (B-202) | B-107 emendado |
| RN-206 | fixture de prova | conjunto esperado declarado antes de comparar; limpeza na própria task | nenhuma | EV-F1-01 |

## Fluxo e regras

1. Champion abre a consolidação do período controlado no preview.
2. Sistema agrega lançamentos válidos por participante e classificação (RN-201).
3. Pendências aparecem como bloco separado, fora dos totais (RN-202).
4. Cada número oferece drill-down ao lançamento de origem com trilha (RN-203).
5. Proveniência é exibida em todo número (RN-204).

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | período 2026-08 com 4 itens B-107 | totais por participante/classificação batem com conferência item a item | divergência → pendência + causa |
| Limite | período sem lançamentos | consolidação vazia explícita, sem zeros inventados | — |
| Limite | fórmula de alocação ausente (B-201) | valor indisponível + bloqueio nomeado | Champion entrega fórmula → reprocessa |
| Falha | leitura indisponível | erro explícito sem números parciais | retry manual; sem cache de números |

## Instruções de execução para o Ethos

1. **Ler antes de alterar:** escopo definitivo §5 F2, delta-fase-2, SPEC-1-002/004, Anexo F, B-107 emendado, STATUS/changelog do repo.
2. **Alterar somente:** rotas server-side e telas de consolidação no projeto Skip autorizado.
3. **Não alterar:** lançamentos e histórico da F1, planilha original, regras sem evidência, permissões, conectores, fases futuras.
4. **Executar nesta ordem:** conferir B-201/B-202 → RED → GREEN sobre o período B-107 → bordas → REGRESSÃO → evidência.
5. **Parar e pedir validação quando:** surgir fórmula, campo, regime temporal ou agregação não demonstrada; qualquer acesso além do preview.
6. **Estado válido ao parar:** consolidação lê e não escreve; F1 intacta; bloqueios atualizados.

## Checklist de execução

- [ ] B-201/B-202 conferidos ou regime vigente declarado
- [ ] Fixtures isoladas com limpeza própria (RN-206)
- [ ] Caminhos principal, limite e falha exercitados
- [ ] Varredura de segredos/dados fora do recorte limpa
- [ ] Evidência anexada e teste humano da Champion registrado

## Critérios de aceite

- [ ] **CA-2-001:** consolidação do período B-107 bate item a item com a conferência da Champion (aportes, saídas, saldo).
- [ ] **CA-2-002:** agregação por participante e classificação soma somente lançamentos válidos atômicos; nenhum agrupamento por valor.
- [ ] **CA-2-003:** pendência de validação aparece fora de total/saldo, como bloco separado com contagem, valor e rastreio.
- [ ] **CA-2-004:** todo número exibido carrega proveniência (real/sintético/estimado); baseline segue `[ESTIMATIVA]`.
- [ ] **CA-2-005:** drill-down de qualquer número leva ao lançamento de origem com trilha de correção, sem recalcular histórico.
- [ ] **CA-2-006:** fórmula ausente (B-201) deixa o valor indisponível com bloqueio nomeado — nunca zero inventado.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | consolidação hoje inexistente; pendência somada indevidamente; número sem proveniência | abrir consolidação do período B-107 no preview atual | ausência/falha ligada a CA-2-001..004 | relatório RED |
| GREEN | período B-107 consolidado | rotas + tela; comparar com conferência item a item da Champion | CA-2-001..004 passam | logs/capturas + evidência |
| REGRESSÃO | correção + reprocessamento no período; fórmula ausente | repetir provas de idempotência F1 sobre a consolidação; simular B-201 aberto | CA-2-005/006 passam; F1 sem regressão | trilha/recibo + evidência |

**Fixtures:** período B-107 existente (4 itens reais controlados) + fixtures sintéticas isoladas com limpeza própria (RN-206); nenhum dado real novo.
**Caminhos de erro obrigatórios:** período vazio; leitura indisponível; fórmula ausente; pendência presente.
**Evidência exigida:** `artifacts/` no repo + capturas do preview + aceite humano da Champion.

## Handoff e operação

- **Como demonstrar:** abrir consolidação do período 2026-08, conferir totais, abrir drill-down, ver pendências à parte.
- **Como operar depois:** Champion confere consolidação a cada fechamento antes de disponibilizar (critério global 3).
- **Como monitorar:** divergência consolidação×planilha vira pendência com causa (RN-131).
- **Pendência conhecida:** B-201/B-202 são insumos da Champion; migração integral e multi-período ficam fora.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| F2-T01 | Fechar insumos de consolidação (B-201/B-202) com a Champion | Champion + Consultor | SPEC-2-001 | CA-2-006 (gate de insumo) | B-201/B-202 registrados ou regime vigente declarado | Registro dos bloqueios com aceite da Champion | F1 encerrada; check-fase-1 APROVADO | ☐ |
| F2-T02 | Construir e provar a consolidação no Skip | Ethos | SPEC-2-001 | CA-2-001..006 | RED + GREEN período B-107 + REGRESSÃO | Testes, capturas, evidência `artifacts/` | F2-T01 aceita; Anexo F vigente | ☐ |

## Emendas

<!-- Append-only (D19): mudanças aprovadas depois da geração. A história não é reescrita. -->

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
