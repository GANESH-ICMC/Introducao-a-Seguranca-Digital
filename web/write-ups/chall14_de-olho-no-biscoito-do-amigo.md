# De olho no biscoito do amigo

## Guerra:

**Flag:** `Ganesh{T3m0utr4FlagNe$$3chal7}`

Acessando a URL, obtemos uma página de login:

![](https://i.imgur.com/AeFmaZ3.png)

Temos as credenciais de um usuário: `john@john.com` - senha `123`. Ao fazer a requisição para realizar o login \(um `POST` para `/login.php`\), nota-se que somos redirecionados e o navegador faz uma segunda requisição para `/profile.php`, realizando um `GET` nessa página.

![](https://i.imgur.com/X5MY43v.png)

Analisando essa segunda requisição, observa-se que há um cookie chamado `id`. Capturando essa requisição no Burp Suite e modificando o valor desse cookie para 0,

![](https://i.imgur.com/WWbc07m.png)

obtemos a seguinte página:

![](https://i.imgur.com/6IZ8Dja.png)

Ou seja, obtemos a página no Admin, com a flag, passando o `id` = 0.

