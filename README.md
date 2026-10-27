# Entrega 2 — Modelo Lógico, Implementação SQL e Apresentação Final

## Sistema de Gestão de Informações — Donna Claudia Restaurante e Lanchonete

---

### Integrantes

| Nome completo do aluno | RGM | Usuário do GitHub |
| :--- | :--- | :--- |
| Augusto de Almeida Guelere | 48832588 | guelerzao |
| Felipe Rodrigues da Silva | 47868384 | fevipsilva7-blip |
| Lucas Freitas de Oliveira | 048587885 | dzskl |
| Matheus Faustino da Silva | 47854928 | Matheussil01 |
| Otavio Estevam Ventura | 48763390 | cVenturaDev |

---

## 1. Relatório Técnico Final

### 1.1 Revisão do Modelo Conceitual

#### cccccaracterização da Organização
- **Nome e natureza da organização:** Donna Claudia Restaurante e Lanchonete (CNPJ: 36.276.829/0001-69). Trata-se de uma empresa privada comercial com fins lucrativos do ramo alimentício.
- **Contexto e porte:** O restaurante está em operação há aproximadamente 2 anos e conta atualmente com 5 funcionários. Atende um volume médio de cerca de 3.000 clientes por mês (aproximadamente 750 pedidos/atendimentos por semana), operando com vendas presenciais, lanches, refeições e forte fluxo via WhatsApp e aplicativos de delivery.
- **Problemas e necessidades identificados:**
  - `P1`: **Desorganização e falhas na operação do Delivery:** Dificuldade no acompanhamento dos pedidos em tempo real, integrando o recebimento de canais externos (WhatsApp/Apps), status de preparo na cozinha e despacho/entrega.
  - `P2`: **Falta de controle estruturado para Exceções (Cancelamentos/Reembolsos):** Ausência de histórico unificado quando ocorrem problemas na entrega (itens faltantes, divergências de pedido), gerando retrabalho manual e inconsistências na conferência financeira final.
  - `P3`: **Descentralização dos Dados Financeiros e Canais de Venda:** Dificuldade em comparar diretamente o volume e faturamento entre o WhatsApp e os aplicativos de delivery, além de consolidar despesas operacionais com o faturamento em um só local.
- **Escopo do sistema:** O banco de dados reúne as informações globais da organização, englobando clientes, produtos, categorias de itens, fornecedores, compras de estoque, despesas, funcionários, pedidos, itens do pedido, status de entrega e registros de pagamento/reembolso.
- **Justificativa da escolha:** Organização real de pequeno porte com operação intensa e processos de negócio bem delimitados. Apresenta desafios reais de gestão de dados adequados para o desenvolvimento da modelagem relacional.
- **Evidências da organização:** 
  - **Endereço:** Rua Maciel Monteiro, nº 264.
  - **Perfil Google Meu Negócio / Comprovante:** `[PREENCHER - Inserir Link do Google Business Profile ou Endereço Completo]`
  - **Fotos do Local:** `[PREENCHER - Adicionar imagem PNG/JPG no repositório, ex: /imagens/fachada.jpg e referenciar aqui]`
- **Responsável pela organização:** Proprietária e Administradora. `[PREENCHER - Inserir Nome Completo da Proprietária e Telefone de Contato]`.

#### Relato da Entrevista
- **Quem:** Entrevistas realizadas com a proprietária/gerente do estabelecimento.
- **Quando e onde:** Entrevistas presencialmente no ambiente do restaurante.
- **Achados da Observação Presencial:** Observou-se a dinâmica de recepção de mensagens via WhatsApp, a impressão/anotação manual de pedidos para a cozinha, a conferência diária do estoque pelo gerente e o fechamento do caixa ao final do expediente.
- **Comprovação:** `[PREENCHER - Adicionar a foto da entrevista no local no repositório, ex: /imagens/entrevista.jpg]`
- **O que foi levantado:** O detalhamento completo da rotina operacional, regras de exceção e requisitos foi consolidado no documento dedicado no repositório: [Acessar Levantamento Completo (levantamento/levantamento.md)](./levantamento/levantamento.md).

#### Resumo do Levantamento

##### Processos de Negócio Mapeados
1. **Cadastro e Gestão de Clientes:** Identificação obrigatória para entregas de delivery (nome, telefone, endereço) e opcional para atendimentos presenciais.
2. **Emissão e Acompanhamento de Pedidos:** Registro da origem (WhatsApp ou App), composição dos itens, status de preparo e atribuição de entregas.
3. **Controle de Estoque e Compras:** Atualização diária dos insumos/produtos e registro de aquisições junto a fornecedores ou mercados.
4. **Gestão de Pagamentos e Reembolsos:** Liquidação das vendas por múltiplos meios (Pix, Cartão, Dinheiro) e controle de estornos decorrentes de cancelamentos.
5. **Gestão Financeira e Despesas:** Lançamento de custos operacionais e fechamento de caixa diário/mensal.

