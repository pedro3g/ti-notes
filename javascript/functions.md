# Funções em JS

<aside>
📌 **Funções em JavaScript são como assistentes pessoais que realizam tarefas específicas para você.**

</aside>

Imagine que você tem um assistente pessoal que é especializado em diferentes tarefas. Por exemplo, um assistente para fazer cálculos matemáticos, outro para traduzir idiomas e um terceiro para organizar eventos.

Quando você precisa de ajuda em uma tarefa específica, você chama o assistente adequado. Por exemplo, quando precisa de um cálculo, você chama o assistente matemático. Você não precisa entender como ele realiza o cálculo internamente; você apenas passa os números e ele fornece a resposta.

Em programação, as funções são como esses assistentes pessoais. Elas são blocos de código que realizam tarefas específicas. Você as cria e as nomeia para que, sempre que precisar realizar aquela tarefa, basta chamar a função pelo nome. Isso torna seu código mais organizado e reutilizável, pois você não precisa repetir o mesmo código toda vez que desejar realizar a mesma tarefa.

Aqui está um exemplo simples de como uma função funciona em JavaScript:

```jsx
// Definindo uma função para calcular a soma de dois números
function calcularSoma(numero1, numero2) {
    return numero1 + numero2;
}

// Chamando a função para calcular a soma
let resultado = calcularSoma(5, 3); // O resultado será 8
```

Neste exemplo, **`calcularSoma`** é a função que realiza a tarefa de adicionar dois números. Você a chama passando os números que deseja somar, e ela retorna o resultado. Dessa forma, você pode usar essa função sempre que precisar calcular uma soma, sem escrever o código de adição repetidamente.

<aside>
📌 Isso torna seu código mais organizado, mais fácil de entender e economiza tempo, assim como ter assistentes pessoais especializados em diferentes tarefas facilita a sua vida.

</aside>

## Funções Construtoras

Funções construtoras em JavaScript são funções comuns que são usadas para criar objetos. Elas são frequentemente usadas em conjunto com a palavra-chave **`new`** para criar instâncias de objetos com base em um "modelo" ou "protótipo" definido pela função construtora. Aqui está como elas funcionam:

1. **Definindo uma Função Construtora**: Você define uma função construtora como faria com qualquer outra função em JavaScript, mas geralmente começa com uma letra maiúscula por convenção. Dentro dessa função, você define propriedades e métodos que serão compartilhados por todos os objetos criados a partir dela.
    
    ```jsx
    function Carro(marca, modelo) {
      this.marca = marca;
      this.modelo = modelo;
      this.ano = new Date().getFullYear();
      this.ligar = function() {
        console.log('O carro está ligado.');
      };
    }
    ```
    
2. **Criando Instâncias com `new`**: Para criar um objeto a partir da função construtora, você usa a palavra-chave **`new`**, seguida do nome da função construtora.
    
    ```jsx
    const meuCarro = new Carro('Toyota', 'Corolla');
    ```
    
3. **Propriedades e Métodos Compartilhados**: As propriedades e métodos definidos na função construtora são compartilhados por todas as instâncias criadas a partir dela. Portanto, todos os objetos criados com **`Carro`** terão as propriedades **`marca`**, **`modelo`**, **`ano`** e o método **`ligar`**.
    
    ```jsx
    console.log(meuCarro.marca); // Saída: Toyota
    meuCarro.ligar(); // Saída: O carro está ligado.
    ```
    

As funções construtoras são uma das maneiras de criar objetos em JavaScript e são especialmente úteis quando você precisa criar muitos objetos com a mesma estrutura. Com elas, você pode criar objetos personalizados com propriedades e métodos predefinidos, o que torna o código mais organizado e fácil de manter.

## Declarando Funções

<aside>
📌 Em JavaScript, você pode declarar uma função de várias maneiras. Aqui estão as principais formas de declarar funções em JavaScript:

</aside>

1. **Declaração de Função**:
    
    ```jsx
    
    function nomeDaFuncao(parametro1, parametro2) {
        // Código da função
    
    ```
    
    Esta é a forma mais comum de declarar funções. Ela cria uma função nomeada que pode ser chamada posteriormente no código.
    
