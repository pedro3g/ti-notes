Em um banco de dados distribuído, o **esquema externo** é a camada que define a visão específica de dados para cada usuário ou aplicação. É a "visão" personalizada de dados que o sistema oferece aos diferentes usuários, com base em suas necessidades e permissões.

No contexto de um banco de dados distribuído, essa camada permite:

1. **Personalização**: Cada usuário ou aplicação vê apenas os dados relevantes para ele, sem acesso a dados desnecessários.

2. **Segurança**: É possível restringir o acesso a dados confidenciais ou sensíveis, controlando o que cada usuário pode visualizar e modificar.

3. **Simplificação**: Esconde a complexidade do armazenamento distribuído, oferecendo uma visão unificada dos dados.

## Exemplo Real

Imagine uma empresa multinacional que utiliza um banco de dados distribuído para armazenar dados de vendas, funcionários e finanças em diferentes filiais ao redor do mundo. O *esquema externo* permite que cada departamento veja apenas as informações necessárias para suas operações diárias:

- **Departamento de Vendas**: Visualiza apenas dados de vendas específicos para sua região.

- **Departamento de Recursos Humanos (RH)**: Acessa dados de funcionários para gerenciar pessoas.

- **Departamento Financeiro**: Consulta informações financeiras consolidadas.

## Implementação em Banco de Dados

Usando um banco de dados relacional, como MySQL ou PostgreSQL, é possível aplicar o conceito de *esquema externo* com *views* (visões). Abaixo, segue um exemplo prático.

### 1. Estrutura das Tabelas

Vamos criar três tabelas principais no banco de dados, representando diferentes áreas da empresa:

```sql

-- Tabela de Vendas

CREATE TABLE vendas (

id INT PRIMARY KEY,

data DATE,

filial VARCHAR(50),

produto VARCHAR(50),

quantidade INT,

valor_total DECIMAL(10, 2)

);

  

-- Tabela de Funcionários

CREATE TABLE funcionarios (

id INT PRIMARY KEY,

nome VARCHAR(100),

cargo VARCHAR(50),

filial VARCHAR(50),

salario DECIMAL(10, 2)

);

  

-- Tabela de Finanças

CREATE TABLE financas (

id INT PRIMARY KEY,

filial VARCHAR(50),

receita DECIMAL(10, 2),

despesa DECIMAL(10, 2)

);

```

  

### 2. Inserindo Dados

Agora, vamos inserir alguns dados nessas tabelas para simular um ambiente realista:

```sql

-- Inserindo dados em vendas

INSERT INTO vendas (id, data, filial, produto, quantidade, valor_total)

VALUES

(1, '2024-10-01', 'São Paulo', 'Produto A', 10, 500.00),

(2, '2024-10-02', 'Rio de Janeiro', 'Produto B', 5, 300.00),

(3, '2024-10-03', 'São Paulo', 'Produto A', 8, 400.00);

  

-- Inserindo dados em funcionarios

INSERT INTO funcionarios (id, nome, cargo, filial, salario)

VALUES

(1, 'Alice', 'Vendedor', 'São Paulo', 3000.00),

(2, 'Bob', 'Gerente', 'Rio de Janeiro', 5000.00),

(3, 'Carlos', 'Analista', 'São Paulo', 4500.00);

  

-- Inserindo dados em finanças

INSERT INTO financas (id, filial, receita, despesa)

VALUES

(1, 'São Paulo', 10000.00, 3000.00),

(2, 'Rio de Janeiro', 7000.00, 2000.00);

```

### 3. Criando Views (Esquemas Externos)

Agora, vamos criar as visões específicas para cada departamento. Cada *view* vai restringir os dados exibidos para mostrar apenas o que é necessário para cada grupo.

#### View para o Departamento de Vendas

Os vendedores devem ver apenas os dados de vendas, sem acesso a salários ou dados financeiros.

  

```sql

CREATE VIEW view_vendas AS

SELECT data, filial, produto, quantidade, valor_total

FROM vendas;

```

#### View para o Departamento de Recursos Humanos (RH)

O RH precisa ver os dados dos funcionários, mas não deve ter acesso às informações financeiras ou de vendas detalhadas.

```sql

CREATE VIEW view_funcionarios AS

SELECT nome, cargo, filial, salario

FROM funcionarios;

```

  

#### View para o Departamento Financeiro

  

O departamento financeiro precisa de uma visão consolidada das receitas e despesas de cada filial, sem acesso aos dados pessoais dos funcionários.

  

```sql

CREATE VIEW view_financas AS

SELECT filial, receita, despesa

FROM financas;

```

  

### 4. Consultando as Views

  

Cada departamento pode agora acessar os dados de sua view específica:

  

- Departamento de Vendas:

```sql

SELECT * FROM view_vendas;

```

  

- Departamento de RH:

```sql

SELECT * FROM view_funcionarios;

```

  

- Departamento Financeiro:

```sql

SELECT * FROM view_financas;

```

  

## Conclusão

  

Essas *views* representam o conceito de *esquemas externos*, criando uma visão filtrada dos dados de acordo com as necessidades e permissões de cada departamento. Assim, o banco de dados mantém a segurança e a integridade dos dados, enquanto cada usuário ou aplicação recebe uma visão personalizada e adequada.