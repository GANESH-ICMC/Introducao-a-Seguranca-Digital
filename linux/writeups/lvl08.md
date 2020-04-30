# Bandit 8
#### O objetivo do nível é ler uma linha em um arquivo que só ocorre uma única vez
```
$ ssh bandit8@bandit.labs.overthewire.org -p 2220
```
A senha é a flag do nível anterior.

Dando uma olhada nos comandos recomendados pelo próprio site do bandit, vemos que o comando *uniq* parece adequado para resolver esse problema. Ao olhar seu manual, entretanto, é dito que *uniq* filtra apenas linhas adjacentes repetidas. Nesse caso, para organizar as linhas tal que as cópias fiquem próximas umas as outras, de modo que o comando *uniq* seja efetivo, usaremos outro comando recomendado, que é o *sort*, que, segundo seu manual, organiza as linhas de um texto em ordem.

Usaremos o *pipe* novamente para aplicar os comandos sobre a saída de outros comandos e assim achar a flag:
```
$ cat data.txt | sort | uniq -u
```
Onde *sort* será aplicado à saída de *cat*, e, por fim, *uniq* será aplicado à saída de *sort*, que, por meio de sua opção *-u*, printará apenas as linhas não repetidas, nesse caso, a flag.
