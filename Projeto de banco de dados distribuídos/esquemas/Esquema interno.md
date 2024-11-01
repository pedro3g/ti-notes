# Esquema Interno de Banco de Dados

O _esquema interno_ em um banco de dados é a camada mais baixa de abstração no modelo de dados. Ele se refere à forma como os dados são realmente armazenados no sistema, incluindo a estrutura física dos dados em disco, os [[índices]], as alocações de espaço e outros detalhes técnicos de implementação.

## Características do Esquema Interno

1. **Estrutura Física**: Define como os dados são armazenados fisicamente no hardware, incluindo o formato de arquivo, a organização das tabelas e o uso de técnicas de compressão, se aplicável.
2. **Armazenamento de Dados**: Inclui a forma como os registros são armazenados, como a disposição de linhas e colunas em arquivos, e o método de acesso aos dados (por exemplo, seqüencial, baseado em índice).
3. **Gestão de Espaço**: Detalha como o espaço de armazenamento é gerenciado, incluindo alocação de espaço para novos registros, remoção de registros e a re-utilização de espaço em caso de exclusões.
4. **Desempenho**: Impacta a eficiência e o desempenho das operações de leitura e gravação. Um bom esquema interno pode melhorar significativamente a velocidade de acesso aos dados. [[]]

## Exemplo de Esquema Interno

Para ilustrar, considere um banco de dados que armazena informações de clientes e suas compras. O esquema interno pode incluir:

- **Tabelas e Arquivos**: Os dados dos clientes podem ser armazenados em um arquivo separado, enquanto os dados de compras podem estar em outro arquivo.
- **Estruturas de Índice**: Para acelerar as consultas, um índice B-tree pode ser usado para a coluna de ID do cliente, permitindo acesso rápido às informações do cliente.
- **Armazenamento Compactado**: Os dados podem ser compactados para economizar espaço em disco, especialmente se contiverem muitos registros.

### Estrutura Física


```sql

-- Tabela de Clientes

CREATE TABLE clientes (

id INT PRIMARY KEY,

nome VARCHAR(100),

email VARCHAR(100)

);

  

-- Tabela de Compras

CREATE TABLE compras (

id INT PRIMARY KEY,

cliente_id INT,

produto VARCHAR(100),

valor DECIMAL(10, 2),

FOREIGN KEY (cliente_id) REFERENCES clientes(id)

);

```

### Estruturas de Índice

```sql

-- Criando um índice B-tree para a tabela de clientes

CREATE INDEX idx_cliente_email ON clientes(email);

```

### Armazenamento Compactado

A compactação dos dados pode ser realizada em nível de sistema de gerenciamento de banco de dados (SGBD). Por exemplo, no PostgreSQL, você pode usar o tipo de dados [[bytea]] para armazenar dados binários compactados, ou aplicar métodos de compressão em tabelas grandes para reduzir o uso de espaço em disco.

## Importância do Esquema Interno

- **Performance**: O desempenho do banco de dados em termos de velocidade de consulta e escrita está diretamente relacionado à eficiência do esquema interno.
- **Escalabilidade**: Um esquema interno bem projetado pode suportar um aumento no volume de dados sem comprometer o desempenho.
- **Manutenção**: Um bom design facilita a manutenção e a administração do banco de dados, como backup e recuperação de dados.

## Conclusão

Em resumo, o _esquema interno_ é essencial para o funcionamento eficiente de um banco de dados. Enquanto o [[Esquema externo]] define como os usuários interagem com os dados e o [[Esquema conceitual]] fornece uma visão abstrata dos dados, o _esquema interno_ cuida dos detalhes técnicos que garantem que os dados sejam armazenados e acessados de forma eficiente.