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
- - `P1`: **Acompanhamento dos pedidos de delivery:** dificuldade para acompanhar o recebimento, a preparação e o encaminhamento dos pedidos realizados por WhatsApp e aplicativos de delivery.

- `P2`: **Controle de cancelamentos e reembolsos:** necessidade de manter o histórico de pedidos cancelados, motivos, itens e informações financeiras relacionadas.

- `P3`: **Comparação entre canais de venda:** necessidade de consultar e comparar as vendas realizadas presencialmente, pelo WhatsApp e pelos aplicativos de delivery.

- `P4`: **Organização das informações financeiras:** necessidade de acompanhar vendas, pagamentos e despesas por período para facilitar o fechamento e a análise dos resultados.

- `P5`: **Acompanhamento dos produtos e do estoque:** necessidade de identificar produtos abaixo do estoque mínimo, acompanhar compras e reduzir o risco de falta de mercadorias.

  

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
- `RN02`: O sistema deve impedir a inclusão de produtos em pedidos quando não houver estoque suficiente.
- `RN03`: Quando um pedido for cancelado, seu registro e as informações relevantes — como número, data, valor, produtos, motivo e registro de pagamento/reembolso — devem ser preservados para consulta histórica.
- `RN04`: O preço registrado no item do pedido deve preservar o valor praticado no momento da venda, sem ser alterado por futuras mudanças no cadastro do produto.
- `RN05`: Cada pedido deve possuir um identificador único. A numeração deve ser sequencial e gerada automaticamente pelo sistema.


#### Notação do DER Conceitual
- **Ferramenta utilizada:** brModelo.
- **Link/Imagem do DER:** ![DER Conceitual](./DER%20conceitual/der_conceitual.png)

#### Ajustes do Modelo em Relação à Entrega 1
| Apontamento da Entrega 1 | Alteração realizada | Justificativa |
|---|---|---|
| Ausência de controle dos itens do pedido | Criada a entidade associativa `ITEM_PEDIDO` | Permitir registrar vários produtos no mesmo pedido |
| Falta de controle de compras | Criadas `COMPRA` e `ITEM_COMPRA` | Registrar produtos adquiridos e seus custos |
| Falta de acompanhamento de entregas | Criada a entidade `ENTREGA` | Controlar pedidos enviados por delivery |



---

### 1.2 Conversão do Modelo Conceitual para o Modelo Lógico

O modelo lógico foi obtido do DER conceitual aplicando as regras de conversão abaixo. O resultado são 13 tabelas: 11 vindas de entidades e 2 tabelas associativas (`ITEM_PEDIDO` e `ITEM_COMPRA`).

1. **Entidades → Tabelas:** Cada entidade do modelo conceitual (`CLIENTE`, `ENDERECO`, `PRODUTO`, `CATEGORIA`, `PEDIDO`, `PAGAMENTO`, `ENTREGA`, `FORNECEDOR`, `COMPRA`, `DESPESA` e `FUNCIONARIO`) foi convertida em uma tabela relacional, com uma chave primária inteira própria (`id_<entidade>`).
2. **Atributos → Colunas:** Cada atributo virou uma coluna com tipo SQL, conforme o modelo lógico e o script. Os campos monetários usam `DECIMAL(10,2)`. O brModelo não oferece esse tipo e mostra `FLOAT` no diagrama, por isso o dicionário de dados e o script SQL são a referência dos tipos.
3. **Atributo composto e multivalorado → Tabela própria:** O endereço do cliente (rua, número, bairro, CEP e complemento) é composto, e um cliente pode ter mais de um endereço de entrega. Por isso ele virou a tabela `ENDERECO`, com FK para `CLIENTE`. `[VALIDAR COM O DER CONCEITUAL: confirmar que ENDERECO é tratado assim no modelo conceitual]`
4. **Relacionamentos N:N → Tabelas associativas:** Dois relacionamentos N:N foram convertidos em tabelas associativas, cada uma com os atributos próprios da relação:
   - `PEDIDO` N:N `PRODUTO` → `ITEM_PEDIDO` (`quantidade` e `preco_unitario`, o preço praticado na venda).
   - `COMPRA` N:N `PRODUTO` → `ITEM_COMPRA` (`quantidade` e `custo_unitario`, o custo pago na compra).

   Em ambas, a PK é composta pelas duas chaves estrangeiras.
