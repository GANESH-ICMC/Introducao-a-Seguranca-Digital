# Quebrando o site do sobrinho

## Marucs:

Flag: `GANESH{PTjxybVpBkjNMBwDooT5}`

Inspecionando o HTML, verifica-se que existem dois campos ocultos chamados debug com valor 0 \(false\). Muda-se `type="hidden"` para `type="text"`. Ao mudar o campo debug do login para 1 \(true\), é exibida na tela a query SQL feita para o banco de dados:

 

![](https://i.imgur.com/nXV1vub.png%29)

 Página de login com debug="1"

Tentei colocar um ' para ver como o código se comportava:

  

![](https://i.imgur.com/cFQ7JsW.png%29)

Ele não deu escape no caractere, o que indica que esse campo é vulnerável a SQL injection.

Pensei em fazer algo como `SELECT * FROM usuarios WHERE nome='admin' --' AND senha = 'MTIz'`. Dessa forma, ele ia pegar o admin sem checar a senha, por causa da marcação do comentário \(`--`\). Infelizmente, eu não sabia o nome do admin, então pensei em fazer o sistema logar com o primeiro usuário cadastrado. Para isso, usei essa query: `SELECT * FROM usuarios WHERE nome='marucs' or '1'='1' --' AND senha = 'MTIz'`. 

Dessa forma, se o banco de ordenar por ordem de criação, eu vou logar com o primeiro usuário criado \(provavelmente o admin\). Então digitei no campo de login `marucs' or '1'='1' --` e voila, o select retornou todos os usuários e o primeiro deles era o admin.

 

![](https://i.imgur.com/OqGSLhl.png%29)

