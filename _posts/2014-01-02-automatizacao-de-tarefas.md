---
layout: post
title: Automatização de Tarefas
---

Por muito tempo, fugi das linhas de comando. Fazer o quê? Eu sou um cara visual. Prefiro lidar com interfaces - que de preferência, sejam agradáveis e fáceis de usar. Afinal, se meu trabalho é proporcionar essa experiência para os outros, porque eu não posso querer também no meu dia-a-dia, não?

Já faz um tempo que vinha ouvindo falar de automação de tarefas, mas como todos usam linhas de comando, fugia como o diabo da cruz. Apesar disso, acabei encontrando soluções interessantes como o [Mixture](http://mixture.io/) por exemplo. E apesar de tê-lo abandonado, ainda recomendo uma checada. Ele possui todas as características possíveis para seduzir um cara como eu. Porém, um dia a amor acabou. Mas não quero ser injusto, o Mixture é excelente quando você está, por exemplo, está trabalhando num site estático. Mas quando você o usa apenas para concatenar e comprimir arquivos (Simple Mode), ele começa a apresentar bugs de sincronismo. Fora que as atualizações de recursos de terceiros, como Sass, nem sempre estão em dia. Como vinha usando o Mixture muito mais pra isso do que para trabalhar com sites estáticos, precisei tomar uma decisão.

Em resumo, foi isso que me motivou a encarar de uma vez por toda esse mundo “assustador" das linhas de comando.

Você provavelmente já deve ter ouvido falar do [Grunt](http://gruntjs.com/). Ele existe pra que você não tenha que repetir tarefas chatas do cotidiano, como comprimir e concatenar arquivos, gerar arquivos CSS a partir de pré-processadores, e até comprimir imagens ou gerar CSS Sprites. Neste tutorial não vamos usar ele, mas seu irmão mais novo, o [Gulp](http://gulpjs.com/). Simplesmente porque ele promete realizar estas mesmas tarefas de forma mais rápida e simples do que seu concorrente.

-----

## Certo, o que vamos fazer?

Montar um ambiente de trabalho com a última versão do Sass, e instalar o Gulp com todas as dependências mais úteis.O objetivo final: recriar tudo o que tinha no Mixture, com mais opções e automatizações, sem gastar U$40 pra isso. Ou melhor, sem gastar nada.

-----

### Instalação

*Sass*

Here's the quickest way we've found to start using Sass by using the command line. Apesar de existir um port em Node, vamos usar o original. Sass foi escrito em Ruby. Ruby uses Gems to manage its various packages of code like Sass. In your open terminal window type:

`gem install sass`

This will install Sass and any dependencies for you. It's pretty magical. If you get an error message then it's likely you will need to use the sudo command to install the Sass gem. It would look like:

`sudo gem install sass`

You should now have Sass installed, but it never hurts to double-check. In your terminal application you can type:

`sass -v`

It should return `Sass 3.4.3 (Selective Steve)`. Congratulations! You've successfully installed Sass.

*Gulp*

Use o comando abaixo para instalar o CLI do Gulp globalmente. Assim poderemos chamá-lo de qualquer local.

`npm install -g gulp`

Caso você esteja em um sistema baseado em Unix, talvez seja preciso rodar `sudo` antes do comando acima. Agora você vai poder rodar o Gulp na sua linha de comando. Para ver a versão instalada, execute:

`gulp -v`

Se o comando acima retornar a versão do Gulp instalada, a instalação foi um sucesso.

{% highlight bash %}
npm install gulp-ruby-sass --save-dev
npm install gulp-jshint --save-dev
npm install gulp-uglify --save-dev
npm install gulp-concat --save-dev
npm install gulp-livereload --save-dev
{% endhighlight %}

Unless previously installed you'll need Cairo to install canvas, which is a dependency to css-sprite. You can quickly install Cairo and its dependencies for OS X using the one liner below:

`wget https://raw.githubusercontent.com/LearnBoost/node-canvas/master/install -O - | sh`
`npm install canvas`
`npm install css-sprite --save`

### Passo-a-Passo

Este é o nosso arquivo inicial:

{% highlight js %}
var gulp = require('gulp');
gulp.task('default', function ()
{
    gulp.run();
});
{% endhighlight %}

O que estamos fazendo aqui? Invocando o Gulp no início e dando uma tarefa pra ele chamada ‘default’. Grunt actually doesn’t do anything all by itself. Remember Grunt is a task runner. The tasks themselves we will need to add. We actually haven’t set up Grunt to do anything yet, so let’s do that.

**Que tal concatenar alguns arquivos?**

In production, we would concatenate all those files together for performance reasons (one request is better than three). We need to tell Grunt to do this for us.

Chame a seguinte linha abaixo do Gulp.

{% highlight js %}
var concat = require('gulp-concat');
{% endhighlight %}

Em seguida vamos criar uma variável chamada scripts e vamos passar alguns arquivos pra ela:

{% highlight js %}
var scripts = [ 'assets/script/timer.js', 'assets/script/component.js' ];
{% endhighlight %}

Agora vamos criar uma tarefa chamada ‘dist’, que irá cuidar da distribuição dos arquivos.

{% highlight js %}
gulp.task('dist', function()
{
    gulp.src(scripts)
    .pipe(concat('teste.js'))
    .pipe(gulp.dest('assets/script/dist'));
});
{% endhighlight %}

O que estamos fazendo? Passando uma fonte de arquivos para o Gulp (src), em seguida, pilhamos algumas tarefas. Passamos um comando para concatenar para “teste.js” e em seguida, definimos um destino para esse arquivo (gulp.dest).

Agora é só inserir essa tarefa ao gulp.run e rodar o comando gulp na linha de comando.

{% highlight js %}
gulp.run('dist');
{% endhighlight %}

**Um único request é bom, mas se for minificado é ainda melhor**

Agora vamos minificar o arquivo.

{% highlight js %}
var uglify = require('gulp-uglify');
{% endhighlight %}

Acrescentar essa tarefa em nosso dist, logo abaixo de concat.

{% highlight js %}
.pipe(uglify())
{% endhighlight %}

E rodar de novo.

**Poderíamos testar o código toda vez que salvarmos, não?**

Para isso usamos o jsLint.

{% highlight js %}
gulp.task('lint', function()
{
    gulp.src(files)
    .pipe(jshint())
    .pipe(jshint.reporter('default'));
});
{% endhighlight %}

Agora é só inserir essa tarefa ao `gulp.run` e rodar o comando `gulp` na linha de comando.

{% highlight js %}
gulp.run('link', 'dist');
{% endhighlight %}

**E se fosse tudo automático?**

Essa é só para os preguiçosos nível master. É muito fácil. Já vem de fábrica.

{% highlight js %}
gulp.watch(files, function (event)
{
    gulp.run('lint', 'dist');
});
{% endhighlight %}

Basta abraçar o gulp.run com o watch. Ele irá observar os arquivos e disparar as tarefas listadas toda vez que

**Atualizações a cada alteração**

Precisa usar o plugin do extensão do Chrome.

{% highlight js %}
var livereload = require('gulp-livereload');
{% endhighlight %}

Faça a requisição e depois inclua os arquivos no watch.

{% highlight js %}
livereload.listen();

gulp.watch(files, function (event)
{
    gulp.run('lint', 'dist');

}).on('change', livereload.changed);
{% endhighlight %}

**Seria incrível se tivesse isso pra imagens, não?**

Boa notícia: TEM!
