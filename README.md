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
- `P1`: **Acompanhamento dos pedidos de delivery:** dificuldade para acompanhar o recebimento, a preparação e o encaminhamento dos pedidos realizados por WhatsApp e aplicativos de delivery.

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
- **Comprovação:** A entrevista foi registrada no levantamento. A fotografia da entrevista não foi publicada no repositório por motivo de privacidade da entrevistada.
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

Os códigos abaixo são os mesmos do levantamento (`Levantamento/levantamento.md`), do dicionário de dados e das consultas de auditoria do `docs/script.sql`. As regras `RN01` a `RN22` vieram do levantamento com a proprietária; as regras `RN23` a `RN29` formalizam validações de integridade que o script já implementa.

**Cadastro e pedidos**
- `RN01` — **Dados para delivery:** pedidos que exigem entrega (WhatsApp e aplicativo) devem possuir cliente com nome, telefone e endereço.
- `RN02` — **Pedido presencial:** pedidos presenciais podem ser registrados sem cadastro completo de cliente (`PEDIDO.id_cliente` aceita `NULL`).
- `RN03` — **Identificação do pedido:** cada pedido possui identificador único, sequencial e gerado automaticamente.
- `RN04` — **Funcionário responsável:** todo pedido está relacionado a um funcionário.
- `RN05` — **Itens do pedido:** cada item pertence a um pedido e a um produto existentes, sem repetir o produto no mesmo pedido.
- `RN06` — **Preço praticado:** `ITEM_PEDIDO.preco_unitario` preserva o valor da venda, mesmo que o preço atual do produto mude.

**Estoque e compras**
- `RN07` — **Estoque disponível:** a quantidade em estoque nunca é negativa; o atendimento verifica a disponibilidade antes de confirmar o pedido.
- `RN08` — **Estoque mínimo:** produtos abaixo do estoque mínimo são identificados para reposição.
- `RN09` — **Categoria:** todo produto pertence a uma categoria cadastrada.
- `RN10` — **Compra:** toda compra está relacionada a um fornecedor existente.
- `RN11` — **Item de compra:** cada compra possui itens com produto, quantidade e custo unitário.

**Pagamento e entrega**
- `RN12` — **Formas de pagamento:** Pix, cartão e dinheiro.
- `RN13` — **Pagamento relacionado:** todo pagamento pertence a um pedido existente.
- `RN14` — **Pagamentos múltiplos:** um pedido pode ter mais de um pagamento.
- `RN15` — **Entrega:** pedido presencial não possui entrega; pedido de delivery possui no máximo uma.
- `RN16` — **Endereço da entrega:** toda entrega tem um endereço de destino cadastrado.

**Cancelamento e histórico**
- `RN17` — **Preservação do pedido:** pedido cancelado não é apagado; muda de situação para `Cancelado`.
- `RN18` — **Motivo do cancelamento:** o motivo é registrado no pedido cancelado e só existe em pedido cancelado.
- `RN19` — **Histórico financeiro:** os pagamentos de pedidos cancelados permanecem registrados para conferência.
- `RN20` — **Despesas:** toda despesa possui descrição, categoria, data, valor e funcionário responsável.

**Segurança**
- `RN21` — **Acesso financeiro:** informações financeiras só são acessadas por usuários autorizados, conforme `FUNCIONARIO.nivel_acesso`.
- `RN22` — **Dados pessoais:** nome, telefone e endereço de clientes são usados somente para atendimento e entrega (LGPD).

**Integridade dos dados (implementadas no script)**
- `RN23` — **Pedido com itens:** todo pedido possui ao menos um item.
- `RN24` — **Valor total do pedido:** `PEDIDO.valor_total` é igual à soma de `quantidade × preco_unitario` dos itens.
- `RN25` — **Pedido concluído quitado:** a soma dos pagamentos `Pago` de um pedido concluído é igual ao seu valor total.
- `RN26` — **Estorno:** apenas pedido cancelado possui pagamento `Estornado`, e pedido cancelado não mantém pagamento `Pago`.
- `RN27` — **Endereço do cliente:** o endereço da entrega pertence ao cliente do pedido.
- `RN28` — **Datas coerentes:** a entrega não ocorre antes da saída, entrega `Entregue` exige data de entrega e o pagamento não é anterior ao pedido.
- `RN29` — **Valores positivos:** preços, custos, valores de pagamento e quantidades são maiores que zero.