2. **Expressões de Função**:
    
    ```jsx
    const nomeDaFuncao = function(parametro1, parametro2) {
        // Código da função
    };
    ```
    
    Você pode atribuir uma função anônima a uma variável, criando assim uma expressão de função. A função pode ser chamada usando **`nomeDaFuncao()`**.
    
3. **Arrow Functions** (Funções de Seta):
    
    ```jsx
    const nomeDaFuncao = (parametro1, parametro2) => {
        // Código da função
    };
    ```
    
    Arrow functions são uma sintaxe mais curta para criar funções em JavaScript. Elas são frequentemente usadas em funções de callback e em situações onde uma função pequena é necessária.
    
4. **Funções de Construtor**:
    
    Você pode criar objetos de função de construtor usando a palavra-chave **`function`** seguida por **`new`**. Isso é menos comum em JavaScript moderno e é mais usado para criar classes personalizadas.
    
    ```jsx
    function Pessoa(nome, idade) {
        this.nome = nome;
        this.idade = idade;
    }
    
    const pessoa1 = new Pessoa('Alice', 30);
    ```
    

Estas são as principais formas de declarar funções em JavaScript. A escolha entre elas depende do contexto e dos requisitos do seu código. Cada uma delas tem suas vantagens e casos de uso específicos.

### Closures

Uma closure é uma função dentro de outra função. Ela "lembra" do ambiente onde foi criada, mesmo depois de a função externa ter terminado.

**Para que serve uma closure?**
Closures são usadas para criar dados privados, encapsulando variáveis e funções para que não sejam acessadas de fora.

**Como usar closures em JavaScript?**

```jsx
function contador() {
  let contagem = 0; // Variável privada

  function incrementar() {
    contagem++;
    console.log(contagem);
  }

  return incrementar;
}

const contador1 = contador();
contador1(); // Isso imprime 1
contador1(); // Isso imprime 2

const contador2 = contador();
contador2(); // Isso imprime 1 (uma nova contagem)
```

**Quando usar closures?**

Use closures quando precisar de variáveis privadas ou quando quiser criar funções que "lembram" seu ambiente de criação. Isso é útil para design de software modular e evita conflitos de nomes.

## Callback

Funções de callback em JavaScript são funções que você passa como argumentos para outras funções. Essas funções são executadas mais tarde, após um evento específico ou uma tarefa ter sido concluída. Elas são usadas principalmente para lidar com operações assíncronas, como carregamento de arquivos, solicitações de rede ou eventos de usuário.

**Por que usar funções de callback:**

- Permitem que você execute código após uma operação assíncrona ser concluída.
- São úteis para manter seu código organizado e legível, evitando aninhamento excessivo de código assíncrono.
    
    ```jsx
    function realizarOperacaoAssincrona(dados, callback) {
        // Simula uma operação assíncrona, como uma solicitação de API
        setTimeout(function() {
            const resultado = dados * 2;
            callback(resultado);
        }, 1000);
    }
    
    function callbackExemplo(resultado) {
        console.log(`O resultado é: ${resultado}`);
    }
    
    realizarOperacaoAssincrona(5, callbackExemplo);
    ```
    
- Permitem reutilizar funções em várias partes do seu código.

**Como usar funções de callback:**

Neste exemplo, a função **`realizarOperacaoAssincrona`** aceita dados e uma função de callback como argumentos. Ela simula uma operação assíncrona e, após concluída, chama a função de callback **`callbackExemplo`** com o resultado.

**Quando usar funções de callback:**

- Quando você precisa lidar com operações assíncronas, como solicitações de rede ou leitura de arquivos.
- Para manter seu código mais organizado e legível, especialmente quando lida com várias operações assíncronas.
- Para tornar suas funções mais flexíveis, permitindo que diferentes ações sejam executadas após a conclusão de uma tarefa.

As funções de callback são uma parte fundamental do JavaScript, especialmente no desenvolvimento de aplicativos da web, onde muitas operações são assíncronas. Elas ajudam a garantir que seu código seja eficiente e capaz de lidar com tarefas assíncronas de maneira controlada.

## Funções Imediatas

<aside>
📌 Funções imediatas, também conhecidas como Immediately Invoked Function Expressions (IIFE) em inglês, são funções que são declaradas e executadas imediatamente após sua definição. Elas são usadas para criar escopo local e proteger variáveis de poluir o escopo global em JavaScript.

</aside>