##### Requisitos do Sistema
- **Requisitos Funcionais:**
  - `RF01`: O sistema deve permitir cadastrar clientes informando nome completo, telefone e endereço (logradouro, número, bairro, CEP).
  - `RF02`: O sistema deve registrar produtos com código, nome, categoria, preço unitário e quantidade atual em estoque.
  - `RF03`: O sistema deve registrar pedidos contendo número único, data/hora, cliente, origem/canal, valor total e status do pedido.
  - `RF04`: O sistema deve associar itens ao pedido, indicando o produto, a quantidade solicitada e o preço praticado.
  - `RF05`: O sistema deve registrar pagamentos vinculados ao pedido, especificando forma de pagamento e status (pendente, pago, reembolsado).
  - `RF06`: O sistema deve emitir alertas automáticos quando a quantidade de um produto atingir o limite mínimo de estoque.
  - `RF07`: O sistema deve registrar justificativas e históricos em pedidos cancelados ou reembolsados.
- **Requisitos Não Funcionais:**
  - `RNF01`: O sistema deve possuir interface adaptável para execução em computador desktop e dispositivos móveis.
  - `RNF02`: O sistema deve ser de simples usabilidade, voltado para operadores com perfil leigo em tecnologia.
  - `RNF03`: O acesso às informações financeiras e aos relatórios estratégicos deve ser restrito por permissões por perfil (proprietária/gerente).

##### Regras de Negócio
- `RN01`: Todo pedido de delivery precisa obrigatoriamente estar vinculado a um cliente cadastrado com telefone e endereço válidos.
- `RN02`: Um item só pode ser adicionado ao pedido se houver quantidade disponível suficiente em estoque.
- `RN03`: Em caso de cancelamento do pedido, o registro do pedido não é excluído do banco; altera-se seu status para "Cancelado" mantendo o motivo e o histórico financeiro associado.
- `RN04`: A alteração do preço de um produto no cadastro não pode alterar o valor unitário já registrado nos pedidos passados.
- `RN05`: Cada pedido possui uma numeração única gerada sequencialmente pelo sistema.

#### Notação do DER Conceitual
- **Ferramenta Utilizada:** Criado no software `[PREENCHER - Ex: brModelo / Lucidchart / Draw.io]`.
- **Link/Imagem do DER:** `[PREENCHER - Adicionar a imagem do DER no repositório em /imagens/der_conceitual.png]`

#### Ajustes do Modelo em Relação à Entrega 1

| Apontamento da correção da E1 | O que mudou no trabalho | Por quê |
| :--- | :--- | :--- |
| *Exemplo: Ausência de entidade para cancelamentos/reembolsos* | *Criado o controle de status e histórico financeiro na tabela PAGAMENTO e PEDIDO* | *Para cobrir o problema P2 e garantir que valores estornados sejam computados na auditoria de caixa.* |
| *Exemplo: Ausência de vínculo de canal de venda* | *Adicionado o campo do canal do pedido (WhatsApp vs. Apps)* | *Necessário para resolver o problema P3 de comparação de métricas.* |
| `[PREENCHER OU ADAPTAR - Inserir correções feitas]` | `[PREENCHER - Detalhar alteração]` | `[PREENCHER - Justificar]` |

---

### 1.2 Conversão do Modelo Conceitual para o Modelo Lógico

1. **Entidades $\rightarrow$ Tabelas:** Cada entidade do modelo conceitual (`CLIENTE`, `PRODUTO`, `CATEGORIA`, `PEDIDO`, `PAGAMENTO`, `ENTREGA`, `FORNECEDOR`, `COMPRA`, `DESPESA`, `FUNCIONARIO`) foi convertida em uma tabela relacional.
2. **Atributos $\rightarrow$ Colunas:** Atributos simples viraram colunas com seus respectivos tipos de dados SQL (`VARCHAR`, `INT`, `DECIMAL`, `DATETIME`).
3. **Relacionamentos N:N $\rightarrow$ Tabelas Associativas:** O relacionamento N:N entre `PEDIDO` e `PRODUTO` foi convertido na tabela associativa `ITEM_PEDIDO`, que guarda os atributos próprios da relação (quantidade e preço unitário praticado na venda).
4. **Relacionamentos 1:N:** A chave primária (PK) da tabela do lado "1" foi propagada como chave estrangeira (FK) na tabela do lado "N" (ex.: `id_cliente` em `PEDIDO`).
5. **Relacionamentos 1:1:** O relacionamento entre `PEDIDO` e `ENTREGA`/`PAGAMENTO` utiliza a PK de `PEDIDO` como FK com restrição de unicidade (`UNIQUE`), garantindo a integridade do vínculo.

