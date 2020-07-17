# Injetando biscoito no veneno do amigo

## Guerra:

**Flag:** `Ganesh{SQLInjEc71onB4byst3psC0mplet3d}` Ainda na página no desafio 14, precisamos achar outra flag.

Analisando, novamente, a requisição feita para `/profile.php` e "brincando" com o valor do cookie `id` descobrimos que há uma falha que possibilita SQL Injection.

Enviando essa requisição com um payload de SQL Injection no campo id \(`0' or 1=1 -- -`\) obtemos a lista de todos os usuários presentes no banco de dados:

![](https://i.imgur.com/fiNLntW.png)

Buscando por "Ganesh" \(presente no ínicio de toda flag\), temos 2 _matches_. Uma é a flag do desafio anterior e a outra é a flag que buscávamos agora.