**O que são:** Funções imediatas são como pequenos pedaços de código que você executa assim que os cria.

**Para que servem:** Elas são úteis para isolar variáveis, evitando conflitos no escopo global, e para encapsular funcionalidades, tornando o código mais organizado e seguro.

**Como usar:** Para criar uma IIFE, você a declara entre parênteses e a segue com **`();`** para executá-la imediatamente. Veja um exemplo:

```jsx
(function() {
    var mensagem = "Olá, mundo!";
    console.log(mensagem);
})();
```

**Quando usar:** Você pode usar funções imediatas sempre que desejar criar um escopo local temporário para evitar que variáveis entrem no escopo global. Isso é especialmente útil quando você está trabalhando com bibliotecas ou frameworks que podem ter variáveis com nomes semelhantes.

Por exemplo, se você estiver desenvolvendo um código JavaScript que será incorporado em um site maior, uma IIFE pode ajudar a garantir que suas variáveis não colidam com as do site principal.

Lembre-se de que as funções imediatas não são tão necessárias com a introdução do **`let`** e **`const`**, que têm escopo de bloco e ajudam a evitar vazamento de variáveis no escopo global. Ainda assim, as IIFE são uma ferramenta útil, especialmente para manter o código legado ou trabalhar em cenários mais complexos.

## Funções de Fábrica

**Funções de fábrica** em JavaScript são funções que retornam objetos. Elas são usadas para criar e retornar instâncias de objetos com propriedades e métodos específicos. Isso é útil quando você precisa criar várias instâncias de um objeto com a mesma estrutura.

**O que são:** Funções de fábrica são como máquinas que produzem objetos com base em um modelo que você define.

**Para que servem:** Elas servem para criar múltiplas instâncias de objetos com a mesma estrutura, economizando tempo e evitando duplicação de código.

**Como usar:** Você define uma função que cria um objeto com propriedades e métodos desejados e a chama sempre que precisa criar uma nova instância desse objeto. Veja um exemplo:

```jsx
function criarPessoa(nome, idade) {
    return {
        nome: nome,
        idade: idade,
        saudacao: function() {
            console.log(`Olá, meu nome é ${this.nome} e tenho ${this.idade} anos.`);
        }
    };
}

const pessoa1 = criarPessoa("Alice", 30);
const pessoa2 = criarPessoa("Bob", 25);

pessoa1.saudacao(); // Saída: Olá, meu nome é Alice e tenho 30 anos.
pessoa2.saudacao(); // Saída: Olá, meu nome é Bob e tenho 25 anos.
```

**Quando usar:** Use funções de fábrica quando precisar criar múltiplas instâncias de objetos com a mesma estrutura, como objetos do tipo "pessoa", "carro", "produto", etc. Elas ajudam a manter seu código organizado e evitam a repetição de código na criação de objetos similares.

As funções de fábrica também podem ser usadas em conjunto com herança e encapsulamento para criar objetos com base em classes ou protótipos personalizados, dependendo das necessidades do seu projeto.

- Por que tem esse o nome de Function Factory
    
    A função é chamada de **"função de fábrica"** porque ela age como uma fábrica que produz objetos. Ela é responsável por criar e retornar instâncias de objetos com base em um modelo ou estrutura predefinida.
    
    O termo **"fábrica"** é usado porque essa função é projetada para ser reutilizável e criar várias instâncias de objetos com a mesma estrutura, assim como uma fábrica cria várias cópias de um produto comum. Em vez de criar cada objeto manualmente, você pode usar a função de fábrica para automatizar o processo de criação.
    
    Em resumo, a função de fábrica é chamada assim porque sua principal função é "fabricar" ou criar objetos de maneira eficiente e consistente. Isso ajuda a manter o código limpo, organizado e reutilizável.
    

## Funções Recursivas

Uma função recursiva é uma função que se chama a si mesma durante sua execução. Em outras palavras, é como se a função "pedisse ajuda a si mesma" para realizar uma tarefa.

**Para que serve?**
Funções recursivas são frequentemente usadas para resolver problemas que podem ser divididos em casos menores e idênticos ao problema original. Elas ajudam a simplificar a lógica de programação.

**Como usar?**
Para criar uma função recursiva, você precisa definir a condição de parada (quando a função deve parar de chamar a si mesma) e a lógica recursiva (o que fazer nas chamadas subsequentes).

