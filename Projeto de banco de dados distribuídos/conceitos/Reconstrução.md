No contexto de bancos de dados distribuídos, **reconstrução** refere-se à capacidade de recompor a relação original a partir de seus fragmentos distribuídos. Essa propriedade assegura que, mesmo após a [[Fragmentação]] e distribuição dos dados entre diferentes [[Nós]], é possível recuperar integralmente a tabela ou relação original sem perda de informações. A reconstrução é essencial para manter a integridade e a consistência dos dados, permitindo operações que necessitam de uma visão completa da relação.

Por exemplo, se uma tabela de clientes foi fragmentada horizontalmente ([[Fragmentação Horizontal]]) por regiões geográficas e distribuída entre vários servidores, a propriedade de reconstrução garante que seja possível combinar esses fragmentos para obter novamente a tabela completa de clientes.

## Tipos de Reconstrução

Existem diferentes abordagens para reconstrução, dependendo da fragmentação dos dados e das consultas realizadas:

- **Reconstrução Horizontal**: Envolve a agregação de dados de diferentes fragmentos horizontais (dados divididos por linhas).
- **Reconstrução Vertical**: Refere-se à combinação de dados de diferentes fragmentos verticais (dados divididos por colunas).
- **Reconstrução Global**: Envolve a combinação de dados de diferentes shards, que podem incluir tanto fragmentação horizontal quanto vertical.

## Exemplo Prático: Banco de Dados de Funcionários

Imaginemos um sistema de banco de dados distribuído que armazena informações de funcionários. Os dados podem ser fragmentados horizontalmente, com base no local de trabalho, e verticalmente, com base no tipo de informação (dados pessoais, salário, etc.).

### Estrutura Original da Tabela de Funcionários

| id_funcionario | nome         | cargo      | salario | pais   |
|----------------|--------------|------------|---------|--------|
| 1              | Alice Smith  | Gerente    | 7000    | EUA    |
| 2              | John Doe     | Analista  | 5000    | EUA    |
| 3              | Maria Garcia | Diretor    | 8000    | Espanha|
| 4              | Liam Taylor  | Analista  | 4500    | Reino Unido|
| 5              | Mei Ling     | Gerente    | 7500    | China  |

### Fragmentação Horizontal

O banco de dados pode estar fragmentado horizontalmente por região, com um *shard* para cada país.

#### Shard 1: EUA

| id_funcionario | nome         | cargo      | salario | pais   |
|----------------|--------------|------------|---------|--------|
| 1              | Alice Smith  | Gerente    | 7000    | EUA    |
| 2              | John Doe     | Analista  | 5000    | EUA    |

#### Shard 2: Europa

| id_funcionario | nome         | cargo      | salario | pais   |
|----------------|--------------|------------|---------|--------|
| 3              | Maria Garcia | Diretor    | 8000    | Espanha|
| 4              | Liam Taylor  | Analista  | 4500    | Reino Unido|

#### Shard 3: Ásia

| id_funcionario | nome         | cargo      | salario | pais   |
|----------------|--------------|------------|---------|--------|
| 5              | Mei Ling     | Gerente    | 7500    | China  |

### Fragmentação Vertical

Os dados também podem ser fragmentados verticalmente, separando as informações pessoais (nome, cargo) das informações de salário.

#### Fragmento 1: Informações Pessoais

| id_funcionario | nome         | cargo      | pais   |
|----------------|--------------|------------|--------|
| 1              | Alice Smith  | Gerente    | EUA    |
| 2              | John Doe     | Analista  | EUA    |
| 3              | Maria Garcia | Diretor    | Espanha|
| 4              | Liam Taylor  | Analista  | Reino Unido|
| 5              | Mei Ling     | Gerente    | China  |

#### Fragmento 2: Informações de Salário

| id_funcionario | salario |
|----------------|---------|
| 1              | 7000    |
| 2              | 5000    |
| 3              | 8000    |
| 4              | 4500    |
| 5              | 7500    |

### Reconstrução Horizontal

Quando é necessário obter todos os dados dos funcionários da empresa, a reconstrução envolve a combinação de dados dos diferentes *shards*. Para uma consulta que retorna os funcionários de todos os países, o sistema executa uma leitura nos *shards* EUA, Europa e Ásia, e depois combina as informações em um único conjunto de resultados.

```sql
-- Consulta para retornar todos os funcionários
SELECT * FROM funcionarios_eua
UNION
SELECT * FROM funcionarios_europa
UNION
SELECT * FROM funcionarios_asia;