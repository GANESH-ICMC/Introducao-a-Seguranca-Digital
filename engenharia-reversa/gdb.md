---
description: Um manual de referência para o gdb
---

# GDB

Gdb é o acrônimo para Gnu Project Debugger. Ele é, como o nome diz, um debugger \(depurador\), que pode ser utilizado em engenharia reversa para obter o assembly e analisar arquivos binários.

### Rodando e obtendo o Assembly \(Disassembling\)

Para abrir o programa, execute:

```text
gdb nomeDoPrograma
```

Por padrão, o gdb utiliza a sintaxe AT&T. Como nós vamos utilizar principalmente a sintaxe da Intel, podemos alterar usando:

```text
set disassembly-flavor intel
```

Para obter o assembly de uma função \(por exemplo, a 'main'\), devemos usar:

```text
disassemble main
```

É importante notar que o programa será mostrado do jeito que está em memória, porém podemos utilizar outros softwares para visualizar melhor o fluxo do programa.

### GDB - Principais Comandos

Apertar somente 'Enter' é equivalente a digitar e rodar o último comando novamente. \(é bem útil quando precisamos repetir o mesmo comando diversas vezes\).

#### Controle de Fluxo

* `run arg1, arg2...`   

```text
     Roda o programa, passando os argumentos arg1, arg2... (pode ser utilizado sem os argumentos também)
```

* `break *address`   

```text
     Define um breakpoint no endereço dado. Pode também ser utilizado passando o nome da função ao invés do endereço
```

* `del`   

```text
     Remove todos os breakpoints
```

* `si`   

```text
     Executa a instrução atual
```

* `ni`   

```text
     Igual o si, porém não mostra a execução de chamadas de função (caso a instrução seja uma chamada de função, ele continua executando até o retorno da chamada)
```

* `set $eax=x`   

```text
     Define o valor do registrador \(eax por exemplo\) para o valor dado 'x'
```

* `define hook-stop`   

```text
     Define uma ação para acontecer sempre que a execução parar (um 'stop'), como o exemplo:
```

```text
  define hook-stop
  info registers
  x/24wx $esp
  x/2i $eip
  end
```

#### Registradores

* `info registers`   

```text
     Mostra o valor dos registradores do programa
```

* `x/wx $reg`   

```text
     Mostra o conteúdo de "reg" em hexadecimal
```

* `x/s $reg`   

```text
     Mostra o conteúdo de "reg" em ascii
```

* `x/24wx $esp`    

```text
     Mostra parte da stack do programa \(24 words, no exemplo\)
```

* `x/2i $eip`   

```text
     Mostra as próximas duas instruções
```

* `x NomeDaFunção`   

```text
     Mostra o endereço da função
```

* `p NomeDaFunção`   

```text
     Mostra o endereço e o tipo de retorno da função
```

* `info proc mappings`   

```text
     Mostra o mapa da memória
```

