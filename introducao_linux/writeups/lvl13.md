# Nível 13

## O objetivo do nível é se conectar ao bandit 14 utilizando uma chave privada de ssh

```text
$ ssh bandit13@bandit.labs.overthewire.org -p 2220
```

A senha é a flag do nível anterior.

Ao conectarmos no bandit13, vemos a chave privada de SSH mencionada no problema: o arquivo _sshkey.private_. Para nos conectarmos via SSH usando uma chave privada, usaremos a opção _-i_ do comando _SSH_. Assim:

```text
$ ssh -i sshkey.private bandit14@localhost
```

Agora só preciamos ler o arquivo que contém a senha:

```text
$ cat /etc/bandit_pass/bandit14
```

