# Debug Summary
**Task e problema:** F1-T07 — no passo 2 do teste humano, o cliente não conseguia inserir as informações.

**Reprodução:** no preview, o painel exibia apenas “Registrar os 3 cenários B-107”; não havia campos de descrição, valores, referência, responsável ou motivo. A rota também usava cenários fixos.

**Causa raiz:** o primeiro desenho do painel era somente uma ação fixa de fixture; o frontend não tinha formulário editável e o backend não recebia os dados do usuário. O rollback também deixava a competência única em status `rollback`, impedindo reabertura posterior.

**Correção:** formulário editável para os três cenários com rascunhos revisáveis; validação de competência, catálogo, valores, ausência documental e divergência; transporte normalizado de itens; reabertura idempotente e reutilização segura dos itens após rollback, preservando eventos.

**Verificação automática:** QA Skip 0.0.15 (`79d7fc2`) passou integralmente. Smoke autenticado registrou `Adapta - revisão manual` como pendência, manteve `Papel de Parede` rastreável e `Internet Starlink` divergente, e limpou 3 itens/2 lançamentos sintéticos. Logs confirmaram abertura HTTP 200, conferência HTTP 201 e limpeza HTTP 200. Ambiente final sem itens do período.

**Gate atual:** aguardando teste humano.
