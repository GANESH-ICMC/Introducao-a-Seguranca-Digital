# Nível 05

## O objetivo do nível é ler um arquivo human-readable e que tenha 1033 bytes de tamanho

```text
$ ssh bandit5@bandit.labs.overthewire.org -p 2220
```

A senha é a flag do nível anterior.

Diferente do nível anterior, tentar abrir arquivo por arquivo nesse nível seria demasiadamente desgastante.

Então, dessa vez, usaremos o comando _find_ e duas opções que podem ser encontradas em seu manual: _-readable_, que procura apenas por arquivos que podem ser lidos, e _-size_, que procura por arquivos com o tamanho que passarmos como argumento. Assim, o comando que retornará o arquivo com a flag ficará:

```text
$ find . -readable -1033c
```

Onde "." significa que a busca recursiva que o comando _find_ executará irá começar no diretório atual.

