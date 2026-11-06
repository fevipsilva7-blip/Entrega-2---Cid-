# Entrega 2 — Modelo Lógico, Implementação SQL e Apresentação Final

## Sistema de Gestão de Informações — Donna Claudia Restaurante e Lanchonete

---

### Integrantes

| Nome completo do aluno | RGM | Usuário do GitHub |
| :--- | :--- | :--- |
| Augusto de Almeida Guelere | 48832588 | guelerzao |
| Felipe Rodrigues da Silva | 47868384 | fevipsilva7-blip |
| Lucas Freitas de Oliveira  | 048587885 | dzskl |
| Matheus Faustino da Silva | 47854928 | Matheussil01 |
| Otavio Estevam Ventura | 48763390 | cVenturaDev |

---

## 1. Relatório Técnico Final

### 1.1 Revisão do Modelo Conceitual

#### Caracterização da Organização
- Nome e natureza da organização: Donna Claudia Restaurante e Lanchonete (CNPJ: 36.276.829/0001-69). Trata-se de uma empresa privada comercial com fins lucrativos do ramo alimentício.
- Contexto e porte: O restaurante está em operação há aproximadamente 2 anos e conta atualmente com 5 funcionários. Atende um volume médio de cerca de 3.000 clientes por mês (aproximadamente 750 pedidos/atendimentos por semana), operando com vendas presenciais, lanches, refeições e forte fluxo via WhatsApp e aplicativos de delivery.
- **Problemas e necessidades identificados:**
  - `P1`: **Acompanhamento na operação do Delivery:** Dificuldade no acompanhamento dos pedidos em tempo real, integrando o recebimento de canais externos (WhatsApp/Apps), status de preparo na cozinha e despacho/entrega.
  - `P2`: **Controle  para Exceções (Cancelamentos/Reembolsos):** Ausência de histórico unificado quando ocorrem problemas na entrega (itens faltantes, divergências de pedido), gerando retrabalho manual e inconsistências na conferência financeira final.
  - `P3`: **Consolidação dos dados financeiros e dos canais de venda:** necessidade de consultar e comparar as vendas por canal (WhatsApp e aplicativos de delivery) e reunir informações sobre vendas e despesas.

- **Escopo do sistema:** O banco de dados reúne as informações globais da organização, englobando clientes, produtos, categorias de itens, fornecedores, compras de estoque, despesas, funcionários, pedidos, itens do pedido, status de entrega e registros de pagamento/reembolso.
- **Justificativa da escolha:** Organização real de pequeno porte com operação intensa e processos de negócio bem delimitados. Apresenta desafios reais de gestão de dados adequados para o desenvolvimento da modelagem relacional.
- **Evidências da organização:** 
  - **Endereço:** Rua Maciel Monteiro, nº 264.
  - **Perfil Google Meu Negócio / Comprovante:** Rua Maciel monteiro 264 Gopouva
  - **Fotos do Local:** imagem.faixada.png
- **Responsável pela organização:** Antonia Claudia Freitas da Silva Oliveira, proprietária e administradora. A entrevistada autorizou a utilização de seu nome completo neste trabalho.
#### Relato das Entrevistas
- **Quem:** Antonia Claudia Freitas da Silva Oliveira, proprietária do estabelecimento.
- **Quando:** 20/10/2026. 
- **Onde:** Presencialmente, no ambiente do restaurante.
- **Participante do grupo:** Lucas Freitas de Oliveira foi o único integrante que participou das duas entrevistas.
- **Autorização:** A entrevistada autorizou a utilização de seu nome completo no trabalho.
- **Objetivo:** Levantar informações sobre os processos administrativos e operacionais, identificar necessidades e coletar requisitos para a modelagem do banco de dados.
- **Principais assuntos abordados:** Gestão de pedidos, delivery, cadastro de clientes, controle de estoque, compras, pagamentos, cancelamentos, reembolsos e despesas.
- **Comprovação:** `imagem.entrevista.png`.
- **Levantamento completo:** O detalhamento das respostas, processos, requisitos e regras de negócio está disponível no documento. [Acessar o Levantamento](./Levantamento/levantamento.md)


