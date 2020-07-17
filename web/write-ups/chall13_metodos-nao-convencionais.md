## Chall 13 - Métodos não convencionais (made by Guerra - PInG 2020)

**Flag:** `Ganesh{tRu3_h4Ck3R_M@n}`

Ao entrarmos nesse chall nos deparamos com uma página em HTML estático. Ao explorarmos o código fonte fica claro que a página é estática e não possui nenhum tipo de funcionalidade atrelada a ela. Analisando outros locais como Cookies, Local Storage e cabeçalhos de retorno da requisição também reparamos que não há nada para fazer aqui.

Vamos então verificar a existência do `robots.txt` buscando-o pela URL. Verificamos então que o mesmo existe e possui o seguinte conteúdo:

```
User-agent: *
Disallow: /phpinfo.php
# Later: Disallow: /68696464656e666c616770616765776f772e706870
```

Ao abrir o arquivo `phpinfo.php` nos deparamos com o retorno da função phpinfo(); padrão e não há nada de muito interessante para tirar de tais dados no momento (~~apesar de que em um cenário real, tais informações expostas podem ser de fato muito valiosas para pessoas má intencionadas~~). Há no entanto um disallow comentado no arquivo e que parece ter sido ofuscado.

Vamos testar então algumas conversões de base básicas como base64 -> ASCII, base32 -> ASCII, base16 -> ASCII, etc...

`(base64):ν뎸랞뮜^N뾹ﾟ～N (o.O)'`
`(base32): também não é :(`
`(base16): hiddenflagpagewow.php \o/`

Conseguimos então encontrar outro arquivo mas ao tentar acessá-lo nos deparamos com o erro *403 Proibido – você não tem permissão para acessar*. Apesar de não conseguirmos ver nada, ao menos o erro 403 nos dá uma ideia de que o arquivo de fato existe pois caso contrário o servidor retornaria um 404.

Sabemos então que alguma verificação está sendo feita para validar o acesso ao arquivo, mas o que está sendo levado em conta?

Bom, como o erro ocorre como retorno da requisição, poderiamos começar avaliando o que poderiamos modificar/acrescentar nela que talvez nos dê acesso a página.

* **Parâmetros:** poderiamos testar alguns parâmetros via url. Mas honestamente não faria muito sentido, uma vez que teriamos que advinhar o nome do possível parâmetro sendo utilizado e em seguida descobrir o valor? Wow, pouco provável.
* **Cookies:** idem acima, a página não possui nenhum cookie para ser modificado e não queremos brincar de advinhação.
* **Authorization:** é um cabeçalho que pode ser enviado com credenciais em uma requisição.
* **Tipo da Requisição:** esse parece fazer mais sentido, uma vez que o erro recebido é um erro padrão e isso nos dá a impressão de que o redirecionamento está sendo feito pelo servidor e não à nível de programação.

Dentre as 4 opções acima, as três primeiras parecem depender muito do fator advinhação. Sabemos que eles existem mas vamos deixá-los em aberto no momento e abordar o 4º tópico.

*Obs: Caso não se lembre, esses são os possíveis [métodos](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods) existentes.*

Utilizando o proxy do BurpSuite, ou editando a requisição diretamente pelo DevTools do Firefox, modifiquei a requisição de GET para POST a fim de ver como o servidor responderia.

SUCESSO!!! O servidor permitiu o acesso ao arquivo, retornando para nós a flag do chall. Não foi necessário, portanto, explorar nenhum dos outros 3 tópicos (ufa!).

*Obs: este chall também aceita o método de requisição OPTIONS, recomendo que você leia a sua utilização e tente enviá-lo para ver o que o servidor retornaria nesse tipo de requisição.*