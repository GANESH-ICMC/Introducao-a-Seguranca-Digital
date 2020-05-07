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

