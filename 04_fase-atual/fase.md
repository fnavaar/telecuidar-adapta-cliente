# Tasks Gerais — Fase 2 — MAX Soluções / Telecuidar

**Total:** 5 tasks · **Concluídas:** 0/5 · **Próxima task:** F2-T01 · **Regra simples:** uma task por vez; análise e autorização precedem execução; teste humano precede conclusão.

## Tasks

| ID | Task | Dono | SPEC | Critério | Subseção exata | Recorte da prova | Evidência esperada | Pré-condições | Ponto de parada | Leva | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|
| F2-T01 | Fechar insumos de consolidação (B-201/B-202) com a Champion | Champion + Consultor | SPEC-2-001 | CA-2-006 (gate de insumo) | Contexto e decisões fechadas; Dados e regras | B-201/B-202 registrados ou regime vigente declarado | Registro dos bloqueios com aceite da Champion | F1 encerrada; check-fase-1 APROVADO | Insumos documentais aceitos; nenhuma implementação iniciada | 1 | PENDENTE |
| F2-T02 | Construir e provar a consolidação no Skip | Ethos | SPEC-2-001 | CA-2-001..006 | Fluxo e regras; TDD da SPEC | RED + GREEN período B-107 + REGRESSÃO | Testes, capturas do preview, evidência `artifacts/` | F2-T01 aceita; Anexo F vigente | Consolidação lê e não escreve; F1 intacta | 2 | BLOQUEADA por F2-T01 |
| F2-T03 | Construir e provar o dashboard do período | Ethos | SPEC-2-002 | CA-2-007..011 | Fluxo e regras; TDD da SPEC | RED prova negativa da pendência fora do gráfico + GREEN + conferência humana | Capturas, evidência, aceite do formato (B-203) | F2-T02 aceita; B-203 | Dashboard lê somente da consolidação; prestação oficial só após conferência | 3 | BLOQUEADA por F2-T02 |
| F2-T04 | Formalizar roteiro de conferência (B-204) | Champion + Consultor | SPEC-2-003 | CA-2-013 (gate de insumo) | Contexto e decisões fechadas; Fluxo e regras | B-204 registrado ou padrão F1-T08 declarado | Roteiro com aceite da Champion | F2-T03 aceita | Roteiro documental aceito; nenhuma alteração de telas | 4 | BLOQUEADA por F2-T03 |
| F2-T05 | Executar a conferência da prestação e fechar a F2 | Champion + Consultor | SPEC-2-003 | CA-2-012..015 | Resultado observável; TDD da SPEC; Handoff e operação | Conferência executada + registro | Roteiro executado, aceite/pendências com causa, STATUS/changelog | F2-T04 aceita | Prestação oficial com proveniência e aceite registrado; não iniciar F3 | 5 | BLOQUEADA por F2-T04 |

## Notas

- **Sequência:** F2-T01 → F2-T02 → F2-T03 → F2-T04 → F2-T05 (linear; cada task exige a anterior aceita com teste humano).
- **Invariantes transversais:** pendência fora de totais (RN-112/202/208); proveniência em todo número (RN-204/209/215); agregação só sobre lançamentos atômicos (RN-201); valor corrente + trilha (RN-203); fixtures isoladas com limpeza própria (RN-206); fallback B-106 preservado; RBAC/diretores na F3.
- **Dados reais:** nenhum dado real novo é exigido pela F2; provas usam o período B-107 e fixtures sintéticas isoladas.
