---
layout: post
title: "Privacidade Mobile"
date: 2012-02-09 21:22
comments: true
categories: 
---

Privacidade. Essa palavrinha que faz mágica quando se quer criar histerias coletivas.

Minha opinião sobre isso é a seguinte: quer privacidade? Então saia do Foursquare e pare de postar suas fotos no Instagram e no Facebook, pois
privacidade na internet é uma questão de escolha pessoal - em alguns casos como o [Path](https://www.path.com/) mostrou.

Path se vende como uma "rede social privada": você compartilha seus momentos com as pessoas mais próximas. Essa semana, um desenvolvedor 
[descobriu](http://mclov.in/2012/02/08/path-uploads-your-entire-address-book-to-their-servers.html) que o aplicativo deles enviava para um servidor
**toda** a sua lista de contatos do iPhone sem pedir autorização. 

<!-- more -->

## A decisão errada: A API é fácil e está ali para ser utilizada ##

Na web o usuário sempre foi tratado de forma _ativa_. Porém, em dispositivos móveis muitas vezes o usuário faz o papel de agente _passivo_, pois
é algo pequeno e com o qual as pessoas não querem ter muito trabalho ao utilizar (ao contrário do paradigma de se utilizar um computador). Então
por que continuamos programando como se o usuário não carregasse informações importantes?

Qualquer um que utilize o iPhone sabe que existem dois pedidos básicos de informação que ele faz para cada aplicativo, quando necessário:
se você autoriza o aplicativo a utilizar sua localização e se você autoriza receber notificações (_Push_). 

Porém, a API da lista de contatos não pede autorização e alguns desenvolvedores que 
[é aceitável utilizar essa informação](http://dcurt.is/stealing-your-address-book) sem a permissão do usuário. Mais errado do que esse
pensamento, só jogar a culpa na Apple.

## Don't shoot the messenger ##

Imagine ser bombardeado por pedidos de autorização cada vez que o aplicativo resolve acessar alguma informação do usuário.

A Apple não faz isso pois ela conta com um item que todo desenvolvedor e empreendedor deve ter: ética. O Path mostrou isso no 
[pedido de desculpas](http://blog.path.com/post/17274932484/we-are-sorry) ao dizer que todos os dados seriam apagados.

Muitas vezes o maior desafio não é desenvolver um sistema, prevendo sua alta disponibilidade e outras _buzzwords_. O maior desafio
pode ser fazer o seu usuário confiar em você, sabendo que os dados dele serão tratados como algo sagrado e inviolável.

## Privacidade, mesmo quando autorizado o uso da informação ##

Certa vez, comecei um aplicativo em que seria necessário requisitar a geolocalização do usuário e enviar essa informação para um servidor.
Minha preocupação desde o início era: como vou guardar essas informações sem que elas sejam relacionados diretamente a alguém?

A solução que encontrei foi guardar separadamente a localização sem que ela estivesse relacionada diretamente com qualquer outra coisa 
dentro do sistema. Assim garanto que ela não seria de fácil manipulação e ao mesmo tempo consigo os dados que o meu sistema precisaria.

Seja transparante. Só pegue os dados que realmente precisar. Criptografe. Identifique de uma maneira que somente o seu sistema entenda.
[Crie um hash](http://blog.securemacprogramming.com/2012/02/on-privacy-hashing-and-your-customers/) das informações.


São esses tipos de detalhes que fazem a diferença. Confiança é a melhor moeda de troca com a pessoa que vai utilizar seu sistema.


