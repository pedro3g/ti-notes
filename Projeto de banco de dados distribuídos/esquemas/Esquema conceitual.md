## Introdução

Um banco de dados distribuído é um sistema onde os dados são armazenados em diferentes locais físicos, mas são percebidos pelos usuários como um único banco de dados lógico. Isso oferece vantagens como melhor desempenho, escalabilidade e disponibilidade. Entretanto, a distribuição dos dados adiciona complexidade ao projeto e à manutenção do sistema.

O esquema conceitual é uma representação de alto nível da estrutura lógica de um banco de dados. Ele descreve as entidades, os relacionamentos entre elas e as restrições, sem se preocupar com detalhes físicos de armazenamento ou implementação. Em um ambiente distribuído, o esquema conceitual é fundamental para proporcionar uma visão unificada dos dados, independentemente de onde estejam armazenados.

## Componentes do Esquema Conceitual

- **Entidades**: Objetos ou conceitos sobre os quais informações são armazenadas (por exemplo, Cliente, Produto, Pedido).
- **Atributos**: Propriedades das entidades (por exemplo, Nome, Endereço, Preço).
- **Relacionamentos**: Associações entre entidades (por exemplo, um Cliente faz um Pedido).
- **Restrições**: Regras que garantem a integridade dos dados (por exemplo, uma chave primária deve ser única).

## Exemplo Prático

Imagine uma empresa de varejo com lojas em diferentes cidades. Cada loja possui seu próprio banco de dados local para operações diárias, mas a empresa deseja analisar os dados de todas as lojas de forma unificada.

## Definição do Esquema Conceitual em SQL

Embora o SQL seja uma linguagem de definição e manipulação de dados, podemos usá-lo para representar o esquema conceitual.

### Tabela Cliente

```sql
CREATE TABLE Cliente (
	ClienteID INT PRIMARY KEY,
	Nome VARCHAR(100),
	Endereco VARCHAR(200),
	Cidade VARCHAR(50),
	Estado VARCHAR(50)
);
```

### Tabela Produto

```sql
	CREATE TABLE Produto (
	ProdutoID INT PRIMARY KEY,
	Nome VARCHAR(100),
	Preco DECIMAL(10, 2)
);
```

### Tabela Pedido

```sql
CREATE TABLE Pedido (
	PedidoID INT PRIMARY KEY,
	DataPedido DATE,
	ClienteID INT,
	FOREIGN KEY (ClienteID) REFERENCES Cliente(ClienteID)
);
```

### Tabela PedidoItem

```sql
CREATE TABLE PedidoItem (
	PedidoID INT,
	ProdutoID INT,
	Quantidade INT,
	PrecoUnitario DECIMAL(10, 2),
	PRIMARY KEY (PedidoID, ProdutoID),
	FOREIGN KEY (PedidoID) REFERENCES Pedido(PedidoID),
	FOREIGN KEY (ProdutoID) REFERENCES Produto(ProdutoID)
);
```

## Distribuição dos Dados

Embora o esquema conceitual seja único, os dados são distribuídos entre os bancos de dados locais das lojas.

### [[Fragmentação Horizontal]]

Cada loja armazena os dados relacionados a suas operações. Por exemplo:
- **Loja São Paulo**
	- Cliente: Clientes que realizaram compras na loja de São Paulo.
	- Pedido e PedidoItem: Pedidos realizados na loja de São Paulo.

- **Loja Rio de Janeiro**
	- Cliente: Clientes que realizaram compras na loja do Rio de Janeiro.
	- Pedido e PedidoItem: Pedidos realizados na loja do Rio de Janeiro.

### [[Fragmentação Vertical]]

Podemos também distribuir colunas específicas entre diferentes bancos de dados, mas neste exemplo, focaremos na fragmentação horizontal.

### Consulta Unificada

Mesmo com os dados distribuídos, é possível realizar consultas que englobam todas as lojas.

#### Exemplo de Consulta Global
  

```sql
-- Total de vendas em todas as lojas
SELECT SUM(PedidoItem.Quantidade * PedidoItem.PrecoUnitario) AS TotalVendas
FROM PedidoItem;
```

Para executar essa consulta, o sistema de gerenciamento de banco de dados distribuído (SGBDD) precisa reunir dados de todas as lojas.

## Sincronização e Replicação

Para manter a integridade e a consistência dos dados, é necessário sincronizar os bancos de dados locais regularmente. A replicação de dados críticos (como informações de produtos) para todas as lojas pode ser utilizada.

## Considerações sobre o Esquema Conceitual em Ambiente Distribuído

- **Transparência de Localização**: Os usuários não precisam saber onde os dados estão armazenados.
- **Transparência de Fragmentação**: As fragmentações das tabelas são transparentes para o usuário.
- **Transparência de Replicação**: Se os dados são replicados, isso é invisível para o usuário.

## Benefícios do Esquema Conceitual

- **Simplificação**: Facilita o entendimento e o desenvolvimento de aplicações.
- **Consistência**: Garante que todos os usuários e aplicações tenham uma visão uniforme dos dados.
- **Flexibilidade**: Permite mudanças na distribuição física dos dados sem impactar as aplicações.

## Conclusão

O esquema conceitual de um banco de dados distribuído desempenha um papel vital ao fornecer uma visão unificada e consistente dos dados. Ele abstrai a complexidade da distribuição física, permitindo que desenvolvedores e usuários se concentrem na lógica do negócio. O uso de exemplos em SQL ilustra como as entidades e relacionamentos são definidos no nível conceitual, enquanto a distribuição e fragmentação dos dados são gerenciadas no nível físico.