**Exemplo Prático - Cálculo de Fatorial:**
Vamos calcular o fatorial de um número usando uma função recursiva:

```jsx
function calcularFatorial(numero) {
  // Condição de parada
  if (numero === 0) {
    return 1; // Fatorial de 0 é 1
  } else {
    // Chamada recursiva com um caso menor
    return numero * calcularFatorial(numero - 1);
  }
}

const resultado = calcularFatorial(5); // Isso calculará 5!
console.log(resultado); // O resultado será 120
```

Neste exemplo, a função **`calcularFatorial`** se chama a si mesma com um número menor a cada chamada até atingir a condição de parada (quando **`numero`** se torna 0). Ela multiplica os números ao longo do caminho para calcular o fatorial.

**Quando usar funções recursivas?**
Você deve usar funções recursivas quando estiver lidando com problemas que podem ser divididos em subproblemas idênticos ou semelhantes. Elas são úteis para simplificar a lógica em casos assim, mas é importante definir uma condição de parada para evitar recursão infinita.

## Funções Geradoras

Imagine que você está assistindo a um filme e quer fazer pausas para pegar mais pipoca. Em vez de parar o filme completamente, você pausa e anota o tempo exato em que parou. Depois, quando você retorna, você continua do mesmo ponto.

As funções geradoras são como fazer pausas em um filme. Elas permitem que você pause a execução de uma função e retome de onde parou, mantendo todo o contexto. Isso é útil quando você precisa calcular muitos valores, mas não quer fazer todos de uma vez, economizando memória e recursos.

**Lazy evaluation**

**Exemplo Prático:**

Aqui está um exemplo de função geradora que gera números pares infinitamente:

```jsx
function* gerarNumerosPares() {
  let numero = 0;
  while (true) {
    yield numero;
    numero += 2;
  }
}

const numerosPares = gerarNumerosPares();

console.log(numerosPares.next().value); // 0
console.log(numerosPares.next().value); // 2
console.log(numerosPares.next().value); // 4
// E assim por diante...
```

Neste exemplo, **`gerarNumerosPares`** é uma função geradora que retorna números pares consecutivos toda vez que chamamos **`next()`**. Isso permite que você gere esses números de forma preguiçosa, apenas quando necessário.

**Quando Usar:**

Você pode usar funções geradoras sempre que precisar lidar com sequências de dados preguiçosamente ou lidar com grandes conjuntos de dados de uma maneira mais eficiente em termos de memória e desempenho. Eles são úteis em situações em que você não deseja calcular tudo de uma vez, mas sim conforme necessário.

- **O que são `yield`, o `*`na Function e o `next()`?**
    
    **Yield e *:**
    
    - O **`yield`** é uma palavra-chave que indica onde uma função geradora deve pausar e "entregar" um valor.
    - O **``** (asterisco) na declaração da função, como em **`function*`**, sinaliza que é uma função geradora.
    
    **Next:**
    
    - O método **`next()`** é usado para avançar a execução de uma função geradora.
    - Quando você chama **`next()`**, a função geradora é executada até encontrar o próximo **`yield`**.
    - O **`next()`** retorna um objeto com duas propriedades: **`value`** (o valor entregue pelo **`yield`**) e **`done`** (um valor booleano que indica se a função geradora está concluída).
    
    Aqui está como funciona:
    
    1. Quando você chama **`next()`** pela primeira vez, a função geradora começa a ser executada até encontrar o primeiro **`yield`**. Ela pausa a execução e entrega o valor indicado por esse **`yield`**.
    2. Quando você chama **`next()`** novamente, a execução da função geradora continua a partir do ponto onde foi pausada e continua até encontrar o próximo **`yield`**, pausando novamente e entregando o próximo valor.
    3. Esse processo se repete até que a função geradora seja concluída ou até você decidir parar de chamá-la.
    
    No exemplo anterior:
    
    - O **`yield numero;`** indica que a função deve pausar e entregar o valor atual de **`numero`**.
    - O **`numero += 2;`** aumenta **`numero`** para o próximo valor par.
    
    Ao chamar **`next()`**, a função geradora é executada até o próximo **`yield`**, entregando o valor correspondente. Isso permite que você obtenha os números pares um de cada vez, em vez de calcular todos de uma vez.