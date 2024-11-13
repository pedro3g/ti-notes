É quando uma tabela do esquema global é mapeada para duas ou mais tabelas no esquema local que não são idênticas à tabela global.
Na fragmentação, o banco não fica limitado à memória secundária do servidor e, em comparação com uma solução centralizada, aumenta a confiabilidade e eficiência se a maioria das consultas acessa apenas dados locais.

## Exemplo Prático: Banco de Dados de Funcionários

Imagine um banco de dados distribuído que armazena informações sobre funcionários de uma empresa global. Os dados dos funcionários são divididos entre diferentes nós com base no tipo de fragmentação, seja horizontal ([[Fragmentação Horizontal]]) ou vertical ([[Fragmentação Horizontal]]), para otimizar consultas específicas.

#### Tabela Original de Funcionários

| id_funcionario | nome           | cargo      | salario | pais           |
|----------------|----------------|------------|---------|----------------|
| 1              | Alice Smith    | Gerente    | 7000    | EUA            |
| 2              | John Doe       | Analista  | 5000    | EUA            |
| 3              | Maria Garcia   | Diretor    | 8000    | Espanha        |
| 4              | Liam Taylor    | Analista  | 4500    | Reino Unido    |
| 5              | Mei Ling       | Gerente    | 7500    | China          |

#### Shard 1: Funcionários da América do Norte

| id_funcionario | nome         | cargo      | salario | pais   |
|----------------|--------------|------------|---------|--------|
| 1              | Alice Smith  | Gerente    | 7000    | EUA    |
| 2              | John Doe     | Analista  | 5000    | EUA    |

#### Shard 2: Funcionários da Europa

| id_funcionario | nome         | cargo      | salario | pais         |
|----------------|--------------|------------|---------|--------------|
| 3              | Maria Garcia | Diretor    | 8000    | Espanha      |
| 4              | Liam Taylor  | Analista  | 4500    | Reino Unido  |

#### Shard 3: Funcionários da Ásia

| id_funcionario | nome         | cargo      | salario | pais   |
|----------------|--------------|------------|---------|--------|
| 5              | Mei Ling     | Gerente    | 7500    | China  |

### Consulta para um Fragmento Horizontal

Se quisermos encontrar todos os funcionários da América do Norte, a consulta será direcionada apenas para o *shard* ([[Agrupamento]]) que contém os dados dos funcionários dessa região:

```sql
-- Consulta executada apenas no Shard 1 (América do Norte)
SELECT * FROM funcionarios
WHERE pais = 'EUA';