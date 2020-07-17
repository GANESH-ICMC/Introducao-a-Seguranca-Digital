## Chall 20 - REST in Peace (made by Van Loon - PInG 2020)

**Flag:** `Ganesh{W3B_w4S_Ch4ot1c_3v1L}`

Neste desafio nos deparamos primeiramente com uma página bem simples com apenas alguns textos e inglês e nenhum tipo de formulário, botão, link ou funcionalidade aparente. Como procedimento padrão vamos então analisar o código fonte da página para ver se encontramos algo de interessante... 

Analisando o HTML vemos que de de fato não há nada além de um style.css sendo incluso. Podemos ver, porém, que há um rodapé contendo um **link comentado** logo no fim da página.

```htmlembedded=
<footer>
   <!-- <p class="text-center"><a href="donate.html">Donation</a></p> -->
</footer>
```

Seguindo então para o link `/donate.html` nos deparamos com o que aparenta ser um formulário de doações. 

Para testar o formulário, insiro alguns dados de teste mas aparentemente o botão de envio não funciona e os dados não são enviados.

Novamente, realizo a inspeção do HTML para verificar a estrutura da página e me deparo com algo que parece ser código *Javascript* porém obfuscado e minificado.

```javascript=
var _0x451a=['value','name','querySelectorAll','querySelector','change','onreadystatechange','send','preventDefault','floor','onsubmit','Content-type','open','form','Zm9vbGluZyB0aGUgZm9vbA.php','random','application/x-www-form-urlencoded','input','&aaa=','length'];(function(_0xbf8d17,_0x451a78){var _0x424f6d=function(_0x3df864){while(--_0x3df864){_0xbf8d17['push'](_0xbf8d17['shift']());}};_0x424f6d(++_0x451a78);}(_0x451a,0x96));var _0x424f=function(_0xbf8d17,_0x451a78){_0xbf8d17=_0xbf8d17-0x0;var _0x424f6d=_0x451a[_0xbf8d17];return _0x424f6d;};var randomID=Math[_0x424f('0xa')](Math[_0x424f('0x10')]()*0x81b79)+0x2;var inputs=document[_0x424f('0x4')](_0x424f('0x12'));function prv(_0x5003b2){_0x5003b2[_0x424f('0x9')]();}document[_0x424f('0x5')](_0x424f('0xe'))[_0x424f('0xb')]=prv;for(i=0x0;i<inputs[_0x424f('0x1')];i++){inputs[i]['addEventListener'](_0x424f('0x6'),function(_0x4560b5,_0x4098fd){let _0x2308ad='f='+this[_0x424f('0x3')]+'&v='+this[_0x424f('0x2')]+_0x424f('0x0')+randomID;setTimeout(function(){var _0x268119=new XMLHttpRequest();_0x268119[_0x424f('0xd')]('POST',_0x424f('0xf'),!![]);_0x268119['setRequestHeader'](_0x424f('0xc'),_0x424f('0x11'));_0x268119[_0x424f('0x7')]=null;_0x268119[_0x424f('0x8')](_0x2308ad);},0x1f40);});}
```

Começo então à procurar formas de desobfuscar o código e a primeira coisa que me vem á mente é deixar o código mas legível utilizando alguma ferramenta que reverta a minificação. Para isso utilizo o site: https://beautifier.io/

```javascript=
(function(_0xbf8d17, _0x451a78) {
    var _0x424f6d = function(_0x3df864) {
...
...
...
document[_0x424f('0x5')](_0x424f('0xe'))[_0x424f('0xb')] = prv;
for (i = 0x0; i < inputs[_0x424f('0x1')]; i++) {
    inputs[i]['addEventListener'](_0x424f('0x6'), function(_0x4560b5, _0x4098fd) {
        let _0x2308ad = 'f=' + this[_0x424f('0x3')] + '&v=' + this[_0x424f('0x2')] + _0x424f('0x0') + randomID;
        setTimeout(function() {
            var _0x268119 = new XMLHttpRequest();
            _0x268119[_0x424f('0xd')]('POST', _0x424f('0xf'), !![]);
            _0x268119['setRequestHeader'](_0x424f('0xc'), _0x424f('0x11'));
            _0x268119[_0x424f('0x7')] = null;
            _0x268119[_0x424f('0x8')](_0x2308ad);
        }, 0x1f40);
    });
}
```

Reparo então que algumas funções não foram devidamente ofuscadas, dentre elas as funções: `addEventListener`, `setTimeout` e `XMLHttpRequest`. 

Mesmo com o código obfuscado, podemos analisar e inferir que em algum momento, um **timer** será declarado e irá esperar ***0x1f40 = 8000 ms (8 seg.)*** para realizar alguma requisição assíncrona via javascript.

Olhando o início do código obfuscado, vemos também uma sequência de strings e, dentre elas, `change` e `onsubmit`. Vamos testar no site então, analisando a aba de Redes, se algum desses gatilhos de fato dispara o XMLHttpRequest.

