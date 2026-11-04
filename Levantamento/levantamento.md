# Levantamento de Requisitos — Donna Claudia Restaurante e Lanchonete

## 1. Identificação da organização

- **Nome da organização:** Donna Claudia Restaurante e Lanchonete.
- **CNPJ:** 36.276.829/0001-69.
- **Endereço:** Rua Maciel Monteiro, nº 264.
- **Natureza:** Empresa privada com fins lucrativos, do ramo alimentício.
- **Responsável entrevistada:** Antonia Claudia Freitas da Silva Oliveira.
- **Cargo:** Proprietária e responsável pela administração do estabelecimento.
- **Autorização:** A proprietária autorizou a utilização de seu nome completo neste trabalho.
- **Tempo de funcionamento:** Aproximadamente dois anos.
- **Quantidade de funcionários:** Cinco.
- **Média de atendimento:** Aproximadamente 3.000 pessoas por mês.

Os contatos de e-mail, telefone comercial, site e redes sociais não foram informados durante as entrevistas.

## 2. Registro das entrevistas

Foram realizadas duas entrevistas presenciais com a proprietária da Donna Claudia Restaurante e Lanchonete, ambas em 20/10/2026.

- **Data:** 20/10/2026.
- **Entrevistada:** Antonia Claudia Freitas da Silva Oliveira.
- **Cargo:** Proprietária.
- **Integrante participante:** Lucas Freitas de Oliveira.
- **Participação:** Lucas Freitas de Oliveira participou das duas entrevistas.
- **Objetivo:** Conhecer os processos administrativos e operacionais do estabelecimento, identificar dificuldades, validar informações e levantar requisitos para a modelagem do banco de dados.

A primeira entrevista teve como foco a caracterização da organização, os processos de negócio, os requisitos funcionais e não funcionais e as regras operacionais.

A segunda entrevista foi realizada para complementar e validar as informações anteriores, detalhar situações de cancelamento e reembolso, identificar informações que precisam manter histórico e levantar indicadores importantes para a administração.

## 3. Caracterização dos processos da organização

### 3.1 Funcionamento geral

O restaurante trabalha com a venda de refeições e lanches, atendendo clientes presencialmente e por meio de canais de delivery.

A proprietária participa da administração e costuma realizar a abertura do estabelecimento. Durante o expediente, os funcionários executam as atividades necessárias para o funcionamento. O fechamento é acompanhado pelo gerente ou pela própria proprietária.

O estabelecimento conta com cinco funcionários e utiliza ferramentas digitais para auxiliar no controle das atividades.

### 3.2 Sistemas e ferramentas utilizados

Atualmente, o restaurante utiliza:

- **Bion Finance:** sistema online utilizado para organizar informações de vendas, despesas e estoque.
- **WhatsApp:** canal utilizado para receber pedidos dos clientes.
- **Aplicativos de delivery:** utilizados para receber e acompanhar pedidos.
- **Aplicativos de fornecedores e mercados:** utilizados para realizar compras e acompanhar algumas entregas de mercadorias.

O Bion Finance continua sendo utilizado pela organização. Portanto, o projeto de banco de dados considera as necessidades de organização e consulta das informações, sem afirmar que o estabelecimento pretende substituir seu sistema atual.

### 3.3 Cadastro de clientes

Para pedidos de delivery, são solicitadas informações básicas do cliente, principalmente:

- Nome;
- Telefone;
- Endereço.

Essas informações são necessárias para identificar o cliente e permitir a entrega do pedido.

Informações adicionais, como segundo telefone e observações, podem ser opcionais.

### 3.4 Recebimento e preparação dos pedidos

O cliente realiza o pedido pelo WhatsApp ou por um aplicativo de delivery.

Após o recebimento, são verificadas as informações necessárias para o atendimento. O pedido é encaminhado para a preparação na cozinha e, quando fica pronto, é enviado ao endereço informado pelo cliente, quando se trata de uma entrega.

O processo envolve diferentes atividades e funcionários, principalmente na recepção, preparação e encaminhamento dos pedidos.

### 3.5 Controle de estoque

O controle de estoque é realizado pelo Bion Finance, que apresenta avisos quando algum produto está próximo de acabar.

O gerente ou a proprietária verifica as informações e atualiza o estoque diariamente.

Conforme confirmação posterior, o restaurante impede a venda de produtos quando não há quantidade disponível em estoque.

