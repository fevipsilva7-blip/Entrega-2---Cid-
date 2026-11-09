# Relatório de execução do `docs/script.sql` no MySQL 8

## Ambiente

- SGBD: MySQL 8.0.46
- Banco criado: `donna_claudia_academico`
- Script executado: `docs/script.sql`
- Método: execução do arquivo SQL completo pelo cliente MySQL

## Resultado geral

O script foi executado sem erros no MySQL 8.0.46.

## Tabelas

A consulta realizada em `information_schema.tables` retornou 13 tabelas.

As 13 tabelas criadas foram:

```text
FORNECEDOR, COMPRA, ITEM_COMPRA, PRODUTO, CATEGORIA, ITEM_PEDIDO,
PEDIDO, CLIENTE, ENDERECO, PAGAMENTO, ENTREGA, FUNCIONARIO, DESPESA
```

## Consultas gerenciais

As consultas `G01` a `G15` foram executadas sem erro. A `G15` detalha pedidos cancelados, seus itens e os registros financeiros relacionados.

## Auditorias

As 18 auditorias foram executadas no MySQL e todas retornaram zero registros:

| Auditoria | Linhas encontradas |
|---|---:|
| A01 | 0 |
| A02 | 0 |
| A03 | 0 |
| A04 | 0 |
| A05 | 0 |
| A06 | 0 |
| A07 | 0 |
| A08 | 0 |
| A09 | 0 |
| A10 | 0 |
| A11 | 0 |
| A12 | 0 |
| A13 | 0 |
| A14 | 0 |
| A15 | 0 |
| A16 | 0 |
| A17 | 0 |
| A18 | 0 |

## Massa confirmada

| Tabela | Registros |
|---|---:|
| FORNECEDOR | 5 |
| COMPRA | 40 |
| ITEM_COMPRA | 120 |
| PRODUTO | 16 |
| CATEGORIA | 5 |
| ITEM_PEDIDO | 1495 |
| PEDIDO | 900 |
| CLIENTE | 60 |
| ENDERECO | 55 |
| PAGAMENTO | 947 |
| ENTREGA | 313 |
| FUNCIONARIO | 6 |
| DESPESA | 60 |

## Conclusão

O `docs/script.sql` é compatível com o MySQL 8.0.46 no ambiente testado. A criação do banco, as 13 tabelas, a massa de dados, as consultas `G01` a `G15` e as auditorias `A01` a `A18` foram executadas sem erros.
