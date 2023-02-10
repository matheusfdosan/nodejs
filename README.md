# O que é o NodeJS:

O NodeJS é um JS Runtime Enviroment (Ambiente de Execução para JavaScript). Antigamente, o JavaScript era usado apenas no client-side, para construção de páginas web, logo, foi criado o NodeJS, que foi feito para ser executado fora do navegador (e ele NÃO É UM FRAMEWORK E NEM UMA LINGUAGEM).

# O que podemos fazer com o NodeJS:

- Back-end
- Front-end
- Micro-serviços
- APIs
  - WebApp
  - Mobile
  - Desktop
- Scripts e Automação
- Machine Learning
- I.A

Tudo isso, com JavaScript.

Uma coisa que, não é recomendado para o NodeJS, o uso de muito processamento de CPU.

# Vantagens:

Ele é muito rápido, tanto na execução quanto na produção de APIs, scripts e etc. Além dele ser de alta escalabilidade, ou seja, podemos fazer aplicação de alta qualidade com o NodeJS. E também, o JavaScript está em todo o lugar e a comunidade é enorme.

# V8

É um **interpretador de JS** para linguagem de máquina, foi desenvolvida pela **Google**, e é utilizada no navegador Google Chrome. Criado em C++, que está bem próximo da **linguagem de máquina**.

## Como o V8 conversa com a máquina?

Imaginamos:

Com a linguagem de máquina (binária), foi criada uma outra linguagem, o Assembly. Que foi usada para dar vida ao C++, e utilizando o C++ foi criado o motor V8 da Google.

## Como funciona?

O V8 é baseado nas últimas features (recursos) do JavaScript, contudo, seu foco está no Chrome, mas também, por conta disso, não deixa o NodeJS disfuncional. E por isso, o V8 em seu interior não possui a **DOM**, pois a DOM é uma **API do próprio browser**, o **console** também não vem embutido no V8, mas roda no NodeJS. E também o V8 não trabalha com sistema de arquivos, e sim, quem trabalha é o ambiente do NodeJs.

# Como funciona?

Por que o JavaScript é tão rápido?

O NodeJs é uma plataforma orientada a eventos, que usa uma arquitetura de **Single Threaded Event Loop**, para gerenciar vários eventos simultâneos, ou seja, o NodeJS trabalha de uma maneira assíncrona, que faz mais de um evento de cada vez.

# Avançando nos entendimentos do NodeJs

Tudo começa com uma aplicação Node, o Node utiliza o V8 do Chrome, contudo, o V8, junto com o NodeJs, conversam com outro sistema, o Libuv, uma biblioteca que trabalha de forma assíncrona, e conversa diretamente com o sistema operacional. 

O núcleo do Node.js é baseado em um modelo de E/S não bloqueante e orientado a eventos, o que o torna leve e eficiente. Neste modelo, uma única thread é responsável por executar o código e o sistema usa um loop de eventos para escutar e responder a vários eventos. Quando um evento ocorre, como um cliente solicitando dados do servidor, o loop de eventos envia a solicitação para uma função de retorno, que processa a solicitação e envia uma resposta de volta para o cliente.

Uma das principais vantagens deste modelo é que ele permite que o Node.js lide com um grande número de conexões concorrentes sem criar uma nova thread para cada uma delas. Isso o torna adequado para aplicativos em tempo real, como aplicativos de chat e jogos online, que exigem baixa latência e tempos de resposta rápidos.

# Globals

Os **objetos globais** são objetos que compõe todos os módulos do NodeJs, como:

- __dirname
- __filename
- exports
- module
- require()

Existem também os *objetos internos* que fazem parte da própria linguagem JavaScript, que também são globalmente acessível.

# required('arg'): 
  
O require() chama as funcionalidade que estão dentro dos módulos (./node_modules), dentro dele, há sempre uma string com o nome do módulo:

```js
const path = require("path")
```

O módulo 'path' é um módulo nativo do Node, ou seja, não é necessário instalá-lo pois já está. Claro que, também há como criar módulos e instalá-los no Node por meio de NPM.

Colocamos o required dentro de uma variável, normalmente com o nome do módulo que iremos usar. Usando essa variável para ativar as funcionalidades do módulo, veja algumas funcionalidades do módulo path:

O método `path.dirname(caminho)` retorna os diretórios do caminho de um arquivo.

```js
console.log("\n" + path.dirname(C:\Users\mathe\Desktop\testes\code.js))
// C:\Users\mathe\Desktop\testes\
```

O método `path.extname()` retorna o nome da extensão de um arquivo. 

```js
console.log("\n" + path.extname("index.html"))
// .html
console.log(path.extname("style.css"))
// .css
console.log(path.extname("script.js"))
// .js
```

O `path.basename()` retorna a última parte de um caminho.

```js
console.log("\n" + path.basename(__filename))
// C:\Users\mathe\Desktop\testes\code.js
```

# Criando o módulo para exportação

O primeiro passo é criar o arquivo onde vai ficar o módulo, e então escrever, 'module.exports =...' que vai deixar o módulo disponível para a importação por outros arquivos. O 'module.exports' pode receber qualquer valor, seja uma string, number, function e etc.

```js
module.exports = {
  name: "Carlos Miranda",
  age: 48,
  height: 1.78,
}
```

# Importação do módulo

```js
const data = require('./criando_modulo')
```

Assim conseguindo ligar os dados do outro arquivo até esse.

```js
console.log(data)
// { name: 'Carlos Miranda', age: 48, height: 1.78 }
```

# Process

```js
const path = require("path")
```

Com o process temos outros tipos de funcionalidades, como por exemplo: o `process.argv`, que retorna um array com o caminho de execução do Node que estamos utilizando, e o caminho do arquivo passado para ele.

```js
console.log("\n" + process.argv)
// C:\Program Files\nodejs\node.exe
```

O `process.argv` retorna um array, então para pegarmos os dados desse array, precisamos então especifica-lo por meio das posições.

```js
console.log(
  process.argv[0],
  // caminho relativo até o executavel do Node.js
  path.basename(__filename),
  // nome desse arquivo 
  process.argv[1],
  // caminho relativo desse arquivo
)
```

No terminal, escrevendo, `node process`, é possível escrever ainda mais, `node process Matheus Faustino`, depois disso, o array vai estar com mais dois valores, "Matheus" e "Faustino", e então é só pegar por meio das posições.

```js
console.log("\nNome:", process.argv[2] + " " + process.argv[3])
// Nome: Matheus Faustino
```

# Flags

No terminal, ao invés de passarmos os valores para o `process.argv` dessa forma: `node process Matheus Faustino`, podemos fazer de uma maneira mais simples: `node process --name "Matheus Faustino" --message "Hello, World!"`, e isso é o que chamamos de flags.

```js
console.log(process.argv)
/*
  [
    "C:\\Program Files\\nodejs\\node.exe",
    "C:\\Users\\mathe\\Desktop\\testes\\process.js",
    "--name",
    "Matheus Faustino",
    "--message",
    "Hello, World!"
  ]
*/
```

Assim retornando um array com o caminho até o executável do Node.js, caminho relativo até o arquivo local, e as flags.
