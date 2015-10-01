---
layout: post
title: Seus usuários possuem Gravatar?
tags: [ruby, dicas]
---
Hoje em dia, todo sistema possui usuários com fotos, comumente chamados de [avatar][2].

Pra não se preocupar com upload de fotos, processamento, cropping e storage, você pode integrar seu sistema com o [Gravatar][1]. É bem simples.
Você consegue buscar a URL do avatar do usuário através do hash MD5 do e-mail registrado no Gravatar.

{% highlight ruby %}
class User
  def avatar
    "http://www.gravatar.com/avatar/#{digest_email}"
  end

  def secure_avatar
    "https://secure.gravatar.com/avatar/#{digest_email}"
  end

  private

  def digest_email
    Digest::MD5.hexdigest(email.downcase)
  end
end
{% endhighlight %}

Essa foi a forma mais simples e direta de buscar o avatar de um usuário.

Caso queira ver mais detalhes sobre as opções que você utilizar, só ver [aqui][3].

[1]: http://en.gravatar.com
[2]: https://en.wikipedia.org/wiki/Avatar_(computing)
[3]: https://en.gravatar.com/site/implement/images/
