# Cross Site Scripting \(XSS\)

XSS é a sigla para Cross-Site Scripting \(porque CSS já estava sendo usada\). Cross-Site Scripting é uma técnica que utiliza de certas vulnerabilidades para inserir código malicioso em uma página legítima na web. Geralmente, o código é escrito em Javascript, por ser a linguagem que o navegador usa durante a renderização de páginas web.

Se quiser saber mais sobre Javascript, [clique aqui](05_Introdução_Javascript.md).

As injeções de código por XSS, geralmente, têm o mesmo ponto de partida: falta de sanitização do _input_ do usuário.

Por exemplo, num formulário de cadastro, existem diversos campos nos quais o usuário pode digitar, como nome ou endereço. Mais tarde, quando outras pessoas visualizarem o nome que você cadastrou, o servidor vai entregar ao navegador delas o texto que você digitou. Ou seja, o navegador está executando uma instrução que é parte feita pelo desenvolvedor da página e parte feita por você.

Para deixar o exemplo um pouco mais claro, suponha esse exemplo fictício de uma página que quando vai exibir o nome do usuário usa essa função:

```javascript
function render_username(username) {
        //Code ...
    document.write('<h4>' + username + '</h4>')
}
```

Essa função pega o nome, coloca a tag de título em volta e coloca na página. Se o parâmetro _username_ estiver corretamente sanitizado, não há maiores problemas, mas se este não for o caso, temos uma vulnerabilidade de XSS.

Nesse exemplo, bastaria eu escrever `<script>alert("oi")</script>` como nome de usuário no cadastro e todos que lerem meu nome receberão um pop-up com o texto "oi". Se trocarmos na função o valor do username, fica mais claro:

```javascript
function render_username(username) {
        //Code ...
    document.write('<h4>' + '<script>alert("oi")</script>' + '</h4>')
}
```

Exemplo de site que sanitiza a entrada do usuário ![Google](https://i.imgur.com/EUT6AGI.png)

## Diferentes Classificações de XSS

O exemplo que foi dado acima é chamado de DOM Based XSS, isso porque é o Javascript que modifica a página HTML por meio do [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction). Além do ataque ter a classificação de ser ou não DOM Based, ainda existe outra classificação quanto ao ataque XSS: onde ele está armazenado.

### Reflected XSS

Esse é o XSS que é executado apenas do lado do cliente por exemplo, uma página de busca que exibe o conteúdo buscado \(ver imagem abaixo\). Nessa página, o texto "Conteúdo buscado" não é armazenado no servidor, mas é exibido no cliente e fica salvo na url do site. Por isso, se o site tiver vulnerabilidade XSS no campo de busca e alguém te mandar o link `http://site.vulneravel.tk/busca?q=<script>alert("oi")</script>` Basta você clicar nele e você já está executando o código potencialmente malicioso.

![Exemplo reflected](https://i.imgur.com/isfD885.png)

Justamente por não ser armazenado no servidor, o ataque XSS Refletido é mais difícil de rastrear, porém é possível que a vítima tenha uma ideia do que está acontecendo ao ler a URL.

Nesse tipo de ataque, os agentes maliciosos utilizam de engenharia social para que pessoas acessem o link afetado, como envio de e-mails para várias pessoas sobre promoções e sorteios falsos, que clicando no link, a pessoa vai ganhar algum prêmio. 

No exemplo da imagem, o "Conteúdo buscado" pode ser colocado na página de duas formas: pelo servidor, antes de enviar a resposta da requisição, ou pelo cliente, após receber a página. Se a página já vem com o conteúdo escrito, o ataque XSS não é DOM Based, mas caso ele seja modificado posteriormente por meio de Javascript ele é.

### Stored XSS

Esse tipo de ataque XSS, ao contrário do Refletido, é armazenado no servidor. Um exemplo clássico seria um post de um usuário em uma rede social. Se o texto do post não for sanitizado quando salvo no banco de dados, na hora de exibí-lo, código malicioso poderá ser executado.

Dessa vez, é impossível a vítima evitar o ataque, já que ela está apenas navegando no site, e não é possível diferenciar o código malicioso do código genuíno da página.

Portanto, o Stored XSS é mais nocivo \(em se tratando de medidas de proteção que o usuário pode tomar\), mas é "facilmente" identificado pelos administradores, uma vez que o código é armazenado no servidor.

## Prevenção contra o XSS

Conforme dito, o XSS se apoia, majoritariamente, na falta de filtros aplicados no conteúdo digitado pelo usuário, portanto a forma mais simples e eficiente de acabar com vulnerabilidades XSS nos campos de uma página é aplicar [filtros](http://htmlpurifier.org/comparison#striptags) e sanitizações, de modo a remover caractéres especiais que possam vir a causar problemas.

### CSP

Outra forma de garantir que a página não sofrerá de vulnerabilidades XSS, mesmo que os campos não possuam filtros é criar um sistema de "autenticação de scripts". O [CSP](https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html) faz exatamente isso: ele restringe quais elementos da página HTML terão permissão de executar scripts. Dessa forma, impede a execução de código que não pertença genuinamente à página.

## Fontes

* [https://www.welivesecurity.com/br/2017/07/07/vulnerabilidade-cross-site-scripting/](https://www.welivesecurity.com/br/2017/07/07/vulnerabilidade-cross-site-scripting/)
* [https://pt.pmgacademy.com/blog/artigos/tudo-sobre-xss](https://pt.pmgacademy.com/blog/artigos/tudo-sobre-xss)
* [https://littlemaninmyhead.wordpress.com/2018/06/24/demonstrating-reflected-versus-dom-based-xss/](https://littlemaninmyhead.wordpress.com/2018/06/24/demonstrating-reflected-versus-dom-based-xss/)

* [Slides](https://docs.google.com/presentation/d/13nax37vFi-T5ZyQp0VmpsP1NDS1LUkGkYBeg5cP4TUw/edit?usp=sharing)
