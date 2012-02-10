---
layout: post
title: "Backend X Mobile App: o que fazer o que não fazer e como fazer"
date: 2011-11-23 21:43
comments: true
categories: 
---

Dificilmente um aplicativo mobile (qualquer plataforma, choose one) vive sozinho, 90% das vezes é necessário um back-end para guardar,
transmitir, processar as informações.

A programação nos dois lados não é igual, tanto em arquitetura quanto em padrões. E sofri muito até perceber isso, por isso apresento aqui
os principais problemas, tanto de programação quanto humanos, que os dois lados encontram.

<!-- more -->

## Nunca confie no dev na outra ponta (a menos que ele sente na mesma mesa que você) ##

A interface de um aplicativo mobile é, sim, complicada e cheia de detalhes. Esses detalhes, muitas vezes, só são vistos durante o desenvolvimento.

Enquanto isso, as informações no back-end estão, geralmente, dispersas. A forma como elas devem ser reunidas e transmitidas afeta a 
arquitetura do projeto.

Isso significa que alterações na forma que a informação deve ser enviada e recebida são inevitáveis nas duas pontas do projeto. É irreal esperar
que somente um dos lados decida como isso será feito, esse tipo de decisão tem e deve ser tomada em conjunto (princípio 
[ACID](http://en.wikipedia.org/wiki/ACID) se aplica nesse caso, já que os dois lados tem que garantir o que acontecerá com a informação).

Se os dois desenvolvedores estiverem sentados perto um do outro, essas alterações e definições ficarão muito mais claras e fáceis de serem 
explicadas até que chegue a um consenso ou ao um meio-termo que fique bom para ambos.

E o tema seguinte exemplifica por que isso é o ideal.

## Reutilização não funciona aqui ##

"Não reinvente a roda", eles dizem. Se já existe uma API pronta para acessar as informações que o aplicativo precisa, o dev do back-end 
não vai (com razão) criar outro serviço somente para o aplicativo. Afinal a informação já está lá, não?

Não, não está.

A forma como a informação deve ser apresentada em um aplicativo é bem diferente de qualquer outra plataforma. A informação tem que ser menor, 
mais direta, mais informativa e, ao mesmo tempo, mais condensada. O aplicativo não deve possuir todas as regras de negócio de um projeto, portanto
o back-end deve trazer as informações do jeito certo e avisar caso tenha algum erro.

Um número que outras plataformas apresentaram de modo inteiro, pode acontecer de no aplicativo precisar ser em string e já tratada. Se isso acontecer,
como o desenvolvedor do back-end resolve? Cria-se uma nova chave somente para essa informação? (sim, fizeram isso comigo)

## A conexão pode ser pior do que o dispositivo diz que é ##

Conexão móvel não é a melhor do mundo, lide com isso.

Qualquer atraso na conexão pode gerar erro no retorno, informações inconsistentes com o que foi pedido e lentidão para o usuário. 

Isso também significa que a conexão do usuário está sendo utilizada enquanto esses erros são tratados pela plataforma. Conexão sendo utilizada
leva a consumo do limite da banda do usuário e leva a um uso maior da bateria do dispositivo. 

Isso nos leva ao próximo item, que é...

## Mobile, só você sabe o quanto de informação precisa (e pode) transmitir ##

Se der para fazer cache, faça. Se der para [verificar no servidor](http://en.wikipedia.org/wiki/HTTP_ETag) se o conteúdo é novo, faça.

Os dados do usuário não são infinitos e o seu aplicativo não tem direito a consumir tudo sozinho. E quanto mais informações, mais lento o
aplicativo ficará.

O back-end deve sempre retornar somente o necessário. O back-end retorna um item que o aplicativo não está utilizando? Remova-o. O aplicativo 
está enviando informação inútil para o back-end? Não envie. E é justamente por esses motivos que o JSON foi estabelecido e padronizado. 
Simples, direto e fácil.

Já vivi situações em que o back-end retornava o JSON dos dados dentro de um pacote SOAP (sim, em XML). E o aplicativo enviava 
em SOAP também. E a conexão sofria com a quantidade de informações inúteis. E o aplicativo gastava processamento capturando o JSON dentro de um XML. 

## Se é back-end, programe em mobile. Se é mobile, programe em back-end ##

Já vivi os dois lados. Separados e juntos.

No [School Rating](http://bit.ly/school_rating), produzi todo o back-end em Python e o aplicativo em Objective-C.

Primeiro, o programador back-end (eu) estruturou todo o banco de dados, chamadas e retornos da API, conforme o que o programador mobile (eu) passou.
Aí o programador mobile (eu) descobriu que precisava de algumas informações a mais. O programador back-end (eu) não gostou por ter que alterar
a lógica para incluir mais dados. Mas o programador mobile (eu) foi legal e passou as informações do melhor jeito possível.

Tudo isso me ajudou a ter uma visão de como os dois lados devem interagir e por que alterações nesse caso são necessárias (e quando elas devem
ser necessárias).

## Tipagem de dados foi inventada por um motivo ##

Um array deve sempre ser um array. Uma string sempre uma string. E um número sempre um número.

Quem requisita os dados deve fazer o menor tratamento possível, principalmente quando estamos falando de um sistema mobile 
com memória e processamento limitados. Se uma determinada chave do JSON é uma lista (array), então **sempre** retorne uma lista, mesmo que ela
seja vazia, e nunca um valor nulo ou string vazia. 

## Use e abuse dos http headers ##

Os cabeçalhos de uma requisição HTTP serão sempre tratados automaticamente, não importa o método de requisição utlizado, portanto é mais simples
ler o response code do que perder tempo e processamento interpretando o corpo da resposta. O Level 2 do 
[Richardson Maturity Model](http://martinfowler.com/articles/richardsonMaturityModel.html) explica bem sobre isso.

Isso vale para as duas pontas da requisição. Um __User-Agent__ pode diferenciar quem estão fazendo a requisição (se é um Android
ou um iPhone, por exemplo). Um __MIME__ pode [especificar](http://blog.steveklabnik.com/2011/08/07/some-people-understand-rest-and-http.html) 
o que está sendo enviado.

## Simplifique. Ou morra afogado no mar de informações. ##

Tudo o que disse leva a esse ponto: simplificar. Informações sem tratamento são apenas dados, e isso não interessa a quem quer a informação.

Simplifique e seja feliz. Seu usuário agradece.