**Regras prováveis não incluídas:** descontos e cupons, taxas dos aplicativos, programa de fidelidade e emissão fiscal integrada não entram nesta versão, porque o restaurante os executa em sistemas externos ou ainda não os controla e porque o DER aprovado não possui tabelas para eles (ver seção 7 do levantamento).

#### Notação do DER Conceitual
- **Ferramenta utilizada:** brModelo.
- **Link/Imagem do DER:** ![DER Conceitual](./DER%20conceitual/der_conceitual.png)

#### Ajustes do Modelo em Relação à Entrega 1

A tabela compara o modelo da Entrega 1 com o modelo atual. A coluna da esquerda descreve a lacuna encontrada na revisão.

| Apontamento da correção da E1 | O que mudou no trabalho | Por quê |
|---|---|---|
| Produto sem estoque mínimo, o que impedia identificar reposição (P5) | Criada a coluna `PRODUTO.estoque_minimo`, com `CHECK >= 0` | Permite a consulta `G01` (KPI 1) e a auditoria `A02` (`RN07`, `RN08`) |
| Pedido sem valor total e sem motivo de cancelamento | Criadas `PEDIDO.valor_total` e `PEDIDO.motivo_cancelamento` | O valor total alimenta os KPIs 2, 3, 4 e 6 (`RN24`); o motivo registra o cancelamento (`RN18`, P2) |
| Entrega sem horários, sem como acompanhar o delivery (P1) | Criadas `ENTREGA.data_hora_saida` e `ENTREGA.data_hora_entrega`, com `CHECK` de ordem cronológica | Permite acompanhar a entrega (`G11`) e auditar as datas (`A12`, `A15`, `RN28`) |
| `PEDIDO` e `PAGAMENTO` tratados como 1:1, com `UNIQUE` | Relação alterada para 1:N; `PAGAMENTO.id_pedido` não tem `UNIQUE` | Um pedido pode ter pagamento dividido e pagamento estornado (`RN14`, `RN26`, KPI 13) |
| Valores monetários em `FLOAT` | Todos os campos monetários passaram a `DECIMAL(10,2)` | Evita erro de arredondamento nas somas financeiras (`G02`, `G14`) |
| Dicionário sem restrições de integridade | Dicionário com colunas de obrigatoriedade, unicidade, valores permitidos e padrão | Documenta o que o script implementa (seção 1.5) |
| Três problemas declarados (`P1` a `P3`), sem consulta que os responda | Problemas ampliados para `P1` a `P5`, cada um com consultas `G` na tabela de rastreabilidade | Todo problema declarado precisa ser respondido por consulta (seção 1.6) |

---

### 1.2 Conversão do Modelo Conceitual para o Modelo Lógico

O modelo lógico foi obtido do DER conceitual aplicando as regras de conversão abaixo. O resultado são 13 tabelas: 11 vindas de entidades e 2 tabelas associativas (`ITEM_PEDIDO` e `ITEM_COMPRA`).

1. **Entidades → Tabelas:** Cada entidade do modelo conceitual (`CLIENTE`, `ENDERECO`, `PRODUTO`, `CATEGORIA`, `PEDIDO`, `PAGAMENTO`, `ENTREGA`, `FORNECEDOR`, `COMPRA`, `DESPESA` e `FUNCIONARIO`) foi convertida em uma tabela relacional, com uma chave primária inteira própria (`id_<entidade>`).
2. **Atributos → Colunas:** Cada atributo virou uma coluna com tipo SQL, conforme o modelo lógico e o script. Os campos monetários usam `DECIMAL(10,2)`. O brModelo não oferece esse tipo e mostra `FLOAT` no diagrama, por isso o dicionário de dados e o script SQL são a referência dos tipos.
3. **Atributo composto e multivalorado → Tabela própria:** O endereço do cliente (rua, número, bairro, CEP e complemento) é composto, e um cliente pode ter mais de um endereço de entrega. Por isso ele virou a tabela `ENDERECO`, com FK para `CLIENTE`. `A entidade `ENDERECO` está representada no DER conceitual e foi convertida para a tabela `ENDERECO`.`
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
A coluna `ENTREGA.id_pedido` possui `UNIQUE`, garantindo no máximo uma entrega por pedido. Já `PEDIDO` e `PAGAMENTO` são **1:N**, e não 1:1, porque um pedido pode ser pago em mais de uma transação (RF05 e KPI 13, pedidos com pagamento dividido) e pode ter pagamento estornado (auditoria A16). Por isso `PAGAMENTO.id_pedido` não tem `UNIQUE`.

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

