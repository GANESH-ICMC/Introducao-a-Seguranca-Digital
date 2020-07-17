## Chall 01 - Intro à web (bem intro mesmo) (PInG 2019)
#### Guerra:
**Flag:** `GANESH{G3T_3XP3RT}`

Ao acessar a página, obtemos a página a seguir.

<img style='border: 1px solid black; margin: 0 0 10px' src='https://i.imgur.com/V9QRBM1.png' alt='Login page - Not Admin' />

Observando a URL, nota-se que ele tem um parâmetro `admin=0`. Com base nisso, tentamos trocar o valor de `admin` para `1`, enviando uma requisição com a URL `http://url_do_chall/?admin=1`.

Como resposta, recebemos essa página:

<img style='border: 1px solid black; margin: 0 0 10px' src='https://i.imgur.com/F9VVh4v.png' alt='Login page - Admin and flag' />

E, assim, obtemos a flag!