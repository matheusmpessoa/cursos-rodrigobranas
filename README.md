# grunt-gulp-example
Criando aplicações Grunt e Gulp para exemplo.

## Características

### O que são?
Grunt e gulp são utilizados para automatização de tarefas utilizando JavaScript e executando na plataforma Node.js (necessita sua instalação).

Ambos são extensíveis e funcionam por meio de plugins.

### Comunidade
Grunt tem mais de 60 contribuidores e mais de 10 mil stars no Github.
Gulp tem mais de 160 contribuidores e mais de 19 mil stars no Github.

### StackOverflow
Grunt tem mais de 20 mil perguntas enquanto o Gulp tem mais de 15 mil.

### Por que utilizar?
Cria um controle da produção do software, melhorando a perfomance.

### Minificação
Cria um replace em variaveis, ajuda na proteção do código.

Remove coisas que não são necessariamente úteis, são úteis apenas para legibilidade e não no processo de  interpretação.

Remove cerca de 30% a 40% de coisas desnecessárias na interpretação.

Remove coisas como:
- /n
- comentários
- espaços em branco

---

## Grunt ou Gulp?

### Plugins
Grunt tem mais de 5 mil plugins. O Gulp tem mais de 2 mil.

Plugins úteis
- jshints
- concat
- uglify
- cssmin
- htmlmin
- copy

### Forma de utilizar
MUITO útil na ESCOLHA da ferramenta a ser utilizada.

#### Grunt 
Grunt trabalha com configuração (configuration over code) para criar o workflow. Cria-se um arquivo plugin-a-plugin para se dizer o que deve fazer, executando sequencialmente.

É criado um 'gruntfile' configurando cada plugin e depois chama a task no fim do código.

#### Gulp
Gulp é um código no qual é realmente necessário codificar tarefas. Gulp tem uma estrutura semelhante ao Node.js.

### Velocidade
Execução das mesmas tarefas (uglify, minificação de arquivos, concatenação) executadas nas ferramentas.
- Grunt leva 920ms.
-  Gulp leva 493ms.

Grunt funciona passo a passo. É necessário realizar um I/O, utilizando o disco, para encadear tarefas em que a saída de uma é a entrada de outra.

O Gulp é possível realizar as tarefas sem realizar I/O utilizando a memória, por meio da API de Stream do Node.js.