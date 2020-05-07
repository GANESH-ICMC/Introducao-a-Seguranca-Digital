# Nível 10

## O objetivo do nível é ler um arquivo com o conteúdo criptografado em base 64

```text
$ ssh bandit10@bandit.labs.overthewire.org -p 2220
```

A senha é a flag do nível anterior.

Como recomendado pelo site do bandit, usaremos o comando _base64_ nesse desafio. Lendo seu manual, vemos que esse comando possui a opção _-d_ para descriptografar uma entrada em base 64. Logo, o comando final ficará:

```text
$ cat data.txt | base64 -d
```

