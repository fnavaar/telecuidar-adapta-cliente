# AP-2026-09-23-1316 — Escopo de auxiliares em hooks PocketBase

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: F2-T02 / SPEC-2-001
- Sinal: o QA de integração do Skip reprovou quando funções auxiliares do hook ficaram declaradas no escopo superior; a correção foi mover as auxiliares para dentro do callback da rota.
- Evidência: Skip 0.0.22 (`d483072`) reprovado na integração; Skip 0.0.23 (`87c622e`) com escopo corrigido passou setup, análise estática, build, integração e testes; revalidação independente da F2-T02 passou novamente.
- Regra reutilizável: em hooks PocketBase deste projeto, declarar funções e variáveis auxiliares dentro do callback registrado por `routerAdd`; não depender de declarações top-level no callback em runtime.
- Quando aplicar: ao criar ou revisar qualquer hook server-side PocketBase no projeto Telecuidar.
- Quando não aplicar: código de frontend, serviços TypeScript do cliente ou runtime fora dos hooks PocketBase.
- Confiança: alta — falha e correção foram observadas no QA oficial e repetidas na revalidação.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto
