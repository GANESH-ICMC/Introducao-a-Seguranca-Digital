# Buffer Overflow

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