![Requisições Assíncronas](https://i.imgur.com/TTnm7Bm.png)

Boa! Após inserir alguns dados, apertar submit e esperar os 8 segundos vemos que de fato há o fluxo de algumas requisições aparecendo em nossa aba de redes e, aparentemente, o gatilho do AJAX foram as mudanças nos campos de texto (`change`). Vamos analisar essas requisições.

*Obs: foram removidos os cabeçalhos automáticos do navegador*

```
POST /Zm9vbGluZyB0aGUgZm9vbA.php HTTP/1.1
Host: web.ganeshicmc.com:1331
Content-type: application/x-www-form-urlencoded
Content-Length: 24

f=name&v=Teste&aaa=30899
```

Vemos então que os dados são enviados em `x-www-form-urlencoded` com 3 campos com nomes não tão legiveis. Mas após analisar um pouco o HTML reparamos que `f` sempre se remetia ao `name` do campo de texto e `v` ao value do campo durante o disparo da requisição.

Além disso, ao analisarmos a `Response` dessas requisições, vemos que o site retorna `1 Row inserted.`. Ou seja, a requisição deve estar realizando alguma espécie de cadastro.

Bom... temos uma nova URL para desbravar. Entrando nela diretamente pelo Browser nos deparamos com algo curioso: uma lista de resultados que nos permite inferir que os dados enviados via Ajax estão, na verdade, sendo salvos em uma espécia de banco de dados.

![Página GET](https://i.imgur.com/y1J8txJ.png)

Nessa vez, ao realizar a inspeção da página, não nos deparamos com nenhum outro dado que pareça nos dar alguma dica (*até há algumas tags PHP e javascript, mas elas aparentam ter sido salvas pelos outros jogadores e não fazer parte do CTF*).

Neste ponto, nos resta apenas tentar trabalhar diretamente na própria requisição para verificar como a url irá responder à tais mudanças. 

Podemos pensar em: 
- Variar o métodos HTTP
- alterar os Cookies
- alterar os parâmetros
- alterar as variáveis via URL (?a=A&b=B)
- inserir/alterar novos cabeçalhos.

*Obs: Para tornar essa parte mais fácil, eu utilizei a ferramenta Insomnia. Porém é possível utilizar também o ZAP, BurpSuite ou qualquer outra ferramenta capaz de realizar disparos de requisições da sua preferência.*

Quanto à inserção de Cookies e novos cabeçalhos, acredito que essas são as opções mais improváveis e complicadas de testar por necessitar de muita adivinhação e força bruta, portanto deixo elas para última necessidade.

**Alterando o Método:**

Lembrando um pouco de API's REST. Ja vimos que a URL realiza um cadastro durante o `POST` e retorna dados durante o `GET`. E se tentarmos então o método DELETE?

![Insomnia DELETE](https://i.imgur.com/K5kjNXD.png)

Nos deparamos então com uma linguagem em outra lingua que o Google Tradutor prontamente nos socorre identificando que é alemão e que diz:

```
Acesso negado.
Se o erro persistir, leia a documentação OPEN API YAML.
```

Essa mensagem aparece para todos os métodos com exceção de `POST` e `GET` e sempre nos exibe um link com uma documentação doida sobre uma ferramenta que, aparentemente, serve para documentar API's mas deixei isto de lado por enquanto...

**Alterando os parâmetros**

Voltando ao `POST` anterior, após realizar alguns testes foi possível descobrir que os campos `f` e `v` são obrigatórios e o `aaa` não. Tentei realizar alguns SQL Injections para verificar se a query era vulnerável e o site retornava uma resposta quebrada mas não houve nenhum efeito.

![Insomnia POST](https://i.imgur.com/hmQc6ed.png)

**Alterando a query da URL (?a=A&b=B)**

Por fim, a última tentativa foi a de verificar se os parâmetros da URL influenciariam a resposta do servidor. A primeira opção poderia ser tentar fazer um brute force de nomes de parâmetros. Porém, como no POST ja são utilizadas `f`,`v` e `aaa` vamos primeiro testar estas e ver o que acontece.

![Insomnia GET aaa=30899](https://i.imgur.com/xk3WjQ5.png)

Boa! Vemos que o resultado já difere do `GET` recebiamos antes e aparentemente somente os dados enviados pelos nossos `POST` são exibidos.

Brincando um pouco mais, podemos ver que o campo `aaa` é o que de fato está sendo utilizado para filtrar os dados de resultado!!!.

Fazendo uma enumeração de valores baixos começando com 0, encontramos a flag quando `aaa = 1` e **encerramos o Chall.**

![Insomnia GET aaa=1](https://i.imgur.com/Gxul1wh.png)


**Mas e o tal do link de documentação que encontramos ao mudar o Método?** Bom, ao analizar o link com um pouco mais de calma vemos que se trata de uma forma de documentar as entradas e saídas de uma API utilizando uma ferramenta que gera um arquivo `openapi.yaml` ou `openapi.json`.

Ao testarmos a existência desses arquivos na url nos deparamos com a seguinte resposta:

![openapi.yaml](https://i.imgur.com/JZk6OCI.png)

Este poderia ser um outro caminho para a resolução do chall. Pois podemos ver que a documentação diz que o método GET pode ser utilizado em conjunto com o parâmetro `aaa` para buscar dados específicos do servidor. Este no entanto demandaria um pouco mais da intuição e paciência em entender do que o link se tratava.

```yaml
paths:
  /Zm9vbGluZyB0aGUgZm9vbA.php:
    get:
      summary: Return a sublist of stolen data.
      description: Return a sublist of stolen data or all data identified from the given parameter.
      parameters:
        - name: aaa
          in: path
          description: Get all data identified from the given value. 
          required: false
          schema:
              type : integer
              format: int64
              minimum: 1
      responses:
        '200':  
          description: Table with stolen data.
```
