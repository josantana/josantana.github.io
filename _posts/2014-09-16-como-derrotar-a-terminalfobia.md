---
layout: post
title: Como derrotar a Terminalfobia?
---

Por muito tempo fugi das linhas de comando. Fazer o quê? Eu sou um cara visual. Prefiro softwares com interfaces que sejam, de preferência, agradáveis e fáceis de usar. Afinal, se meu trabalho é proporcionar essa experiência para os outros, porque eu não posso querer isso também no meu dia-a-dia?

Fora que linhas de comando me remetem aos tempos do DOS, computadores 386, e todo tipo de coisa ultrapassada. Mas por trás de todo esse preconceito bobo, a verdade é que linhas de comando são intimidantes. E essa fobia acabou me distanciando de novidades bacanas que surgiam  para nos ajudar nas tarefas do dia-a-dia.

Não que seja impossível de viver sem ela. De tempos em tempos sempre surgia uma boa alma trazendo GUIs como o [GitHub](https://mac.github.com/) (oficial ou não, para versionamento) ou o [Mixture](http://mixture.io/) (para automatização de tarefas e geração de sites estáticos), fizeram parte do meu workflow por um bom tempo. Porém, sua simplicidade excessiva e limitações sempre acabavam esbarrando no meu desenvolvimento. E ao invés de ganhar tempo, eu perdia.

## Passo #1: Não use o Terminal

WTF?! Você não leu errado, é isso mesmo. Mas só digo isso porque existem alternativas melhores ao Terminal padrão da Apple. Ao abrir o Terminal, por exemplo, essa será sua primeira visão (à esquerda).

!["Terminal Padrão"](/assets/images/terminalfobia-default.png) !["iTerm"](/assets/images/terminalfobia-iterm.png)

Assustador, não? Mas se você utilizar o iTerm, a coisa já começa um pouquinho melhor (à direita). Fora isso, ele possui diversos recursos e opções de personalização que irão nos ajudar a deixar essa janela aberta o dia todo, sem nos incomodar tanto. E o melhor de tudo: ele é grátis.

## Personalizando

Instale [essa fonte](https://github.com/Lokaltog/powerline-fonts/blob/master/InconsolataDz/Inconsolata-dz%20for%20Powerline.otf), uma [versão modificada](https://github.com/Lokaltog/powerline-fonts/tree/master/InconsolataDz) em cima da [versão modificada](http://nodnod.net/2009/feb/12/adding-straight-single-and-double-quotes-inconsola/) da [Inconsolata](http://levien.com/type/myfonts/inconsolata.html).

## Passo #2: Adote dotfiles bacanas de algum outro desenvolvedor

*Dotfiles* são arquivos de configuração que dão super poderes ao seu Mac e/ou Terminal. Alguns mexem em configurações padrão do Mac (que não podem ser acessadas através das Preferências de Sistema). Outros deixam seu Terminal parecido com seu editor preferido. Enfim, cada dotfile libera um poder diferente. Eles são chamados assim porque o nome dos arquivos começam com um “.”, e por ter esse ponto no nome é que eles ficam escondidos no sistema.

Existem diversos *dotfiles* no [GitHub](http://dotfiles.github.io), alguns criados por desenvolvedores famosos (como [Paul Irish](http://www.paulirish.com/), [Mathias Bynens](https://mathiasbynens.be/), etc), e outros por desenvolvedores como eu (:P). Aqui vou ensinar como instalar facilmente meus *dotfiles* na sua máquina e explicar o que cada um faz. Mas recomendo que você dê uma checada nos demais. Tem pra todo gosto.

Os meus *dotfiles* são um “catado” dos *dotfiles* de outros desenvolveres. Juntei tudo o que fazia sentido pra mim, e acrescentei algumas peças próprias.

### Como instalar?

Vá até o Terminal e digite os comandos abaixo:

{% highlight bash %}
mv ~/.bash_profile ~/.dotbackup/.bash_profile && mv ~/.bashrc ~/.dotbackup/.bashrc_backup
cd; curl --silent -#L https://github.com/josantana/dotfiles/tarball/master | tar -xzv --strip-components 1 --exclude={LICENSE,README.md}
~/.dotfiles/install.sh
{% endhighlight %}

Abra o iTerm e confira.

### OWWW! O que aconteceu?!

Os *dotfiles* são divididos em dois grupos: Aqueles que rodam apenas uma vez, dando super poderes ao sistema; e aqueles que rodam toda vez que você inicia uma nova sessão no Terminal, dando poderes a esse nosso novo amigo.

Vamos explicar o que foi feito acima. A primeira linha irá mover seus arquivos atuais para a pasta `~/.dotbackup/`. Caso algo dê errado, basta substituir os novos arquivos pelos antigos. Na segunda linha, copiamos todos os meus dotfiles para a raiz do seu Mac. Nesse momento, seu Terminal já irá receber uma bela melhoria. E na terceira e última linha, usamos um instalador para executamos uma série de comandos. É como se tivéssemos ligado a chave do seu carro. Só que o ronco do motor agora é muito mais nervoso.

## Show! Mas agora, vamos voltar e cada *dotfile*.

#### .bash_profile / .bashrc

O Bash Profile é um arquivo roda quando você inicia o Terminal - carregando atalhos, funções e quaisquer outras personalizações criadas pelo usuário. Ele está localizado no diretório raiz do seu usuário. Ele é responsável por carregar os demais *dotfiles*. Fizemos dessa forma pra manter tudo organizado.

#### .bash_prompt

Este arquivo serve para personalizar e alterar as cores do prompt de comando. Com as configurações do meu dotfile, você verá:

`[Usuário] @ [Computador] in [Pasta] on [Repositório]`

Obviamente, a parte referente a repositório só irá dar as caras se a pasta atual for um repositório. Este dotfile é uma cópia descarada do excelente prompt do [gf3](https://github.com/gf3/dotfiles), com (poucas) alterações. Você pode personalizar o nome de usuário e do computador usando as seguintes variáveis em `.custom`.

{% highlight bash %}
custom_username="josantana"
custom_machine="Mac OS X"
{% endhighlight %}

