Markdown
# Modelagem de Dados

Este documento descreve a estrutura das tabelas, tipos de dados e relacionamentos da aplicação de gestão de pedidos.

## Entidades

### Pedido (`orders`)

A tabela `orders` armazena o cabeçalho e as informações gerais do pedido.

| Coluna | Tipo | Restrições / Padrão | Descrição |
| :--- | :--- | :--- | :--- |
| `id` | `VARCHAR` / `TEXT` | `PRIMARY KEY`, Default: `UUID v4` | Identificador único do pedido gerado via UUID. |
| `customer` | `VARCHAR` / `TEXT` | `NOT NULL` | Nome ou identificação do cliente. |
| `status` | `VARCHAR` / `TEXT` | Default: `"open"` | Estado atual do pedido (ex.: `open`, `completed`). |
| `created_at` | `TIMESTAMP WITH TIMEZONE` | Default: `now()` (UTC) | Data e hora de criação do registro em formato UTC. |

### Item (`items`)

A tabela `items` armazena os itens associados a cada pedido.

| Coluna | Tipo | Restrições / Padrão | Descrição |
| :--- | :--- | :--- | :--- |
| `id` | `VARCHAR` / `TEXT` | `PRIMARY KEY`, Default: `UUID v4` | Identificador único do item gerado via UUID. |
| `order_id` | `VARCHAR` / `TEXT` | `FOREIGN KEY` (`orders.id`), `NOT NULL` | Chave estrangeira que conecta o item ao seu pedido pai. |
| `sku` | `VARCHAR` / `TEXT` | `NOT NULL` | Código identificador (Stock Keeping Unit) do produto. |
| `description` | `VARCHAR` / `TEXT` | `NOT NULL` | Descrição do produto. |
| `quantity` | `INTEGER` | `NOT NULL` | Quantidade do item no pedido. |

---

## Relacionamento

O modelo estabelece um relacionamento **1:N (Um para Muitos)** entre as tabelas `orders` e `items`:

* **1 Pedido possui N Itens:** Um pedido pode ter múltiplos itens associados. A relação possui exclusão em cascata (`cascade="all, delete-orphan"`), ou seja, deletar um pedido remove automaticamente seus itens.
* **1 Item pertence a 1 Pedido:** Cada item está atrelado obrigatoriamente a um registro da tabela `orders` através da chave estrangeira `order_id`.

```text
+-----------------------------------+             +-----------------------------------+
|              orders               |             |               items               |
+-----------------------------------+             +-----------------------------------+
| id (PK, String/UUID)              | 1         N | id (PK, String/UUID)              |
| customer (String)                 |-------------| order_id (FK -> orders.id, String)|
| status (String)                   |             | sku (String)                      |
| created_at (DateTime w/ Timezone) |             | description (String)              |
+-----------------------------------+             | quantity (Integer)                |
                                                  +-----------------------------------+