O sistema proposto deve considerar o registro das quantidades disponíveis, os limites mínimos e o histórico de alterações.

### 3.6 Compras e fornecedores

O restaurante realiza compras por meio de aplicativos de fornecedores e também diretamente em mercados.

Quando as mercadorias são recebidas ou retiradas, é realizada uma conferência com base na nota da compra.

O controle dessas informações é importante para acompanhar os produtos adquiridos e os custos relacionados ao estoque.

### 3.7 Pagamentos

O restaurante aceita diferentes formas de pagamento:

- Dinheiro;
- Pix;
- Cartão.

O registro dos pagamentos é importante para acompanhar as movimentações financeiras e facilitar a conferência do caixa.

### 3.8 Cancelamentos, devoluções e reembolsos

Os cancelamentos e problemas de pedidos acontecem principalmente nos aplicativos de delivery.

Entre as situações relatadas estão pedidos entregues incorretamente ou com itens faltantes.

Dependendo do problema, o restaurante pode realizar o reembolso do valor ou preparar outro pedido para o cliente.

Essas ocorrências demonstram a importância de manter um histórico dos pedidos, dos motivos de cancelamento e dos pagamentos ou reembolsos realizados.

### 3.9 Fechamento e controle financeiro

O fechamento do caixa é realizado pelo gerente ou pela proprietária, utilizando o Bion Finance para consultar e conferir as movimentações.

A proprietária considera importantes as consultas de vendas mensais, os relatórios de despesas e a comparação entre os valores vendidos e os gastos do período.

## 4. Problemas e necessidades identificados

Com base nas entrevistas, foram identificados os seguintes pontos de atenção:

### P1 — Organização dos pedidos de delivery

O delivery exige atenção porque envolve o recebimento dos pedidos, a preparação e o encaminhamento correto para os clientes.

O acompanhamento das informações e dos diferentes canais de atendimento é importante para reduzir erros e retrabalho.

### P2 — Controle de cancelamentos e reembolsos

Quando ocorre algum problema, como pedido incorreto ou item faltante, pode ser necessário realizar um reembolso ou preparar um novo pedido.

É importante manter o histórico dessas ocorrências para facilitar a conferência financeira e evitar perda de informações.

### P3 — Comparação entre canais de venda

O restaurante utiliza WhatsApp e aplicativos de delivery. Foi identificada a necessidade de consultar e comparar melhor as vendas realizadas por cada canal.

### P4 — Organização das informações financeiras

A proprietária considera importante visualizar as vendas e despesas de cada mês de forma organizada, facilitando a análise dos resultados do estabelecimento.

### P5 — Acompanhamento do estoque

O controle de estoque já é realizado pelo sistema atual, mas o registro de alterações e o acompanhamento dos produtos são importantes para evitar divergências e falta de mercadorias.

## 5. Requisitos do sistema

Os requisitos abaixo representam as necessidades levantadas para o sistema proposto.

### 5.1 Requisitos funcionais

| Código | Requisito |
|---|---|
| RF01 | Permitir o cadastro de clientes com nome, telefone e endereço. |
| RF02 | Permitir o cadastro de produtos com código, nome, categoria, preço e quantidade em estoque. |
| RF03 | Registrar pedidos com número único, data, cliente, canal de atendimento, valor total e situação. |
| RF04 | Registrar os produtos de cada pedido, suas quantidades e os preços praticados. |
| RF05 | Registrar pagamentos, incluindo valor, forma de pagamento e situação. |
| RF06 | Permitir o acompanhamento das quantidades disponíveis em estoque e a identificação de produtos próximos do limite mínimo. |
| RF07 | Impedir a venda de produtos sem quantidade disponível em estoque. |
| RF08 | Registrar cancelamentos, seus motivos e os respectivos históricos financeiros. |
| RF09 | Manter o histórico de alterações de preços e estoque. |
| RF10 | Permitir consultas de vendas e despesas por período. |
| RF11 | Permitir a comparação de vendas por canal de atendimento. |
| RF12 | Permitir a consulta de produtos mais vendidos, pagamentos pendentes e pedidos cancelados. |

### 5.2 Requisitos não funcionais