#### Resumo do Levantamento

##### Processos de Negócio Mapeados
1. **Cadastro e gestão de clientes:** Para pedidos de delivery são coletados nome, telefone e endereço. O levantamento também indica que os dados de clientes são necessários para a entrega.
2. **Emissão e acompanhamento de pedidos:** Registro da origem do pedido (como WhatsApp ou aplicativo), dos produtos, valores, data e situação do pedido.
3. **Controle de estoque e compras:** Acompanhamento do estoque, com verificação diária e alertas do sistema Bion Finance quando um produto está próximo de acabar; compras realizadas com fornecedores e mercados.
4. **Gestão de pagamentos e reembolsos:** Recebimento por Pix, cartão e dinheiro; em situações de problemas ou cancelamentos, pode ocorrer reembolso ou preparação de um novo pedido.
5. **Gestão financeira e despesas:** Registro e consulta de vendas e despesas, com necessidade de relatórios para acompanhamento financeiro.


##### Requisitos do Sistema

**Requisitos Funcionais:**
- `RF01`: O sistema deve permitir registrar os dados de clientes necessários para a entrega, incluindo nome, telefone e endereço.
- `RF02`: O sistema deve registrar produtos com identificação, nome, preço e quantidade em estoque.
- `RF03`: O sistema deve registrar pedidos contendo número único, data, produtos, valor total, forma de pagamento e canal de origem.
- `RF04`: O sistema deve associar itens ao pedido, indicando o produto, a quantidade solicitada e o preço praticado.
- `RF05`: O sistema deve registrar pagamentos vinculados aos pedidos, especificando a forma de pagamento e a situação do pagamento.
- `RF06`: O sistema deve permitir acompanhar o estoque e identificar produtos próximos de acabar.
- `RF07`: O sistema deve registrar cancelamentos, seus motivos e as informações de pagamento ou reembolso relacionadas.
- `RF08`: O sistema deve permitir consultar informações gerenciais, como vendas mensais, despesas, produtos mais vendidos, pagamentos pendentes, cancelamentos e vendas por canal.

**Requisitos Não Funcionais:**
- `RNF01`: O sistema deve permitir acesso por computador e dispositivo móvel, com conexão à internet.
- `RNF02`: O sistema deve possuir interface simples, adequada a usuários com diferentes níveis de familiaridade com tecnologia.
- `RNF03`: O acesso às informações financeiras deve ser controlado conforme as permissões dos usuários.
- `RNF04`: O sistema deve permitir que informações registradas manualmente durante uma indisponibilidade sejam atualizadas posteriormente.

##### Regras de Negócio
- `RN01`: Para pedidos que exigem entrega, devem ser registrados os dados necessários para localizar e contatar o cliente, incluindo nome, telefone e endereço.
- `RN02`: **[VALIDAR COM O GRUPO/ENTREVISTADA]** Confirmar se o sistema deverá impedir a inclusão de produtos em pedidos quando não houver estoque suficiente. O levantamento confirma o acompanhamento do estoque, mas não confirma essa restrição de venda.
- `RN03`: Quando um pedido for cancelado, seu registro e as informações relevantes — como número, data, valor, produtos, motivo e registro de pagamento/reembolso — devem ser preservados para consulta histórica.
- `RN04`: O preço registrado no item do pedido deve preservar o valor praticado no momento da venda, sem ser alterado por futuras mudanças no cadastro do produto.
- `RN05`: Cada pedido deve possuir um identificador único. **[VALIDAR]** Confirmar se a numeração deve ser sequencial e gerada automaticamente pelo sistema.


#### Notação do DER Conceitual
- **Ferramenta utilizada:** brModelo.
- **Link/Imagem do DER:** ![DER Conceitual](./DER%20conceitual/der_conceitual.png)

#### Ajustes do Modelo em Relação à Entrega 1

