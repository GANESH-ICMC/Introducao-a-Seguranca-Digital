# Nível 02

## O objetivo do nível é ler um arquivo na pasta home do servidor

```text
$ ssh bandit2@bandit.labs.overthewire.org -p 2220
```

A senha é a flag do nível anterior.

Nesse nível, o objetivo do programa é ler um arquivo que contém espaços no nome. Nesse caso, `$ cat Nome Do Arquivo` não irá funcionar. Para ler um arquivo com espaços em seu nome, há duas maneiras principais:

* `$ cat "Nome Do Arquivo"` pois as aspas fazem cat considerar todo o nome do arquivo, inclusive os espaços, como uma única string.
* `$ cat Nome\ Do\ Arquivo` pois a contra barra faz o espaço ser considerado como parte da string, e não como delimitador.

