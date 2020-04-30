# Bandit 5
#### O objetivo do nível é ler um arquivo human-readable e que tenha 1033 bytes de tamanho
```
$ ssh bandit5@bandit.labs.overthewire.org -p 2220
```
A senha é a flag do nível anterior.

Diferente do nível anterior, tentar abrir arquivo por arquivo nesse nível seria demasiadamente desgastante.

Então, dessa vez, usaremos o comando *find* e duas opções que podem ser encontradas em seu manual: *-readable*, que procura apenas por arquivos que podem ser lidos, e *-size*, que procura por arquivos com o tamanho que passarmos como argumento. Assim, o comando que retornará o arquivo com a flag ficará:
```
$ find . -readable -1033c
```
Onde "." significa que a busca recursiva que o comando *find* executará irá começar no diretório atual.

