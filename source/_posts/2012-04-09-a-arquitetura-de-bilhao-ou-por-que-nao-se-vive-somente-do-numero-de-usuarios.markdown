---
layout: post
title: "A arquitetura de $1 bilhão (ou por que não se vive somente do número de usuários)"
date: 2012-04-09 20:55
comments: true
categories: 
---

Ultimamente, todas as métricas sobre uma startup falam do seu número de usuários. Claro que com a compra Instagram não poderia ser diferente.
Mas existe, sim, algo além disso que poucos falam: a arquitetura do sistema.

A arquitetura do Facebook é tosca, como sempre foi e será por um bom tempo. Um destino [pior que a morte](http://gigaom.com/cloud/facebook-trapped-in-mysql-fate-worse-than-death/), 
mesmo com as constantes inovações, como o [Cassandra](http://cassandra.apache.org/) e o [HipHop](https://github.com/facebook/hiphop-php). 90%
dos sistemas feitos são os famosos [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete), então quando um sistema deixa 
de ser somente isso, fica difícil pensar como fazer sem deixar gargalos.

<!--more-->

## O milagre da multiplicação dos usuários

{% tweet https://twitter.com/ShaneMac/status/182559236763553792 align='center' %} 

A matemática é simples: quanto mais usuários, mais gente consumindo os anúncios. Não somente o Facebook, mas todos dependem de você: Google,
boo-box e tantos outros. Nesse cenário fica mais fácil se apegarem somente a métricas de quanto cada usuário vale para a startup.

Só que essa métrica não é nada sem que esses milhares de usuários tenham uma boa experiência no uso da plataforma. As pessoas não utilizam 
o Instagram apenas por causa de seus filtros, elas utilizam por que ele é rápido, confiável e fácil. E isso não se consegue do dia para a noite.

## A engenharia e arquitetura do sistema é tudo

Vejamos a arquitetura do Instagram:

> * Gunicorn as their WSGI server. Apache harder to configure and more CPU intensive.
> * Fabric is used to execute commands in parallel on all machines. A deploy takes only seconds.
> * PostgreSQL (users, photo metadata, tags, etc) runs on 12 Quadruple Extra-Large memory instances.
> * Pgbouncer is used pool connections to PostgreSQL.
> * Redis powers their main feed, activity feed, sessions system, and other services.
>
> Fonte: <a href="http://highscalability.com/blog/2012/4/9/the-instagram-architecture-facebook-bought-for-a-cool-billio.html">High Scalability</a>

Pois é. Tudo tecnologia de ponta (_cutting edge tech_, como eles gostam de chamar) que o Facebook não utiliza pois o sistema deles não foi 
feito com isso em mente e implementar tudo isso agora, a beira de um IPO, seria caro demais. Solução? _Acqui-hire_.

Comprando o Instagram, o Facebook leva todo esse sistema e, de brinde, a equipe de 16 pessoas que conseguiu construir tudo isso do zero. É o tipo 
de situação win-win: investidores, fundadores e funcionários do Instagram conseguem um bom dinheiro, Facebook consegue uma equipe já experiente 
com o tipo de tecnologia que eles mais precisam.

## A mágica acontece por trás

Vivemos em uma indústria onde tudo isso muda rapidamente. A arquitetura do Facebook é tosca por que isso fazia sentido quando ele foi feito. Hoje, 
o Facebook não tem mais fôlego nem tamanho para sair testando e batendo cabeça com essas novas tecnologias como uma equipe de 16 pessoas consegue.

Desenvolvedores são as pessoas que ficam por trás da cortina, por isso mesmo que eles são os mais importantes. Sem conhecer o que há 
de mais novo, você estará sempre para trás na corrida pela inovação.