5. **Relacionamentos 1:N:** A chave primária da tabela do lado “1” foi propagada como chave estrangeira na tabela do lado “N”:
   - `CATEGORIA` 1:N `PRODUTO` (`PRODUTO.id_categoria`)
   - `CLIENTE` 1:N `PEDIDO` (`PEDIDO.id_cliente`)
   - `FUNCIONARIO` 1:N `PEDIDO` (`PEDIDO.id_funcionario`)
   - `CLIENTE` 1:N `ENDERECO` (`ENDERECO.id_cliente`)
   - `ENDERECO` 1:N `ENTREGA` (`ENTREGA.id_endereco`)
   - `PEDIDO` 1:N `PAGAMENTO` (`PAGAMENTO.id_pedido`)
   - `FORNECEDOR` 1:N `COMPRA` (`COMPRA.id_fornecedor`)
   - `FUNCIONARIO` 1:N `DESPESA` (`DESPESA.id_funcionario`)
6. **Relacionamentos 1:1:** `PEDIDO` e `ENTREGA` têm relação 1:1: um pedido de delivery gera uma única entrega. Para garantir isso, a FK `ENTREGA.id_pedido` recebe a restrição `UNIQUE`. `[VALIDAR NO SCRIPT SQL: confirmar o UNIQUE em ENTREGA.id_pedido]` Já `PEDIDO` e `PAGAMENTO` são **1:N**, e não 1:1, porque um pedido pode ser pago em mais de uma transação (RF05 e KPI 14, pedidos com pagamento dividido) e pode ter pagamento reembolsado (KPI 15). Por isso `PAGAMENTO.id_pedido` não tem `UNIQUE`.

---

### 1.3 Definição de Chaves Primárias e Estrangeiras

#### Chaves primárias

Todas as tabelas que representam uma entidade usam uma PK **substituta**, do tipo `INT AUTO_INCREMENT`. Nenhum atributo do negócio serve bem como chave: nomes se repetem, telefones mudam e descrições podem ser editadas. Um inteiro curto e sem significado próprio nunca precisa ser alterado, ocupa pouco espaço nas FKs e agiliza os `JOIN`s. No caso de `PEDIDO`, o `AUTO_INCREMENT` também gera a numeração única e sequencial exigida pela `RN05`.

As tabelas associativas usam **PK composta**, formada pelas duas FKs. Isso identifica cada linha pelo par (pedido, produto) ou (compra, produto) e impede que o mesmo produto apareça duas vezes no mesmo pedido ou na mesma compra; se o cliente pede mais unidades, aumenta-se a `quantidade`. Não é necessário criar uma chave artificial para essas tabelas.

#### Resumo de chaves e justificativas

