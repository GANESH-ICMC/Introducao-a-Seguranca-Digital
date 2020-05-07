# Nível 15

## O objetivo do nível é se conectar na porta 30001 a partir do bandit15 em localhost usando SSL encryption

```text
$ ssh bandit15@bandit.labs.overthewire.org -p 2220
```

A senha é a flag do nível anterior.

Para se conectar usando SSL, usaremos o comando _openssl_. Como seremos o cliente, que irá se conectar ao servidor, usaremos a opção "s\_client", e, para passarmos o endereço, usaremos "-connect localhost:30001". Assim:

```text
$ openssl s_client -connect localhost:30001
```

Colando a senha do nível atual, receberemos a flag.