| Apontamento da correção da E1 | O que mudou no trabalho | Por quê |
| :--- | :--- | :--- |
| *Exemplo: Ausência de entidade para cancelamentos/reembolsos* | *Criado o controle de status e histórico financeiro na tabela PAGAMENTO e PEDIDO* | *Para cobrir o problema P2 e garantir que valores estornados sejam computados na auditoria de caixa.* |
| *Exemplo: Ausência de vínculo de canal de venda* | *Adicionado o campo do canal do pedido (WhatsApp vs. Apps)* | *Necessário para resolver o problema P3 de comparação de métricas.* |
| `[PREENCHER OU ADAPTAR - Inserir correções feitas]` | `[PREENCHER - Detalhar alteração]` | `[PREENCHER - Justificar]` |

---

### 1.2 Conversão do Modelo Conceitual para o Modelo Lógico
1. **Entidades → Tabelas:** Cada entidade do modelo conceitual (`CLIENTE`, `PRODUTO`, `CATEGORIA`, `PEDIDO`, `PAGAMENTO`, `ENTREGA`, `FORNECEDOR`, `COMPRA`, `DESPESA` e `FUNCIONARIO`) foi convertida em uma tabela relacional.
2. **Atributos → Colunas:** Os atributos foram convertidos em colunas com tipos de dados SQL, conforme definidos no modelo lógico e no script.
3. **Relacionamentos N:N → Tabelas associativas:** O relacionamento N:N entre `PEDIDO` e `PRODUTO` foi convertido na tabela associativa `ITEM_PEDIDO`, que armazena atributos da relação, como quantidade e preço unitário praticado na venda.
4. **Relacionamentos 1:N:** A chave primária da tabela do lado “1” foi propagada como chave estrangeira na tabela do lado “N”, conforme o relacionamento definido no modelo.
5. **Relacionamentos 1:1:** `[VALIDAR COM O MODELO LÓGICO]` Conferir se os relacionamentos entre `PEDIDO` e `ENTREGA` e entre `PEDIDO` e `PAGAMENTO` são realmente 1:1 e se existe restrição `UNIQUE` nas respectivas chaves estrangeiras.


---

### 1.3 Definição de Chaves Primárias e Estrangeiras
- `CATEGORIA`: PK (`id_categoria`).
- `FORNECEDOR`: PK (`id_fornecedor`).
- `CLIENTE`: PK (`id_cliente`).
- `FUNCIONARIO`: PK (`id_funcionario`).
- `PRODUTO`: PK (`id_produto`), FK (`id_categoria` → `CATEGORIA.id_categoria`).
- `PEDIDO`: PK (`id_pedido`), FK (`id_cliente` → `CLIENTE.id_cliente`), FK (`id_funcionario` → `FUNCIONARIO.id_funcionario`).
- `ITEM_PEDIDO`: PK composta (`id_pedido`, `id_produto`), FKs (`id_pedido` → `PEDIDO.id_pedido`; `id_produto` → `PRODUTO.id_produto`).
- `ENTREGA`: PK (`id_entrega`), FK (`id_pedido` → `PEDIDO.id_pedido`).
- `PAGAMENTO`: PK (`id_pagamento`), FK (`id_pedido` → `PEDIDO.id_pedido`).
- `COMPRA`: PK (`id_compra`), FK (`id_fornecedor` → `FORNECEDOR.id_fornecedor`).
- `DESPESA`: PK (`id_despesa`).

---

### 1.4 Processo de Normalização (1FN, 2FN e 3FN)
- **1ª Forma Normal (1FN):** Os atributos devem conter valores atômicos. Os dados de endereço foram separados em campos individuais, e os produtos de cada pedido foram representados na tabela `ITEM_PEDIDO`, em vez de armazenados como uma lista em uma única coluna.
- **2ª Forma Normal (2FN):** Na tabela associativa `ITEM_PEDIDO`, os atributos próprios da venda, como quantidade e preço unitário praticado, devem depender da chave composta (`id_pedido`, `id_produto`). Os dados cadastrais do produto permanecem na tabela `PRODUTO`.
- **3ª Forma Normal (3FN):** Os dados de categoria foram separados na tabela `CATEGORIA`, evitando repetir informações descritivas da categoria em cada registro de produto.


