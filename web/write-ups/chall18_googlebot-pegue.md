# Googlebot, pegue?

**Flag:** `Ganesh{Cr4wl1nG_!n_My_w3b5ite}`

**Requer a finalização do Chall 4 Googlebot, não pegue!**

Neste chall, nos deparamos com um título muito similar ao visto no Chall "Googlebot, não pegue!" e portanto podemos proceder da mesma forma e averiguar o arquivo robots.txt.

```text
# Atualizado :)
User-agent: *
Disallow: /
Disallow: /w/
Disallow: /api/
Disallow: /trap/
Disallow: /test/Special:
Disallow: /test/Spezial:
Disallow: /test/Spesial:
Disallow: /test/Special%3A
Disallow: /test/Spezial%3A
Disallow: /test/Spesial%3A
```

Dessa vez, não encontramos nenhuma referência ao arquivo flag.php, só que refletindo sobre o título, a impressão que temos é que o site quer sim que o google visite a página. Vamos então apenas testar o mesmo caminho utilizado no chall anterior `/test/ganesh/flag.php`.

Nos deparamos então com a seguinte página mensagem.

![NOT GOOGLE BOT](https://i.imgur.com/qS7iN24.png)

Precisamos então que a página pense que somos na verdade um dos crawlers do Google.

Pesquisando um pouco, encontramos que os bots do google definem algums cabeçalhos na requisição HTTP que permite identificar o tipo de bot por meio do `User-agent` \([Veja aqui](https://support.google.com/webmasters/answer/1061943?hl=pt-BR)\).

Vamos então forjar uma requisição utilizando a ferramenta curl do console:

```markup
$ curl -v -H "User-agent: Googlebot" http://url.chall/test/ganesh/flag.php
...
<h1> Olá Googlebot! </h1> 
<div style='text-align: center; border: 1px solid grey; border-radius: 5px; background-color: #a2fcf2; width: 600px; margin: auto;'>
    <h2> Aqui está sua flag: Ganesh{Cr4wl1nG_!n_My_w3b5ite} </h2>
</div>
```

PRONTO! O site acreditou que eramos o GoogleBot e nos retornou a flag.