- **`PEDIDO.id_cliente` é opcional.** A `RN01` exige dados do cliente apenas para pedidos com entrega; pedidos presenciais podem ser registrados sem cliente. `A coluna `PEDIDO.id_cliente` aceita `NULL`, pois pedidos presenciais podem ser registrados sem cliente.`
- **`ENTREGA.id_endereco` é obrigatória.** Uma entrega sem endereço de destino não pode ser realizada (`RN01`).
- **`PAGAMENTO.id_pedido` aponta para o pedido, e não o contrário.** Assim um mesmo pedido pode ter vários pagamentos, o que atende o KPI 14.
- **As FKs não usam exclusão em cascata.** Pedidos cancelados e seus registros financeiros devem ser preservados (`RN03`), então não se apaga um registro que ainda é referenciado. `As FKs não utilizam exclusão em cascata, preservando o histórico de pedidos e pagamentos.`

---

### 1.4 Processo de Normalização (1FN, 2FN e 3FN)

#### 1ª Forma Normal (1FN)

Na 1FN, todo atributo tem um único valor atômico e não há grupos repetidos. Foram feitos estes ajustes:

- **Itens de pedido e de compra:** Em vez de guardar a lista de produtos em uma coluna do pedido ou da compra, cada produto ocupa uma linha própria em `ITEM_PEDIDO` ou `ITEM_COMPRA`.
- **Endereço:** Os dados de endereço foram separados em colunas individuais (`rua`, `numero`, `bairro`, `cep` e `complemento`), e como um cliente pode ter mais de um, eles ficam em uma tabela própria (`ENDERECO`).
- **Telefones de `CLIENTE`:** A tabela tem `telefone` e `telefone_2`. O modelo mantém os dois campos na tabela `CLIENTE`, conforme o diagrama e o SQL.

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
- **Dados derivados:** o subtotal de cada item pode ser calculado a partir de `ITEM_PEDIDO`. O campo `PEDIDO.valor_total` é mantido como desnormalização controlada para facilitar consultas gerenciais, e a auditoria `A06` verifica sua correspondência com a soma dos itens.

Com isso, todas as 13 tabelas estão na 3FN.

---

### 1.5 Justificativas Técnicas das Decisões

#### Chaves primárias

As chaves primárias das 11 tabelas de entidade são inteiros substitutos (`INT AUTO_INCREMENT`), explicados na seção 1.3. Em `PEDIDO`, o `AUTO_INCREMENT` implementa a numeração única e sequencial da `RN03`. `ITEM_PEDIDO` e `ITEM_COMPRA` usam chave composta, o que impede o mesmo produto repetido no mesmo pedido ou na mesma compra (`RN05`, `RN11`).

#### Chaves estrangeiras

Todas as FKs usam o comportamento padrão do MySQL (`RESTRICT`), sem exclusão em cascata. O banco recusa apagar um registro que ainda é referenciado, o que preserva pedidos cancelados e seus pagamentos (`RN17`, `RN19`). As principais:

