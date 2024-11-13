O seu funcionamento inclui a realização do controle da passagem do tempo necessário para realizar uma cópia substitutiva.

O tempo decorrido antes do descarte do extrato atual e sua substituição por um novo é definido pelas necessidades dos usuários e das aplicações na fase de projeto da replicação.

O mecanismo básico de funcionamento consiste na criação de um procedimento em batch executado periodicamente que gera um novo extrato e substitui o antigo nos diversos sites.

Nesse tipo de replicação, podem ser utilizados utilitários existentes no próprio SGBDD ou programas desenvolvidos especificamente para a tarefa, sendo o seu controle realizado pelos administradores do banco de dados.

Existem dois métodos usados para criar um extrato periodicamente atualizado:

### Método 1

Realizar uma cópia completa para o BD de destino em cada intervalo. Esse método é mais simples e pode ser preferido para pequenos extratos.

### Método 2

Realizar uma cópia completa e executar cópias incrementais em cada intervalo. Esse método minimiza o fluxo de dados.

![[extrato periodicamenta atualizado.png]]