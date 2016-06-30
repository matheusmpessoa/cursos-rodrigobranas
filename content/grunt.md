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

### Arquivo mínimo grunt

Arquivo mínimo de configuração - visualizando o arquivo **gruntifile.js**:
``` js
module.exports = function (grunt) {
    grunt.initConfig({

    });

    grunt.registerTask('default',[]);
};
```
Para executar um arquivo grunt, digita-se:
```
grunt
```
Digitando apenas **grunt** se entende que é para realizar a leitura do arquivo **default**

---

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

### Plugins Grunt
- __[grunt-contrib-jshint](https://www.npmjs.com/package/grunt-contrib-jshint)__
- __[grunt-contrib-concat](https://www.npmjs.com/package/grunt-contrib-concat)__
- grunt-contrib-uglify
- grunt-contrib-cssmin
- grunt-contrib-htmlmin
- grunt-contrib-clean
- grunt-contrib-copy

### Utilização de plugins
Para se utilizar qualquer plugin, sempre se deve seguir DOIS passos: Instalar o plugin (**1**) e chamar o plugin no arquivo grunt (**2**).

#### Passo a passo prático de como criar um **gruntfile.js**
1. Digitar o comando **npm** para instalar o plugin.
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
3. Declarar subtasks para realizar a ação do plugin **jshint**
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

4. Alterando o nome da workflow, de **default** para **prod**.
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

        grunt.registerTask('prod',['jshint']);
    };
```

5. Para executar o arquivo grunt criado, digita-se:
``` js
grunt prod
```
Executando assim o arquivo **prod**.
    
6. Agora, será inserido o plugin **concat**

    O plugin é encontrado no site do **npm**. O processo de utilização do plugin é o mesmo processo do **jshints** que foi feito nos passos **1** e **2**.

    Instalação dos pacotes do plugin **concat**.
    ``` js
    npm install grunt-contrib-concat --save-dev
    ```

    Carregou o plugin
    ``` js
    grunt.loadNpmTasks('grunt-contrib-concat');
    ```

    O código ficou assim após a inserção do plugin **concat**, plugin que serve para juntar todo o código.
    ``` js
    module.exports = function (grunt) {
            grunt.initConfig({
                jshint: {
                    dist:{
                        src: ['js/**/*.js']
                    }
                },
                concat: {
                    dist: {

                    }
                }
            });

            grunt.loadNpmTasks('grunt-contrib-jshint');
            grunt.loadNpmTasks('grunt-contrib-concat');

            grunt.registerTask('prod',['jshint']);
        };
    ```

    Perceba que nesse trecho, existe uma origem (**src:**) e destino (**dest:**):
    ``` js
    concat: {
        scripts: {
            src: [
                'js/**/*.js'
                'lib/**/*.js'

            ],
            dest: 'dist/js/scripts.js'
        },
        libs: {
            src: [
                'bower_components/angular/angular.min.js',
                'bower_components/angular-route/angular-route.min.js',
                'bower_components/angular-messages/angular-messages.min.js',
            ],
        }
    }
    ```

7. Para executar o arquivo grunt, junto do plugin **concat**, digita-se:
    ``` js
    grunt concat
    ```

    Terminando assim a concatenação dos arquivos JS