| FK | Relacionamento implementado | Regra |
|---|---|---|
| `PEDIDO.id_cliente` (aceita `NULL`) | `CLIENTE` 1:N `PEDIDO` | `RN01`, `RN02` |
| `PEDIDO.id_funcionario` (`NOT NULL`) | `FUNCIONARIO` 1:N `PEDIDO` | `RN04` |
| `PRODUTO.id_categoria` (`NOT NULL`) | `CATEGORIA` 1:N `PRODUTO` | `RN09` |
| `PAGAMENTO.id_pedido` (`NOT NULL`, sem `UNIQUE`) | `PEDIDO` 1:N `PAGAMENTO` | `RN13`, `RN14` |
| `ENTREGA.id_pedido` (`NOT NULL`, `UNIQUE`) | `PEDIDO` 1:1 `ENTREGA` | `RN15` |
| `ENTREGA.id_endereco` (`NOT NULL`) | `ENDERECO` 1:N `ENTREGA` | `RN16` |
| `COMPRA.id_fornecedor` (`NOT NULL`) | `FORNECEDOR` 1:N `COMPRA` | `RN10` |
| `ITEM_COMPRA` (`id_compra`, `id_produto`) | `COMPRA` N:N `PRODUTO` | `RN11` |
| `ITEM_PEDIDO` (`id_pedido`, `id_produto`) | `PEDIDO` N:N `PRODUTO` | `RN05` |
| `DESPESA.id_funcionario` (`NOT NULL`) | `FUNCIONARIO` 1:N `DESPESA` | `RN20` |

#### Restrições aplicadas no banco

| Tabela.coluna | Restrição | Regra | Justificativa |
|---|---|---|---|
| `CATEGORIA.nome_categoria` | `NOT NULL`, `UNIQUE` | `RN09` | Evita duas categorias com o mesmo nome |
| `FORNECEDOR.nome_empresa` | `NOT NULL`, `UNIQUE` | `RN10` | Evita fornecedor cadastrado em duplicidade |
| `FUNCIONARIO.nivel_acesso` | `CHECK` em (`Proprietária`, `Gerente`, `Atendente`); padrão `Atendente` | `RN21` | O nível define quem acessa informações financeiras; o padrão é o menor privilégio |
| `CLIENTE.nome`, `CLIENTE.telefone` | `NOT NULL` | `RN01` | Sem nome e telefone não há como contatar o cliente do delivery |
| `PRODUTO.nome_produto` | `NOT NULL`, `UNIQUE` | `RN09` | Um produto não é cadastrado duas vezes |
| `PRODUTO.preco` | `CHECK > 0` | `RN29` | Produto sem preço não pode ser vendido |
| `PRODUTO.quantidade_estoque`, `estoque_minimo` | `CHECK >= 0`; padrão `0` | `RN07`, `RN08` | O estoque nunca fica negativo |
| `ENDERECO.cep` | `CHECK` com 8 dígitos | `RN16` | Impede CEP inválido no destino da entrega |
| `ENDERECO.rua`, `numero`, `bairro`, `id_cliente` | `NOT NULL` | `RN01`, `RN16` | Todo endereço é localizável e pertence a um cliente |
| `PEDIDO.canal_atendimento` | `CHECK` em (`WhatsApp`, `App`, `Presencial`) | `RN01`, `RN02` | Padroniza o canal usado na comparação de vendas (P3) |
| `PEDIDO.status` | `CHECK` em (`Pendente`, `Em preparo`, `Pronto`, `Em entrega`, `Concluido`, `Cancelado`); padrão `Pendente` | `RN17` | Cancelamento é um status; o registro nunca é apagado |
| `PEDIDO.valor_total` | `NOT NULL`, `CHECK >= 0`; padrão `0.00` | `RN24` | Valor usado pelos KPIs financeiros |
| `PEDIDO` (`ck_pedido_motivo`) | `CHECK` (`status = 'Cancelado'` ou `motivo_cancelamento` nulo) | `RN18` | O motivo só existe em pedido cancelado |
| `PEDIDO` (`ck_pedido_cliente_canal`) | `CHECK` (canal `Presencial` ou `id_cliente` preenchido) | `RN01`, `RN02` | Delivery exige cliente; presencial não |
| `ITEM_PEDIDO.quantidade`, `preco_unitario` | `CHECK > 0` | `RN05`, `RN06`, `RN29` | O item vendido tem quantidade e preço praticado válidos |
| `ITEM_COMPRA.quantidade`, `custo_unitario` | `CHECK > 0` | `RN11`, `RN29` | A compra registra o que e quanto foi pago |
| `PAGAMENTO.forma_pagamento` | `CHECK` em (`Pix`, `Cartão`, `Dinheiro`) | `RN12` | Formas aceitas pelo restaurante (KPI 7) |
| `PAGAMENTO.valor` | `CHECK > 0` | `RN29` | Pagamento sem valor não existe |
| `PAGAMENTO.status_pagamento` | `CHECK` em (`Pendente`, `Pago`, `Estornado`); padrão `Pendente` | `RN19`, `RN26` | O estorno fica registrado em vez de apagar o pagamento |
| `ENTREGA.id_pedido` | `NOT NULL`, `UNIQUE` | `RN15` | Um pedido tem no máximo uma entrega |
| `ENTREGA.status_entrega` | `CHECK` em (`Aguardando`, `Em rota`, `Entregue`, `Cancelada`); padrão `Aguardando` | `RN15` | Permite acompanhar o delivery (P1) |
| `ENTREGA` (`ck_entrega_datas`, `ck_entrega_final`) | `CHECK` de ordem cronológica e de data obrigatória em `Entregue` | `RN28` | Impede entrega anterior à saída |
| `DESPESA.descricao`, `categoria`, `valor`, `id_funcionario` | `NOT NULL`; `valor` com `CHECK > 0` | `RN20`, `RN29` | Toda despesa é completa e tem responsável |

