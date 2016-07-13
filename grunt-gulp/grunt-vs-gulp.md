## Grunt vs Gulp
![Grunt vs Gulp](http://fiticu.fr/wp-content/uploads/2016/04/grunt-vs-gulp.jpg "Grunt vs Gulp")

## Características

### O que são?
Grunt e gulp são utilizados para automatização de tarefas utilizando JavaScript e executando na plataforma Node.js (necessita sua instalação).

Ambos são extensíveis e funcionam por meio de plugins.

### Interesse

| *Em 06/2016* | __[Grunt](grunt/grunt.md)__ | __[Gulp](gulp/gulp.md)__ | Vencedor |
| --------- | ------ | ------ | ------ |
| **Downloads** | 1.632.998 | 2.149.907 | **Gulp**
| **Plugins**   | 5.778 | 2.501 | **Grunt**
| **Tamanho da comunidade** | 63 contribuidores, 10.887 stars no Github | 176 contribuidores, 21.883 stars no Github | **Gulp**
| **StackOverflow** | 22.032 perguntas | 20.066 perguntas | **Grunt**
| **Velocidade** | 920ms para executar algumas tasks | 493ms para as mesmas tasks. | **Gulp**

### Por que utiliza-los?
Cria um controle da produção do software, melhorando a perfomance.

### Minificação
Cria um replace em variaveis, ajuda na proteção do código.

Remove coisas que não são necessariamente úteis, são úteis apenas para legibilidade e não no processo de  interpretação.

Remove cerca de 30% a 40% de coisas desnecessárias na interpretação do código.

Remove coisas como:
- /n
- comentários
- espaços em branco

## Grunt ou Gulp?

### Plugins
Plugins mais conhecidos:
- jshints
- concat
- uglify
- cssmin
- htmlmin
- copy

### Forma de utilizar
MUITO útil na ESCOLHA da ferramenta a ser utilizada.

#### Grunt 
Grunt trabalha com configuração (configuration over code) para criar o workflow, ou seja, cria-se um arquivo de configurações, com plugin-a-plugin para se dizer o que deve fazer, executando sequencialmente.

É criado um **gruntfile** configurando cada plugin e depois chama a task no fim do código.

#### Gulp
Gulp é um código no qual é realmente necessário codificar tarefas, você cria um arquivo de códigos (code over configuration). Gulp tem uma estrutura semelhante ao Node.js.

### Velocidade
Execução das mesmas tarefas (uglify, minificação de arquivos, concatenação) executadas nas ferramentas.
- Grunt leva 920ms.
-  Gulp leva 493ms.

Grunt funciona passo a passo. É necessário realizar um I/O, utilizando o disco, para encadear tarefas em que a saída de uma é a entrada de outra.

No Gulp é possível realizar as tarefas sem realizar I/O utilizando a memória, por meio da API de Stream do Node.js.
O Gulp excecuta as tarefas em paralelo ao contrário do Grunt.

### Curva de aprendizado
Grunt declara plugin e executa basicamente.

O Gulp requer conhecimento sobre a API de Stream do Node.js

---

## Webpack
Uma outra alternativa ao Grunt e Gulp, o Webpack unifica todos os componentes para que você não perca tempo configurando todos esses itens.

__[Webpack Tutorial](https://www.youtube.com/watch?v=9kJVYpOqcVU)__

__[Site oficial](https://webpack.github.io/)__

__[O que é o Webpack](https://webpack.github.io/docs/what-is-webpack.html)__