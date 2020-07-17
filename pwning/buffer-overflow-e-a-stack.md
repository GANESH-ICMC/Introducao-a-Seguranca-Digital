# Buffer Overflow

## Buffer Overflow

Buffer Overflow, também chamado de _Buffer Overrun_, é uma anomalia em um programa em que, ao escrever dados em um buffer \(armazenamento temporário de dados\), a escrita ultrapassa o tamanho do buffer e começa a escrever nos espaços adjacentes.

Quando começamos a programar em C, é muito comum usarmos o seguinte _statement_ para ler strings:

`scanf("%s", str);`

Porém, quando usamos dessa forma, não especificamos quantos caracteres devemos ler.

Se lermos uma quantidade de caracteres maior que o tamanho da alocação que fizemos para o buffer da string, nosso programa pode se comportar de formas estranhas, como por exemplo causar um erro chamado **segmentation fault**.

### Segmentation Fault

Segmentation fault \(falha de segmentação\), também conhecido como _segfault_ ou _access violation_, é uma falha causada por um acesso indevido a uma posição de memória protegida.

Os segmentos de memória possuem diferentes tipos de permissões atreladas a elas. Os três tipos de permissão são:

* Leitura \(Read\)
* Escrita \(Write\)
* Execução \(Execution\)

Caso o programa tente acessar um segmento da memória sem a devida permissão, ocorre o _segfault_.

Por exemplo, digamos que uma certa região da memória está marcada para apenas leitura. Se o programa tentar escrever algo nessa região da memória, será causado o _segmentation fault_.

### Algumas funções comuns em C que permitem Buffer Overflow

* scanf\(\) com %s e suas variações
* gets\(\)
* strcpy\(\)
* strcat\(\)
* sprintf\(\)

Lembrando também que funções supostamente seguras como fgets\(\) com um limite de caracteres errado também pode causar buffer overflow.

### Tipos de Buffer Overflow

Há certas peculiaridades do local da memória em que o buffer está armazenado que podem causar comportamentos especiais em um buffer overflow. Note que a organização desses locais pode variar dependendo da implementação.

#### Stack Buffer Overflow

Um ataque de buffer overflow na stack costuma utilizar certas características da stack, como por exemplo ela crescer para baixo e possuir o endereço de retorno da função salvo na chamada da função. Essa última característica pode permitir que um ataque de buffer overflow possa mudar o fluxo do programa e até executar código arbitrário.

#### Heap Overflow

Heap Overflow, conhecido também como _Heap Overrun_, é um buffer overflow na memória Heap. Ataques de heap overflow costumam involver a corrupção de valores do cabeçalho de chunks \(regiões de memória alocadas ou desalocadas\) da heap.

## Stack Buffer Overflow

Vamos ver o que um buffer overflow na stack pode causar de comportamento anômalo.

```text
int var1 = 500;
char var2[4];
```

```text
+------------------+        
|    0x000001f4    | <-- RSP 
|    0xffff0ffc    |         
|    0x7fffffff    |        
|    0x????????    |        
+------------------+        
|   RBP anterior   | <-- RBP
+------------------+        
|   RIP anterior   |        
+------------------+        
|      Stack       |        
|      Frame       |        
+------------------+        
|    RBP antigo    |        
+------------------+        
|    RIP antigo    |        
+------------------+
```

Utilizando essa chamada como exemplo, em que `RBP = 0x7fffffffffff1000` e `RSP = 0x7fffffffffff0ff0`, se antes da função retornar, fosse lido um valor para a string, a stack estaria assim:

```text
Leitura de 3 caracteres 'A' (0x41) finalizado com '\0'
+------------------+        
|    0x000001f4    | <-- RSP 
|    0xffff0ffc    |         
|    0x7fffffff    |        
|    0x00414141    |        
+------------------+        
|   RBP anterior   | <-- RBP
+------------------+        
|   RIP anterior   |        
+------------------+        
|      Stack       |        
|      Frame       |        
+------------------+        
|    RBP antigo    |        
+------------------+        
|    RIP antigo    |        
+------------------+
```

O espaço de memória para a string que havia sido alocada e continha lixo agora passa a guardar 3 'A' e um '\0', ou seja, 0x00414141.

Mas se estivermos lendo com o seguinte _statement_:

`scanf("%s", var2);`

...não estamos especificando o número máximo de caracteres a serem lidos.

O que aconteceria se alguem digitasse "ABCDEFG"?

**Tabela ASCII:**

| Caractere | Hexadecimal |
| :---: | :---: |
| '\0' | 0x00 |
| 'A' | 0x41 |
| 'B' | 0x42 |
| 'C' | 0x43 |
| 'D' | 0x44 |
| 'E' | 0x45 |
| 'F' | 0x46 |
| 'G' | 0x47 |

