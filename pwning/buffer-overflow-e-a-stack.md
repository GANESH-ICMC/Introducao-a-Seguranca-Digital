# Buffer Overflow e a Stack

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

## Stack \(Pilha\)

Para entender como um ataque de buffer overflow na stack funciona, é necessário entender como a stack funciona ao longo das chamadas de função.

A stack, como o nome diz, é uma pilha. Pode-se imaginar como uma pilha de pratos ou uma pilha de caixas. As operações básicas de uma pilha são empilhar, desempilhar e checar seu topo. Para entender a stack, é importante saber essas duas primeiras operações.

Quando empilha-se algo em uma pilha, coloca-se o novo elemento em cima. Caso vá desempilhar, retira-se o elemento mais ao topo.

Agora vamos ver como isso se aplica na memória stack:

```text
+------------------+
|      Stack       | <-- RSP
|      Frame       |
+------------------+
|    RBP antigo    | <-- RBP
+------------------+
|    RIP antigo    |
+------------------+
```

Na memória stack, há dois registradores que realizam operações nela. Eles são o `RSP` \(ou ESP para sistemas de 32-bits\) e o `RBP` \(ou EBP para sistemas de 32-bits\).

* O RSP é o _stack pointer_ e sua função é guardar o endereço do topo da pilha.
* O RBP é o _base pointer_ e sua função é guardar o endereço da base da pilha.

Com esses dois registradores, é possível saber onde a pilha começa e onde ela termina.

Outro registrador importante de se ter conhecimento é o `RIP` \(ou EIP\). Quando estamos executando um programa, ele está carregado na memória RAM. Para saber qual endereço devemos executar, utiliza-se o RIP, o _instruction pointer_.

Quando uma função é chamada, é possivel ver no assembly da função que a chamou que há a seguinte linha de código:

```text
call <função>
```

Nesse caso,  é o endereço dessa função na memória RAM. O endereço pode ser representado pelo rótulo \(nome\) da função em assembly e é o que iremos encontrar na maioria dos casos caso olharmos o assembly do código no GDB.

Essa linha faz duas ações:

```text
Empilha o RIP atual na stack
RIP = <função>
```

É necessário guardar o RIP atual na stack, pois ao chamar uma função, estamos no meio da execução de uma outra função. Quando acabarmos de executar essa nova função, queremos saber exatamente onde estavamos para continuar o que estavamos fazendo.

Considerando o desenho da stack acima, caso executarmos o `call`, a stack ficará assim:

```text
 Stack antes do call          | Stack depois do call
                              | +------------------+
                              | |   RIP anterior   | <-- RSP
+------------------+          | +------------------+
|      Stack       | <-- RSP  | |      Stack       |
|      Frame       |          | |      Frame       |
+------------------+          | +------------------+
|    RBP antigo    | <-- RBP  | |    RBP antigo    | <-- RBP
+------------------+          | +------------------+
|    RIP antigo    |          | |    RIP antigo    |
+------------------+          | +------------------+
```

Depois disso, se olharmos as primeiras duas linhas do assembly da nova função, veremos as seguintes linhas:

```text
push rbp        # Empilha o RBP
mov rbp, rsp    # RBP = RSP
```

Quando chamamos uma função, criamos uma "nova stack" em cima da nossa stack. Para isso, o endereço do topo atual \(RSP\) é atribuido a nova base \(RBP\). Porém, se apenas fizermos a atribuição, perderemos a referência de onde estava a base da stack anterior quando formos voltar a função anterior. Por isso, antes de atribuir, empilhamos o endereço da base atual \(RBP\) na stack.

Visualmente, ocorrerá o seguinte:

```text
Stack depois do call          |  Stack após o push
                              | +------------------+
                              | |   RBP anterior   | <-- RSP
+------------------+          | +------------------+
|   RIP anterior   | <-- RSP  | |   RIP anterior   |
+------------------+          | +------------------+
|      Stack       |          | |      Stack       |
|      Frame       |          | |      Frame       |
+------------------+          | +------------------+
|    RBP antigo    | <-- RBP  | |    RBP antigo    | <-- RBP
+------------------+          | +------------------+
|    RIP antigo    |          | |    RIP antigo    |
+------------------+          | +------------------+
```

Ao fazer a atribuição:

```text
 Stack após o push            | Stack após atribuição
+------------------+          | +------------------+ <-- RSP
|   RBP anterior   | <-- RSP  | |   RBP anterior   | <-- RBP
+------------------+          | +------------------+
|   RIP anterior   |          | |   RIP anterior   |
+------------------+          | +------------------+
|      Stack       |          | |      Stack       |
|      Frame       |          | |      Frame       |
+------------------+          | +------------------+
|    RBP antigo    | <-- RBP  | |    RBP antigo    |
+------------------+          | +------------------+
|    RIP antigo    |          | |    RIP antigo    |
+------------------+          | +------------------+
```

Para finalizar, caso a nova função utilize variáveis locais, será alocado o número de bytes necessário para essas variáveis, criando um espaço chamado _stack frame_.

Para fins ilustrativos, considere uma função que utilize 16 bytes para variáveis locais, ou seja, 0x10 bytes em hexadecimal. Seguido do push e do mov \(atribuição\), haverá a seguinte linha:

```text
sub rsp, 0x10
```

