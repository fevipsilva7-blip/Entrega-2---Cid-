# Massa de dados — documentação para o trabalho acadêmico

**Arquivo de entrega SQL:** [`docs/script.sql`](script.sql)  
**SGBD previsto:** MySQL 8.0.16 ou superior  
**Natureza dos registros:** exclusivamente fictícios e demonstrativos

> **Atenção:** esta documentação descreve o arquivo `docs/script.sql` atual, com 102 registros na tabela `despesas`. O log de execução enviado anteriormente no chat corresponde a uma versão que retornou 30 despesas. Portanto, para comprovar a execução *desta versão*, é necessário repetir o teste no MySQL com este arquivo.

## Texto sugerido para a seção 4 — Massa de dados

A massa de dados fictícia está **integrada ao arquivo `docs/script.sql`**, na seção identificada pelo comentário `SECAO 4 - INSERT INTO`. Não há necessidade de entregar `massa_de_dados.sql` em separado. Nenhum nome de cliente ou valor utilizado deve ser interpretado como dado real da organização.

O conjunto representa um **cenário ilustrativo de operação de restaurante**, abrangendo agosto, setembro e outubro de 2026. Foram preparados 900 pedidos, correspondentes a uma média **simulada** de aproximadamente 300 pedidos mensais (10 por dia, considerando três meses de 30 dias). A quantidade de cadastros, produtos e transações foi escolhida para demonstrar as relações entre cadastro, vendas, pagamentos, estoque e despesas.

### Volume no arquivo SQL atual

| Tabela | Registros da carga inicial | Finalidade |
|---|---:|---|
| `categorias` | 4 | Classificar produtos |
| `usuarios_sistema` | 4 | Simular papéis e autorizações |
| `clientes` | 60 | Simular clientes com e sem compras |
| `enderecos` | 65 | Testar diferentes endereços e entregas |
| `produtos` | 16 | Simular cardápio, preços, custos e níveis de estoque |
| `canais_venda` | 5 | Distinguir balcão e delivery |
| `pedidos` | 900 | Criar histórico de pedidos de três meses |
| `itens_pedido` | 1.530 | Demonstrar pedidos com um ou mais produtos |
| `pagamentos` | 893 | Demonstrar diferentes formas e estados de pagamento |
| `movimentacoes_estoque` | 1.488 | Rastrear entradas e saídas |
| `despesas` | 102 | Representar despesas operacionais e insumos em três meses |

A carga de pedidos inclui **850 concluídos, 30 cancelados e 20 abertos**. Os pagamentos abrangem **880 registros aprovados, 8 pendentes e 5 estornados**. O cadastro de produtos permite obter registros abaixo do estoque mínimo (10 produtos com estoque atual inferior ao mínimo na carga inicial). A massa também contém diferentes canais de venda, formas de pagamento e datas, permitindo a execução de consultas gerenciais e auditorias.

Os relacionamentos são definidos por chaves estrangeiras, que impedem referências a clientes, pedidos ou produtos inexistentes. Além disso, as consultas A01–A16 foram preparadas para detectar violações relevantes das regras do modelo didático.

### Relação com a realidade da organização — **completar com a seção 1.1**

A escolha de **300 pedidos por mês, 60 clientes cadastrados e 16 produtos** é uma **premissa didática da massa**, não um volume confirmado pela organização. Antes da entrega, preencher o quadro com os dados coletados na entrevista ou na observação:

| Indicador de porte | Informação obtida da organização | Comparação com a massa |
|---|---|---|
| Pedidos por mês | **[preencher com a seção 1.1]** | 300 pedidos/mês simulados |
| Clientes ativos/cadastrados | **[preencher com a seção 1.1]** | 60 clientes fictícios |
| Produtos/itens comercializados | **[preencher com a seção 1.1]** | 16 produtos fictícios |
| Canais de venda | **[preencher com a seção 1.1]** | 5 canais simulados |
| Frequência de reposição de estoque | **[preencher com a seção 1.1]** | 1.488 movimentações fictícias |

