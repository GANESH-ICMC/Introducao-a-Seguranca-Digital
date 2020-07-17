# Nível 04

## O objetivo do nível é conseguir a flag a partir do único arquivo legível para humanos

```text
$ ssh bandit4@bandit.labs.overthewire.org -p 2220
```

A senha é a flag do nível anterior.

Na pasta **inhere** no servidor, é possível ver vários arquivos, entretando, nem todos são _human-readable_. Uma possibilidade de resolver esse desafio é utilizar o comando _cat_ individualmente em cada arquivo até achar o arquivo que retorne a flag, nesse caso, `$ cat ./-file07`. Entretando, essa solução pode ser muito mais demorada se feita em uma pasta que contém muito mais arquivos.

Uma solução mais otimizada seria procurar strings em todos os arquivos ao mesmo tempo utilizando o comando _strings_ e o metacaracter "?", que é um curinga para um único caracter. Assim, o comando ficará:

```text
$ strings ./-file0?
```

[Post para saber mais sobre metacaracteres](https://www.lifewire.com/linux-metacharacters-using-them-2192773)