#### Regras que o banco não impõe diretamente

Algumas regras envolvem mais de uma tabela, e o `CHECK` do MySQL só enxerga a própria linha. Por isso elas são conferidas pelas consultas de auditoria do script, e as de acesso ficam na aplicação:

| Regra | Como é conferida |
|---|---|
| `RN03` (identificador único) | `A04` |
| `RN07` (verificar estoque antes de confirmar o pedido) | Aplicação; o banco impede estoque negativo e `A02` confere |
| `RN18` (motivo só em cancelado) | `CHECK` e `A01` |
| `RN23` (pedido com itens) | `A05` |
| `RN24` (valor total igual à soma dos itens) | `A06` |
| `RN25` (pedido concluído quitado) | `A07` |
| `RN26` (estorno só em cancelado) | `A08`, `A16` |
| `RN27` (endereço pertence ao cliente do pedido) | `A10` |
| `RN15`, `RN28` (presencial sem entrega, datas coerentes) | `A11`, `A12`, `A14`, `A15` |
| `RN21`, `RN22` (acesso e LGPD) | Controle de acesso da aplicação (RNF03, RNF05) |

#### Decisões arquiteturais

- **13 tabelas em 3FN,** sem tabelas auxiliares fora do DER aprovado.
- **`DECIMAL(10,2)` para dinheiro,** porque `FLOAT` acumula erro de arredondamento nas somas de `G02` e `G14`.
- **`CHECK` em vez de `ENUM`** para canais, formas de pagamento e status: a lista permitida fica visível no `CREATE TABLE` e pode ser alterada sem recriar a coluna.
- **`PEDIDO.valor_total` desnormalizado de propósito:** evita somar os itens a cada consulta mensal, e a auditoria `A06` garante que não divirja dos itens.
- **Índices** em `PEDIDO(data_hora, status)`, `PEDIDO(canal_atendimento)`, `PAGAMENTO(id_pedido, status_pagamento)`, `COMPRA(data_compra)` e `DESPESA(data_despesa)`, que sustentam as consultas mensais (`G02` a `G08`, `G10`, `G13`).
- **MySQL 8.0.16+ com InnoDB e `utf8mb4`:** InnoDB para chaves estrangeiras e transações; 8.0.16 é a primeira versão que aplica `CHECK`.

---

### 1.6 Proposta de Arquitetura Analítica para BI e IA

#### Informações Estratégicas e Métricas Gerenciais (KPIs)

Cada KPI tem fórmula, período e meta, e é calculado por uma consulta do script. Os valores de referência vêm da massa fictícia, que representa cerca de 10% do volume real (ver seção 4). Por isso as metas usam proporções e comparação entre meses, e não valores absolutos em reais. As metas são **propostas do grupo, a validar com a proprietária.**

