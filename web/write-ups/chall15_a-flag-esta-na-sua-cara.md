# A flag está na sua cara

**Flag:** `GANESH{Fl4G_D3_ScHR0d1NG3r}`

Neste chall, ao entrarmos na página inicial nos deparamos com uma página cujo retorno HTML é extremamente simples e cuja única mensagem é:

`This site is under construction. Currently, there's no files related to this page in server's folder.`

Podemos perceber também que há um parâmetro `?file=WIP.txt` sendo enviado pela URL. Vamos então alterá-lo para ver como isso ira afetar o comportamento da página.

Fazendo a troca para algo aleatório como `?file=X.txt` vemos que ocorre um erro ao tentar carregar o arquivo.

Apenas por caráter de teste, vamos tentar fazer o arquivo a ser incluido seja à própria `index.php` uma vez que podemos inferir que esse arquivo é o que está sendo executado na raiz do site.

Sucesso!!! Apesar da página estar vazia, ao analizarmos o HTML por meio das DevTools do navegador podemos ver que o código PHP utilizado foi exposto como texto comum para nós e dentro dele, em um comentário PHP, encontramos a nossa desejada flag.