---

### 1.3 Definição de Chaves Primárias e Estrangeiras

- `CATEGORIA`: PK (`id_categoria`)
- `FORNECEDOR`: PK (`id_fornecedor`)
- `CLIENTE`: PK (`id_cliente`)
- `FUNCIONARIO`: PK (`id_funcionario`)
- `PRODUTO`: PK (`id_produto`), FK (`id_categoria` $\rightarrow$ `CATEGORIA.id_categoria`)
- `PEDIDO`: PK (`id_pedido`), FK (`id_cliente` $\rightarrow$ `CLIENTE.id_cliente`), FK (`id_funcionario` $\rightarrow$ `FUNCIONARIO.id_funcionario`)
- `ITEM_PEDIDO`: PK Composta (`id_pedido`, `id_produto`), FK (`id_pedido` $\rightarrow$ `PEDIDO.id_pedido`), FK (`id_produto` $\rightarrow$ `PRODUTO.id_produto`)
- `ENTREGA`: PK (`id_entrega`), FK (`id_pedido` $\rightarrow$ `PEDIDO.id_pedido`)
- `PAGAMENTO`: PK (`id_pagamento`), FK (`id_pedido` $\rightarrow$ `PEDIDO.id_pedido`)
- `COMPRA`: PK (`id_compra`), FK (`id_fornecedor` $\rightarrow$ `FORNECEDOR.id_fornecedor`)
- `DESPESA`: PK (`id_despesa`)

---

### 1.4 Processo de Normalização (1FN, 2FN e 3FN)

- **1ª Forma Normal (1FN):**
  - **Ação:** Eliminação de atributos multivalorados e compostos. Atributos de endereço do cliente foram atomizados em colunas individuais (`logradouro`, `numero`, `bairro`, `cep`). Listas de itens em pedidos foram removidas e transferidas para a tabela `ITEM_PEDIDO`.
- **2ª Forma Normal (2FN):**
  - **Ação:** Eliminação de dependências parciais. Na tabela associativa `ITEM_PEDIDO` (chave composta `id_pedido` + `id_produto`), o atributo `preco_unitario` registrado no momento da compra e a `quantidade` dependem de toda a chave composta, enquanto dados cadastrais do produto pertencem apenas a `PRODUTO`.
- **3ª Forma Normal (3FN):**
  - **Ação:** Eliminação de dependências transitivas. Dados da categoria do produto (ex.: `nome_categoria`) foram isolados na tabela `CATEGORIA`, evitando que colunas não-chave dependam de outros atributos não-chave na tabela `PRODUTO`.

---

### 1.5 Justificativas Técnicas das Decisões

- **Chaves Primárias Autoincrementais (`INT AUTO_INCREMENT`):** Adotadas para simplificar o indexamento físico no MySQL e acelerar operações de junção (`JOIN`).
- **Inclusão do atributo `preco_unitario` em `ITEM_PEDIDO`:** Garante o cumprimento da regra `RN04`. Previne que alterações no preço da tabela de produtos afetem o histórico financeiro de vendas passadas.
- **Uso de Enums / Restrições `CHECK`:** Restrições aplicadas sobre canais de atendimento, formas de pagamento e status (`pendente`, `pago`, `reembolsado`, `cancelado`) garantem a consistência e integridade dos dados no nível do SGBD.
- **Manutenção de Registros em Cancelamentos:** Atende à regra `RN03`, garantindo a rastreabilidade exigida pela contabilidade e protegendo o sistema contra fraudes ou perdas de dados operacionais.

---

### 1.6 Proposta de Arquitetura Analítica para BI e IA

#### Informações Estratégicas e Métricas Gerenciais (KPIs)
- **KPI 1 — Ticket Médio por Canal de Venda:** Identifica a rentabilidade média dos pedidos vindos do WhatsApp versus aplicativos de delivery.
- **KPI 2 — Índice de Cancelamento e Reembolso:** Percentual de pedidos cancelados no mês e valor total reembolsado.
- **KPI 3 — Relatório de Ruptura de Estoque:** Lista de produtos com saldo abaixo do estoque mínimo definido.
- **KPI 4 — Produtos mais Vendidos:** Ranking de faturamento e volume por item/categoria.

