**Redirect-on-Write (ROW)** é uma técnica de otimização de armazenamento semelhante ao *[[Copy-on-Write (COW)]]*, mas que utiliza uma abordagem diferente para gerenciar alterações em dados. Em vez de copiar dados existentes para um novo local ao serem modificados, como no COW, o ROW redireciona a escrita para um local de armazenamento separado, mantendo os dados originais inalterados. Esse método é amplamente utilizado em sistemas de arquivos e em [[Snapshot]]s para gerenciar mudanças de forma eficiente.

## Funcionamento

1. **Inicialização**: O sistema armazena os dados originais em um local específico.
2. **Modificação**: Quando uma alteração é solicitada, o sistema redireciona a escrita para um novo local no disco em vez de sobrescrever o dado original.
3. **Metadados**: O sistema atualiza os metadados para apontar para o novo local dos dados modificados, preservando o estado anterior.

Essa abordagem permite que o sistema mantenha uma versão imutável dos dados originais, ao mesmo tempo que registra as alterações de maneira eficiente em termos de espaço e desempenho.

## Aplicações Comuns

- **Snapshots Incrementais**: Em sistemas de armazenamento, como dispositivos [[NAS]] (Network Attached Storage) e [[SAN]] (Storage Area Network), o ROW facilita a criação de snapshots incrementais, onde apenas as mudanças são salvas.
- **Sistemas de Arquivos Avançados**: Sistemas de arquivos como o [[Btrfs]] e o [[ZFS]] utilizam ROW para gerenciar snapshots e oferecer suporte para restauração de estados anteriores de dados sem duplicar as informações.
- **Virtualização**: ROW também é usado em alguns ambientes de virtualização para gerenciar o armazenamento de máquinas virtuais, otimizando o espaço necessário para dados que são constantemente modificados.

## Vantagens e Desvantagens

| Vantagens                                   | Desvantagens                       |
| ------------------------------------------- | ---------------------------------- |
| Eficiência de armazenamento                 | Exige metadados adicionais         |
| Preserva o estado original dos dados        | Implementação mais complexa        |
| Ideal para snapshots e backups incrementais | Pode ter maior latência em acessos |

## Exemplo no Sistema de Arquivos ZFS

No sistema de arquivos ZFS, o ROW é usado para snapshots e clones. Quando uma alteração é feita, em vez de sobrescrever o dado original, o ZFS redireciona a alteração para um novo local. Isso permite a criação de snapshots com baixo uso de espaço, pois apenas as modificações são armazenadas. Além disso, esse método facilita a restauração para versões anteriores, já que os dados originais permanecem intactos.

## Conclusão

A técnica Redirect-on-Write é essencial para gerenciar mudanças em sistemas de arquivos modernos, especialmente em ambientes que dependem de snapshots e backups frequentes. Ela oferece uma forma eficaz de preservar dados originais e armazenar apenas as alterações, o que torna o gerenciamento de versões e a restauração de dados muito mais eficientes.