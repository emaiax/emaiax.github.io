---
layout: post
title: Rodando os testes em loop
tags: [shell, dicas]
---
Outro dia precisei rodar minha suite de testes diversas vezes até encontrar um erro intermitente pra ajudar a entender e debugar o problema.

Cansado de apertar `cima + enter`, acabei encontrando uma dica bacana pra facilitar esse processo.
Isso vai rodar 50 vezes o `rspec spec` até todas as sequências passarem ou algum teste quebrar.

{% highlight sh %}
$ for i in `seq 50` ; do rspec spec ; [[ ! $? = 0 ]] && break ; done
{% endhighlight %}

Enquanto não acabar, basta buscar um café. :coffee:
