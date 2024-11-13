Um **snapshot** é uma cópia exata do estado atual de um sistema, arquivo ou conjunto de dados em um momento específico no tempo. Ele funciona como uma "fotografia" que permite capturar e preservar o conteúdo e a estrutura de dados em seu estado original, possibilitando a restauração ou análise futura. Esse recurso é amplamente utilizado em várias áreas da computação, como sistemas de arquivos, virtualização e gerenciamento de bancos de dados.

## Principais Características

1. **Não altera o original**: Um snapshot geralmente não modifica o estado original dos dados, apenas registra suas referências para restaurá-los conforme necessário.
2. **Eficiência de Armazenamento**: A maioria dos sistemas que suportam snapshots usa *[[Copy-on-write (COW)]]* ou *[[Redirect-on-write (ROW)]]*, técnicas que otimizam o espaço de armazenamento, mantendo as partes inalteradas dos dados.
3. **Recuperação Rápida**: Em caso de falhas ou necessidade de recuperação, snapshots permitem restaurar rapidamente o estado anterior do sistema sem exigir restauração completa a partir de um backup externo.

## Aplicações Comuns

- **Sistemas de Arquivos**: Permitem a criação de snapshots de arquivos ou volumes para preservar o estado de dados em casos de modificações ou exclusões acidentais.
- **Virtualização**: Em ambientes de máquinas virtuais, snapshots possibilitam a restauração do estado de uma VM para um ponto específico, útil para testes e atualizações.
- **Bancos de Dados**: Snapshots de bancos de dados facilitam o backup incremental, evitando perda de dados e simplificando a recuperação.

## Vantagens e Desvantagens

| Vantagens                        | Desvantagens                         |
|----------------------------------|--------------------------------------|
| Restauração rápida               | Ocupa espaço de armazenamento        |
| Ideal para testes e atualizações | Dependência da implementação         |
| Reduz impacto de falhas          | Pode impactar a performance          |

## Exemplo de Uso em Virtualização

Em ambientes de [[Virtualização]], snapshots são amplamente usados para criar pontos de recuperação em uma [[Máquina virtual (VM)]]. Um snapshot pode ser tirado antes de uma atualização ou configuração importante, permitindo reverter a VM ao estado anterior caso ocorra algum problema.

## Conclusão

O uso de snapshots proporciona uma forma prática de preservar e restaurar estados de sistemas, arquivos e dados, sendo uma ferramenta essencial para recuperação rápida, suporte a testes e continuidade de negócios.