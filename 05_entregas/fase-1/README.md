# Fase 1 — Núcleo financeiro e rastreabilidade (encerrada)

**Encerrada em:** 2026-09-21 · **Check:** `check-fase-1.md` APROVADO (consultor Navaar) · **Digest do estado encerrado:** `1ae1cd83a3753b3f03f6e2de52adbf9a21df3ba7e7a20fb2a26da1ebdcf4a27d` (repo HEAD `9a21fbf`)

## Resultado

Primeiro período controlado no sistema: 8/8 tasks concluídas com teste humano da Champion Daniela em cada uma (última: F1-T08, "confirmado", 2026-09-15). QA final Skip 0.0.21 (`027719e`), migrations 0001–0006.

- Contrato da pasta/allowlist e política (SPEC-1-001); gate de zero ingestão provado.
- Catálogo e regras financeiras formalizados com exemplos (Anexos E/F aceitos).
- Lançamentos controlados com aporte/saída, pendência fora de totais (RN-112), correção append-only e idempotência provadas.
- Spike OAuth2 do Drive (B-106) com fallback manual idempotente declarado; vínculo documental com deduplicação e recuperação.
- Período controlado 2026-08 (B-107 emendado: 4 itens; Starlink/Vivo separados) com histórico, baseline `[ESTIMATIVA]` e revalidação independente final.

## Conteúdo desta pasta

- `fase.md` — quadro operacional da Fase 1 no estado encerrado.
- `specs/` — SPEC-1-001..004 integrais.
- `phase-closure-manifest.json` — selo de fechamento (digest, hashes, drift registrado).

Evidências das tasks: `artifacts/f1-t05..t08-evidencia.md` (raiz do repo); debugs: `06_notas/debug/`.