| Tabela | Chave primária | Chaves estrangeiras | Justificativa |
| :--- | :--- | :--- | :--- |
| `CATEGORIA` | `id_categoria` | — | Identifica a categoria sem depender do nome, que pode ser renomeado. |
| `FORNECEDOR` | `id_fornecedor` | — | Dois fornecedores podem ter nomes parecidos; o código identifica cada um. |
| `CLIENTE` | `id_cliente` | — | O telefone muda e pode ser compartilhado, então não serve como chave. |
| `FUNCIONARIO` | `id_funcionario` | — | Identifica o funcionário em pedidos e despesas sem expor dados pessoais. |
| `PRODUTO` | `id_produto` | `id_categoria` → `CATEGORIA.id_categoria` | Todo produto pertence a uma categoria existente, e a FK impede categoria inválida. |
| `PEDIDO` | `id_pedido` | `id_cliente` → `CLIENTE.id_cliente`<br>`id_funcionario` → `FUNCIONARIO.id_funcionario` | Numeração única e sequencial (RN05). As FKs registram quem comprou e quem atendeu. |
| `ITEM_PEDIDO` | (`id_pedido`, `id_produto`) | `id_pedido` → `PEDIDO.id_pedido`<br>`id_produto` → `PRODUTO.id_produto` | A PK composta evita o mesmo produto repetido no pedido; as FKs impedem item sem pedido ou sem produto. |
| `ENDERECO` | `id_endereco` | `id_cliente` → `CLIENTE.id_cliente` | Um cliente pode ter vários endereços; cada um pertence a um cliente existente. |
| `PAGAMENTO` | `id_pagamento` | `id_pedido` → `PEDIDO.id_pedido` | Um pedido pode ter vários pagamentos (pagamento dividido e reembolso), então o pagamento tem chave própria. |
| `ENTREGA` | `id_entrega` | `id_pedido` → `PEDIDO.id_pedido`<br>`id_endereco` → `ENDERECO.id_endereco` | Liga a entrega ao pedido e ao endereço de destino, que precisa existir (RN01). |
| `COMPRA` | `id_compra` | `id_fornecedor` → `FORNECEDOR.id_fornecedor` | Toda compra tem um fornecedor cadastrado. |
| `ITEM_COMPRA` | (`id_compra`, `id_produto`) | `id_compra` → `COMPRA.id_compra`<br>`id_produto` → `PRODUTO.id_produto` | Mesmo raciocínio de `ITEM_PEDIDO`: um produto por compra, com quantidade e custo. |
| `DESPESA` | `id_despesa` | `id_funcionario` → `FUNCIONARIO.id_funcionario` | Registra quem lançou a despesa. |

#### Justificativa das chaves estrangeiras

As chaves estrangeiras representam os relacionamentos do modelo e garantem a **integridade referencial**: o banco recusa um pedido de cliente inexistente, um item de produto removido ou uma entrega sem endereço. Algumas decisões merecem destaque:

- **`PEDIDO.id_cliente` é opcional.** A `RN01` exige dados do cliente apenas para pedidos com entrega; pedidos presenciais podem ser registrados sem cliente. `[VALIDAR NO SCRIPT SQL: confirmar que a coluna aceita NULL]`
- **`ENTREGA.id_endereco` é obrigatória.** Uma entrega sem endereço de destino não pode ser realizada (`RN01`).
- **`PAGAMENTO.id_pedido` aponta para o pedido, e não o contrário.** Assim um mesmo pedido pode ter vários pagamentos, o que atende o KPI 14.
- **As FKs não usam exclusão em cascata.** Pedidos cancelados e seus registros financeiros devem ser preservados (`RN03`), então não se apaga um registro que ainda é referenciado. `[VALIDAR NO SCRIPT SQL: ON DELETE/ON UPDATE]`

---

### 1.4 Processo de Normalização (1FN, 2FN e 3FN)

#### 1ª Forma Normal (1FN)

Na 1FN, todo atributo tem um único valor atômico e não há grupos repetidos. Foram feitos estes ajustes:

- **Itens de pedido e de compra:** Em vez de guardar a lista de produtos em uma coluna do pedido ou da compra, cada produto ocupa uma linha própria em `ITEM_PEDIDO` ou `ITEM_COMPRA`.
- **Endereço:** Os dados de endereço foram separados em colunas individuais (`rua`, `numero`, `bairro`, `cep` e `complemento`), e como um cliente pode ter mais de um, eles ficam em uma tabela própria (`ENDERECO`).
- **Telefones de `CLIENTE`:** A tabela tem `telefone` e `telefone_2`. Cada coluna guarda um único valor, mas estritamente são dois campos do mesmo tipo. A decisão proposta é mantê-los, porque o modelo prevê apenas um telefone principal e um alternativo, e nenhum requisito ou KPI do relatório exige consultar todos os telefones de um cliente. `[VALIDAR COM O GRUPO: manter os dois campos ou criar uma tabela TELEFONE]`

