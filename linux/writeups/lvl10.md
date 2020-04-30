# Bandit 10
#### O objetivo do nível é ler um arquivo com o conteúdo criptografado em base 64
```
$ ssh bandit10@bandit.labs.overthewire.org -p 2220
```
A senha é a flag do nível anterior.

Como recomendado pelo site do bandit, usaremos o comando *base64* nesse desafio. Lendo seu manual, vemos que esse comando possui a opção *-d* para descriptografar uma entrada em base 64. Logo, o comando final ficará:
```
$ cat data.txt | base64 -d
```

