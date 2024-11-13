No contexto de bancos de dados distribuídos, **completude** refere-se à propriedade que assegura que todos os dados de uma relação global estão presentes nos fragmentos ([[Fragmentação]]) distribuídos. Isso significa que, ao fragmentar uma tabela em várias partes para distribuição entre diferentes nós, cada [[Tupla]] ou atributo da tabela original deve estar contido em pelo menos um dos fragmentos. A completude garante que não haja perda de dados durante o processo de fragmentação, permitindo que a relação global possa ser reconstruída a partir de seus fragmentos. Essa propriedade é essencial para manter a integridade e a consistência dos dados em sistemas distribuídos.

## Exemplo Prático: Consulta Completa em Dados Distribuídos

Considere um banco de dados distribuído com um sistema de gerenciamento de inventário global para uma rede de lojas. O inventário está distribuído entre várias regiões, com cada nó ([[Nós]]) (ou *shard* - [[Agrupamento]]) armazenando informações de estoque de uma região específica. No entanto, a central de gerenciamento precisa visualizar o inventário completo de determinado produto em todas as lojas.

### Estrutura da Tabela de Estoque

Suponha que temos a tabela `estoque` que armazena informações de produtos, quantidades e regiões onde estão localizados.

| Campo          | Tipo         | Descrição                                |
|----------------|--------------|------------------------------------------|
| id_produto     | INTEGER      | Identificador único do produto           |
| nome_produto   | VARCHAR(100) | Nome do produto                          |
| quantidade     | INTEGER      | Quantidade do produto em estoque         |
| regiao         | VARCHAR(20)  | Região onde o produto está armazenado    |

### Dados Distribuídos por Região

Cada *shard* contém os dados da tabela `estoque` para uma região específica.

#### Shard 1: América do Norte

| id_produto | nome_produto | quantidade | regiao           |
|------------|--------------|------------|------------------|
| 1          | Notebook A   | 50         | América do Norte |
| 2          | Teclado B    | 120        | América do Norte |

#### Shard 2: Europa

| id_produto | nome_produto | quantidade | regiao           |
|------------|--------------|------------|------------------|
| 1          | Notebook A   | 30         | Europa           |
| 3          | Mouse C      | 200        | Europa           |

#### Shard 3: Ásia

| id_produto | nome_produto | quantidade | regiao           |
|------------|--------------|------------|------------------|
| 1          | Notebook A   | 70         | Ásia             |
| 2          | Teclado B    | 150        | Ásia             |

### Consulta Completa: Total de Produtos

Para obter o total de `Notebook A` em todas as regiões, o sistema distribui a consulta para cada *shard* e agrega os resultados:

```sql
SELECT SUM(quantidade) AS total_quantidade
FROM estoque
WHERE nome_produto = 'Notebook A';
-- Consulta para cada shard individualmente (América do Norte, Europa e Ásia)

-- Shard 1: América do Norte
SELECT 'América do Norte' AS regiao, SUM(quantidade) AS quantidade_total
FROM estoque
WHERE nome_produto = 'Notebook A';

-- Shard 2: Europa
SELECT 'Europa' AS regiao, SUM(quantidade) AS quantidade_total
FROM estoque
WHERE nome_produto = 'Notebook A';

-- Shard 3: Ásia
SELECT 'Ásia' AS regiao, SUM(quantidade) AS quantidade_total
FROM estoque
WHERE nome_produto = 'Notebook A';

-- Resultado combinado em uma tabela central para garantir completude

-- Consulta agregada final (em um sistema central de agregação)
WITH dados_distribuidos AS (
    SELECT 'América do Norte' AS regiao, SUM(quantidade) AS quantidade_total
    FROM shard_1.estoque
    WHERE nome_produto = 'Notebook A'
    UNION ALL
    SELECT 'Europa' AS regiao, SUM(quantidade) AS quantidade_total
    FROM shard_2.estoque
    WHERE nome_produto = 'Notebook A'
    UNION ALL
    SELECT 'Ásia' AS regiao, SUM(quantidade) AS quantidade_total
    FROM shard_3.estoque
    WHERE nome_produto = 'Notebook A'
)

-- Total agregado de todas as regiões
SELECT SUM(quantidade_total) AS total_quantidade
FROM dados_distribuidos;