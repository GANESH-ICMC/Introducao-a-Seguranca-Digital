# Rock you \(Removido\)

## Marucs:

Flag: `GANESH{eZTBZamJNd8DIJyeAy5w}`

Ao Carregar a página, vemos uma tela de login, e links que levam para um lorem ipsum. Após tentar um login e uma senha aleatórios, percebe-se que o sistema possui uma potencial falha de segurança, a mensagem: `Usuário não encontrado`. Por que isso é uma falha? porque é possível saber se um usuário existe ou não sem nem saber a senha dele. Eu tentei o clássico login: admin e senha: admin e a mensagem agora foi `Senha do usuário incorreta`. Ou seja, a conta admin existe. Para adivinhar a senha também não foi muito difícil, usei a famigerada wordlist _rockyou_. Testei algumas senhas, quando cheguei na quinta - _iloveyou_ - o sistema me redirecionou para uma página com a flag. 

![](https://i.imgur.com/eZKQKfU.png)

