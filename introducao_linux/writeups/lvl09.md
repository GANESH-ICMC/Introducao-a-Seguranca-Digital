# Nível 09

## O objetivo do nível é ler uma das das linhas legíveis e que começa com '='

```text
$ ssh bandit9@bandit.labs.overthewire.org -p 2220
```

A senha é a flag do nível anterior.

Nesse nível, utilizaremos novamente o comando que nos permite ler as linhas _human-readable_ em um arquivo, o comando _strings_, mas com o adicional de que precisamos procurar uma linha com um padrão específico. Para tal, utilizaremos também o comando _grep_. Assim:

```text
$ strings data.txt | grep "="
```

