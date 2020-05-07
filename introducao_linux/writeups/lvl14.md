# Nível 14

## O objetivo do nível é submeter a senha do nível atual na porta 30000 em localhost

```text
$ ssh bandit14@bandit.labs.overthewire.org -p 2220
```

A senha é a flag do nível anterior.

Com um problema bem direto, apenas precisaremos conectar a porta e submeter a senha. Usaremos o _netcat_ para isso:

```text
$ nc localhost 30000
```

Copiando e colando a flag, receberemos a flag do próximo nivel.

