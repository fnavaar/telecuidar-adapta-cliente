# AP-2026-09-11-1918 — Booleano false e campo obrigatório no PocketBase

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: F1-T04 / SPEC-1-002
- Sinal: o PocketBase rejeitou o valor booleano `false` como blank quando o campo `pendencia_validacao` estava marcado como obrigatório.
- Evidência: log de request `POST /backend/v1/lancamentos` com erro `pendencia_validacao: cannot be blank`; migration `0002_fix_pendencia_validacao.js`; QA 0.0.6 e smoke test posterior aprovados.
- Regra reutilizável: não marcar booleanos que precisam aceitar `false` como `required` no schema PocketBase; validar a presença/tipo na borda server-side quando a regra de negócio exigir.
- Quando aplicar: campos booleanos em migrations PocketBase v0.36 cujo valor falso seja um estado válido.
- Quando não aplicar: campos cuja ausência seja semanticamente diferente de `false` e exija uma modelagem tri-state explícita.
- Confiança: alta — restrição reproduzida no runtime e corrigida por migration reversível.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto
