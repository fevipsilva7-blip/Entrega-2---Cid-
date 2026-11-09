# Base para a modelagem do sistema

## Donna Claudia Restaurante e Lanchonete

Este documento consolida os processos, problemas, requisitos, regras de negócio, entidades e decisões que devem ser utilizados pelo grupo para finalizar o DER, o modelo lógico, o SQL, o dicionário de dados e a massa de dados.

A proposta foi mantida compatível com o diagrama atual. Portanto, não foram criadas entidades novas para histórico de estoque, histórico separado de preços, taxas de aplicativos, reembolso ou estorno.

---

# 1. Processos da organização

## 1.1 Cadastro de clientes e endereços

Para pedidos de delivery, o restaurante coleta o nome, o telefone e o endereço do cliente. O endereço contém rua, número, bairro, CEP e complemento.

O sistema deve permitir organizar os dados do cliente e relacioná-los ao endereço utilizado para a entrega. O telefone principal e o telefone alternativo ficam registrados no cadastro de cliente, conforme o modelo atual.

## 1.2 Recebimento e acompanhamento de pedidos

Os pedidos podem ser recebidos pelo WhatsApp, por aplicativos de delivery ou presencialmente. Após o recebimento, o pedido é conferido e encaminhado para preparação.

O sistema deve registrar:

- número do pedido;
- data e hora;
- canal de atendimento;
- cliente, quando aplicável;
- funcionário responsável;
- situação do pedido;
- observações;
- valor total;
- produtos e quantidades.

## 1.3 Preparação e entrega

Depois de registrado, o pedido é encaminhado para preparação. Quando o pedido é de delivery, ele pode possuir uma entrega associada.

A entrega deve registrar:

- pedido relacionado;
- endereço de destino;
- situação da entrega;
- horário de saída;
- horário de conclusão.

Pedidos presenciais não precisam possuir registro de entrega.

## 1.4 Cadastro de produtos e categorias

Os produtos são organizados por categorias. O cadastro de produto deve conter:

- nome;
- descrição;
- preço atual;
- quantidade disponível em estoque;
- estoque mínimo;
- categoria relacionada.

## 1.5 Controle de estoque

O restaurante utiliza o Bion Finance para acompanhar o estoque e receber alertas quando os produtos estão próximos de acabar. O gerente ou a proprietária verifica as quantidades diariamente.

Nesta entrega, o controle será feito pela quantidade atual e pelo estoque mínimo armazenados na tabela `PRODUTO`. A consulta de estoque baixo deverá localizar produtos cuja quantidade esteja menor ou igual ao estoque mínimo.

Não será criada uma tabela separada de movimentação de estoque, pois ela não existe no diagrama atual.

## 1.6 Compras e fornecedores

O restaurante realiza compras com fornecedores e também diretamente em mercados. A compra é conferida com base na nota ou nos produtos recebidos.

O sistema deve registrar:

- fornecedor;
- data da compra;
- produtos comprados;
- quantidade;
- custo unitário.

Como uma compra pode conter vários produtos e um produto pode aparecer em várias compras, o relacionamento é representado pela entidade associativa `ITEM_COMPRA`.

## 1.7 Pagamentos

O restaurante aceita dinheiro, Pix e cartão. O pagamento deve ser relacionado ao pedido correspondente e deve registrar:

- forma de pagamento;
- valor;
- situação;
- data e hora;
- pedido relacionado.

O modelo atual permite mais de um registro de pagamento para o mesmo pedido. Essa decisão representa pagamento dividido ou mais de uma movimentação financeira relacionada ao pedido.

## 1.8 Cancelamentos e reembolsos

Cancelamentos e problemas ocorrem principalmente em pedidos de delivery. As situações relatadas incluem pedidos entregues incorretamente e itens faltantes.

O restaurante pode realizar um reembolso ou preparar outro pedido, dependendo da situação. Nesta entrega, o histórico básico será mantido em `PEDIDO` e `PAGAMENTO`:

- o pedido permanece registrado;
- o status indica o cancelamento;
- o motivo do cancelamento é armazenado;
- os itens continuam associados ao pedido;
- os registros financeiros permanecem relacionados ao pedido.

Não será criada uma entidade específica para reembolso ou estorno, pois ela não existe no diagrama atual.

## 1.9 Registro de despesas e fechamento financeiro

O gerente ou a proprietária acompanha o fechamento do caixa utilizando o Bion Finance. As despesas devem ser registradas com:

- descrição;
- categoria;
- data;
- valor;
- funcionário responsável.

O sistema deve permitir comparar vendas, pagamentos e despesas em determinado período.

---

# 2. Problemas e necessidades — P1 a P5

## P1 — Acompanhamento dos pedidos de delivery

O restaurante precisa acompanhar os pedidos recebidos, preparados e encaminhados para entrega. A falta de organização pode gerar erros, atrasos e retrabalho.

**Tabelas relacionadas:** `PEDIDO`, `ITEM_PEDIDO`, `ENTREGA`, `CLIENTE` e `FUNCIONARIO`.

**Consulta que deve existir:** pedidos por situação e acompanhamento das entregas.

## P2 — Controle de cancelamentos e reembolsos

Quando ocorre um pedido incorreto ou item faltante, pode ser necessário cancelar, reembolsar ou preparar novamente o pedido. É necessário preservar o pedido, seus itens, o motivo e os registros financeiros.

**Tabelas relacionadas:** `PEDIDO`, `ITEM_PEDIDO` e `PAGAMENTO`.

**Consulta que deve existir:** pedidos cancelados e respectivos valores financeiros.

## P3 — Comparação entre canais de venda

O restaurante utiliza atendimento presencial, WhatsApp e aplicativos de delivery. É necessário comparar a quantidade e o valor das vendas por canal.

**Tabelas relacionadas:** `PEDIDO` e `PAGAMENTO`.

**Consulta que deve existir:** vendas agrupadas por canal de atendimento.

## P4 — Organização das informações financeiras

A proprietária precisa acompanhar vendas, pagamentos e despesas por período para conferir os resultados do restaurante.

**Tabelas relacionadas:** `PEDIDO`, `PAGAMENTO` e `DESPESA`.

**Consulta que deve existir:** comparação entre vendas e despesas por período.

## P5 — Acompanhamento de produtos e estoque

O restaurante precisa identificar produtos próximos de acabar, acompanhar o estoque mínimo e consultar as compras realizadas.

**Tabelas relacionadas:** `PRODUTO`, `CATEGORIA`, `FORNECEDOR`, `COMPRA` e `ITEM_COMPRA`.

**Consulta que deve existir:** produtos abaixo do estoque mínimo e produtos mais vendidos.

---

# 3. Requisitos do sistema

## 3.1 Requisitos funcionais

| Código | Requisito |
|---|---|
| RF01 | O sistema deve permitir cadastrar clientes com nome, telefone e telefone alternativo. |
| RF02 | O sistema deve permitir cadastrar endereços com rua, número, bairro, CEP, complemento e cliente relacionado. |
| RF03 | O sistema deve permitir cadastrar categorias de produtos. |
| RF04 | O sistema deve permitir cadastrar produtos com nome, descrição, preço, quantidade em estoque, estoque mínimo e categoria. |
| RF05 | O sistema deve registrar pedidos com número, data e hora, cliente quando aplicável, funcionário, canal, situação, observação e valor total. |
| RF06 | O sistema deve registrar os produtos de cada pedido com quantidade e preço unitário praticado. |
| RF07 | O sistema deve registrar pagamentos com pedido, valor, forma de pagamento, situação e data. |
| RF08 | O sistema deve registrar entregas com pedido, endereço, situação e horários de saída e conclusão. |
| RF09 | O sistema deve cadastrar fornecedores e registrar compras realizadas. |
| RF10 | O sistema deve registrar os produtos, as quantidades e os custos unitários de cada compra por meio de `ITEM_COMPRA`. |
| RF11 | O sistema deve registrar despesas com descrição, categoria, data, valor e funcionário responsável. |
| RF12 | O sistema deve permitir consultar produtos cuja quantidade esteja abaixo ou igual ao estoque mínimo. |
| RF13 | O sistema deve manter pedidos cancelados com situação, motivo, itens e informações financeiras relacionadas. |
| RF14 | O sistema deve permitir consultar vendas, pagamentos, despesas, cancelamentos e vendas por canal. |
| RF15 | O sistema deve permitir consultar produtos mais vendidos e pagamentos pendentes. |