---

### 1.5 Justificativas Técnicas das Decisões

- **Chaves primárias autoincrementais (`INT AUTO_INCREMENT`):** Utilizadas para identificar unicamente os registros e facilitar os relacionamentos entre tabelas, conforme implementação no script SQL.
- **Inclusão do atributo `preco_unitario` em `ITEM_PEDIDO`:** Preserva o preço praticado no momento da venda, evitando que alterações futuras no cadastro do produto modifiquem o histórico de pedidos.
- **Uso de enums e/ou restrições `CHECK`:** Podem ser utilizados para limitar valores de canais, formas de pagamento e status, desde que correspondam às restrições efetivamente implementadas no script SQL.
- **Manutenção de registros de cancelamentos:** Permite consultar o histórico de pedidos cancelados, seus motivos e os registros financeiros relacionados.

---

### 1.6 Proposta de Arquitetura Analítica para BI e IA

#### Informações Estratégicas e Métricas Gerenciais (KPIs)
- **KPI 1 — Faturamento mensal:** acompanha o valor total das vendas concluídas por mês.
- **KPI 2 — Receita após taxas:** identifica quanto a organização recebe após as taxas dos canais de venda.
- **KPI 3 — Pedidos concluídos:** acompanha a quantidade de pedidos concluídos mensalmente.
- **KPI 4 — Ticket médio:** calcula o valor médio dos pedidos concluídos.
- **KPI 5 — Estoque baixo:** identifica produtos abaixo do estoque mínimo.
- **KPI 6 — Produtos mais vendidos:** identifica os produtos com maior volume de vendas.
- **KPI 7 — Vendas por canal:** compara o faturamento e as taxas dos diferentes canais.
- **KPI 8 — Taxa de cancelamento:** acompanha o percentual de pedidos cancelados.
- **KPI 9 — Arrecadação por pagamento:** compara os valores recebidos por forma de pagamento.
- **KPI 10 — Pedidos em aberto:** identifica pedidos que ainda possuem pagamentos pendentes.
- **KPI 11 — Margem por produto:** calcula a margem bruta gerada pelos produtos.
- **KPI 12 — Resultado operacional:** estima o resultado após custos, taxas e despesas.
- **KPI 13 — Clientes sem compra:** identifica clientes cadastrados sem pedidos concluídos.
- **KPI 14 — Pagamentos divididos:** identifica pedidos pagos por mais de uma transação.
- **KPI 15 — Estornos:** acompanha os valores estornados em pedidos cancelados.

#### Tabela de Rastreabilidade

| Problema ou KPI | Tabelas envolvidas | Consulta no script |
| :--- | :--- | :--- |
| `P1` — Ruptura de estoque | `PRODUTO` | `G03` |
| `P2` — Acompanhamento financeiro e de vendas | `PEDIDO`, `PAGAMENTO`, `CLIENTE`, `DESPESA` | `G01, G02, G10, G11` |
| `P3` — Falta de análise dos canais e controle dos recebimentos | `PEDIDO`, `PAGAMENTO` | `G05, G07, G08, G12` |
| `P4` — Falta de controle de cancelamentos e reembolsos | `PEDIDO`, `PAGAMENTO` | `G06, G13` |
| `P5` — Desconhecimento dos produtos e da rentabilidade | `PRODUTO`, `PEDIDO`, `ITEM_PEDIDO`, `DESPESA` | `G04, G09, G10` |
| `KPI 1` — Faturamento mensal | `PEDIDO` | `G01` |
| `KPI 2` — Receita após taxas | `PEDIDO` | `G01` |
| `KPI 3` — Pedidos concluídos por mês | `PEDIDO` | `G02` |
| `KPI 4` — Ticket médio | `PEDIDO` | `G02` |
| `KPI 5` — Produtos abaixo do estoque mínimo | `PRODUTO` | `G03` |
| `KPI 6` — Produtos mais vendidos | `PRODUTO`, `PEDIDO`, `ITEM_PEDIDO` | `G04` |
| `KPI 7` — Vendas por canal | `PEDIDO` | `G05` |
| `KPI 8` — Taxa de cancelamento | `PEDIDO` | `G06` |
| `KPI 9` — Arrecadação por forma de pagamento | `PAGAMENTO` | `G07` |
| `KPI 10` — Pedidos em aberto | `PEDIDO`, `PAGAMENTO` | `G08` |
| `KPI 11` — Margem por produto | `PRODUTO`, `PEDIDO`, `ITEM_PEDIDO` | `G09` |
| `KPI 12` — Resultado operacional estimado | `PRODUTO`, `PEDIDO`, `ITEM_PEDIDO`, `DESPESA` | `G10` |
| `KPI 13` — Clientes sem compra efetiva | `CLIENTE`, `PEDIDO` | `G11` |
| `KPI 14` — Pedidos com pagamento dividido | `PAGAMENTO`, `PEDIDO` | `G12` |
| `KPI 15` — Estornos por cancelamento | `PAGAMENTO`, `PEDIDO` | `G13` |

