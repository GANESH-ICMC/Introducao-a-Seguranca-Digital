# Intro à web \(só que um pouco menos\)

## Guerra:

**Flag:** `GANESH{RhoY8fv9ZOFhQkTyI3WP}`

Ao acessar a página do chall, recebemos uma página de acesso não autorizado.

![Login page - Admin and flag](https://i.imgur.com/IhaHniK.png)

Analisando a requisição a partir da aba 'Network' das ferramentas de desenvolvedor do browser, observa-se que há um cookie `admin` com valor `0`.

![Login page - Admin and flag](https://i.imgur.com/qOcbDF9.png)

Capturando essa requisição com o BurpSuite, alterando o valor desse cookie de 0 para 1 e o enviando para o servidor obtemos uma página avisando que fomos logados com sucesso.

![Login page - Admin and flag](https://i.imgur.com/U569vGi.png)

![Login page - Admin and flag](https://i.imgur.com/PqjNfXv.png)

Assim, obtemos a flag!