## 3.2 Requisitos não funcionais

| Código | Requisito |
|---|---|
| RNF01 | O sistema deve permitir acesso por computador e dispositivo móvel. |
| RNF02 | O sistema deve possuir interface simples e adequada a usuários com diferentes níveis de familiaridade tecnológica. |
| RNF03 | O acesso às informações financeiras deve ser controlado conforme as permissões dos usuários. |
| RNF04 | O sistema deve considerar aproximadamente dois usuários simultâneos. |
| RNF05 | Os dados pessoais dos clientes devem ser tratados conforme os princípios da LGPD. |
| RNF06 | O sistema deve permitir atualizar posteriormente informações registradas manualmente durante uma indisponibilidade. |

---

# 4. Regras de negócio

## 4.1 Regras de cadastro e pedidos

- **RN01 — Dados para delivery:** pedidos que exigem entrega devem possuir nome, telefone e endereço do cliente.
- **RN02 — Pedido presencial:** pedidos presenciais podem ser registrados sem cadastro completo de cliente, pois não exigem entrega.
- **RN03 — Identificação do pedido:** cada pedido deve possuir um identificador único e gerado automaticamente.
- **RN04 — Funcionário responsável:** todo pedido deve estar relacionado a um funcionário responsável pelo atendimento ou registro.
- **RN05 — Itens do pedido:** cada item deve estar relacionado a um pedido e a um produto existente.
- **RN06 — Preço praticado:** o preço registrado em `ITEM_PEDIDO` deve preservar o valor praticado no momento da venda, mesmo que o preço atual do produto seja alterado.

## 4.2 Regras de estoque e produtos

- **RN07 — Estoque disponível:** o atendimento deve verificar a disponibilidade do produto antes de confirmar o pedido.
- **RN08 — Estoque mínimo:** produtos cuja quantidade seja menor ou igual ao estoque mínimo devem ser identificados para reposição.
- **RN09 — Categoria:** todo produto deve estar relacionado a uma categoria cadastrada.
- **RN10 — Compra:** toda compra deve estar relacionada a um fornecedor existente.
- **RN11 — Item de compra:** cada item de compra deve informar o produto, a quantidade e o custo unitário.

## 4.3 Regras de pagamento e entrega

- **RN12 — Formas de pagamento:** as formas consideradas são dinheiro, Pix e cartão.
- **RN13 — Pagamento relacionado:** todo pagamento deve estar relacionado a um pedido existente.
- **RN14 — Pagamentos múltiplos:** um pedido pode possuir mais de um registro de pagamento.
- **RN15 — Entrega:** pedidos presenciais não precisam possuir entrega; pedidos de delivery podem possuir uma entrega relacionada.
- **RN16 — Endereço da entrega:** toda entrega deve possuir um endereço de destino cadastrado.

## 4.4 Regras de cancelamento e histórico

- **RN17 — Preservação do pedido:** pedidos cancelados não devem ser apagados.
- **RN18 — Motivo do cancelamento:** pedidos cancelados devem possuir motivo registrado.
- **RN19 — Histórico financeiro:** os pagamentos relacionados a pedidos cancelados devem permanecer registrados para conferência.
- **RN20 — Despesas:** toda despesa deve possuir descrição, categoria, data, valor e funcionário responsável.

## 4.5 Regras de segurança

- **RN21 — Acesso financeiro:** informações financeiras devem ser acessadas somente por usuários autorizados.
- **RN22 — Dados pessoais:** nome, telefone e endereço de clientes devem ser utilizados somente para as finalidades do atendimento e da entrega.


## 4.6 Regras de integridade dos dados

Regras implementadas no script e conferidas pelas consultas de auditoria. Foram acrescentadas ao levantamento para que README, script e levantamento usem os mesmos códigos.

