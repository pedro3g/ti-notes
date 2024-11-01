A **Fragmentação Horizontal** é uma técnica utilizada em [[bancos de dados distribuídos]] para dividir as [[tabelas]] em subconjuntos de [[linhas]], também chamados de **fragmentos** ou **partições**. Cada fragmento contém uma porção dos dados e é armazenado em diferentes [[Nós]] ou [[servidores]] dentro do sistema distribuído. O objetivo principal é melhorar o desempenho e a **localidade de dados** – ou seja, garantir que os dados mais próximos de uma determinada localização geográfica estejam armazenados no nó mais próximo daquela localização.

## Como Funciona

Na fragmentação horizontal, os dados são divididos de acordo com um critério, que pode ser baseado em uma [[condição lógica]] ou em uma [[coluna de chave]] específica. Por exemplo, em uma [[tabela de clientes]], a fragmentação horizontal pode ocorrer dividindo os [[registros]] de clientes de acordo com seu [[país]] de origem. Assim, todos os clientes do [[Brasil]] poderiam estar em um [[servidor]] específico, enquanto clientes de outros países estariam em outros servidores. Dessa forma, operações de [[consulta]] ou [[manipulação]] de dados podem ser feitas localmente sem a necessidade de acessar todos os nós da rede, reduzindo a [[latência]].

### Exemplo

Imagine uma tabela chamada **Clientes**, onde temos os seguintes dados:

| ID   | Nome       | País         |
|------|------------|--------------|
| 1    | Ana        | Brasil       |
| 2    | Pedro      | México       |
| 3    | Joana      | Brasil       |
| 4    | Miguel     | Canadá       |

Ao aplicar a **fragmentação horizontal**, poderíamos dividir os dados em dois fragmentos, como:

- Fragmento 1 (nó 1): Clientes do Brasil
  - Contém Ana e Joana
- Fragmento 2 (nó 2): Clientes de outros países
  - Contém Pedro e Miguel

Cada fragmento é armazenado em um nó distinto, de modo que os dados dos clientes brasileiros estejam fisicamente mais próximos dos usuários do Brasil, enquanto os clientes de outros países estejam em seus respectivos fragmentos.

## Vantagens

1. **Melhoria no desempenho de consulta**: A fragmentação horizontal reduz o número de linhas que precisam ser analisadas em cada nó, o que torna as operações de consulta mais rápidas.
2. **Escalabilidade**: O sistema distribuído pode crescer horizontalmente ao adicionar mais nós e distribuir os fragmentos, facilitando a expansão do [[banco de dados]].
3. **Manutenção de dados geograficamente próximos**: Para aplicações que necessitam de dados em diferentes regiões, a fragmentação horizontal mantém os dados mais próximos dos usuários locais, o que reduz a [[latência]].

## Desvantagens

1. **Complexidade de manutenção**: A sincronização entre fragmentos e a garantia de [[consistência de dados]] tornam-se mais complexas, pois é necessário gerenciar [[transações distribuídas]].
2. **Rebalanceamento de fragmentos**: Com o crescimento dos dados, pode ser necessário redistribuir os fragmentos entre os nós, o que pode afetar o [[desempenho]] durante o processo.
3. **Possível duplicação de dados**: Dependendo das consultas, algumas [[colunas]] podem precisar estar duplicadas em múltiplos fragmentos para facilitar o acesso, o que pode aumentar o espaço em disco.

## Casos de Uso

A fragmentação horizontal é amplamente utilizada em bancos de dados [[NoSQL]] e em sistemas de grande escala que exigem **alta disponibilidade** e **baixa latência**. Alguns exemplos comuns são:

- Sistemas de [[e-commerce]], onde os dados dos [[clientes]] são armazenados em fragmentos distribuídos por regiões.
- Aplicações de [[redes sociais]] que mantêm dados dos usuários em diferentes regiões para otimizar o tempo de resposta.
- Plataformas de [[streaming]] que fragmentam os dados de visualização de acordo com a [[região]] dos usuários.

A técnica de fragmentação horizontal, quando implementada de forma adequada, contribui significativamente para a escalabilidade e o desempenho de um [[banco de dados distribuído]], garantindo que os dados estejam próximos das operações que mais os acessam.

## Conclusão

A **fragmentação horizontal** é uma técnica essencial em [[sistemas distribuídos]], sendo especialmente relevante para grandes bancos de dados que lidam com milhões de registros e atendem a usuários distribuídos geograficamente. Ela permite que o sistema seja mais eficiente ao distribuir a carga de trabalho entre os nós e reduzir o tempo de acesso aos dados, contribuindo para uma melhor [[experiência do usuário]] e para o sucesso da aplicação como um todo.