# Nível 00

## O objetivo do nível é apenas conectar via SSH ao servidor do jogo pelo username bandit0

```text
$ ssh bandit0@bandit.labs.overthewire.org -p 2220
```

O servidor pedirá senha, que é "bandit0". Após conectar ao servidor e digitar o comando `$ ls`, é possível ver um arquivo "readme". `$ cat readme` revelará a flag, e senha para o próximo nível.