| Código | Requisito |
|---|---|
| RNF01 | O sistema deve funcionar em computador e celular. |
| RNF02 | O sistema deve possuir interface simples e de fácil utilização. |
| RNF03 | O sistema deve permitir o acesso online. |
| RNF04 | O sistema deve considerar aproximadamente dois usuários simultâneos. |
| RNF05 | O acesso às informações financeiras deve ser controlado por permissões. |
| RNF06 | O sistema deve permitir a atualização das informações quando houver retorno após uma indisponibilidade. |
| RNF07 | Os dados pessoais dos clientes devem ser tratados com cuidado, respeitando a legislação de proteção de dados. |

## 6. Regras de negócio

As regras foram organizadas conforme as informações fornecidas nas entrevistas. Quando uma condição não foi confirmada, ela está identificada como proposta ou ponto a validar.

### 6.1 Regras identificadas nas entrevistas

- **RN01 — Cadastro para delivery:** pedidos de entrega precisam das informações do cliente, incluindo nome, telefone e endereço.
- **RN02 — Controle de estoque:** não é permitida a venda de produtos sem quantidade disponível em estoque.
- **RN03 — Histórico de cancelamentos:** pedidos cancelados devem permanecer registrados, incluindo número, data, valor, produtos e motivo do cancelamento.
- **RN04 — Histórico de preços:** alterações nos preços dos produtos devem preservar os valores praticados em vendas anteriores.
- **RN05 — Identificação dos registros:** pedidos, produtos e pagamentos precisam possuir códigos próprios para evitar confusão entre registros.
- **RN06 — Registro financeiro:** pagamentos e reembolsos precisam permanecer associados aos respectivos pedidos.
- **RN07 — Histórico de estoque:** alterações nas quantidades dos produtos devem ser registradas para permitir consultas posteriores.
- **RN08 — Atendimento em caso de falha:** quando o sistema estiver indisponível, as informações podem ser controladas manualmente e atualizadas posteriormente.

### 6.2 Regras propostas para validação

- **RN09:** permitir que vendas presenciais sejam registradas sem cadastro de cliente, caso essa seja a prática adotada pelo restaurante.
- **RN10:** definir quais funcionários podem autorizar cancelamentos, descontos e reembolsos.
- **RN11:** definir se um pedido pode possuir mais de um pagamento.
- **RN12:** definir o prazo de armazenamento dos dados e documentos.
- **RN13:** definir se um cliente pode manter vários endereços cadastrados.

## 7. Informações e dados necessários

A partir das entrevistas, foram identificados os principais dados que precisam ser organizados no banco.

| Entidade | Principais informações |
|---|---|
| Cliente | Código, nome, telefone e endereço. |
| Produto | Código, nome, categoria, preço e quantidade disponível. |
| Categoria | Código e nome da categoria. |
| Pedido | Número, data, cliente, canal de atendimento, valor e situação. |
| ItemPedido | Pedido, produto, quantidade e preço unitário praticado. |
| Pagamento | Código, pedido, valor, forma e situação do pagamento. |
| Fornecedor | Código, nome e informações de contato. |
| Compra | Código, fornecedor, data e informações da aquisição. |
| Despesa | Código, descrição, categoria, data e valor. |
| Funcionário | Código, nome, cargo e nível de acesso. |
| Entrega | Código, pedido, endereço e situação da entrega. |

### 7.1 Campos obrigatórios e opcionais

Para clientes de delivery, são necessários nome, telefone e endereço.

Nos produtos, são importantes nome, preço e quantidade disponível.

Nos pedidos, devem ser registrados os produtos, o valor, a data e a forma de pagamento.

Informações adicionais, como segundo telefone e observações do pedido, podem ser opcionais.

### 7.2 Identificadores únicos

Cada pedido precisa ter um número próprio. Os produtos e os registros de pagamento também precisam de identificadores diferentes.

Esses códigos ajudam a localizar informações e evitam confusão entre registros.

### 7.3 Histórico de informações

É necessário preservar informações importantes, mesmo quando ocorrerem alterações.

Entre os históricos relevantes estão:

- Vendas realizadas;
- Pagamentos recebidos;
- Cancelamentos e reembolsos;
- Preços antigos dos produtos;
- Alterações de estoque.

No caso de cancelamento, devem permanecer registrados o número do pedido, a data, o valor, os produtos, o motivo e as informações de pagamento ou reembolso.

## 8. Relacionamentos considerados na modelagem

Com base nos processos apresentados, foram identificados os seguintes relacionamentos para o modelo conceitual e lógico:

