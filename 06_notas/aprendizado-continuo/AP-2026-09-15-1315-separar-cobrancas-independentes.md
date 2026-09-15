# AP-2026-09-15 — Separar cobranças independentes antes da conferência

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: F1-T07 / SPEC-1-004
- Sinal: Starlink R$339,00 e Vivo R$99,99 apareciam como uma suposta divergência, mas eram lançamentos independentes com faturas próprias.
- Evidência: `artifacts/f1-t07-evidencia.md`; smoke Skip 0.0.16; referências documentais distintas `NF 010898811 - STALINK.pdf` e `FATURA VIVO.pdf`.
- Regra reutilizável: antes de classificar uma diferença como divergência sistema×planilha, confirmar identidade do serviço, competência, documento comprobatório e chave do lançamento; despesas distintas devem gerar itens independentes.
- Quando aplicar: conferência de extrato, planilha e documentos quando houver valores parecidos ou serviços recorrentes.
- Quando não aplicar: quando a mesma despesa tiver uma única identidade documental e os valores realmente divergirem entre fontes.
- Confiança: alta — confirmado por duas planilhas, metadados documentais, smoke automatizado e teste humano aprovado.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
