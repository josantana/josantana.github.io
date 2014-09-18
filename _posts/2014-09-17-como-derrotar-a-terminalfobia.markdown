---
layout: post
title:  "Como derrotar a Terminalfobia?"
date:   2014-09-17 12:00:00
categories: terminal
tags: terminal bash
image: /assets/articles/como-derrotar-a-terminalfobia/background.jpg
---

<img src="/assets/articles/como-derrotar-a-terminalfobia/background.jpg" width="1" height="1" style="float: right;">

Por muito tempo fugi das linhas de comando. Fazer o quê? Eu sou um cara visual. Prefiro softwares com interfaces que sejam, de preferência, agradáveis e fáceis de usar. Afinal, se meu trabalho é proporcionar essa experiência para os outros, porque eu não posso querer isso também no meu dia-a-dia?

Fora que linhas de comando me remetem aos tempos de DOS, computadores 386, e todo tipo de coisa ultrapassada. Mas por trás de todo esse preconceito bobo, a verdade é que linhas de comando são intimidantes. E essa fobia acabou me distanciando de novidades bacanas que surgiam  para nos ajudar nas tarefas do dia-a-dia.

Não que seja impossível de viver sem ela, veja bem. De tempos em tempos, uma boa alma sempre surgia trazendo *[GUIs](http://en.wikipedia.org/wiki/Graphical_user_interface)* como o [GitHub Oficial](https://mac.github.com/) (para versionamento de arquivos) ou o [Mixture](http://mixture.io/) (para automatização de tarefas e geração de sites estáticos). Ambas ferramentas fizeram parte do meu workflow por um bom tempo. Porém, sua simplicidade excessiva e limitações acabavam esbarrando no meu desenvolvimento. E ao invés de ganhar tempo com elas, eu perdia.

Resumindo: quero te ajudar a derrotar sua "*Terminalfobia*". <img src="https://abs.twimg.com/emoji/v1/72x72/1f608.png" width="24" style="margin-bottom: -5px;">

---

## Passo #1: Não use o Terminal

WTF?! Você não leu errado, é isso mesmo. Mas só porque existem alternativas melhores do que o Terminal padrão da Apple. Ao abrir o Terminal, por exemplo, essa será sua primeira visão (à esquerda).

<div style="width: 50%; float: left;"><img src="/assets/images/terminalfobia-default.png" alt="Terminal Padrão"></div>
<div style="width: 50%; float: right;"><img src="/assets/images/terminalfobia-iterm.png" alt="iTerm"></div>

Assustador, não? Mas se você utilizar o [iTerm](http://iterm2.com/), a coisa já começa um pouquinho melhor (à direita). O fato é que ele possui uma série de [recursos e opções de personalização](http://iterm2.com/features.html) que irão nos ajudar a deixar essa janela aberta o dia todo, sem nos incomodar tanto. E o melhor de tudo: é grátis.

#### Tapa no visual
<br/>
Primeiro, vamos alterar a fonte padrão. Vamos usar [essa fonte](http://nodnod.net/2009/feb/12/adding-straight-single-and-double-quotes-inconsola/), que é uma versão modificada da [Inconsolata](http://levien.com/type/myfonts/inconsolata.html) - que é agradável e possui uma leitura excelente, independente do tamanho.

Em seguida, abra as preferências do iTerm e em General, marque o checkbox abaixo e selecione uma pasta onde o programa deve salvar suas preferências.

<img src="/assets/articles/como-derrotar-a-terminalfobia/iterm-setup.png" alt="Alterando as configurações do iTerm">

Em seguida, baixe [estas configurações](https://www.dropbox.com/s/ewngtbznbf9cqbm/com.googlecode.iterm2.plist?dl=0) e substitua pelas suas.

Agora seu iTerm deve estar um pouco mais *classudo*:

- Eliminamos alguns Prompts chatos ao fechar a sessão.
- Adicionamos animações de transição quando inativo/ativo.
- Mudamos o cursor para uma linha vertical (como editores de texto).
- Já selecionamos a fonte Inconsolata-dz, que você instalou há poucos minutos.
- Adicionamos uma leve transparência na janela e além de um elegante efeito de blur no que estiver por trás do iTerm.

Mas isso é só o começo. Continue comigo.

---

## Passo #2: Adote dotfiles bacanas de algum outro desenvolvedor
<br/>
*Dotfiles* são arquivos de configuração que dão super poderes ao seu Mac e/ou Terminal. Alguns mexem em configurações avançadas do Mac (aquelas que não estão acessíveis através das Preferências de Sistema), outros deixam o Terminal parecido com seu editor preferido. Enfim, cada *dotfile* libera um poder diferente. Eles são chamados assim porque o nome dos arquivos começam com um ponto. E por ter esse ponto no nome, eles ficam escondidos no sistema.

Existem diversos *dotfiles* no [GitHub](http://dotfiles.github.io), alguns criados por desenvolvedores famosos (como o [Paul Irish](http://www.paulirish.com/) e o [Mathias Bynens](https://mathiasbynens.be/)), e outros por caras como eu - <img src="https://abs.twimg.com/emoji/v1/72x72/1f605.png" width="24" style="margin-bottom: -5px;">. Nos próximos parágrafos vou ensinar como instalar [meus *dotfiles*](https://github.com/josantana/dotfiles) na sua máquina e mais: *Explicar o que cada um faz*.

#### Como instalar?

É muito simples. Vá até o Terminal e insira esse único comando abaixo:

{% highlight bash %}
$ curl --silent https://raw.githubusercontent.com/josantana/dotfiles/master/.dotfiles/install.sh | sh
{% endhighlight %}

Se você já instalou nossos dotfiles e desejar apenas atualizar dessa vez, use:

{% highlight bash %}
$ curl --silent https://raw.githubusercontent.com/josantana/dotfiles/master/.dotfiles/sync.sh | sh
{% endhighlight %}

É isso. Uma linha. Trabalho feito. Agora abra o iTerm e confira.

#### OWWW! O que aconteceu?!

Vamos lá: Essa linha de comando serve unicamente para baixar e executar nosso script de instalação. Ele move seus arquivos atuais para uma nova pasta chamada *.dotbackup* na raiz do seu usuário. Caso algo dê errado, basta substituir os novos arquivos pelos antigos, ok? Em seguida, ele copia todos o conteúdo do [repositório](https://github.com/josantana/dotfiles) para a raiz do seu usuário - o que irá instantâneamente dar um tapa no seu Terminal (#1). E pra finalizar, ele executa uma série de comandos para turbinar seu OS (#2). É como se tivéssemos ligado seu carro com uma chave mágica, que deixa o ronco do motor muito mais nervoso.

Os *dotfiles* são divididos em dois grupos: aqueles que rodam toda vez que você inicia uma nova sessão no Terminal, dando poderes ao seu mais novo amigo (#1), e aqueles que rodam apenas uma vez, dando super poderes ao sistema (#2).

---

## Entendendo cada *dotfile*
<br/>
#### .bash_profile / .bashrc

O Bash Profile é um arquivo roda quando você inicia o Terminal - carregando atalhos, funções e quaisquer outras personalizações criadas pelo usuário. Ele está localizado no diretório raiz do seu usuário. Meu Bash Profile é responsável por carregar todos os demais *dotfiles*. Utilizei essa modularização pra facilitar na manutenção do repositório.

#### .hushlogin

A simples presença desse arquivo no seu diretório raiz remove aquelas informações sobre o último login feito no Terminal.

#### .bash_prompt

Este arquivo serve para personalizar a aparência do prompt de comando. Com as configurações do meu dotfile, você verá:

`[Usuário] @ [Computador] in [Pasta] on [Repositório]`

Cada elemento dessa linha é apresentada com uma cor diferente, para ser visualmente mais fácil de distinguir. Obviamente, a parte referente a repositório só irá dar as caras se a pasta atual for um repositório Git. Este *dotfile* é uma cópia descarada do excelente prompt do [gf3](https://github.com/gf3/dotfiles), com leves alterações. Aqui, por exemplo, você pode personalizar o nome de usuário e do computador usando as variáveis abaixo que estão no arquivo *.custom* (que veremos em breve). Além disso o prompt exibe se a pasta possui (ou não) commits pendentes para dar um pull/push através de ícones de setas.

{% highlight bash %}
custom_username="josantana"
custom_machine="Mac OS X"
{% endhighlight %}

#### .aliases

Acho que o nome já é bem auto-explicativo. Os atalhos irão te ajudar a economizar um tempo incrível, eliminando a necessidade de digitar longos comandos.

**Exemplo de Atalho: Pasta de Trabalho**

Apesar de intimidante, o Terminal não é um bicho de sete cabeças. Você pode inclusive, fazer coisas legais como essa abaixo.

<img src="/assets/images/terminalfobia-drop.gif" alt="Tente arraste e solte uma pasta sobre o Terminal. Legal, não?">

Porém, existe um jeito ainda mais fácil de chegar à sua pasta de trabalho: você pode criar um atalho pra ela.

{% highlight bash %}
alias 2work="cd /caminho/para/minha/pasta/de/trabalho/"
{% endhighlight %}

Na próxima vez que você quiser chegar à pasta onde ficam seus aplicativos web, basta digitar `2work`. Um atalho simples, que deve salvar um bom tempo do seu dia a dia.

###### Z

Falando em atalhos, estes *dotfiles* (assim como a maioria) incluem o **Z**, do [Rupa](https://github.com/rupa). E vai por mim: Este é um dos melhores recursos disponíveis.

O Z remove a necessidade de navegar entre diferentes pastas para chegar onde você deseja. Ao invés de digitar `cd pasta/desejada/em/um/longo/diretorio`, você simplesmente insere `z diretorio`. Ou melhor ainda, que tal digitar apenas `z dir`? O Z irá usar qualquer pedaço do nome da pasta pra te levar até o resultado mais comum. É mais ou menos como o “Estou com Sorte” do Google, mas pra navegação no Terminal.

!["Estou com Sorte!"](/assets/images/terminalfobia-google.png)

Isso significa que você não terá que criar tantos atalhos para cada uma das suas pastas mais acessadas. <img src="https://abs.twimg.com/emoji/v1/72x72/1f609.png" width="24" style="margin-bottom: -5px;">

#### .functions

Atalhos são legais para substituir strings, mas se você precisar de algo mais complexo, com alguma lógica, parâmetros, etc; o que você procura é uma função.

**Exemplo de Função: Abrir no browser**

Disparar o browser a partir da pasta onde você está trabalhando, com apenas teclas pode ser bem mais rápido do que abrir uma nova Janela, encontrar seu browser favorito em Aplicativos, navegar por menus para encontrar o arquivo HTML, etc, etc... Você pode criar uma função para, por exemplo, abrir seu browser favorito com o arquivo no qual está trabalhando. Algo como:

{% highlight bash %}
$ surf2 index.html
{% endhighlight %}

#### .custom

Se em algum momento você precisar acrescentar criar um novo atalho ou função, esse é o cara. Apesar de parecer correto, não altere nada em *.aliases* ou *.functions*. Porquê? Digamos que daqui há algumas semanas eu adiciono um recurso bacana ou corrijo um bug. Lógico que você também vai querer, certo? Ao sincronizar, todos os arquivos são substituídos, com excessão do *.custom*. Por isso, acrescentar suas linhas nesse cara. Esse arquivo já vem com algumas variáveis para você personalizar (algumas até já foram citadas acima).

Algo que vez ou outra precisamos alterar é o PATH. O arquivo *.custom* padrão, por exemplo, já vem uma configuração bem esperta:

{% highlight bash %}
      PATH=/usr/local/bin
PATH=$PATH:/usr/local/sbin
PATH=$PATH:/usr/bin
PATH=$PATH:/bin
{% endhighlight %}

*Obs. Se você achar que suas linhas personalizadas salvariam a vida de outros desenvolvedores, lance a proposta de um Pull Request (no arquivo aliases, functions ou exports) no [repositório](https://github.com/josantana/dotfiles) e contribua com a melhoria destes dotfiles.* <img src="https://abs.twimg.com/emoji/v1/72x72/1f609.png" width="24" style="margin-bottom: -5px;">

#### .osx

Todos os *dotfiles* acima são aqueles que rodam sempre que uma nova sessão do Terminal é iniciada, como já expliquei. Já este e o *.brew* (abaixo) são aqueles que rodam apenas uma vez. São tantas alterações (mais de 125) que o ideal é que você examine o arquivo para conferir todas. Estas estão entre as minhas favoritas:

- Desabilitar a Central de Notificações e remover seu ícone da barra de menu.
- Controlar a luminosidade do teclado automaticamente.
- Limitar buscas à pasta atual, por padrão (ao invés de buscar em todo o Mac).
- Impedir o Time Machine de tentar transformar cada HD externo conectado em um backup.
- Desabilitar a irritante pergunta "Deseja mesmo abrir esse programa que não veio da nossa loja?".
- Remover de vez aquele peso morto do Dashboard. Aliás, porque isso ainda existe, Apple?

#### .brew

O [Homebrew](http://brew.sh/) é um gerenciador de pacotes, que instala tudo em seu próprio diretório e depois cria links para estes arquivos na pasta padrão ("/usr/local”). Isso é ótimo porque as instalações do "Brew" (para os mais chegados) ficam num local reservado, evitando assim conflitos com as demais instalações do sistema. Além disso, o Brew toma conta das atualizações pra você. Você realmente não pode sobreviver sem ele. O ideal é que você tente usá-lo em toda e qualquer instalação de um novo recurso, simplesmente porque com ele você não tem dor-de-cabeça.

O *.brew* é um ponto de partida. Ele instala pacotes básicos, que atualizam comandos nativos do Mac e acrescentam novas funcionalidades.

*Obs. Caso você já tenha o Homebrew instalado, recomendo rodar o comando `brew doctor` após a execução do `.osx` e `.brew`. Só pra checar se está tudo bem.*

## Finalizando
<br/>
A esta altura, você já deve estar olhando para seu Terminal com mais carinho. E porque seria diferente? Ele se perfumou todo pra você. Conseguimos deixar sua máquina tunada com um mínimo de esforço. Agora vá fazer suas próprias personalizações. E não esqueça de compartilhar as mais legais com a gente. <img src="https://abs.twimg.com/emoji/v1/72x72/1f64c.png" width="24" style="margin-bottom: -5px;">

No próximo post, irei ensinar alguns comandos básicos, pra qualquer *[noobie](http://www.thefreedictionary.com/Noobie)* se virar como um *pro* no Terminal. Se gostou, manda um <img src="https://abs.twimg.com/emoji/v1/72x72/1f44d.png" width="24" style="margin-bottom: -3px;">, compartilha, e deixa um comentário. Até a próxima!