1. **Cliente e Pedido:** um cliente pode realizar vários pedidos ao longo do tempo.
2. **Pedido e Produto:** um pedido pode conter vários produtos, e um produto pode aparecer em diferentes pedidos. Esse relacionamento é representado pela entidade associativa ItemPedido.
3. **Categoria e Produto:** uma categoria pode possuir vários produtos.
4. **Fornecedor e Produto:** um fornecedor pode fornecer vários produtos, e um produto pode ser adquirido de diferentes fornecedores.
5. **Fornecedor e Compra:** uma compra está relacionada ao fornecedor correspondente.
6. **Funcionário e Pedido:** um funcionário pode participar do atendimento de vários pedidos.
7. **Pedido e Entrega:** uma entrega está relacionada ao pedido correspondente. Pedidos sem entrega podem não possuir registro de entrega.
8. **Pedido e Pagamento:** os pagamentos devem estar relacionados aos pedidos. A possibilidade de mais de um pagamento por pedido ainda precisa ser definida.

Esses relacionamentos representam a proposta de organização dos dados e devem estar de acordo com o DER e o modelo lógico implementados pelo grupo.

## 9. Indicadores e consultas gerenciais

Durante a segunda entrevista, foram identificadas informações importantes para auxiliar a proprietária na administração do restaurante.

Os principais indicadores são:

- **Vendas mensais:** consultar o total vendido em cada mês.
- **Despesas mensais:** acompanhar os gastos do estabelecimento.
- **Comparação entre vendas e despesas:** analisar os resultados financeiros de cada período.
- **Produtos mais vendidos:** identificar os itens com maior quantidade de vendas.
- **Estoque baixo:** identificar produtos próximos do limite mínimo.
- **Pagamentos pendentes:** acompanhar valores que ainda precisam ser regularizados.
- **Pedidos cancelados:** consultar a quantidade de cancelamentos e os valores envolvidos.
- **Vendas por canal:** comparar os pedidos recebidos pelo WhatsApp e pelos aplicativos de delivery.

Essas consultas podem auxiliar no planejamento de compras, no acompanhamento financeiro e na identificação de oportunidades de melhoria.

## 10. Segurança e proteção de dados

O restaurante coleta informações pessoais de clientes, principalmente nome, telefone e endereço, para viabilizar os pedidos e as entregas.

O sistema proposto deve limitar o acesso a essas informações às pessoas que precisam utilizá-las nas atividades do estabelecimento.

Também é necessário considerar os princípios da Lei Geral de Proteção de Dados Pessoais (LGPD), especialmente quanto à finalidade da coleta, à utilização adequada e à conservação dos dados pelo período necessário.

As práticas atuais de segurança e os prazos específicos de armazenamento não foram detalhados nas entrevistas e precisam ser definidos pela organização.

## 11. Considerações finais

As duas entrevistas permitiram compreender melhor o funcionamento da Donna Claudia Restaurante e Lanchonete, seus processos de atendimento, controle de estoque, compras, pagamentos e gestão financeira.

Foi identificado que o estabelecimento já utiliza o Bion Finance para auxiliar na administração, além do WhatsApp e de aplicativos de delivery para receber pedidos.

As principais necessidades levantadas estão relacionadas ao acompanhamento dos pedidos, ao histórico de cancelamentos e reembolsos, à comparação das vendas por canal, ao controle de estoque e à organização das informações financeiras.

Com essas informações, foi possível estabelecer uma base para a construção do modelo conceitual, do modelo lógico e da implementação do banco de dados.

As regras e os relacionamentos que não foram confirmados diretamente deverão ser tratados como decisões de modelagem do projeto, e não como procedimentos necessariamente adotados pelo restaurante.

## 12. Utilização de inteligência artificial

O ChatGPT, da OpenAI, foi utilizado como ferramenta de apoio na organização das respostas das entrevistas e na estruturação deste documento.

A ferramenta auxiliou na organização dos processos de negócio, na elaboração inicial dos requisitos e na identificação de possíveis entidades e relacionamentos para o banco de dados.

As informações apresentadas foram baseadas nas respostas fornecidas durante as entrevistas. As sugestões de regras e modelagem foram identificadas separadamente para permitir a revisão pelo grupo.

A inteligência artificial foi utilizada como apoio à redação e organização, não como substituta das informações fornecidas pela entrevistada.