- **RN23 — Pedido com itens:** todo pedido possui ao menos um item.
- **RN24 — Valor total do pedido:** `PEDIDO.valor_total` é igual à soma de `quantidade × preco_unitario` dos itens.
- **RN25 — Pedido concluído quitado:** a soma dos pagamentos `Pago` de um pedido concluído é igual ao seu valor total.
- **RN26 — Estorno:** apenas pedido cancelado possui pagamento `Estornado`, e pedido cancelado não mantém pagamento `Pago`.
- **RN27 — Endereço do cliente:** o endereço da entrega pertence ao cliente do pedido.
- **RN28 — Datas coerentes:** a entrega não ocorre antes da saída, entrega `Entregue` exige data de entrega e o pagamento não é anterior ao pedido.
- **RN29 — Valores positivos:** preços, custos, valores de pagamento e quantidades são maiores que zero.

---

# 5. Entidades necessárias no diagrama atual

O modelo deve utilizar as entidades e tabelas abaixo, sem acrescentar novas entidades nesta etapa.

| Entidade/tabela | Finalidade |
|---|---|
| `CLIENTE` | Armazenar dados dos clientes. |
| `ENDERECO` | Armazenar os endereços relacionados aos clientes e às entregas. |
| `CATEGORIA` | Organizar os produtos por categoria. |
| `PRODUTO` | Armazenar produtos, preços e informações atuais de estoque. |
| `PEDIDO` | Armazenar pedidos, canais, situações, valores e responsáveis. |
| `ITEM_PEDIDO` | Registrar os produtos, quantidades e preços de cada pedido. |
| `PAGAMENTO` | Registrar valores, formas e situações dos pagamentos. |
| `ENTREGA` | Registrar situação, endereço e horários das entregas. |
| `FORNECEDOR` | Armazenar fornecedores. |
| `COMPRA` | Registrar compras realizadas. |
| `ITEM_COMPRA` | Registrar produtos, quantidades e custos de cada compra. |
| `FUNCIONARIO` | Armazenar funcionários, cargos e níveis de acesso. |
| `DESPESA` | Registrar despesas e o funcionário responsável. |

## 5.1 Relacionamentos necessários

- `CLIENTE` relaciona-se com `PEDIDO`.
- `CLIENTE` relaciona-se com `ENDERECO`.
- `PEDIDO` relaciona-se com `ITEM_PEDIDO`.
- `PRODUTO` relaciona-se com `ITEM_PEDIDO`.
- `CATEGORIA` relaciona-se com `PRODUTO`.
- `FORNECEDOR` relaciona-se com `COMPRA`.
- `COMPRA` relaciona-se com `ITEM_COMPRA`.
- `PRODUTO` relaciona-se com `ITEM_COMPRA`.
- `FUNCIONARIO` relaciona-se com `PEDIDO`.
- `FUNCIONARIO` relaciona-se com `DESPESA`.
- `PEDIDO` relaciona-se com `PAGAMENTO`.
- `PEDIDO` relaciona-se com `ENTREGA`.
- `ENDERECO` relaciona-se com `ENTREGA`.

---

# 6. Decisões de modelagem

## 6.1 Pagamentos

Foi adotada a decisão de que um pedido pode possuir mais de um pagamento. Portanto:

- `PAGAMENTO.id_pedido` não deve ser `UNIQUE`;
- a relação entre `PEDIDO` e `PAGAMENTO` é 1:N;
- o pagamento possui identificador próprio;
- pagamentos pendentes e registros financeiros relacionados ao pedido podem ser consultados.

## 6.2 Pedidos presenciais

Foi adotada a decisão de que pedidos presenciais podem ser registrados sem cadastro completo de cliente. Portanto:

- `PEDIDO.id_cliente` pode aceitar `NULL`;
- pedidos de delivery devem possuir os dados necessários para entrega;
- pedidos presenciais não precisam possuir registro em `ENTREGA`.

## 6.3 Entregas

Foi adotada a decisão de que um pedido pode possuir no máximo uma entrega. Portanto:

