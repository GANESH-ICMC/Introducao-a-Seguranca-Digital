# Arquivos

No fundo, todos os arquivos são compostos por bytes \(ou seja, vários 1s e 0s\), porém podemos dividir os arquivos em duas grandes classificações, arquivos binários, e arquivos de texto.

Em arquivos de texto, cada byte representa um caractere, arquivos de texto podem ser abertos com programas simples de edição de texto, e podem ter seu conteúdo lido sem dificuldade.

Já arquivos binários são todos os arquivos que não são de texto, em arquivos binários os bytes podem representar diversas coisas, não necessariamente characteres, por exemplo, em imagens os bytes podem representar a cor de cada pixel, já em arquivos executáveis, os bytes podem ser utilizados para representar instruções para o computador.

Um arquivo binário aberto com um editor de texto pode mostrar coisas completamente ilegíveis.

## Alguns comandos importantes

### strings

O comando strings é utilizado para recuperar strings \(texto\), de arquivos binários. Ele percorre o arquivo binário e retorna todas as strings 'human-readable', ou seja, que possuem characteres que podem ser lidos por nós.

### xxd

O comando xxd, ou Hexdump, pode ser utilizado para mostrar os bytes de um arquivo \(em hexadecimal, por isso o nome\), o hex dump pode ser muito importante para analisar ou ver as informações que compõem um arquivo.

### objdump e readelf

Os comandos objdump e redelf são utilizados para obter informações sobre binários ou arquivos objeto \(arquivos resultantes da compilação de algum código fonte\), o objdump pode ser utilizado para obter o código Assembly de um executável.

## Magic Numbers

Os primeiros bytes de um arquivo são chamados de Magic Numbers, e eles são utilizados para identificar qual tipo de arquivo é. A ideia de se colocar os magic numbers no início é para evitar que o computador precisa percorrer o arquivo para identificar seu tipo.

Por exemplo, quando vamos abrir uma imagem, o computador precisa saber que o arquivo é uma imagem, para isso ele pode verificar os primeiros bytes e descobrir qual o formato do arquivo.

O comando "file" do Linux verifica os magic numbers e retorna o tipo do arquivo \(caso consiga identificá-lo\).

## Exemplo

Abaixo podemos ver um hexdump de uma imagem, e podemos ver seu Magic Number \(424d\). ![Exemplo hexdump](https://i.imgur.com/aVYW6tT.png)

