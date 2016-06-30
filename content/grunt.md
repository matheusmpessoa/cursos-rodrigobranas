## Grunt

### Sites
- __[Grunt](http://gruntjs.com/)__
- __[Github Grunt](https://github.com/gruntjs/grunt)__
- __[npm](https://www.npmjs.com/)__

### Processo de instalação
Necessário ter o Node.js instalado.

Para executar o comando de instalação do Grunt, digite no npm a instalação do **grunt-client-line** e **--save-dev** para adicionar dependências do desenvolvedor:
``` js 
npm install -g grunt-cli
npm install grunt --save-dev
```

Para exibir a versão do Grunt instalada, digita-se:
``` js
grunt --version
```

### Arquivo de configuração
O arquivo de configuração é chamado de: **gruntfile.js**

O **init config**, aonde se encontra a configuração de cada plugin.

### Criando um workflow
Passos essenciais para qualquer projeto:

- Limpar todos arquivos deixados pelo processo da distribuição anterior
- Verificar a qualidade do código
- Concatenar os arquivos JS
- Minificar todos os arquivos JS já concatenados em um arquivo único
- Minificar os arquivos CSS
- Minificar os arquivos HTML
- Copiar recursos necessários
- Limpar arquivos intermediários

### Arquivo mínimo grunt

Arquivo mínimo:
``` js
module.exports = function (grunt) {
    grunt.initConfig({

    });

    grunt.registerTask('default',[]);
};
```
Para executar, digita-se:
'`grunt`'

### Utilização de plugins
Plugins utilizado no exemplo abaixo: __[jshint](https://www.npmjs.com/package/grunt-contrib-jshint)__, na página oficial do npm.

Para se utilizar qualquer plugin, sempre se deve seguir DOIS passos:

1. Digitar o comando '`npm`' para instalar o plugin.
``` js
npm install grunt-contrib-jshint --save-dev
```
2. Carregar o plugin no arquivo grunt.
``` js
module.exports = function (grunt) {
        grunt.initConfig({

        });

        grunt.loadNpmTasks('grunt-contrib-jshint');

        grunt.registerTask('default',[]);
    };
```
    2.1 Declarar subtasks para realizar a ação do jshint
    ``` js
    module.exports = function (grunt) {
            grunt.initConfig({
                jshint: {
                    dist:{
                        src: ['js/**/*.js']
                    }
                }
            });

            grunt.loadNpmTasks('grunt-contrib-jshint');

            grunt.registerTask('default',[]);
        };
    ```