| KPI | Fórmula | Período | Meta proposta | Referência na massa | Consulta |
|---|---|---|---|---|---|
| **KPI 1 — Estoque baixo** | Produtos com `quantidade_estoque < estoque_minimo` | Diário | 0 produtos abaixo do mínimo | 6 de 16 produtos | `G01` |
| **KPI 2 — Faturamento mensal** | Σ `valor_total` dos pedidos `Concluido` | Mensal | Não cair em relação ao mês anterior | ago R$ 8.388 · set R$ 8.801 · out R$ 8.671 | `G02` |
| **KPI 3 — Pedidos concluídos e ticket médio** | Contagem de pedidos `Concluido` e média de `valor_total` | Mensal | Ticket médio ≥ R$ 30,00 | 290, 290 e 270 pedidos; ticket de R$ 28,92 a R$ 32,11 | `G03` |
| **KPI 4 — Taxa de cancelamento** | pedidos `Cancelado` ÷ total de pedidos × 100 | Mensal | ≤ 5% | 3,33% | `G04` |
| **KPI 5 — Produtos mais vendidos** | Σ `quantidade` dos itens de pedidos concluídos, por produto (top 10) | Mensal | Todo produto do top 10 com estoque ≥ mínimo | Marmita de frango lidera, com 195 unidades | `G05` |
| **KPI 6 — Vendas por canal** | Pedidos concluídos e Σ `valor_total` por `canal_atendimento` | Mensal | Acompanhar a participação de cada canal | Presencial 40,6%, App 37,9%, WhatsApp 21,5% dos pedidos concluídos | `G06` |
| **KPI 7 — Arrecadação por forma de pagamento** | Σ `valor` dos pagamentos `Pago`, por `forma_pagamento` | Mensal | Acompanhar a participação de cada forma | Pix R$ 10.520 · Cartão R$ 10.146 · Dinheiro R$ 5.194 | `G07` |
| **KPI 8 — Compras por fornecedor** | Σ `quantidade × custo_unitario` dos itens de compra | Mensal | Compras ≤ 30% do faturamento do mês | 20% a 29% do faturamento | `G08` |
| **KPI 9 — Clientes sem pedido** | clientes sem nenhum pedido ÷ total de clientes × 100 | Mensal | ≤ 20% | 25% (15 de 60) | `G09` |
| **KPI 10 — Despesas por categoria** | Σ `valor` das despesas, por `categoria` | Mensal | Variação ≤ 15% entre meses | R$ 5.044 · R$ 5.015 · R$ 5.548 | `G10` |
| **KPI 11 — Situação das entregas** | entregas `Entregue` ÷ total de entregas × 100 | Mensal | ≥ 95% entregues nos meses fechados | 100% entregues em ago e set | `G11` |
| **KPI 12 — Pedidos por funcionário** | Contagem de pedidos `Concluido` e Σ `valor_total`, por funcionário | Mensal | Nenhum funcionário com mais de 40% dos pedidos | 252 pedidos é o maior valor, 30% do total | `G12` |
| **KPI 13 — Pagamentos divididos** | pedidos concluídos com mais de 1 pagamento `Pago` ÷ pedidos concluídos × 100 | Mensal | Acompanhar (sem meta) | 9,2% (78 de 850) | `G13` |
| **KPI 14 — Saldo demonstrativo** | faturamento − compras − despesas | Mensal | Saldo > 0 em todo mês | R$ 920 · R$ 2.018 · R$ 1.058 | `G14` |

O saldo do KPI 14 é demonstrativo, não é lucro contábil, porque compras e consumo de estoque não ocorrem necessariamente no mesmo mês.

A análise de estornos é realizada pela auditoria `A16`, que identifica estornos associados a pedidos que não estão cancelados. Receita após taxas e margem contábil não são apresentados como KPIs, pois o modelo atual não possui dados de taxas nem metodologia contábil de custo médio.

#### Potencial dos dados para BI

