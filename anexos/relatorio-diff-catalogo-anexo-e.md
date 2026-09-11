# Relatório de diff — catálogo candidato × Anexo E

- **Task/SPEC:** F1-T03 / SPEC-1-002
- **Fonte:** `anexos/E-catalogo-observado.md`
- **Candidato:** `anexos/catalogo-executavel-f1-t03.md`
- **Fonte original:** `CUSTEIO_NOVO.xlsx`
- **SHA-256:** `50b3dfd912d12d1de231aa43f4d7280730e0a16fcb39ef5c3e68222e9ed0166d`
- **Método:** comparação automatizada das listas de campos, valores de domínio e lacunas estruturais extraídas dos dois documentos; nenhum valor de lançamento individual foi usado.

## Resultado

**PASSOU — igualdade estrutural do catálogo candidato com o Anexo E.**

| Verificação | Resultado |
|---|---|
| Campos de `CUSTEIO` | PASSOU — 8 campos, mesma ordem e mesma grafia |
| Valores de Forma de Pagamento | PASSOU — 2 valores observados |
| Valores de Status | PASSOU — 4 valores observados |
| Valores de Classificação | PASSOU — 3 valores observados; opção 4 continua vazia |
| Valores de Responsável | PASSOU — 3 valores observados |
| Lacunas P-1-001..003 | PASSOU — preservadas sem default |
| Obrigatoriedade | PASSOU — os oito campos foram marcados obrigatórios conforme decisão recebida; essa regra comportamental pertence ao Anexo F |
| Fórmulas, modelo e migration | NÃO APLICÁVEL nesta task — nenhum foi criado |

## Evidência do comando

```text
catalog_fields_match: PASS
payment_values_match: PASS
status_values_match: PASS
classification_values_match: PASS
responsible_values_match: PASS
known_pendencies_preserved: PASS
mandatory_fields_received: PASS
unexpected_catalog_item: none
```

O diff estrutural está limpo. B-104 pode ser fechado após confirmação da consistência final; B-105 permanece bloqueado pela dúvida documentada no Anexo F.