#### Tabela de Rastreabilidade

| Problema ou KPI | Tabelas envolvidas | Consulta no script |
| :--- | :--- | :--- |
| `P1` — Gestão de entregas e acompanhamento de status | `PEDIDO`, `ENTREGA`, `CLIENTE` | `G01` |
| `P2` — Auditoria de cancelamentos e reembolsos | `PEDIDO`, `PAGAMENTO` | `G02` |
| `P3` — Comparativo de faturamento por canal de vendas | `PEDIDO`, `PAGAMENTO` | `G03` |
| `KPI 3` — Alertas de ruptura de estoque | `PRODUTO` | `G04` |
| `RN03` — Verificação de integridade nos pedidos cancelados | `PEDIDO`, `PAGAMENTO` | `A01` |
| `RN02` — Auditoria de estoque negativo ou incoerente | `PRODUTO` | `A02` |

---

## 2. Modelo Lógico Relacional

- **Ferramenta utilizada:** brModelo (modelo lógico)
- **Arquivo do modelo lógico:** [Logic model - BRMW 02.pdf](./Logic%20model%20-%20BRMW%2002.pdf)
- - **Observação sobre tipos:** o brModelo não oferece DECIMAL nem tamanho de VARCHAR. Por isso o diagrama mostra FLOAT nos campos monetários; no dicionário de dados e no script SQL esses campos são `DECIMAL(10,2)`, para evitar erros de arredondamento em valores financeiros.
---

## 3. Script SQL Completo

O script SQL completo para criação do banco de dados MySQL, inserção de tabelas, restrições e consultas está localizado em:
👉 **[Acessar Script SQL Completo (docs/script.sql)](./docs/script.sql)**

---

## 4. Massa de Dados

A massa de dados foi elaborada de forma fictícia e coerente com a escala da organização (simulando proporções reais de seus 3.000 atendimentos mensais) para testar o comportamento do sistema sob cenários operacionais variados.

O arquivo contendo a carga de dados está integrado no script principal ou disponível separadamente em:
👉 **[Acessar Massa de Dados SQL (docs/massa_de_dados.sql)](./docs/massa_de_dados.sql)** `[PREENCHER OU ATUALIZAR CONFORME A ESTRUTURA DO SEU REPOSITÓRIO]`

---

## 5. Repositório GitHub e Dicionário de Dados

- **Dicionário de Dados:** descreve tipos, chaves e restrições (obrigatoriedade, unicidade, valores permitidos e padrão) de cada coluna: [dicionario_de_dados.html](./dicionario_de_dados.html)

---

## 6. Uso de Inteligência Artificial

| Item | O que registrar |
| :--- | :--- |
| **Ferramenta e etapa** | ChatGPT (OpenAI) / Gemini (Google) utilizado nas etapas de redação do relatório técnico, estruturação da massa de dados e auxílio na escrita das queries SQL. |
| **Motivação** | Agilizar a estruturação do texto dentro do padrão do esqueleto e acelerar a geração de inserts sintéticos e coerentes para a massa de dados. |
| **Prompt(s) utilizados** | *"Gere 20 inserts SQL fictícios para a tabela PEDIDO considerando canais como WhatsApp e Delivery, status variados e mantendo coerência com dados de clientes."* |
| **Resposta recebida** | Códigos `INSERT INTO` contendo dados sintéticos para popular o banco. |
| **Fontes consultadas e verificadas** | Manual de referência do MySQL 8.0 para validação das sintaxes de `CONSTRAINT` e `CHECK`. |
| **Trechos rejeitados ou corrigidos** | Foram ajustados os tipos de dados monetários para `DECIMAL(10,2)` onde a IA havia sugerido `FLOAT`. |
| **Justificativa da escolha final** | O uso de `DECIMAL` evita problemas de arredondamento em cálculos financeiros no MySQL. |
| **Reflexão crítica** | A IA acelera a escrita repetitiva, mas exige validação rigorosa sobre as restrições relacionais para não gerar inconsistências de chave estrangeira (`FK`) |

---

## 7. Apresentação Corporativa Final

- **Estrutura dos Slides:** Os slides para a apresentação corporativa de 8 minutos estão disponíveis na pasta `/docs` do repositório:
  👉 **[Acessar Slides da Apresentação (docs/apresentacao.pdf)](./docs/apresentacao.pdf)** `[PREENCHER - Inserir o link correto dos seus slides]`