As consultas `G01` a `G14` já retornam dados agregados por mês, canal, forma de pagamento, produto e funcionário. Isso permite que uma ferramenta como Power BI ou Metabase, ligada diretamente ao MySQL, monte um painel com cinco áreas: vendas (KPIs 2, 3 e 6), cancelamentos (KPI 4), estoque (KPIs 1 e 5), financeiro (KPIs 7, 8, 10 e 14) e delivery (KPIs 11 e 12). As consultas de auditoria `A01` a `A18` servem como painel de qualidade dos dados: todas devem retornar zero linhas.

#### Aplicações analíticas e de IA

- **Previsão de demanda:** `ITEM_PEDIDO` e `PEDIDO.data_hora` formam uma série histórica de vendas por produto, que pode alimentar um modelo de previsão para apoiar as compras.
- **Alerta inteligente de reposição:** cruzar a previsão com `PRODUTO.estoque_minimo` e `ITEM_COMPRA` indica quando e quanto comprar, em vez de esperar o produto acabar (P5).
- **Risco de cancelamento:** `PEDIDO.canal_atendimento`, horário e `motivo_cancelamento` permitem identificar os padrões que mais geram cancelamento (P2).
- **Segmentação de clientes:** frequência de pedidos e ticket médio por cliente permitem separar clientes recorrentes de clientes sem pedido (KPI 9) e planejar ações de retorno.
- **Tempo de entrega:** com `data_hora_saida` e `data_hora_entrega` é possível estimar o tempo de entrega por bairro, usando `ENDERECO.bairro` (P1).

#### Tabela de Rastreabilidade

| Problema ou KPI | Tabelas envolvidas | Consulta no script |
| :--- | :--- | :--- |
| `P1` — Acompanhamento dos pedidos de delivery | `PEDIDO`, `ITEM_PEDIDO`, `ENTREGA`, `CLIENTE`, `FUNCIONARIO` | `G11, G12` |
| `P2` — Controle de cancelamentos e reembolsos | `PEDIDO`, `ITEM_PEDIDO`, `PAGAMENTO` | `G04, A16` |
| `P3` — Comparação entre canais de venda | `PEDIDO`, `PAGAMENTO` | `G06, G13` |
| `P4` — Organização das informações financeiras | `PEDIDO`, `PAGAMENTO`, `COMPRA`, `ITEM_COMPRA`, `DESPESA` | `G02, G03, G07, G10, G14` |
| `P5` — Acompanhamento dos produtos e do estoque | `PRODUTO`, `CATEGORIA`, `FORNECEDOR`, `COMPRA`, `ITEM_COMPRA` | `G01, G05, G08` |
| `KPI 1` — Estoque baixo | `PRODUTO`, `CATEGORIA` | `G01` |
| `KPI 2` — Faturamento mensal | `PEDIDO` | `G02` |
| `KPI 3` — Pedidos concluídos e ticket médio | `PEDIDO` | `G03` |
| `KPI 4` — Taxa de cancelamento | `PEDIDO` | `G04` |
| `KPI 5` — Produtos mais vendidos | `PRODUTO`, `PEDIDO`, `ITEM_PEDIDO` | `G05` |
| `KPI 6` — Vendas por canal | `PEDIDO` | `G06` |
| `KPI 7` — Arrecadação por forma de pagamento | `PAGAMENTO` | `G07` |
| `KPI 8` — Compras por fornecedor | `FORNECEDOR`, `COMPRA`, `ITEM_COMPRA`, `PRODUTO` | `G08` |
| `KPI 9` — Clientes sem pedido | `CLIENTE`, `PEDIDO` | `G09` |
| `KPI 10` — Despesas por categoria | `DESPESA` | `G10` |
| `KPI 11` — Situação das entregas | `PEDIDO`, `ENTREGA` | `G11` |
| `KPI 12` — Pedidos por funcionário | `FUNCIONARIO`, `PEDIDO` | `G12` |
| `KPI 13` — Pagamentos divididos | `PAGAMENTO`, `PEDIDO` | `G13` |
| `KPI 14` — Saldo demonstrativo | `PEDIDO`, `COMPRA`, `ITEM_COMPRA`, `DESPESA` | `G14` |
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

