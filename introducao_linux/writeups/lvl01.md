# Nível 01

## O objetivo do nível é ler um arquivo na pasta home do servidor

```text
$ ssh bandit1@bandit.labs.overthewire.org -p 2220
```

A senha é a flag do nível anterior.

Nesse nível, apenas `cat <nome_do_arquivo>` não resultará na flag pois o arquivo possui um caracter especial para cat, que significa "stdin" \(-\) Nesse caso, para resolver o conflito, o comando a ser executado pode ser cat `$ cat ./-`, pois, graças a "./", que é o caminho relativo ao diretorio atual, o comando 'cat' entende que "-" é um arquivo.

