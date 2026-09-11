# Debug Summary — F1-T02

**Task e problema:** F1-T02 precisava comprovar CA-1-006, mas a primeira execução encontrou que o Skip não possuía enforcement runtime; havia apenas uma sonda contratual em memória.

**Reprodução:** baseline do projeto 57934 mostrou preview no template inicial, 0 migrations, somente coleção auth `users` e nenhum hook/integração. A sonda em memória retornava REJECT, mas não exercitava uma requisição real.

**Causa raiz:** ausência de um ponto de entrada server-side para aplicar o gate; a regra existia apenas documentalmente.

**Correção:** criado `pocketbase/hooks/corte_gate_probe.js`, uma rota POST `/backend/v1/corte-gate/probe` que aceita somente metadados sintéticos, recusa política não selada com 403 `POLICY_NOT_SEALED`, recusa fora da allowlist com 403 `OUTSIDE_ALLOWLIST`, rejeita campos extras com 400 e só retorna 200 `GATE_PASS` para o caso sintético selado dentro de `TESTE`. A rota não usa banco, não grava, não acessa Drive e retorna `persisted:false`.

**Verificação automática:** pipeline Skip verde em setup, análise estática, build, integrações e testes. Teste real da rota: 403, 403, 200 e 400 nos casos RED/GREEN/entrada inválida; três reprocessamentos GREEN retornaram 200. Logs sanitizados confirmaram as respostas sem payloads. Estado pós-teste: 0 migrations, somente coleção auth `users`, nenhuma coleção financeira e nenhuma persistência.

**Gate atual:** aguardando teste humano da Champion. A F1-T02 não foi concluída nesta etapa e a F1-T03 não foi iniciada.
