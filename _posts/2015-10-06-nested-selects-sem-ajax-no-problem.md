---
layout: post
title: Nested selects sem AJAX? No problem
tags: [ruby, javascript, dicas]
---
Vez ou outra, todos precisamos de selects com sub-níveis e a primeira coisa que pensamos é: *`vamos usar AJAX!`*.

Boa parte das informações, nós já conseguimos trazer de uma vez ao carregar a view, então deve ter alguma forma mais fácil.
Um dos grandes problemas que sempre encontro é: como organizar todas essas informações sem precisar ir buscar no controller com AJAX toda hora?

Pra começar, vamos tornar o hash disponível para view em forma de helper.

{% highlight ruby %}
class MyController < ApplicationController
  helper_method :structure_as_hash

  def structure_as_hash
    {
      "level1_tem1" => ["level2_item1"],
      "level1_tem2" => ["level2_item2"]
    }
  end
end
{% endhighlight %}

Na view, vamos parsear esse hash e torná-lo disponível pro javascript em formato json.

**PS:** A sintaxe abaixo é [Slim][1]! :wink:

{% highlight slim %}
= simple_form_for @my_model do |f|
  = f.input :level1_select, input_html: { id: "js-level1" }, collection: structure_as_hash.keys
  = f.input :level2_select, input_html: { id: "js-level2" }, collection: []

javascript:
  var structure_as_json = JSON.parse("#{escape_javascript(structure_as_hash.to_json.html_safe)}")
{% endhighlight %}

E finalmente seu javascript será algo assim:

{% highlight js %}
var $selectLevel1 = $('#js-level1'),
  $selectLevel2 = $('#js-level2');

$selectLevel1.on('change', function (e) {
  var selected = $(e.target).val();

  $selectLevel2.html('');

  if (selected.length) {
    $selectLevel2.append(
      $.map(structure_as_json[selected], function(v, k) {
        return $("<option>").val(v).text(v);
      })
    );
  }
});
{% endhighlight %}

Ao selecionar alguma opção do primeiro select, ele irá limpar o segundo select e depois irá montar e carregar os `options` correspondentes.

Isso me parece mais simples do que ficar trafegando AJAX pra todo lado. :sweat_smile:

[1]: http://slim-lang.com
