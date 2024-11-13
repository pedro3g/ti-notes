**Definição**: A **fragmentação vertical** é uma técnica de particionamento de dados em bancos de dados distribuídos que divide uma tabela em subconjuntos de colunas, criando fragmentos que contêm diferentes atributos da tabela original. Cada fragmento armazena um subconjunto específico de colunas, permitindo que consultas que acessem apenas determinados atributos sejam mais eficientes.

## Características Principais

- **Divisão por Colunas**: Cada fragmento vertical contém um conjunto específico de colunas da tabela original.

- **Chave Primária Comum**: Para manter a integridade dos dados, a chave primária é replicada em todos os fragmentos, possibilitando a reconstrução da tabela original quando necessário.

- **Melhoria de Desempenho**: Consultas que acessam apenas um subconjunto de colunas podem ser atendidas mais rapidamente, reduzindo a carga de E/S e melhorando o desempenho.

## Vantagens

- **Eficiência em Consultas**: Reduz o volume de dados processados em consultas que não requerem todas as colunas, diminuindo o tempo de resposta.

- **Segurança e Privacidade**: Permite armazenar dados sensíveis em fragmentos separados, aplicando políticas de segurança específicas para cada fragmento.

- **Manutenção Facilitada**: Atualizações e manutenções podem ser realizadas em fragmentos específicos sem impactar toda a tabela.

## Desvantagens

- **Complexidade de Gerenciamento**: A divisão da tabela em múltiplos fragmentos aumenta a complexidade do sistema, exigindo mecanismos para manter a consistência e a integridade dos dados.

- **Overhead de Junção**: Operações que requerem dados de múltiplos fragmentos podem necessitar de junções, introduzindo overhead e potencialmente afetando o desempenho.

## Exemplo Prático

Considere uma tabela `Clientes` com os seguintes atributos:

- `ID_Cliente` (chave primária)
- `Nome`
- `Endereço`
- `Telefone`
- `Email`
- `Data_Nascimento`

Aplicando a fragmentação vertical, a tabela pode ser dividida em dois fragmentos:

**Fragmento 1**:

| ID_Cliente | Nome | Endereço |
|------------|------|----------|
| 1          | Ana  | Rua A    |
| 2          | João | Rua B    |

**Fragmento 2**:

| ID_Cliente | Telefone | Email          | Data_Nascimento |
|------------|----------|----------------|-----------------|
| 1          | 12345678 | ana@exemplo.com | 01/01/1990      |
| 2          | 87654321 | joao@exemplo.com | 02/02/1985      |

Neste exemplo, a chave primária `ID_Cliente` é replicada em ambos os fragmentos para permitir a reconstrução da tabela original quando necessário.

## Considerações

- **Escolha de Colunas**: A seleção de quais colunas incluir em cada fragmento deve ser baseada nos padrões de acesso das aplicações, visando otimizar o desempenho.

- **Consistência**: Mecanismos devem ser implementados para garantir que as atualizações nos dados sejam refletidas corretamente em todos os fragmentos relevantes.

- **Segurança**: Ao armazenar dados sensíveis em fragmentos separados, é possível aplicar controles de acesso mais rigorosos, aumentando a segurança das informações.
