---
layout: post
title:  Importando arquivos SQL no Postgresql
tags: [postgres, dicas]
---
Como uso OSX já faz um tempo, não perco muito tempo instalando um sgdb e configurando tudo, como fazia no Windows ou Linux.

Para o MySQL eu uso o [homebrew][1], mas para o Postgres existe um app que faz todo esse trabalho pra mim de forma mais simples ainda, é o [Postgresapp][2], que já conta com o PostgreSQL 9.4.4.

Às vezes preciso importar algum arquivo SQL no Postgres, por exemplo um backup direto em SQL ou uma lista de cidades/estados/países, sem ficar perdendo muito tempo.

Acho que a forma mais simples que encontrei foi essa, funcionou muito bem pra mim. :dancers:

`$ psql -h [host] -p [port] -d [database] -U [user] -f [/path/do/arquivo]`

--

**Atenção:** Isso serve para importar um arquivo SQL, restaurar um backup já é outra história. :sunglasses:

---
[1]: https://github.com/Homebrew/homebrew
[2]: http://postgresapp.com
