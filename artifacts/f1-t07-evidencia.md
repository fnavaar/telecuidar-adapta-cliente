# Evidência F1-T07 — Primeiro período controlado B-107

**Task:** F1-T07  
**SPEC:** SPEC-1-004, com emenda operacional B-107 aceita pela Champion  
**B-107 emendado:** competência `2026-08`; fonte `08.AGOSTO`; fronteira `boletos e contas a pagar identificadas`; quatro lançamentos independentes.  
**Pasta:** `1f03hUNACl6PENUI1NHV5p3YEv4opmLm6`  
**Versão Skip final:** 0.0.16 (`1818bfe`)

## Aceite humano

Daniela confirmou em 2026-09-15: **“tudo correto”**.

## Emenda do recorte

A SPEC originalmente exigia três cenários, incluindo uma divergência. A Champion autorizou a emenda para quatro itens sem cenário divergente, porque Starlink e Vivo são lançamentos independentes:

1. Papel de Parede — completo;
2. Adapta — sem documento;
3. Internet Starlink — completo, R$339,00, fatura própria;
4. Internet Vivo — completo, R$99,99, fatura própria.

A limitação “cenário divergente não exercitado” permanece explícita; a SPEC não foi alterada.

## Fontes e escopo

- Metadados da pasta `08.AGOSTO` consultados com HTTP 200; nenhum PDF foi baixado ou aberto.
- Foram usadas somente as planilhas autorizadas de conferência.
- O extrato registra `Pagamento Internet Vivo - Julho 2026` no valor de R$99,99.
- O detalhamento registra `Internet Starlink` no valor de R$339,00, com referência `NF 010898811 - STALINK`.
- Os metadados listam documentos distintos: `FATURA VIVO.pdf` e `NF 010898811 - STALINK.pdf`.
- A planilha local de custeio também confirma Starlink R$339,00 e Internet R$99,99 como linhas independentes, ambas associadas a Geraldo Tadeu.

## Critérios exercitados no recorte emendado

### CA-1-019 — período, fontes e fronteira

**PASSOU.** O sistema registrou competência `2026-08`, fonte `08.AGOSTO`, fronteira aprovada e amostra de 4 itens antes da conferência.

### CA-1-020 — lançamento rastreável ou pendência nomeada

**PASSOU.** O smoke autenticado registrou:

1. Papel de Parede — R$1.945,00, documento próprio, lançamento rastreável;
2. Adapta — R$5.833,33, documento ausente, status `pendente`, sem lançamento automático;
3. Internet Starlink — R$339,00, referência `NF 010898811 - STALINK.pdf`, lançamento rastreável;
4. Internet Vivo — R$99,99, referência `FATURA VIVO.pdf`, lançamento rastreável.

### CA-1-021 — pendência visível e fora dos totais

**PASSOU.** Adapta permaneceu visível como pendência nomeada, sem lançamento automático.

### CA-1-022 — conferência item a item

**PASSOU no recorte emendado.** Os quatro itens foram registrados separadamente, com data, descrição, valor, responsável, referência documental e status. Starlink e Vivo não foram comparados entre si.

**Limitação:** o cenário divergente da SPEC não foi exercitado, conforme emenda B-107 autorizada pela Champion.

## Recuperação e limpeza

- Reabertura do período após rollback: HTTP 200.
- Conferência dos quatro itens: HTTP 201, `itens_criados=4`.
- Limpeza final: HTTP 200, removeu 4 itens e 3 lançamentos sintéticos.
- Consulta posterior: zero itens do recorte.
- Nenhum arquivo ou planilha do Drive foi alterado.

## Qualidade e segurança

- QA oficial final do Skip 0.0.16 (`1818bfe`): setup, análise estática, build, integrações e testes — todos OK.
- Migration `0005_emenda_b107_quatro_itens` aplicada durante o QA.
- Formulário visual exibe quatro cartões independentes, com documento comprobatório próprio para cada item.
- Nenhum PDF, token, segredo ou conteúdo documental foi persistido.
- Baseline de tempo/esforço ainda não foi medido e não foi inventado.
- Checklist auxiliar `agents/verificador-de-entrega.md` não existe no handoff operacional; checklist equivalente foi executado inline.

## Estado de fechamento

F1-T07 concluída após aceite humano. F1-T08 permanece bloqueada e não foi iniciada.

## Histórico de correções

- O primeiro painel não possuía formulário editável; corrigido na versão 0.0.12.
- O transporte de itens aninhados foi normalizado; corrigido nas versões 0.0.13/0.0.14.
- A reabertura após rollback foi corrigida na versão 0.0.15.
- A mistura Starlink/Vivo foi corrigida na versão 0.0.16, com quatro itens independentes e sem cenário divergente.
