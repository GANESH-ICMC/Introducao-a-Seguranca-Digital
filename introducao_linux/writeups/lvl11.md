# Nível 11

## O objetivo do nível é ler uma string onde cada letra foi rotacionada

```text
$ ssh bandit11@bandit.labs.overthewire.org -p 2220
```

A senha é a flag do nível anterior.

Nesse nível, o comando mais apropriado para resolver o problema é o comando `tr`. Lendo seu manual, podemos ver que ele "traduz" caracteres, ou seja, troca de um SET para outro. Como descrito no problema, a string foi rotacionada em 13 posições. Logo, precisamos traduzir do set atual para o alfabeto original, nesse caso, desrotacionar 13 vezes. Entretando, como o alfabeto tem 26 caracteres, basta rotacionar novamente em 13 posições.

Assim, temos que o primeiro set será o alfabeto, tanto maiúsculas quanto minúsculas. Logo: A-Za-z, onde o comando irá concatenar todas as letras de A até Z e de a até z.

O segundo set será o set anterior, rotacionado 13 posições para frente, ou seja, A se torna N, B se torna O, e assim sucessivamente, até que M se torna Z, e N se torna A, reiniciando o alfabeto. Assim temos o segundo set: N-ZA-Mn-za-m.

Para melhor visualizar os sets: SET 1: ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz SET 2: NOPQRSTUVWXYZABCDEFGHIJKLMnopqrstuvwxyzabcdefghijklm

Portanto, o comando final ficará:

```text
$ cat data.txt | tr A-Za-z N-ZA-Mn-za-m
```

