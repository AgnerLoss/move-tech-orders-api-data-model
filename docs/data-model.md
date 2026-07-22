# Especificação do Modelo de Dados — Orders API

## Tabela: `orders`

Armazena o cabeçalho e o estado dos pedidos da aplicação.

| Coluna | Tipo de Dado | Restrições | Descrição |
| :--- | :--- | :--- | :--- |
| `id` | INTEGER | PRIMARY KEY, AUTOINCREMENT | Identificador único do pedido |
| `status` | VARCHAR | NOT NULL, DEFAULT 'pending' | Status atual do pedido |
| `created_at` | TIMESTAMP | NOT NULL, DEFAULT NOW() | Data e hora da criação |

---

## Tabela: `items`

Armazena os itens vinculados a um pedido.

| Coluna | Tipo de Dado | Restrições | Descrição |
| :--- | :--- | :--- | :--- |
| `id` | INTEGER | PRIMARY KEY, AUTOINCREMENT | Identificador único do item |
| `order_id` | INTEGER | FOREIGN KEY (`orders.id`), NOT NULL | Vínculo com a tabela de pedidos |
| `title` | VARCHAR | NOT NULL | Nome do produto |
| `price` | FLOAT | NOT NULL | Preço unitário |
| `qty` | INTEGER | NOT NULL | Quantidade do item |

---

## Relacionamentos e Regras

- **1:N (orders → items):** Um pedido pode possuir múltiplos itens. Cada item pertence obrigatoriamente a um único pedido.
- **Cascata:** A deleção de um registro na tabela `orders` remove automaticamente todos os registros correspondentes na tabela `items` (`cascade="all, delete-orphan"`).
