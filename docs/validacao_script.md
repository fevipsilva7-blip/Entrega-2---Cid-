# Validação do novo `docs/script.sql`

## Base utilizada

A validação foi realizada com base no DER lógico e no dicionário de dados fornecidos para o projeto.

## Método de teste

Foi realizada uma transposição compatível do script para SQLite em memória, com o objetivo de verificar:

- criação das tabelas;
- inserção da massa de dados;
- integridade referencial;
- restrições `CHECK`;
- consultas com `JOIN`;
- comandos `UPDATE`;
- comando `DELETE`;
- consultas gerenciais;
- consultas de auditoria.

## Resultado

A validação confirmou:

- 13 tabelas criadas;
- integridade referencial sem erros;
- 18 auditorias sem irregularidades;
- 5 tentativas de violação de restrições rejeitadas corretamente.

### Resumo da execução

```json
{
  "quantidade_tabelas": 13,
  "instrucoes": {
    "CREATE TABLE": 13,
    "INSERT INTO": 48,
    "SELECT": 37,
    "UPDATE": 2,
    "DELETE": 1
  },
  "consultas_checadas": 38
}