- `ENTREGA.id_pedido` deve ser `UNIQUE`;
- a relação entre `PEDIDO` e `ENTREGA` é 1:1 quando a entrega existe;
- um pedido presencial pode não possuir entrega.

## 6.4 Endereços

O modelo utiliza `ENDERECO` como entidade própria. O endereço é associado ao cliente e pode ser utilizado na entrega. A decisão sobre a quantidade de endereços permitidos deve seguir exatamente a cardinalidade já desenhada no DER atual.

## 6.5 Estoque

O modelo registra somente:

- quantidade atual;
- estoque mínimo;
- produtos;
- compras e itens de compra.

Não será criada uma tabela de movimentação de estoque nesta versão. A consulta de estoque baixo será feita comparando `quantidade_estoque` com `estoque_minimo` em `PRODUTO`.

## 6.6 Preços

O modelo mantém:

- preço atual em `PRODUTO`;
- preço praticado na venda em `ITEM_PEDIDO`.

Não será criada uma tabela separada para histórico de alterações de preço. O preço do item preserva o valor aplicado no momento do pedido.

## 6.7 Cancelamentos e reembolsos

O cancelamento será representado pelo status e pelo motivo registrados em `PEDIDO`. Os registros financeiros permanecem relacionados em `PAGAMENTO`.

Não será criada uma entidade separada para reembolso ou estorno nesta versão. O grupo não deve prometer no README um detalhamento de reembolso que não possa ser armazenado pelas tabelas atuais.

---

# 7. Processos que não fazem parte desta versão

Para manter a compatibilidade com o diagrama atual, não serão modelados nesta entrega:

- integração automática com WhatsApp ou aplicativos de delivery;
- controle de entregadores próprios;
- programa de fidelidade;
- cupons e descontos detalhados;
- taxas dos aplicativos;
- histórico detalhado de movimentações de estoque;
- histórico separado de alterações de preço;
- tabela própria de reembolso ou estorno;
- controle de pedido substituto;
- emissão fiscal integrada.

Esses processos podem existir na organização ou ser executados por sistemas externos, mas não fazem parte do escopo do banco de dados desta entrega.

---

# 8. Consultas que o SQL possui

| Código | Consulta | Problema ou KPI |
|---|---|---|
| G01 | Produtos abaixo ou iguais ao estoque mínimo | P5, KPI 1 |
| G02 | Faturamento mensal | P4, KPI 2 |
| G03 | Pedidos concluídos e ticket médio mensal | P4, KPI 3 |
| G04 | Taxa de cancelamento por mês | P2, KPI 4 |
| G05 | Dez produtos mais vendidos com situação do estoque | P5, KPI 5 |
| G06 | Pedidos e receita por canal de atendimento | P3, KPI 6 |
| G07 | Recebimentos por forma de pagamento | P4, KPI 7 |
| G08 | Compras por fornecedor, faturamento e percentual mensal | P5, KPI 8 |
| G09 | Percentual de clientes sem pedido | KPI 9 |
| G10 | Despesas por categoria e mês | P4, KPI 10 |
| G11 | Percentual de entregas concluídas por mês | P1, KPI 11 |
| G12 | Pedidos concluídos por funcionário | P1, KPI 12 |
| G13 | Identificação de pedidos com mais de um pagamento Pago | P4, KPI 13 |
| G14 | Saldo demonstrativo mensal | P4, KPI 14 |
| G15 | Pedidos cancelados com itens e informações financeiras | P2, RF13 |

As consultas de auditoria `A01` a `A18` verificam as regras `RN01` a `RN29`. A correspondência entre cada auditoria e sua regra está no cabeçalho de cada consulta em `docs/script.sql`.

---

# 9. Resultado esperado

Depois da aprovação deste documento, os integrantes devem utilizá-lo como base única para:

1. finalizar o DER conceitual;
2. finalizar o modelo lógico;
3. escrever o script SQL;
4. atualizar o dicionário de dados;
5. criar a massa fictícia;
6. atualizar o README;
7. preparar a apresentação.

Nenhum desses artefatos deve criar tabelas, campos, relacionamentos ou regras que não estejam definidos nesta base ou que não sejam aprovados posteriormente pelo grupo.