Os comandos `INSERT INTO` da massa de dados estão integrados ao script principal. Acesse o arquivo [docs/script.sql](./docs/script.sql) para consultar a criação do banco, as tabelas, as restrições, a massa fictícia e as consultas SQL.

**Como o volume real justifica a quantidade de registros.** O restaurante atende cerca de 3.000 clientes por mês (cerca de 750 pedidos por semana). A massa simula **3 meses (agosto a outubro de 2026) com cerca de 300 pedidos por mês**, ou seja, aproximadamente 10% do volume real. O grupo escolheu essa escala para manter o banco leve nos testes e ainda assim ter volume suficiente para as consultas mensais.

| Tabela | Registros | Como foi dimensionado |
|---|---|---|
| `PEDIDO` | 900 | 300 por mês durante 3 meses |
| `ITEM_PEDIDO` | 1.495 | cerca de 1,7 item por pedido |
| `PAGAMENTO` | 947 | um por pedido, mais pagamentos divididos e estornos |
| `ENTREGA` | 313 | pedidos de WhatsApp e aplicativo (os presenciais não têm entrega) |
| `CLIENTE` | 60 (mais 1 temporário usado no `DELETE`) | base ativa reduzida; 15 sem pedido, para o KPI 9 |
| `ENDERECO` | 55 | endereços dos clientes que recebem entrega |
| `PRODUTO` | 16 em 5 categorias | cardápio resumido, com 6 produtos abaixo do estoque mínimo |
| `COMPRA` / `ITEM_COMPRA` | 40 / 120 | cerca de 13 compras por mês, em 5 fornecedores |
| `DESPESA` | 60 | cerca de 20 despesas por mês |
| `FUNCIONARIO` | 6 | equipe de 5 funcionários, mais a proprietária |

A massa cobre as situações reais: 850 pedidos concluídos, 30 cancelados, 10 em preparo e 10 pendentes; 7 pagamentos estornados; 78 pedidos com pagamento dividido; três canais; três formas de pagamento; e entregas `Entregue` e `Aguardando`. Os nomes, telefones e endereços são fictícios e não representam dados reais do restaurante.




---

## 5. Repositório GitHub e Dicionário de Dados
- **Dicionário de Dados:** [Acessar pasta do Dicionário de Dados](./Dicionario%20de%20dados/)

---

## 6. Uso de Inteligência Artificial

| Item | O que registrar |
| :--- | :--- |
| **Ferramenta e etapa** | ChatGPT (OpenAI) / Gemini (Google) utilizado nas etapas de redação do relatório técnico, estruturação da massa de dados, auxílio na escrita das queries SQL, pesquisa sobre KPIs de restaurantes e criação de slides. |
| **Motivação** | Agilizar a estruturação do texto dentro do padrão do esqueleto e acelerar a geração de inserts sintéticos e coerentes para a massa de dados. |
| **Prompt(s) utilizados** | *"Gere 20 inserts SQL fictícios para a tabela PEDIDO considerando canais como WhatsApp e Delivery, status variados e mantendo coerência com dados de clientes.", "Me envie KPIs que são utilizados em restaurantes (vendas, financeiros, estoque, atendimentos e clientes)* |
| **Resposta recebida** | Códigos `INSERT INTO` contendo dados sintéticos para popular o banco. 14 KPIs implementados nas consultas G01 a G14.|
| **Fontes consultadas e verificadas** | Manual de referência do MySQL 8.0 para validação das sintaxes de `CONSTRAINT` e `CHECK`. |
| **Trechos rejeitados ou corrigidos** | Foram ajustados os tipos de dados monetários para `DECIMAL(10,2)` onde a IA havia sugerido `FLOAT`. |
| **Justificativa da escolha final** | O uso de `DECIMAL` evita problemas de arredondamento em cálculos financeiros no MySQL. |
| **Reflexão crítica** | A IA acelera a escrita repetitiva, mas exige validação rigorosa sobre as restrições relacionais para não gerar inconsistências de chave estrangeira (`FK`) |

---

## 7. Apresentação Corporativa Final
[Acessar Slides](./docs/apresentacao.pdf)
