No contexto de bancos de dados distribuídos, **disjunção** é uma propriedade que assegura que os fragmentos resultantes de uma [[Fragmentação]] horizontal não compartilhem [[Tupla]]s entre si. Ou seja, cada tupla da relação original aparece em apenas um dos fragmentos, garantindo que não haja sobreposição de dados entre eles. Essa característica é fundamental para evitar redundâncias e inconsistências nos dados distribuídos.

Por exemplo, ao fragmentar horizontalmente uma tabela de clientes com base em regiões geográficas, a disjunção garante que cada cliente pertença exclusivamente ao fragmento correspondente à sua região, sem duplicações em outros fragmentos.

## Exemplo Prático: Banco de Dados de Clientes por Região

Imagine um banco de dados distribuído que armazena informações de clientes de uma empresa com atuação global. Cada região armazena apenas os dados dos clientes locais, formando uma **disjunção** entre os conjuntos de dados por região.

### Estrutura da Tabela de Clientes

A tabela `clientes` armazena informações sobre clientes e está disjunta entre diferentes regiões, ou seja, cada cliente existe em apenas uma tabela específica de cada região.

| Campo          | Tipo         | Descrição                        |
|----------------|--------------|----------------------------------|
| id_cliente     | INTEGER      | Identificador único do cliente   |
| nome_cliente   | VARCHAR(100) | Nome do cliente                  |
| email          | VARCHAR(100) | E-mail do cliente                |
| pais           | VARCHAR(50)  | País de origem                   |
| regiao         | VARCHAR(20)  | Região onde os dados estão       |

### Dados Distribuídos por Região (Exclusivamente por Shard - [[Agrupamento]])

#### Shard 1: América do Norte

| id_cliente | nome_cliente | email                   | pais         | regiao           |
|------------|--------------|-------------------------|--------------|------------------|
| 1          | Alice Smith  | alice.na@example.com    | EUA          | América do Norte |
| 2          | John Doe     | john.na@example.com     | Canadá       | América do Norte |

#### Shard 2: Europa

| id_cliente | nome_cliente | email                   | pais         | regiao           |
|------------|--------------|-------------------------|--------------|------------------|
| 3          | Emma Brown   | emma.eu@example.com     | Alemanha     | Europa           |
| 4          | Liam Taylor  | liam.eu@example.com     | Reino Unido  | Europa           |

#### Shard 3: Ásia

| id_cliente | nome_cliente | email                   | pais         | regiao           |
|------------|--------------|-------------------------|--------------|------------------|
| 5          | Mei Ling     | mei.as@example.com      | China        | Ásia             |
| 6          | Yuki Tanaka  | yuki.as@example.com     | Japão        | Ásia             |

### Consulta Disjunta

Se quisermos encontrar o cliente com `id_cliente = 3`, sabemos que esse cliente pertence ao *shard* da Europa, pois o dado é **disjunto** e os clientes são exclusivos de suas regiões. A consulta seria feita apenas no *shard* europeu:

```sql
-- Consulta executada apenas no Shard 2 (Europa)
SELECT * FROM clientes
WHERE id_cliente = 3;