Como a stack cresce "para baixo", ou seja, do maior endereço para o menor endereço, ao subtrair um valor do _stack pointer_, estamos deixando o RSP mais "alto" na pilha.

Portanto, essa linha teria o seguinte efeito:

```text
Stack após atribuição         |  Stack após alocação
                              | +------------------+
                              | |                  | <-- RSP
                              | |      Stack       |
                              | |      Frame       |
                              | |                  |
+------------------+ <-- RSP  | +------------------+
|   RBP anterior   | <-- RBP  | |   RBP anterior   | <-- RBP
+------------------+          | +------------------+
|   RIP anterior   |          | |   RIP anterior   |
+------------------+          | +------------------+
|      Stack       |          | |      Stack       |
|      Frame       |          | |      Frame       |
+------------------+          | +------------------+
|    RBP antigo    |          | |    RBP antigo    |
+------------------+          | +------------------+
|    RIP antigo    |          | |    RIP antigo    |
+------------------+          | +------------------+
```

Agora que está alocado, podemos atribuir valores a essas variáveis locais. Para fins didáticos, vamos imaginar que essa stack está em um sistema de 64-bits e queremos colocar nesses 16 bytes um `int` \(4 bytes\) e uma `string` de 4 caracteres \(incluindo o '\0'\). No caso da string, será necessário criar um ponteiro `char*` \(8 bytes para sistemas 64-bits\) e o espaço dos 4 caracteres, totalizando 12 bytes para a string.

As variáveis locais dessa função serão:

```text
int var1 = 500;
char var2[4];
```

Vamos considerar também que RBP = 0x7fffffffffff1000 e RSP = 0x7fffffffffff0ff0.

O código em assembly para essas atribuições é:

```text
mov DWORD PTR[rbp-0x10],0x1f4                # 0x1f4 == 500
mov DWORD PTR[rbp-0xc],0x7fffffffffff0ffc    # 0x7fffffffffff0ffc == RBP-0x4
```

Ao redesenhar a stack:

```text
 Stack após alocação          | Stack após atribuição
+------------------+          | +------------------+
|                  | <-- RSP  | |    0x000001f4    | <-- RSP
|      Stack       |          | |    0xffff0ffc    |
|      Frame       |          | |    0x7fffffff    |
|                  |          | |    0x????????    |
+------------------+          | +------------------+
|   RBP anterior   | <-- RBP  | |   RBP anterior   | <-- RBP
+------------------+          | +------------------+
|   RIP anterior   |          | |   RIP anterior   |
+------------------+          | +------------------+
|      Stack       |          | |      Stack       |
|      Frame       |          | |      Frame       |
+------------------+          | +------------------+
|    RBP antigo    |          | |    RBP antigo    |
+------------------+          | +------------------+
|    RIP antigo    |          | |    RIP antigo    |
+------------------+          | +------------------+
```

A região marcada por `0x????????` é o lixo de memória que está na região da string, já que ainda nao escrevemos nada nela. Perceba que o ponteiro _char\*\* está escrito de trás para frente. Isso é porque a maioria das arquiteturas hoje em dia seguem o modelo_ little-endian\*, em que se escreve os bytes do byte menos significativo para o mais significativo. Por enquanto não precisam se preocupar com isso, veremos novamente mais para frente.

Por fim, vamos encerrar essa nova função.

No fim de uma função, haverá as seguintes linhas:

```text
leave
ret
```

A linha `leave` executa as seguintes operações:

```text
RSP = RBP
Desempilha o RBP antigo para RBP
```

A linha `ret` desempilha o RIP anterior para RIP.

Portanto, visualmente:

```text
Stack após atribuição         |   Stack após leave
+------------------+          |                     
|    0x000001f4    | <-- RSP  |      0x000001f4     
|    0xffff0ffc    |          |      0xffff0ffc     
|    0x7fffffff    |          |      0x7fffffff     
|    0x????????    |          |      0x????????     
+------------------+          |                     
|   RBP anterior   | <-- RBP  |     RBP anterior    
+------------------+          | +------------------+
|   RIP anterior   |          | |   RIP anterior   | <-- RSP
+------------------+          | +------------------+
|      Stack       |          | |      Stack       |
|      Frame       |          | |      Frame       |
+------------------+          | +------------------+
|    RBP antigo    |          | |    RBP antigo    | <-- RBP
+------------------+          | +------------------+
|    RIP antigo    |          | |    RIP antigo    |
+------------------+          | +------------------+
```

```text
Stack após leave              |   Stack após ret
                              |                     
     0x000001f4               |      0x000001f4     
     0xffff0ffc               |      0xffff0ffc     
     0x7fffffff               |      0x7fffffff     
     0x????????               |      0x????????     
                              |                     
    RBP anterior              |     RBP anterior    
+------------------+          |                     
|   RIP anterior   | <-- RSP  |     RIP anterior    
+------------------+          | +------------------+
|      Stack       |          | |      Stack       | <-- RSP
|      Frame       |          | |      Frame       |
+------------------+          | +------------------+
|    RBP antigo    | <-- RBP  | |    RBP antigo    | <-- RBP
+------------------+          | +------------------+
|    RIP antigo    |          | |    RIP antigo    |
+------------------+          | +------------------+
```

O conteúdo da stack permanece como lixo de memória após o retorno da função.

E assim, encerramos a chamada da nova função.

