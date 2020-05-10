# Chall

## A luz sempre tem as respostas

A luz lhe diz tudo, basta confiar nela e então a mensagem se revela por si só.

Gibz spxiawih, d jfal ph meuksuemaoexmyqe.

### Dicas:

1. Auto, do gregos autós. Por si mesmo.

### Resolução:

O desafio consiste em usar a cifra AutoKey com a chave “luz”, a resposta é imediata e corresponde a:

Voce entendeu, a flag eh **ganeshautokeyomg**.

Basta então usar **ganeshautokeyomg** para completar o desafio.

## Hmmmm Bacon

00001 00000 00010 01101 01100 00100 00111 00001 01101 01011 00111 00100 01000 01100 00110 10011 10000 01000 10111 00000 00011 00000 00100 00000 00101 01010 00000 00110 00100 00111 00110 00000 01100 00100 10001 00111 10001 01101 10010 00100 01011 01010 01000 01100 00011 10101

### Resolução:

De início, percebemos que o enunciado é, na verdade, uma mensagem criptografada. Precisamos descobrir agora qual cifra foi utilizada para encriptar tal mensagem. Analisando o título, vemos que tem alguma relação com “Bacon”. Além disso, vemos que o ciphertext é dividido em seções de 5 símbolos, podendo apresentar o valor de 0 ou 1. Uma rápida busca no Google nos diz que essas são características da Cifra de Bacon utilizando o alfabeto binário \([https://en.wikipedia.org/wiki/Bacon%27s\_cipher](https://en.wikipedia.org/wiki/Bacon%27s_cipher)\). Para decriptar, basta utilizarmos uma das seguintes tabelas:

| Letter | Code | Binary | Letter | Code | Binary |
| :--- | :--- | :--- | :--- | :--- | :--- |
| A | aaaaa | 00000 | N | abbaa | 01100 |
| B | aaaab | 00001 | O | abbab | 01101 |
| C | aaaba | 00010 | P | abbba | 01110 |
| D | aaabb | 00011 | Q | abbbb | 01111 |
| E | aabaa | 00100 | R | baaaa | 10000 |
| F | aabab | 00101 | S | baaab | 10001 |
| G | aabba | 00110 | T | baaba | 10010 |
| H | aabbb | 00111 | U, V | baabb | 10011 |
| I, J | abaaa | 01000 | W | babaa | 10100 |
| K | abaab | 01001 | X | babab | 10101 |
| L | ababa | 01010 | Y | babba | 10110 |
| M | ababb | 01011 | Z | babbb | 10111 |

| Letter | Code | Binary | Letter | Code | Binary |
| :--- | :--- | :--- | :--- | :--- | :--- |
| A | aaaaa | 00000 | N | abbab | 01101 |
| B | aaaab | 00001 | O | abbba | 01110 |
| C | aaaba | 00010 | P | abbbb | 01111 |
| D | aaabb | 00011 | Q | baaaa | 10000 |
| E | aabaa | 00100 | R | baaab | 10001 |
| F | aabab | 00101 | S | baaba | 10010 |
| G | aabba | 00110 | T | baabb | 10011 |
| H | aabbb | 00111 | U | babaa | 10100 |
| I | abaaa | 01000 | V | babab | 10101 |
| J | abaab | 01001 | W | babba | 10110 |
| K | ababa | 01010 | X | babbb | 10111 |
| L | ababb | 01011 | Y | bbaaa | 11000 |
| M | abbaa | 01100 | Z | bbaab | 11001 |

Com isso, decriptando a mensagem, encontramos: “baconehbomheingurizadaeaflagehganeshsotemlindx”. Portanto, a flag é **ganeshsotemlindx**.


## Terra média

Esta mensagem foi encontrada no meio dos trabalhos de um grande e conhecido escritor da língua inglesa, mas infelizmente está criptografada. A flag é o nome do ser ao qual a quarta linha se refere.

VALYY LXPFK SQL VAY YCRYP IXPFK BPUYL VAY KIE,

KYRYP SQL VAY UONLS CQLUK XP VAYXL ANCCK QS KVQPY,

PXPY SQL GQLVNC GYP, UQQGYU VQ UXY,

QPY SQL VAY UNLI CQLU QP AXK UNLI VALQPY

XP VAY CNPU QS GQLUQL OAYLY VAY KANUQOK CXY.

QPY LXPF VQ LBCY VAYG NCC, QPY LXPF VQ SXPU VAYG,

QPY LXPF VQ MLXPF VAYG NCC NPU XP VAY UNLIPYKK MXPU VAYG.

XP VAY CNPU QS GQLUQL OAYLY VAY KANUQOK CXY.

### Dicas:

1. One ring to rule them all…

### Resolução:

Pela dica \(escritor inglês\) inferimos que se trata de um fragmento de texto escrito em inglês e pelo tamanho das palavras inferimos que se trata de uma cifra de substituição simples, este chall se baseia então em descobrir o que cada caractere significa com tentativa e erro. Comparando a frequência de cada letra do texto com a frequência de letras da língua inglesa inferimos que a letra “Y” do texto deve corresponder à letra “e”, por ser a letra mais comum do alfabeto inglês. O texto passa a ter a forma:

VALee LXPFK SQL VAe eCReP IXPFK BPUeL VAe KIE,

KeReP SQL VAe UONLS CQLUK XP VAeXL ANCCK QS KVQPe,

PXPe SQL GQLVNC GeP, UQQGeU VQ UXe,

QPe SQL VAe UNLI CQLU QP AXK UNLI VALQPe

XP VAe CNPU QS GQLUQL OAeLe VAe KANUQOK CXe.

QPe LXPF VQ LBCe VAeG NCC, QPe LXPF VQ SXPU VAeG,

QPe LXPF VQ MLXPF VAeG NCC NPU XP VAe UNLIPeKK MXPU VAeG.

XP VAe CNPU QS GQLUQL OAeLe VAe KANUQOK CXe.

Vemos que logo a primeira palavra do texto termina com “ee”. Existem em torno de 40 palavras em inglês que terminam com “ee” porém poquíssimas delas são comumente usadas. Três destas palavras seriam “three”, “agree” e “melee”, todas as outras são muito mais incomuns quando comparadas às 3 listadas. Podemos descartar a palavra “melee” pois a letra “e” já foi substituída, se usarmos a palavra “agree” a palavra de 3 letras “VAe” se torna “age” e se usarmos “three” se torna “the”. Como é uma palavra de 3 letras que ocorre diversas vezes ao longo do texto é mais provável que se trate de “the” e com isso inferimos as seguintes relações: “V” = “t”, “A” = “h”, “L” = “r”. O texto se torna então:

three rXPFK SQr the eCReP IXPFK BPUer the KIE,

KeReP SQr the UONrS CQrUK XP theXr hNCCK QS KtQPe,

PXPe SQr GQrtNC GeP, UQQGeU tQ UXe,

QPe SQr the UNrI CQrU QP hXK UNrI thrQPe

XP the CNPU QS GQrUQr Ohere the KhNUQOK CXe.

QPe rXPF tQ rBCe theG NCC, QPe rXPF tQ SXPU theG,

QPe rXPF tQ MrXPF theG NCC NPU XP the UNrIPeKK MXPU theG.

XP the CNPU QS GQrUQr Ohere the KhNUQOK CXe.

Tendo descoberto estas 4 letras é possível inferir várias palavras caso haja familiaridade com a língua inglesa. Alguns exemplos seriam “SQr” = “for”, “QPe” = “one”, “Ohere” = “where”, “thrQPe” = “throne” etc. O texto final deve ser:

three rings for the elven kings under the sky,

seven for the dwarf lords in their halls of stone,

nine for mortal men doomed to die,

one for the dark lord on his dark throne

in the land of mordor where the shadows lie.

one ring to rule them all, one ring to find them,

one ring to bring them all and in the darkness bind them

in the land of mordor where the shadows lie.

Basta agora identificar que se trata da epígrafe de “O Senhor dos Anéis” e o escritor ao qual a dica se refere é J. R. R. Tolkien. O personagem referenciado na quarta linha “... dark lord ...” é Sauron, a flag que soluciona o desafio é então **Sauron**.


## Maquininha temporizadora

Um criptógrafo inventou uma máquina capaz de automaticamente encriptar mensagens que utilizam letras do alfabeto latino. Cada letra corresponde a um número \(1 para A, 2 para B, …, 26 para Z\). Além disso, algumas letras fazem parte de um conjunto especial \(mantido em segredo\), resultando em um comportamento especial da máquina.

A máquina realiza a encriptação letra por letra, em dois passos, sendo que ambas as etapas levam o mesmo tempo \(mesmo intervalo de tempo\) para serem executadas:

1. Se a letra pertence ao conjunto especial, a máquina não realiza a encriptação, adiciona a letra original ao ciphertext e não executa o passo 2. Caso contrário, execute o passo 2.
2. Substitua a letra atual, associada a um número k, por uma letra y, onde y possui o mesmo resto ao dividir por 10 que k. Após isso, adicione a nova letra ao ciphertext.

Sabendo como a máquina funciona, decripte a seguinte mensagem:

Zkhubyds! U fbkg oh chifjyyhckssu.

![](../../.gitbook/assets/image1.png)

### Dicas:

Nenhuma

### Resolução:

Primeiramente, devemos considerar que o enunciado afirma que ambas as etapas são executadas em um mesmo intervalo de tempo \(não necessariamente ao mesmo tempo\). Assim, de acordo com o gráfico, temos que o tempo máximo de encriptação de uma letra é de 2 segundos e podemos deduzir que cada passo leva 1 segundo para ser executado. Portanto, quando leva 1 segundo, apenas o primeiro passo é feito. Quando leva 2 segundos, ambos são executados.

De acordo com o funcionamento da máquina, as letras que só realizam o passo 1 são transferidas para o ciphertext. Assim, temos:

\_\_\_\_b\_\_s! \_ f\_\_g \_h c\_i\_\_\_\_h\_\_ss\_.

Ao realizar o segundo passo com as letras restantes, obtemos as letras possíveis para substituir as encriptadas:

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| F | **a** |  | **a** |  | **e** |  |  |  |  | **A** |  |  |  |  |  |  |  |  |  |  |  |  |  |  | e | **e** |  |  |  |  |  | **a** |
| **P** | u |  | k |  | o |  |  |  |  | K |  |  |  | **a** |  |  | **e** |  |  |  |  |  |  |  | **o** | o |  |  | **a** |  |  | k |
| Z | k | h | u | **b** | y | d | **s** | ! |  | U |  | **f** | b | k | **g** |  | o | **h** |  | **c** | h | **i** | f | j | y | y | **h** | c | k | **s** | **s** | u |
|  |  | **r** |  |  |  | **n** |  |  |  |  |  |  | **l** | u |  |  | y |  |  |  | **r** |  | **p** | **t** |  |  |  | **m** | u |  |  |  |
|  |  |  |  |  |  | x |  |  |  |  |  |  | v |  |  |  |  |  |  |  |  |  | z |  |  |  |  | w |  |  |  |  |

Ao separar as letras possíveis para cada letra encriptada, além de utilizar um conhecimento prévio do português, podemos deduzir a frase como:

Parabens! A flag eh **criptoehmassa**.

## Purê de Mary

No século XVI, criptografia era utilizada por governantes para enviar mensagens sem que elas tivessem seu conteúdo descoberto. Mary, Rainha da Escócia, usou uma forma de encriptação para se comunicar com seus apoiadores enquanto estava presa na Inglaterra. Em um episódio conhecido como Babington Plot, ao utilizar análise de frequência, foi possível descobrir o significado real de cada caractere na carta.

Com as informações acima, decifre o trecho abaixo e descubra a flag constituída pelo objeto que representa o sinal utilizado por Mary:

![](../../.gitbook/assets/image2.png)

### Dicas:

Nenhuma

### Resolução:

Como dito no enunciado, foi utilizado uma cifra de substituição simples, portanto é necessário fazer uma análise de frequência sobre cada símbolo e substituí-los pelos caracteres mais frequentes do **inglês** até obter um texto plausível. Por fim, obtendo:

To anthony babbington,  
 i agree that you  
 can murder queen  
 elizabeth after  
 getting the signal  
 represented by potato.  
 From Mary.

Assim, vemos que a flag é **potato**.


## Visitando novas bases 3

120 141 162 141 142 303 251 156 163 054 040 166 157 143 303 252 040 162 145 141 154 155 145 156 164 145 040 303 251 040 165 155 040 145 156 164 145 156 144 145 144 157 162 040 144 145 040 142 141 163 145 163 040 156 165 155 303 251 162 151 143 141 163 041 040 101 040 146 154 141 147 040 303 251 040 107 141 156 145 163 150 173 060 143 164 064 154 175

### Dicas:

1.  Símbolo do infinito

### Resolução:

O título sugere que a mensagem está codificada em uma base diferente da usual. Ao ver a mensagem, percebemos que ela possui apenas algarismos entre 0 e 7, e estes estão agrupados em grupos de 3. Com isso, tiramos a conclusão de que  a mensagem está codificada em base octal. Decodificando a mensagem, encontramos:

Parabéns, você realmente é um entendedor de bases numéricas! A flag é **Ganesh{0ct4l}**. 

Obs: Percebe-se que a base é 8 = 2<sup>3</sup>. Ou seja, o título do desafio se refere ao expoente da potência. Esse raciocínio pode ser utilizado para facilitar a resolução dos outros desafios relacionados. 
