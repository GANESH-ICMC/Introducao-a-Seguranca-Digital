# Nível 12

## O objetivo do nível é ler um arquivo que foi compactado diversas vezes

```text
$ ssh bandit12@bandit.labs.overthewire.org -p 2220
```

A senha é a flag do nível anterior.

Primeiro iremos criar um diretório na /tmp, chamaremos de Ganesh. Depois copiaremos data.txt para esse diretório. Dessa forma, poderemos alterar arquivos livremente, pois não temos as permissões necessária para isso na pasta atual. Assim:

```text
$ mkdir /tmp/ganesh
$ cp data.txt /tmp/ganesh
$ cd /tmp/ganesh
```

Primariamente, iremos reverter o hexdump de volta para binário. Para isso, usaremos o comando _xxd_, e a sua opção -r, para reverter.

```text
$ xxd -r data.txt > arquivo.bin
```

Verificando qual o tipo do arquivo gerado com `$ file arquivo.bin`, perceberemos que é um arquivo do tipo gzip. Embora o Linux e a maioria de seus programas utilizem os [magic numbers](http://www.linfo.org/magic_number.html) em detrimento das extensões, o gzip considera também a extensão do arquivo. Logo, renomearemos o arquivo para colocar a extensão do gzip, .gz, e o descompactaremos:

```text
$ mv arquivo.bin arquivo.gz
$ gzip -d arquivo.gz
```

Utilizando o comando file novamente, veremos que o arquivo é um arquivo do tipo bzip2, assim, renomearemos para sua extensão, .bz2, e o descompactaremos:

```text
$ mv arquivo arquivo.bz2
$ bzip2 -d arquivo.bz2
```

A partir daqui, o processo é o mesmo. Usando _file_ para saber os tipos antes \(se é do tipo gzip, tar, etc\), os comandos ficarão:

```text
$ mv arquivo arquivo.gz
$ gzip -d arquivo.gz

$ tar -xvf arquivo

$ tar -xvf data5.bin

$ tar -xvf data6.bin

$ mv data8.bin data8.gz
$ gzip -d data8.bin
```

Finalmente, temos um arquivo do tipo ASCII text, usando _cat_ no arquivo, teremos a flag.