#### 2ª Forma Normal (2FN)

A 2FN exige que todo atributo que não faz parte da chave dependa da chave inteira, e não de apenas uma parte dela. Isso só importa nas tabelas com PK composta. Nas demais, a PK tem uma única coluna e a condição já é satisfeita.

**Normalização de `ITEM_PEDIDO`** (PK: `id_pedido` + `id_produto`):

- **1FN:** cada linha representa um produto em um pedido, com valores atômicos e sem listas.
- **2FN:** `quantidade` e `preco_unitario` dependem do par (pedido, produto) por inteiro: a quantidade de um produto é diferente em cada pedido, e o preço praticado também. O nome, a descrição e o preço atual do produto dependeriam só de `id_produto`, ou seja, de parte da chave. Por isso ficam em `PRODUTO`, e não em `ITEM_PEDIDO`.
- **3FN:** nenhum atributo não-chave determina outro. `preco_unitario` não é repetição de `PRODUTO.preco`: é o preço **praticado na venda**, que pode ser diferente do preço atual (`RN04`). O subtotal do item não é armazenado, porque é calculável (`quantidade × preco_unitario`).

**Normalização de `ITEM_COMPRA`** (PK: `id_compra` + `id_produto`):

- **1FN:** cada linha representa um produto em uma compra.
- **2FN:** `quantidade` e `custo_unitario` dependem do par (compra, produto) por inteiro. O fornecedor depende só de `id_compra`, e por isso `id_fornecedor` fica em `COMPRA`; se estivesse em `ITEM_COMPRA`, seria uma dependência parcial e seria repetido a cada item.
- **3FN:** `custo_unitario` é o custo pago naquela compra, que muda de uma compra para outra. Não é derivado de `PRODUTO.preco`, que é o preço de venda.

#### 3ª Forma Normal (3FN)

A 3FN exige que nenhum atributo não-chave dependa de outro atributo não-chave (dependência transitiva). Foram aplicados estes ajustes:

- **Categoria:** `PRODUTO` guarda apenas `id_categoria`. O nome da categoria fica em `CATEGORIA`, e assim não se repete em cada produto.
- **Cliente, funcionário e fornecedor:** `PEDIDO`, `COMPRA` e `DESPESA` guardam só as chaves estrangeiras; nome, telefone e cargo ficam nas tabelas de origem.
- **Endereço de entrega:** `ENTREGA` guarda `id_endereco` e não repete rua, bairro ou CEP.
- **Dados derivados:** o subtotal de cada item e o total do pedido podem ser calculados a partir de `ITEM_PEDIDO`, então não precisam ser guardados. `[VALIDAR NO SCRIPT SQL: se existir valor_total em PEDIDO (usado nos KPIs 1, 2 e 4), justificar como desnormalização controlada para consulta]`

Com isso, todas as 13 tabelas estão na 3FN.

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
| `P1` — Acompanhamento dos pedidos de delivery | `PEDIDO`, `ITEM_PEDIDO`, `ENTREGA`, `CLIENTE`, `FUNCIONARIO` | `G11, G12` |
| `P2` — Controle de cancelamentos e reembolsos | `PEDIDO`, `ITEM_PEDIDO`, `PAGAMENTO` | `G06, G13` |
| `P3` — Comparação entre canais de venda | `PEDIDO`, `PAGAMENTO` | `G05, G07` |
| `P4` — Organização das informações financeiras | `PEDIDO`, `PAGAMENTO`, `DESPESA` | `G01, G02, G08, G10` |
| `P5` — Acompanhamento dos produtos e do estoque | `PRODUTO`, `CATEGORIA`, `FORNECEDOR`, `COMPRA`, `ITEM_COMPRA` | `G03, G04, G09` |
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

Os comandos INSERT INTO da massa de dados estão integrados ao script principal. Acesse o arquivo docs/script.sql para consultar a criação do banco, as tabelas, as restrições, a massa fictícia e as consultas SQL.



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
