# 0x0C00\(k\)1E==

## Alex:

Flag: `GANESH{xqUsVeHtWRByqPBBfh0y}`

Ao entrar na página foi verificado um texto indicando que o usuário acessando não possuia autorização para acessar a página. 

![page](https://i.imgur.com/7N4ATew.png)

Olhando no Dev-Tools do navegador, foi checada a requisição do arquivo index.php, para verificar se possuia algum parametro que chamasse a atenção.   


![dev\_tools](https://i.imgur.com/bMeL2Sl.png)

Então, observando os cookies dessa requisição, foi percebido um cookie "admin" com o valor "MA==". 

![headers](https://i.imgur.com/sgXP4ni.png)

Ao pesquisar no google o que significava essa string terminada em "\==" percebi que poderia ser um valor encodado em base64. Então, ao decodar o valor "MA==" obtive o valor "0". Então, tentei encodar o valor "1", e obtive o valor "MQ==".

Então a request foi reeditada e reenviada.

![edit](https://i.imgur.com/rSXei9u.png)

![resend](https://i.imgur.com/fBfMbGx.png)

A resposta obtida pelo valor editado de cookie foi a seguinte:  
 

![response](https://i.imgur.com/EimzTu7.png)

A flag então, do chall é: **GANESH{xqUsVeHtWRByqPBBfh0y}**

