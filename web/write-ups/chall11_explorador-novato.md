# Explorador novato

## Marucs:

Flag: `Ganesh{XPl0r3_ThE_W!Ld}`

Ao carregar a página principal, com o DevTools aberto, percebe-se que um GET é feito para a página, devolvendo apenas uma página HTML com imagens e texto sem sentido. Não há arquivos externos \(além de imagens\), botões, ou javascript na página. Então supus que a flag estaria no HTML mesmo, abri o código fonte e busquei por 'Ganesh', e lá estava a flag, no atributo 'alt' de uma imagem. 

![](https://i.imgur.com/CfK7dPX.png)

