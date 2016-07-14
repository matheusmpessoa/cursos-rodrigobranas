## Gulp
![Gulp](https://gfulton-images.s3.amazonaws.com/2015/Dec/gulp_logo-1450648879924.jpg "Gulp")

### Sites
- __[Gulp](http://gulpjs.com/)__
- __[Github Grunt](https://github.com/gulpjs/gulp)__
- __[npm](https://www.npmjs.com/)__

### Processo de instalação
Necessário ter o Node.js instalado.

Para executar o comando de instalação do Gulp, digite no npm a instalação do **Gulp-client-line** e **--save-dev** para adicionar nas dependências do arquivo **package.json**:
``` js 
npm install -g gulp-cli
npm install gulp --save-dev
```

Para exibir a versão do Gulp instalada, digita-se:
``` js
gulp --version
```

### Arquivo de configuração
O arquivo de configuração é chamado de: **gulpfile.js**

O **init config**, aonde se encontra a configuração de cada plugin.

### Arquivo mínimo gulp

Arquivo mínimo de configuração - visualizando o arquivo **gulpfile.js**:
``` js
var gulp = require('gulp');

gulp.task('default', function (){

});
```
Para executar um arquivo gulp, digita-se:
```
gulp
```
Digitando apenas **gulp** se entende que é para realizar a leitura do arquivo **default**

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

### Plugins Gulp
- __[gulp-jshint](https://www.npmjs.com/package/gulp-jshint/)__
- __[gulp-uglify](https://www.npmjs.com/package/gulp-uglify)__
- __[gulp-clean](https://www.npmjs.com/package/gulp-clean)__

### Utilização de plugins
Para se utilizar qualquer plugin, sempre se deve seguir **DOIS** passos: Instalar o plugin (**1**) e chamar a variável para declarar o plugin (**2**).

#### Passo a passo prático de como criar um **gulpfile.js**
1. Digite o comando **npm** para instalar o plugin.
    ``` js
    npm install jshint gulp-jshint --save-dev
    ```

2. Adicione a importação do plugin **jshint** no **gulpfile.js**. A importação é feita declarando uma variável com o nome do plugin e chamando-o em seguida.
    ``` js
    var jshint = require('gulp-jshint');
    ```
    
    A task é criada chamando uma **função**. Com o **gulp.src** é possível especificar aonde se encontra os arquivos que serão lidos. O **gulp.src** é um readable string.
    ``` js
    gulp.task('jshint', function () {
        return gulp.src('js/**/*.js')
        .pipe(jshint())
        .pipe(jshint.reporter('default'));
    });
    ```
    Ao adicionar **return** na task a mesma se torna assíncrona. Se não for retornar nada ela é sincrona. Pode se retornar uma string, promise callback.
    
    É possível adicionar dependências a cada task. Nesse caso a task default seria executada antes do jshint.
    ``` js
    gulp.task('jshint', ['default'], function () {
    
    });
    ```
    
    O código está assim até o momento:
    ``` js
    var gulp = require('gulp');
    var jshint = require('gulp-jshint');
    
    gulp.task('jshint', function () {
        return gulp.src('js/**/*.js')
        .pipe(jshint())
        .pipe(jshint.reporter('default'));
    });
    
    gulp.task('default', ['jshint']);
    ```

3. Para executar **gulpfile.js** pode se digitar:
    ```js
    gulp
    ```
    Ou
    ```js
    gulp default
    ```
    
    Para executar apenas a task **jshint**, digita-se:
    ```js
    gulp jshint
    ```

4.  Agora, será inserido o plugin **uglify**, que para ser instalado digita-se:
    ``` js
    npm install --save-dev gulp-uglify
    ```
    O plugin **uglify** é utilizado para  minificação de arquivos

5. Para dar inicio no código do plugin, chame o plugin com uma variavel.
    ``` js
    var uglify = require('gulp-uglify');
    ```

6. A task do plugin **uglify** será criada agora:
    ```js
    gulp.task('uglify', function () {
        return gulp.src('js/**/*.js')
        .pipe(gulp.dest('dist/js'));
    });
    ```
    Perceba que o **gulp.src** define a origem do código a ser manipulado. O **gulp.dest** define o destino.
    
    Adicione o registro do plugin **uglify** na task.
    ```js
    gulp.task('default', ['jshint', 'uglify']);
    ```
    
    O código está assim até o momento:
    ```js
    var gulp = require('gulp');
    var jshint = require('gulp-jshint');
    var uglify = require('gulp-uglify');
    
    gulp.task('jshint', function () {
        return gulp.src('js/**/*.js')
        .pipe(jshint())
        .pipe(jshint.reporter('default'));
    });
    
    gulp.task('uglify', function () {
        return gulp.src('js/**/*.js')
        .pipe(gulp.dest('dist/js'));
    });
    
    gulp.task('default', ['jshint', 'uglify']);
    ```

    Para executar o **gulpfile.js** digite:
    ```js
    gulp
    ```

7. Neste momento será inserido o plugin **clean**. Utilizado para limpeza de arquivos. Utilize sempre esse plugin com **ATENÇÃO** pois o mesmo deleta arquivos.

    Para realizar a instalação deste plugin, digite:
    ```js
    npm install --save-dev gulp-clean
    ```
    
    Chame a variável:
    ```js
    var clean = require('gulp-clean');
    ```
    
    Crie a task do plugin **clean**.
    ```js
    gulp.task('clean', function () {
        return gulp.src('dist/')
        .pipe(gulp.dest(clean());
    });
    ```

8. Adicione uma dependência na task **uglify**, para que execute a task **clean** antes da task **uglify**.
    ```js
    gulp.task('uglify', ['clean'],function () {
        return gulp.src('js/**/*.js')
        .pipe(gulp.dest('dist/js'));
    });
    ```
    
    Ao adicionar essa dependência a necessidade de chamar a task do plugin **uglify** se torna desnecessária.
    
    O código completo está assim no momento:
    ```js
    var gulp = require('gulp');
    var jshint = require('gulp-jshint');
    var uglify = require('gulp-uglify');
    var clean = require('gulp-clean');
    
    gulp.task('clean', function () {
        return gulp.src('dist/')
        .pipe(gulp.dest(clean());
    });
    
    gulp.task('jshint', function () {
        return gulp.src('js/**/*.js')
        .pipe(jshint())
        .pipe(jshint.reporter('default'));
    });
    
    gulp.task('uglify', ['clean'],function () {
        return gulp.src('js/**/*.js')
        .pipe(gulp.dest('dist/js'));
    });
    
    gulp.task('default', ['jshint', 'uglify']);
    ```