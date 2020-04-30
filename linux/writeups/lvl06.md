# Bandit 6
#### O objetivo do nível é ler um arquivo em algum lugar do server que tenha 33 bytes de tamanho, pertença ao grupo bandit6 e ao user bandit7
```
$ ssh bandit6@bandit.labs.overthewire.org -p 2220
```
A senha é a flag do nível anterior.

Nesse nível, ainda utilizaremos o comando *find*, porém com duas opções diferentes: *-group* e *-user*, com nomes autoexplicativos. Mas, como especificado na descrição do desafio, o arquivo está em algum lugar do servidor. Logo, precisaremos mudar o lugar onde a busca recursiva começa para "/", que é o diretório raiz, fazendo, assim, o comando *find* pesquisar em todos os diretórios.
```
$ find / -user bandit7 -group bandit6
```
O comando acima responderá com várias saídas, sendo que o único arquivo retornado é o que contém a flag.

