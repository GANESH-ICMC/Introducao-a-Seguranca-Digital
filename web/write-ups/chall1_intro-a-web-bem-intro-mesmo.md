# Intro à web

## Guerra:

**Flag:** `GANESH{G3T_3XP3RT}`

Ao acessar a página, obtemos a página a seguir.

![Login page - Not Admin](https://i.imgur.com/V9QRBM1.png)

Observando a URL, nota-se que ele tem um parâmetro `admin=0`. Com base nisso, tentamos trocar o valor de `admin` para `1`, enviando uma requisição com a URL `http://url_do_chall/?admin=1`.

Como resposta, recebemos essa página:

![Login page - Admin and flag](https://i.imgur.com/F9VVh4v.png)

E, assim, obtemos a flag!

