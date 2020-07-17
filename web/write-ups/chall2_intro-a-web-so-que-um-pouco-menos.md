## Chall 02 - Intro à web (só que um pouco menos) (PInG 2019)

#### Guerra:
**Flag:** `GANESH{RhoY8v9ZOFhQkTyI3WP}`

Ao acessar a página do chall, recebemos uma página de acesso não autorizado.

<img style='border: 1px solid black; margin: 0 0 10px' src='https://i.imgur.com/IhaHniK.png' alt='Login page - Admin and flag' />

Analisando a requisição a partir da aba 'Network' das ferramentas de desenvolvedor do browser, observa-se que há um cookie `admin` com valor `0`. 

<img style='border: 1px solid black; margin: 0 0 10px' src='https://i.imgur.com/qOcbDF9.png' alt='Login page - Admin and flag' />

Capturando essa requisição com o BurpSuite, alterando o valor desse cookie de 0 para 1 e o enviando para o servidor obtemos uma página avisando que fomos logados com sucesso.

<img style='border: 1px solid black; margin: 0 0 10px' src='https://i.imgur.com/U569vGi.png' alt='Login page - Admin and flag' />

<img style='border: 1px solid black; margin: 0 0 10px' src='https://i.imgur.com/PqjNfXv.png' alt='Login page - Admin and flag' />

Assim, obtemos a flag!