---

## 2. Modelo Lógico Relacional

- **Ferramenta utilizada:** brModelo (modelo lógico).
- **Imagem do modelo lógico:** ![DER Lógico](./DER%20logico/der_logico.png)
- **Observação sobre tipos:** O brModelo não oferece os tipos `DECIMAL` nem tamanhos para `VARCHAR`. Por isso, o diagrama pode apresentar `FLOAT` nos campos monetários; no dicionário de dados e no script SQL, os campos financeiros devem utilizar `DECIMAL(10,2)`.

---

## 3. Script SQL Completo

O script SQL completo para criação do banco de dados MySQL, inserção de tabelas, restrições e consultas está localizado em:
[Acessar Script SQL](./docs/script.sql)


---

## 4. Massa de Dados

A massa de dados foi elaborada de forma fictícia e coerente com a escala da organização (simulando proporções reais de seus 3.000 atendimentos mensais) para testar o comportamento do sistema sob cenários operacionais variados.

O arquivo contendo a carga de dados está integrado no script principal ou disponível separadamente em:[Acessar Massa de Dados](./docs/massa_de_dados.sql)


---

## 5. Repositório GitHub e Dicionário de Dados
- **Dicionário de Dados:** [Acessar pasta do Dicionário de Dados](./Dicionario%20de%20dados/)

---

## 6. Uso de Inteligência Artificial

| Item | O que registrar |
| :--- | :--- |
| **Ferramenta e etapa** | ChatGPT (OpenAI) / Gemini (Google) utilizado nas etapas de redação do relatório técnico, estruturação da massa de dados, auxílio na escrita das queries SQL, pesquisa sobre KPIs de restaurantes e criação de slides. |
| **Motivação** | Agilizar a estruturação do texto dentro do padrão do esqueleto e acelerar a geração de inserts sintéticos e coerentes para a massa de dados. |
| **Prompt(s) utilizados** | *"Gere 20 inserts SQL fictícios para a tabela PEDIDO considerando canais como WhatsApp e Delivery, status variados e mantendo coerência com dados de clientes.", "Me envie KPIs que são usadas em resturantes (vendas, financeiros, estoque, atendimentos e clientes)* |
| **Resposta recebida** | Códigos `INSERT INTO` contendo dados sintéticos para popular o banco. 29 KPIs utilizadas em restaurantes.|
| **Fontes consultadas e verificadas** | Manual de referência do MySQL 8.0 para validação das sintaxes de `CONSTRAINT` e `CHECK`. |
| **Trechos rejeitados ou corrigidos** | Foram ajustados os tipos de dados monetários para `DECIMAL(10,2)` onde a IA havia sugerido `FLOAT`. |
| **Justificativa da escolha final** | O uso de `DECIMAL` evita problemas de arredondamento em cálculos financeiros no MySQL. |
| **Reflexão crítica** | A IA acelera a escrita repetitiva, mas exige validação rigorosa sobre as restrições relacionais para não gerar inconsistências de chave estrangeira (`FK`) |

---

## 7. Apresentação Corporativa Final
[Acessar Slides](./docs/apresentacao.pdf)

