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

### Utilização de plugins
Para se utilizar qualquer plugin, sempre se deve seguir **DOIS** passos: Instalar o plugin (**1**) e chamar a variável para declarar o plugin (**2**).

#### Passo a passo prático de como criar um **gulpfile.js**
1. Digite o comando **npm** para instalar o plugin.
    ``` js
    npm install jshint gulp-jshint --save-dev
    ```