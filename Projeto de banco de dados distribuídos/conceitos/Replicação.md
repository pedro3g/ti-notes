É caracterizada por uma tabela global “copiada integralmente” para um banco de dados local.
Na replicação, ocorre um aumento da confiabilidade e da disponibilidade, mas apresenta o problema de como propagar as atualizações ocorridas em um dos sites para os outros e exige mais memória secundaria local.

## Tipos de Replicação

- **Replicação Síncrona**: Neste tipo de replicação, uma operação de escrita precisa ser confirmada por todos os nós replicados antes de ser considerada concluída. Isso garante consistência forte, mas pode impactar a performance devido ao tempo de espera para confirmação.

- **Replicação Assíncrona**: Aqui, as operações de escrita são propagadas para os nós replicados sem a necessidade de confirmação imediata. Embora isso possa melhorar a performance, pode causar inconsistências temporárias entre os nós, pois a propagação das mudanças não acontece instantaneamente.

## Exemplo Prático: Banco de Dados de Produtos

Imagine um sistema de banco de dados distribuído que armazena informações sobre produtos em várias regiões do mundo. Para garantir alta disponibilidade e baixa latência, os dados dos produtos são replicados em diferentes servidores localizados em diferentes regiões geográficas.

### Estrutura Original da Tabela de Produtos

| id_produto | nome        | categoria   | preco  | estoque |
|------------|-------------|-------------|--------|---------|
| 1          | Produto A   | Eletrônicos | 1500   | 100     |
| 2          | Produto B   | Móveis      | 300    | 50      |
| 3          | Produto C   | Roupas      | 80     | 200     |

### Replicação Assíncrona

Na replicação assíncrona, quando um produto é adicionado ou atualizado em um servidor, a atualização é propagada para os outros servidores de maneira assíncrona. Isso significa que a mudança pode não ser refletida imediatamente em todos os servidores, mas, eventualmente, os dados estarão consistentes em todas as réplicas.

#### Servidor Primário (EUA)

| id_produto | nome        | categoria   | preco  | estoque |
|------------|-------------|-------------|--------|---------|
| 1          | Produto A   | Eletrônicos | 1500   | 100     |
| 2          | Produto B   | Móveis      | 300    | 50      |

#### Servidor Replicado (Europa)

| id_produto | nome        | categoria   | preco  | estoque |
|------------|-------------|-------------|--------|---------|
| 1          | Produto A   | Eletrônicos | 1500   | 100     |
| 2          | Produto B   | Móveis      | 300    | 50      |

#### Servidor Replicado (Ásia)

| id_produto | nome        | categoria   | preco  | estoque |
|------------|-------------|-------------|--------|---------|
| 1          | Produto A   | Eletrônicos | 1500   | 100     |
| 2          | Produto B   | Móveis      | 300    | 50      |

### Replicação Síncrona

Na replicação síncrona, todas as mudanças feitas em um nó primário são propagadas e confirmadas por todos os nós replicados antes que a operação seja concluída. Isso garante que todos os nós estejam sempre atualizados e consistentes, mas pode adicionar latência às operações de escrita, pois o processo de confirmação exige comunicação com todos os nós.

#### Servidor Primário (EUA)

| id_produto | nome        | categoria   | preco  | estoque |
|------------|-------------|-------------|--------|---------|
| 1          | Produto A   | Eletrônicos | 1500   | 100     |
| 2          | Produto B   | Móveis      | 300    | 50      |

#### Servidor Replicado (Europa)

| id_produto | nome        | categoria   | preco  | estoque |
|------------|-------------|-------------|--------|---------|
| 1          | Produto A   | Eletrônicos | 1500   | 100     |
| 2          | Produto B   | Móveis      | 300    | 50      |

#### Servidor Replicado (Ásia)

| id_produto | nome        | categoria   | preco  | estoque |
|------------|-------------|-------------|--------|---------|
| 1          | Produto A   | Eletrônicos | 1500   | 100     |
| 2          | Produto B   | Móveis      | 300    | 50      |

### Benefícios e Desafios da Replicação

**Benefícios**:
- **Alta Disponibilidade**: Se um nó falhar, os dados ainda estarão disponíveis em outros nós replicados.
- **Desempenho**: A replicação ajuda a melhorar o desempenho ao reduzir a latência, fornecendo dados locais em diferentes regiões geográficas.
- **[[Escalabilidade]]**: Com mais réplicas, o sistema pode lidar com um maior número de requisições de leitura.

**Desafios**:
- **Consistência**: No caso da replicação assíncrona, pode haver uma janela de inconsistência entre as réplicas, o que pode causar problemas em operações que requerem dados consistentes entre os nós.
- **Latência**: A replicação síncrona pode introduzir latência nas operações de escrita devido à necessidade de confirmação em todos os nós.
- **Gerenciamento de Falhas**: O gerenciamento de falhas e recuperação de nós replicados pode ser complexo, especialmente em sistemas distribuídos em larga escala.

## Conclusão

A replicação em bancos de dados distribuídos é uma técnica essencial para garantir alta disponibilidade e desempenho. A escolha entre replicação síncrona e assíncrona depende das necessidades de consistência, desempenho e tolerância a falhas do sistema. A replicação ajuda a garantir que os dados estejam acessíveis e consistentes em toda a rede de nós, mas também traz desafios relacionados ao gerenciamento de consistência e latência.