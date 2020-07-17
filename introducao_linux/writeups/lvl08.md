# Nível 08

## O objetivo do nível é ler uma linha em um arquivo que só ocorre uma única vez

```text
$ ssh bandit8@bandit.labs.overthewire.org -p 2220
```

A senha é a flag do nível anterior.

Dando uma olhada nos comandos recomendados pelo próprio site do bandit, vemos que o comando _uniq_ parece adequado para resolver esse problema. Ao olhar seu manual, entretanto, é dito que _uniq_ filtra apenas linhas adjacentes repetidas. Nesse caso, para organizar as linhas tal que as cópias fiquem próximas umas as outras, de modo que o comando _uniq_ seja efetivo, usaremos outro comando recomendado, que é o _sort_, que, segundo seu manual, organiza as linhas de um texto em ordem.

Usaremos o _pipe_ novamente para aplicar os comandos sobre a saída de outros comandos e assim achar a flag:

```text
$ cat data.txt | sort | uniq -u
```

Onde _sort_ será aplicado à saída de _cat_, e, por fim, _uniq_ será aplicado à saída de _sort_, que, por meio de sua opção _-u_, printará apenas as linhas não repetidas, nesse caso, a flag.

