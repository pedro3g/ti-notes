No contexto de bancos de dados distribuídos, **divisão** refere-se ao processo de [[Fragmentação]] dos dados, que pode ser realizado de duas maneiras principais: [[Fragmentação Horizontal]] e [[Fragmentação Vertical]]

A divisão adequada dos dados é crucial para otimizar o desempenho, a [[Escalabilidade]] e a manutenção da consistência em sistemas de bancos de dados distribuídos. Uma fragmentação bem planejada permite que as operações sejam executadas de forma mais eficiente, reduzindo a latência e melhorando a distribuição da carga de trabalho entre os nós do sistema.

## Exemplo Prático: Banco de Dados de Pedidos

Imagine um banco de dados distribuído que armazena pedidos de clientes de uma empresa global. Para melhorar a performance e reduzir a carga nos servidores, os pedidos são divididos com base na data de criação, garantindo que os pedidos mais antigos sejam armazenados em um *shard* ([[Agrupamento]]) e os mais recentes em outro.

### Estrutura da Tabela de Pedidos

A tabela `pedidos` armazena informações sobre os pedidos feitos pelos clientes.

| Campo          | Tipo         | Descrição                        |
|----------------|--------------|----------------------------------|
| id_pedido      | INTEGER      | Identificador único do pedido    |
| id_cliente     | INTEGER      | Identificador do cliente         |
| data_pedido    | DATE         | Data em que o pedido foi feito  |
| valor          | DECIMAL      | Valor total do pedido            |

### Dados Distribuídos por Divisão (Baseada em Data)

#### Shard 1: Pedidos de 2023

| id_pedido | id_cliente | data_pedido | valor   |
|-----------|------------|-------------|---------|
| 1         | 101        | 2023-02-10  | 100.50  |
| 2         | 102        | 2023-05-22  | 250.00  |
| 3         | 103        | 2023-11-15  | 75.30   |

#### Shard 2: Pedidos de 2024

| id_pedido | id_cliente | data_pedido | valor   |
|-----------|------------|-------------|---------|
| 4         | 104        | 2024-01-05  | 120.00  |
| 5         | 105        | 2024-03-18  | 200.45  |
| 6         | 106        | 2024-07-09  | 90.99   |

### Consulta com Divisão

Quando um usuário consulta os pedidos de 2024, a consulta será direcionada apenas para o *shard* que contém os pedidos de 2024, otimizando a busca. Por exemplo:

```sql
-- Consulta executada apenas no Shard 2 (pedidos de 2024)
SELECT * FROM pedidos
WHERE data_pedido BETWEEN '2024-01-01' AND '2024-12-31';