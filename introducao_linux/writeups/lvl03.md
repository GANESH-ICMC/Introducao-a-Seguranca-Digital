# Nível 03

## O objetivo do nível é ler um diretório oculto no servidor

```text
$ ssh bandit3@bandit.labs.overthewire.org -p 2220
```

A senha é a flag do nível anterior.

Nesse nivel, é descrito que o arquivo com a flag do próximo nível está no diretório **inhere**. Mas, ao utilizar o comando `$ ls` dentro de **inhere**, nada é listado. Como o arquivo está oculto, é necessário adicionar uma opção ao comando ls, que liste arquivos ocultos \(arquivos que comecem com "."\). Ao rodar o comando `$ man ls`, vemos que a opção -a \(ou --all\) não ignora arquivos que comecem com ".", ou seja, arquivos ocultos. `$ ls -a` revelará o arquivo oculto, cujo nome será utilizado no comando _cat_ para conseguir a flag do nível.