**Se a realidade apurada for muito diferente, ajustar a massa em vez de afirmar que esses números foram fornecidos pela organização.** O objetivo é refletir a escala e os processos observados, mantendo a privacidade.

## Texto sugerido para a seção 6 — Uso de Inteligência Artificial

Foi utilizada a ferramenta **ChatGPT, da OpenAI**, como apoio à elaboração do script MySQL e à geração de uma massa de dados fictícia para demonstração acadêmica. O objetivo do uso foi criar registros de pedidos, clientes, itens, pagamentos, movimentos de estoque e despesas, preservando relacionamentos e cobrindo diferentes cenários de teste.

**Prompt representativo da tarefa** (redação-síntese do pedido, não transcrição literal de um histórico de prompts):

> Criar um script MySQL 8 de demonstração para um restaurante de pequeno porte, com tabelas relacionadas por PK e FK e uma massa fictícia suficiente para testar consultas gerenciais e de auditoria. Incluir pedidos concluídos, cancelados e abertos; clientes sem compras; produtos abaixo do estoque mínimo; diferentes canais e formas de pagamento; registros de meses diferentes; e dados de estoque e despesas. Não utilizar dados pessoais reais.

**Verificação e intervenções humanas:** foi realizada uma execução de uma versão anterior do script no **MySQL 8.0.46**, conforme o registro apresentado pela equipe, com criação de tabelas, inserção de dados e consultas retornando resultados. **A versão atual, que contém 102 despesas, deve ser reexecutada** antes da entrega. Acrescentar aqui quaisquer correções manuais efetivamente realizadas pelo grupo (por exemplo, ajustes de nomes de colunas, alterações de regras, revisão de dados ou correção de erros); não declarar ajustes que não foram feitos.

A ferramenta de IA foi utilizada para apoiar a produção de dados artificiais; a responsabilidade de revisar, executar, validar e adequar o material à entrevista, ao DER e às regras reais do projeto permanece com o grupo.

## Como validar esta massa no MySQL

Após executar `SOURCE C:/Users/d/Desktop/script.sql;` no MySQL Command Line Client, executar:

```sql
USE restaurante_academico_demo;

SELECT 'clientes' AS tabela, COUNT(*) AS quantidade FROM clientes
UNION ALL SELECT 'produtos', COUNT(*) FROM produtos
UNION ALL SELECT 'pedidos', COUNT(*) FROM pedidos
UNION ALL SELECT 'itens_pedido', COUNT(*) FROM itens_pedido
UNION ALL SELECT 'pagamentos', COUNT(*) FROM pagamentos
UNION ALL SELECT 'movimentacoes_estoque', COUNT(*) FROM movimentacoes_estoque
UNION ALL SELECT 'despesas', COUNT(*) FROM despesas;

SELECT status, COUNT(*) AS quantidade
FROM pedidos GROUP BY status;

SELECT status, COUNT(*) AS quantidade
FROM pagamentos GROUP BY status;

SELECT id_produto, nome, estoque_atual, estoque_minimo
FROM produtos WHERE estoque_atual < estoque_minimo;

SELECT DATE_FORMAT(data_pedido, '%Y-%m') AS mes, COUNT(*) AS quantidade
FROM pedidos GROUP BY DATE_FORMAT(data_pedido, '%Y-%m') ORDER BY mes;
```

Conferir também que as consultas gerenciais G01–G13 trazem resultados esperados e que as consultas de auditoria A01–A16 não apresentam inconsistências inesperadas.

## Link a adicionar no README

```md
## Script SQL e massa de dados

O banco MySQL, incluindo a massa de dados fictícia, está no arquivo [docs/script.sql](docs/script.sql).

A explicação dos volumes, cenários e uso de IA está em [docs/DOCUMENTACAO_MASSA_DE_DADOS.md](docs/DOCUMENTACAO_MASSA_DE_DADOS.md).
```