Memória:

```text
+------------------+        
|    0x000001f4    | <-- RSP 
|    0xffff0ffc    |         
|    0x7fffffff    |        
|    0x44434241    |        
+------------------+        
|    0x00474645    | <-- RBP
+------------------+        
|   RIP anterior   |        
+------------------+        
|      Stack       |        
|      Frame       |        
+------------------+        
|    RBP antigo    |        
+------------------+        
|    RIP antigo    |        
+------------------+
```

Como podemos ver, a posição de memória que guardava o RBP anterior foi corrompida. Se retornassemos da função, o RBP iria para a posição `0x00474645`, o que talvez possa causar problemas na execução do programa.

E se colocassemos mais 4 caracteres? Para a string "ABCDEFGHIJK", teriamos:

```text
+------------------+        
|    0x000001f4    | <-- RSP 
|    0xffff0ffc    |         
|    0x7fffffff    |        
|    0x44434241    |        
+------------------+        
|    0x48474645    | <-- RBP
+------------------+        
|    0x00515049    |        
+------------------+        
|      Stack       |        
|      Frame       |        
+------------------+        
|    RBP antigo    |        
+------------------+        
|    RIP antigo    |        
+------------------+
```

Nós corrompemos agora o endereço de retorno \(RIP anterior\) também. Mas espera, então após retornar dessa função, será executado a instrução com o endereço `0x00515049`? **Exatamente.** Mas e se essa região não for uma região com permissões para execução? **Nesse caso, teremos um `segmentation fault`.**

Agora vamos pensar por outro lado, e se a região para qual o RIP foi mandado for uma região executável, como por exemplo a região de uma função? **Nesse caso, as instruções nessa região seriam executadas.**

Se fizermos uma engenharia reversa do programa e acharmos o endereço das funções, poderiamos executá-las arbitrariamente com um buffer overflow. Porém, provavelmente o endereço conterá caracteres que não conseguiriamos escrever com um teclado, como por exemplo os caracteres da tabela ASCII de 0 a 31. Nesse caso, poderiamos usar o comando `echo` para escrever esses bytes.

Vamos tentar escrever "ABC" usando o `echo` e as representações dos três caracteres em hexadecimais.

Pela tabela ASCII, 'A' é o caractere `0x41`, 'B' é o `0x42` e 'C' é o `0x43`. O comando `echo` no Terminal para imprimir esses três caracteres seria o seguinte:

`echo -ne '\x41\x42\x43'`

* `echo` imprime a mensagem passada como argumento
* `-e` permite o uso de caracteres de escape com o `\`, igual strings em C
* `-n` faz com que ele não termine com um `\n`

Juntando `-e` e `-n` forma o `-ne`. Assim como em C, para representarmos um caractere de escape dado em hexadecimal, usamos `\x` seguido do número hexadecimal dele.

Um detalhe que precisamos nos atentar ao escrever um endereço ou qualquer outro dado que não seja uma string é que esse dado provavelmente deve estar na representação **little-endian**.

Little-endian é uma representação que começa do byte menos significativo para o mais significativo. Por exemplo, uma representação do inteiro `1` na memória seria `0x00000001`. Porém, o processador leria e escreveria os bytes na seguinte ordem:

`0x01` `0x00` `0x00` `0x00`

Portanto, para escrever um dado como `0x01234567`, teríamos que escrever os bytes na seguinte ordem:

`0x67` `0x45` `0x23` `0x01`

Para escrever esse dado usando `echo`, fariamos assim:

`echo -ne '\x67\x45\x23\x01'`

No exemplo anterior, se quisessemos que o endereço de retorno fosse `0x01234567`, teríamos que escrever qualquer coisa nos 4 bytes do buffer e nos 4 bytes do RBP anterior e por fim escrever o endereço em si. O comando seria:

`echo -ne 'AAAAAAAA\x67\x45\x23\x01'`

Para redirecionar a saida do echo para a entrada do programa \(stdin\), poderiamos usar o `|`. Assim:

`echo -ne 'AAAAAAAA\x67\x45\x23\x01' | ./meuprograma`

Ou também escrever esses dados a serem enviados \(payload\) em um arquivo e redirecioná-lo para o programa:

`echo -ne 'AAAAAAAA\x67\x45\x23\x01' > payload.txt` `./meuprograma < payload.txt`

Esse segundo método é especialmente útil quando estamos usando o gdb, já que não conseguimos usar o \| dentro dele. No gdb, o comando para redirecionar esse `payload.txt` seria:

`run < payload.txt`

Dessa forma, temos todas as ferramentas necessárias para explorar um stack buffer overflow.

