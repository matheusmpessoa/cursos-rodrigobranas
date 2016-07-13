## Grunt
![Grunt](http://helabs.com/blog/images/posts/2014-10-17/grunt_work.jpg "Grunt")

### Sites
- __[Grunt](http://gruntjs.com/)__
- __[Github Grunt](https://github.com/gruntjs/grunt)__
- __[npm](https://www.npmjs.com/)__

### Processo de instalação
Necessário ter o Node.js instalado.

Para executar o comando de instalação do Grunt, digite no npm a instalação do **grunt-client-line** e **--save-dev** para adicionar nas dependências do arquivo **package.json**:
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

Arquivo mínimo de configuração - visualizando o arquivo **gruntfile.js**:
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
- __[grunt-contrib-uglify](https://www.npmjs.com/package/grunt-contrib-uglify)__
- __[grunt-contrib-cssmin](https://www.npmjs.com/package/grunt-contrib-cssmin)__
- __[grunt-contrib-htmlmin](https://www.npmjs.com/package/grunt-contrib-htmlmin)__
- __[grunt-contrib-clean](https://www.npmjs.com/package/grunt-contrib-clean)__
- __[grunt-contrib-copy](https://www.npmjs.com/package/grunt-contrib-copy)__

### Utilização de plugins
Para se utilizar qualquer plugin, sempre se deve seguir **DOIS** passos: Instalar o plugin (**1**) e chamar o plugin no arquivo grunt (**2**).

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

5. Para executar o workflow grunt criado, digita-se:
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

            grunt.registerTask('prod',['jshint', 'concat']);
        };
    ```

    Perceba que: nesse trecho, existe uma **origem** (src) e **destino** (dest). Como também libs apontando para três arquivos (angular.min / angular-route.min / angular-messages.min).
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
    
8. É possível especificar qual tarefa será realizada adicionando **:arquivo** no final
    ``` js
    grunt.registerTask('prod',['jshint', 'concat:scripts']);
    ```
    Só será gerado **scripts**, configurando assim **separadamente**.
    
9. Agora, será inserido o plugin **uglify**. 

    Plugin útil para realizar a minificação de arquivos, reduzindo assim o tamanho (bytes) e unindo a um só arquivo. Normalmente é utilizado em arquivos já concatenados (concat).

    Instalação dos pacotes do plugin **uglify**.
    ``` js
    npm install grunt-contrib-uglify --save-dev
    ```

    Carregou o plugin
    ``` js
    grunt.loadNpmTasks('grunt-contrib-uglify');
    ```

10. Criou a **subtask** para o plugin **uglify**, seguindo o mesmo padrão de **origem** (src) e **destino** (dest).
    ``` js
    uglify: {
        scripts: {
            src: [
                'js/**/*.js'
                'lib/**/*.js'
            ],
        dest: 'dist/js/scripts.js'
    },
    ```

11. O código ficou assim após a inserção do plugin **uglify**. Perceba que será gerado uma arquivo único, chamado de **scripts.js**.
    ``` js
    module.exports = function (grunt) {
        grunt.initConfig({
            jshint: {
                dist:{
                    src: ['js/**/*.js']
                }
            },
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
            },
            uglify: {
                scripts: {
                    src: ['dist/js/scripts.js'],
                    dest: 'dist/js/scripts.js'
                }
            }
            
        });

        grunt.loadNpmTasks('grunt-contrib-jshint');
        grunt.loadNpmTasks('grunt-contrib-concat');
        grunt.loadNpmTasks('grunt-contrib-uglify');

        grunt.registerTask('prod',['jshint', 'concat:scripts', 'uglify']);
    };
    ```
    
    A pasta de arquivos utilizada no **uglify** foi gerada pelo plugin **concat**.
    
12. Para executar o workflow digite:
    ``` js
    grunt prod
    ```

13. A partir de agora, será inserido o plugin **cssmin** no workflow, digitando o seguinte comando:
    ``` js
    npm install grunt-contrib-cssmin --save-dev
    ```

    Lembre-se de sempre digitar **--save-dev** para adicionar nas dependências do **package.json**.

14. Para carregar o plugin **cssmin** adicione a task:
    ``` js
    grunt.loadNpmTasks('grunt-contrib-cssmin');
    ```

15. Agora, será adicionado o **cssmin** no **gruntfile.js**. A task é composta de uma **origem** e **destino** da CSS que será manipulada:
    ``` js
    cssmin: {
        all: {
            src: ['bower_components/bootstrap/dist/css/bootstrap.min.css', 'css/**/*.css'],
            dest: 'dist/css/styles.min.css'
        }
    }
    ```

16. Agora, confira como ficou o arquivo **gruntfile.js** após a inserção do plugin **cssmin**.
    ``` js
    module.exports = function (grunt) {
        grunt.initConfig({
            jshint: {
                dist:{
                    src: ['js/**/*.js']
                }
            },
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
            },
            uglify: {
                scripts: {
                    src: ['dist/js/scripts.js'],
                    dest: 'dist/js/scripts.js'
                }
            }
            cssmin: {
                all: {
                    src: ['bower_components/bootstrap/dist/css/bootstrap.min.css', 'css/**/*.css'],
                    dest: 'dist/css/styles.min.css'
                }
            }
        });

        grunt.loadNpmTasks('grunt-contrib-jshint');
        grunt.loadNpmTasks('grunt-contrib-concat');
        grunt.loadNpmTasks('grunt-contrib-uglify');
        grunt.loadNpmTasks('grunt-contrib-cssmin');

        grunt.registerTask('prod',['jshint', 'concat:scripts', 'uglify', 'concat:libs', 'cssmin']);
    };
    ```
    
17. Seguindo os dois passos de sempre para habilitar o uso de algum plugin, digite o seguinte comando para instalar o **htmlmin** no workflow:
    ``` js
    npm install grunt-contrib-htmlmin --save-dev
    ```

18. Para carregar o plugin **htmlmin** adicione a task:
    ``` js
    grunt.loadNpmTasks('grunt-contrib-htmlmin');
    ```

19. Em seguida, é configurada a task **htmlmin**.
    ``` js
    htmlmin: {
        options: {
            removeComments: true,
            collapseWhitespace: true
        },
        views: {
            expand: true,
            cwd: 'view/',
            src: ['*.html'],
            dest: 'dist/view'
        }
    }
    ```
    - expand: habilita o uso de diretórios.
    - cwd: Aponta o diretório que será manipulado.
    - src: Aponta o arquivo que está na pasta indicada.
    - dest: Destino da pasta

20. Confira o arquivo **gruntfile.js** após a inserção do plugin **htmlmin**.
    ``` js
    module.exports = function (grunt) {
        grunt.initConfig({
            jshint: {
                dist:{
                    src: ['js/**/*.js']
                }
            },
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
            },
            uglify: {
                scripts: {
                    src: ['dist/js/scripts.js'],
                    dest: 'dist/js/scripts.js'
                }
            }
            cssmin: {
                all: {
                    src: ['bower_components/bootstrap/dist/css/bootstrap.min.css', 'css/**/*.css'],
                    dest: 'dist/css/styles.min.css'
                }
            }
            htmlmin: {
                options: {
                    removeComments: true,
                    collapseWhitespace: true
                },
                views: {
                    expand: true,
                    cwd: 'view/',
                    src: ['*.html'],
                    dest: 'dist/view'
                }
            }
        });

        grunt.loadNpmTasks('grunt-contrib-jshint');
        grunt.loadNpmTasks('grunt-contrib-concat');
        grunt.loadNpmTasks('grunt-contrib-uglify');
        grunt.loadNpmTasks('grunt-contrib-cssmin');
        grunt.loadNpmTasks('grunt-contrib-htmlmin');

        grunt.registerTask('prod',['jshint', 'concat:scripts', 'uglify', 'concat:libs', 'cssmin', 'htmlmin']);
    };
    ```
    
21. Para executar apenas a task criada com o plugin **htmlmin** digite:
    ``` js
    grunt htmlmin
    ```
    
    Para executar todo o **gruntfile.js** digite:
    ``` js
    grunt prod
    ```
    
22. Voltando ao plugin **concat**, será adicionado uma subtask para aproveitar os arquivos **.min** gerados, concatenando os arquivos minimos do projeto (libs) e os arquivos mínimos criados pelo usuário (scripts)
    ```js
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
        all: {
            src: ['dist/js/libs.min.js', 'dist/js/scripts.min.js'],
            dest: 'dist/js/all.min.js'
        }
    },
    ```
    
    Para registrar a subtask **all**, carregue-a no final do código.
    ```js
    grunt.registerTask('prod',['jshint', 'concat:scripts', 'uglify', 'concat:libs', 'concat:all' 'cssmin', 'htmlmin']);
    ```
    
    Para testar, digite:
    ```js
    grunt prod
    ```
23. Confira como ficou o código após carregar novamente o plugin **htmlmin** e configurar a subtask **all**
    ```js
    module.exports = function (grunt) {
        grunt.initConfig({
            jshint: {
                dist:{
                    src: ['js/**/*.js']
                }
            },
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
                all: {
                    src: ['dist/js/libs.min.js', 'dist/js/scripts.min.js'],
                    dest: 'dist/js/all.min.js'
                }
            },
            uglify: {
                scripts: {
                    src: ['dist/js/scripts.js'],
                    dest: 'dist/js/scripts.js'
                }
            }
            cssmin: {
                all: {
                    src: ['bower_components/bootstrap/dist/css/bootstrap.min.css', 'css/**/*.css'],
                    dest: 'dist/css/styles.min.css'
                }
            }
            htmlmin: {
                options: {
                    removeComments: true,
                    collapseWhitespace: true
                },
                views: {
                    expand: true,
                    cwd: 'view/',
                    src: ['*.html'],
                    dest: 'dist/view'
                }
            }
        });

        grunt.loadNpmTasks('grunt-contrib-jshint');
        grunt.loadNpmTasks('grunt-contrib-concat');
        grunt.loadNpmTasks('grunt-contrib-uglify');
        grunt.loadNpmTasks('grunt-contrib-cssmin');
        grunt.loadNpmTasks('grunt-contrib-htmlmin');

        grunt.registerTask('prod',['jshint', 'concat:scripts', 'uglify', 'concat:libs', 'concat:all' 'cssmin', 'htmlmin']);
    };
    ```

24. Agora, será incluido o plugin **clean**. Plugin utilizado para limpeza de arquivos, muito utilizado para remover arquivos não utilizados no projeto após fazer a **concatenação** e **minificação**.
    ``` js
    npm install grunt-contrib-clean --save-dev
    ```

    Para carregar o plugin **clean** adicione a task:
    ``` js
    grunt.loadNpmTasks('grunt-contrib-clean');
    ```
26. Para configurar o plugin **clean** adicione-o acima das tasks criadas previamente.
    ``` js
    clean: {
        temp: ['dist/js/libs.js', 'dist/js/libs.min.js', 'dist/js/scripts.js', 'dist/js/scripts.min.js'],
        all: ['dist/']
    }
    ```
    SEMPRE prestar muita atenção na utilização desse plugin, pois ele **apaga** arquivos e diretórios.

27. Para registrar a task criada pelo plugin **clean**. Adicione o mesmo no **começo**.
    ```js
    grunt.registerTask('prod',['clean:all','jshint', 'concat:scripts', 'uglify', 'concat:libs', 'concat:all' 'cssmin', 'htmlmin']);
    ```
    
    Para testar, digite:
    ```js
    grunt prod
    ```
    
    Arquivos serão apagados e gerados novamente após o teste. Terminando assim a configuração do plugin **clean**.

28. Agora, será inserido um último plugin. O plugin **copy**

    Para realizar a instalação digite:
    ``` js
    npm install grunt-contrib-copy --save-dev
    ```

    Para carregar o plugin **copy** adicione a task:
    ``` js
    grunt.loadNpmTasks('grunt-contrib-copy');
    ```

29. A configuração do plugin **copy** se realiza com origem (src) e destino (dest). Esse plugin é utilizado para copiar arquivos.
    ```js
    copy: {
        all: {
            src: 'index-prod.html',
            dest: 'dist/index.html'
        }
    }
    ```
    
    Para testar o plugin, digite:
    ```js
    grunt copy
    ```
    
    Para registrar a tarefa criada pelo plugin, digite:
    ```js
    grunt.registerTask('prod',['clean:all','jshint', 'concat:scripts', 'uglify', 'concat:libs', 'concat:all' 'cssmin', 'htmlmin', 'clean:temp']);
    ```
    
30. Todo o código ficou assim:
    ```js
    module.exports = function (grunt) {
        grunt.initConfig({
            clean: {
                temp: ['dist/js/libs.js', 'dist/js/libs.min.js', 'dist/js/scripts.js', 'dist/js/scripts.min.js'],
                all: ['dist/']
            },
            jshint: {
                dist:{
                    src: ['js/**/*.js']
                }
            },
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
                all: {
                    src: ['dist/js/libs.min.js', 'dist/js/scripts.min.js'],
                    dest: 'dist/js/all.min.js'
                }
            },
            uglify: {
                scripts: {
                    src: ['dist/js/scripts.js'],
                    dest: 'dist/js/scripts.js'
                }
            }
            cssmin: {
                all: {
                    src: ['bower_components/bootstrap/dist/css/bootstrap.min.css', 'css/**/*.css'],
                    dest: 'dist/css/styles.min.css'
                }
            }
            htmlmin: {
                options: {
                    removeComments: true,
                    collapseWhitespace: true
                },
                views: {
                    expand: true,
                    cwd: 'view/',
                    src: ['*.html'],
                    dest: 'dist/view'
                }
            },
            copy: {
                all: {
                    src: 'index-prod.html',
                    dest: 'dist/index.html'
                }
            }
        });

        grunt.loadNpmTasks('grunt-contrib-jshint');
        grunt.loadNpmTasks('grunt-contrib-concat');
        grunt.loadNpmTasks('grunt-contrib-uglify');
        grunt.loadNpmTasks('grunt-contrib-cssmin');
        grunt.loadNpmTasks('grunt-contrib-htmlmin');
        grunt.loadNpmTasks('grunt-contrib-copy');

        grunt.registerTask('prod',['clean:all','jshint', 'concat:scripts', 'uglify', 'concat:libs', 'concat:all' 'cssmin', 'htmlmin', 'copy', 'clean:temp']);
    };
    ```
    
    Para executar TODO o projeto, digite:
    ```js
    grunt prod
    ```
    
    Após inserir esse último plugin, o workflow básico está pronto. 
    
    CSS foi gerada, JavaScript concatenada e modificada, views também minificadas.