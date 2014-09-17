---
layout: post
title:  "Como derrotar a Terminalfobia?"
date:   2014-09-17 12:00:00
categories: terminal
tags: terminal bash
image: /assets/articles/como-derrotar-a-terminalfobia/background.jpg
---
Por muito tempo fugi das linhas de comando. Fazer o quê? Eu sou um cara visual. Prefiro softwares com interfaces que sejam, de preferência, agradáveis e fáceis de usar. Afinal, se meu trabalho é proporcionar essa experiência para os outros, porque eu não posso querer isso também no meu dia-a-dia?

Fora que linhas de comando me remetem aos tempos do DOS, computadores 386, e todo tipo de coisa ultrapassada. Mas por trás de todo esse preconceito bobo, a verdade é que linhas de comando são intimidantes. E essa fobia acabou me distanciando de novidades bacanas que surgiam  para nos ajudar nas tarefas do dia-a-dia.

Não que seja impossível de viver sem ela, veja bem. De tempos em tempos, uma boa alma sempre surgia trazendo GUIs como o [GitHub](https://mac.github.com/) (oficial ou não, para versionamento) ou o [Mixture](http://mixture.io/) (para automatização de tarefas e geração de sites estáticos). Ambas fizeram parte do meu workflow por um bom tempo. Porém, sua simplicidade excessiva e limitações sempre acabavam esbarrando no meu desenvolvimento. E ao invés de ganhar tempo, eu perdia.

Neste artigo, vamos mostrar que o Terminal pode ser um grande aliado, e dar um tapa no seu visual.

---

## Passo #1: Não use o Terminal

WTF?! Você não leu errado, é isso mesmo. Mas só digo isso porque existem alternativas melhores ao Terminal padrão da Apple. Ao abrir o Terminal, por exemplo, essa será sua primeira visão (à esquerda).

<div style="width: 50%; float: left;"><img src="/assets/images/terminalfobia-default.png" alt="Terminal Padrão"></div>
<div style="width: 50%; float: right;"><img src="/assets/images/terminalfobia-iterm.png" alt="iTerm"></div>

Assustador, não? Mas se você utilizar o [iTerm](http://iterm2.com/), a coisa já começa um pouquinho melhor (à direita). Fora isso, ele possui [diversos recursos e opções de personalização](http://iterm2.com/features.html) que irão nos ajudar a deixar essa janela aberta o dia todo, sem nos incomodar tanto. E o melhor de tudo: ele é grátis.

#### Personalizando

Instale [essa fonte](http://nodnod.net/2009/feb/12/adding-straight-single-and-double-quotes-inconsola/), que é uma versão modificada da [Inconsolata](http://levien.com/type/myfonts/inconsolata.html). Ela possui uma leitura excelente, seja qual for o tamanho da fonte.

Em breve acrescentarei mais opções de personalização. Fique ligado.

---

## Passo #2: Adote dotfiles bacanas de algum outro desenvolvedor

*Dotfiles* são arquivos de configuração que dão super poderes ao seu Mac e/ou Terminal. Alguns mexem em configurações padrão do Mac (que não podem ser acessadas através das Preferências de Sistema). Outros deixam seu Terminal parecido com seu editor preferido. Enfim, cada dotfile libera um poder diferente. Eles são chamados assim porque o nome dos arquivos começam com um “.”, e por ter esse ponto no nome, eles ficam escondidos no sistema.

Existem diversos *dotfiles* no [GitHub](http://dotfiles.github.io), alguns criados por desenvolvedores famosos (como o [Paul Irish](http://www.paulirish.com/) e o [Mathias Bynens](https://mathiasbynens.be/)), e outros por desenvolvedores como eu - <img src="https://abs.twimg.com/emoji/v1/72x72/1f605.png" width="24" style="margin-bottom: -5px;">. Nos próximos parágrafos vou ensinar como instalar meus *dotfiles* na sua máquina e explicar o que cada um faz. Mas de qualquer forma, recomendo que você dê uma checada nos demais.

#### Como instalar?

É muito simples. Vá até o Terminal e insira o comando abaixo:

{% highlight bash %}
$ curl --silent https://raw.githubusercontent.com/josantana/dotfiles/master/.dotfiles/install.sh | sh
{% endhighlight %}

Se você já instalou nossos dotfiles e desejar apenas atualizar dessa vez, use:

{% highlight bash %}
$ curl --silent https://raw.githubusercontent.com/josantana/dotfiles/master/.dotfiles/sync.sh | sh
{% endhighlight %}

É isso. Uma linha. Trabalho feito. Agora abra o iTerm e confira.

#### OWWW! O que aconteceu?!

Os *dotfiles* são divididos em dois grupos: aqueles que rodam toda vez que você inicia uma nova sessão no Terminal, dando poderes ao seu mais novo amigo (#1), e aqueles que rodam apenas uma vez, dando super poderes ao sistema (#2).

Vamos explicar o que foi feito acima. Essa linha de comando baixa e executa nosso script de instalação. Ele move seus arquivos atuais para a pasta `~/.dotbackup/` (caso algo dê errado, basta substituir os novos arquivos pelos antigos, ok?). Em seguida, ele copia todos o conteúdo do repositório para a raiz do seu Mac - o que irá instantâneamente dar um tapa no seu Terminal (#1). E pra finalizar, ele executa uma série de comandos para turbinar seu OS (#2). É como se tivéssemos ligado seu carro com uma chave mágica, que deixa o ronco do motor muito mais nervoso.

## Entendendo cada *dotfile*

#### .bash_profile / .bashrc

O Bash Profile é um arquivo roda quando você inicia o Terminal - carregando atalhos, funções e quaisquer outras personalizações criadas pelo usuário. Ele está localizado no diretório raiz do seu usuário. Ele é responsável por carregar os demais *dotfiles*. Essa modularização facilita na manutenção do repositório.

#### .hushlogin

A simples presença desse arquivo no seu diretório raiz remove aquelas informações sobre o último login feito no Terminal. Chega de bla-bla-bla.

#### .bash_prompt

Este arquivo serve para personalizar e alterar as cores do prompt de comando. Com as configurações do meu dotfile, você verá:

`[Usuário] @ [Computador] in [Pasta] on [Repositório]`

Obviamente, a parte referente a repositório só irá dar as caras se a pasta atual for um repositório. Este dotfile é uma cópia descarada do excelente prompt do [gf3](https://github.com/gf3/dotfiles), com algumas alterações. Você pode personalizar o nome de usuário e do computador usando as seguintes variáveis em `.custom`. Além disso o prompt exibe se a pasta possui (ou não) commits pendentes para dar um pull/push através de ícones de setas.

{% highlight bash %}
custom_username="josantana"
custom_machine="Mac OS X"
{% endhighlight %}

#### Atalhos

Acho que o nome já é bem auto-explicativo. Os atalhos irão te ajudar a economizar um tempo incrível, eliminando a necessidade de digitar longos comandos.

**Exemplo de Atalho: Pasta de Trabalho**

Apesar de intimidante, o Terminal não é um bicho de sete cabeças. Você pode inclusive, fazer coisas legais como essa abaixo.

<img src="/assets/images/terminalfobia-drop.gif" alt="Soltando uma pasta no Terminal">

Porém, existe um jeito ainda mais fácil de chegar à sua pasta de trabalho: você pode criar um atalho pra ela.

{% highlight bash %}
alias 2work="cd /path/to/work/space/"
{% endhighlight %}

Na próxima vez que você quiser chegar à pasta onde ficam seus aplicativos web, basta digitar `2work`. Um atalho simples, que deve salvar um bom tempo do seu dia a dia.

###### Z

Falando em atalhos, estes *dotfiles* (assim como a maioria) incluem o **Z**, do [Rupa](https://github.com/rupa). E vai por mim: Este é um dos melhores recursos disponíveis.

O Z remove a necessidade de navegar entre diferentes pastas. Ao invés de digitar `cd pasta/desejada/em/um/longo/diretorio`, você simplesmente insere `z diretorio`. Ou melhor ainda, que tal digitar apenas `z dir`? O Z irá usar qualquer pedaço do nome da pasta pra te levar até o resultado mais comum. É mais ou menos como o “Estou com Sorte” do Google, mas pra navegação no Terminal.

!["Estou com Sorte!"](/assets/images/terminalfobia-google.png)

Isso significa que você não terá que criar tantos atalhos para cada uma das suas pastas mais acessadas. <img src="https://abs.twimg.com/emoji/v1/72x72/1f609.png" width="24" style="margin-bottom: -5px;">

#### .functions

Atalhos são legais para substituir strings, mas se você precisar de algo mais complexo, com alguma lógica, parâmetros, etc; o que você procura uma função.

**Exemplo de Função: Abrir no browser**

Disparar o browser a partir da pasta onde você está trabalhando, com apenas teclas pode ser bem mais rápido do que abrir uma nova Janela, encontrar seu browser favorito em Aplicativos, navegar por menus para encontrar o arquivo HTML. Com a função abaixo, basta passar o nome do arquivo.

{% highlight bash %}
$ surf index.html
{% endhighlight %}

#### .custom

Se em algum momento você precisar acrescentar criar um novo atalho ou uma nova função, esse é o cara. Apesar de parecer correto, não altere nada em `.aliases` ou `.functions`. Porquê? Digamos que daqui há algumas semanas eu adiciono um recurso bacana ou corrijo um bug. Ao sincronizar, todos os arquivos são substituídos, com excessão do `.custom`. Por isso, acrescentar suas linhas nesse cara. O arquivo já vem com algumas variáveis para você personalizar (algumas até já foram citadas acima).

Algo que geralmente precisamos alterar é o PATH. Nosso arquivo já vem uma configuração bem esperta:

{% highlight bash %}
      PATH=/usr/local/bin
PATH=$PATH:/usr/local/sbin
PATH=$PATH:/usr/bin
PATH=$PATH:/bin
{% endhighlight %}

*Obs. Se você achar que suas linhas servem para todo mundo, lance a proposta de um Pull Request no repositório e contribua com a melhoria destes dotfiles.* ;)

#### .osx

Todos os *dotfiles* acima são aqueles que rodam sempre que uma nova sessão do Terminal é iniciada, como já expliquei. Este e o `.brew` (abaixo) são aqueles que rodam apenas uma vez. São tantas alterações (mais de 125) que o ideal é que você examine o arquivo para conferir todas. Estas estão entre as minhas favoritas:

- Desabilitar a Central de Notificações e remover seu ícone da barra de menu.
- Controlar a luminosidade do teclado automaticamente.
- Limitar buscas à pasta atual, por padrão (ao invés de buscar em todo o Mac).
- Impedir o Time Machine de tentar transformar cada HD externo conectado em um backup.
- Desabilitar a irritante pergunta "Deseja mesmo abrir esse programa que não veio da nossa loja?".
- Remover de vez aquele peso morto do Dashboard. Aliás, porque isso ainda existe, Apple?

#### .brew

O [Homebrew](http://brew.sh/) é um gerenciador de pacotes, que instala tudo em seu próprio diretório e depois cria links para estes arquivos na pasta local ("/usr/local”). Isso é ótimo porque as instalações do Brew (para os chagados) ficam num local reservado, evitando assim conflitos com as instalações do sistema. Além disso, o Brew toma conta das atualizações pra você. Você realmente não pode sobreviver sem isso. O ideal é que você tente usá-lo para toda e qualquer instalação de um novo recurso. Simplesmente porque com ele você não dor-de-cabeça.

Este script instala alguns pacotes básicos, que atualizam comandos nativos do Mac e acrescentam novas funcionalidades.

*Obs. Se você já tiver o Homebrew instalado, seria legal se você rodasse `brew doctor` após a execução do `.osx` e `.brew`.*

## Finalizando

A esta altura, você já deve estar olhando para seu Terminal com mais carinho. Ele se perfumou todo pra você. Agora é hora dos pombinhos darem as mãos e deixarem todo ressentimento de lado.

Com apenas uma linha de comando, você consegue pegar uma máquina zerada e deixá-la toda tunada.

No próximo post, você irá aprender comandos básicos pra conseguir se virar no Terminal como um Pro. Lembre-se de deixar um comentário e até a próxima!
