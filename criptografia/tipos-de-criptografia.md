# Tipos de Criptografia

## Cifras de transposição

É uma forma de criptografia do qual os símbolos do alfabeto do texto plano são permutados de acordo com uma regra, gerando o texto cifrado. A forma de decriptação é a permutação inversa.

Diferenças de transposição e substituição

SUBSTITUIÇÃO - POSIÇÃO PRESERVADA, ALFABETO ALTERADO

TRANSPOSIÇÃO - POSIÇÃO ALTERADA, ALFABETO PRESERVADO

Ex.

```text
Texto plano =         Elefante     

Substituição =         Fmfgborf

Transposição =     etnafelE
```

### Transposição por coluna:

Encriptação: escrevemos a chave na primeira linha da tabela e o texto plano nas linhas seguintes, em seguida, lemos o texto na vertical seguindo a ordem alfabética das letras da chave.

```text
Decriptação: escrevemos o texto cifrado na tabela na direção vertical seguindo a ordem alfabética das letras da chave (primeira linha), em seguida lemos o texto na horizontal na direção usual.

**Exemplo:**

    Texto plano: Somos o Ganesh

    Chave: crivo
```

| C | R | I | V | O |
| :--- | :--- | :--- | :--- | :--- |
| S | o | m | o | s |
|  | o |  | G | a |
| n | e | s | h | \_ |

```text
    Texto cifrado: S nm ssa_ooeoGh
```

### Como identificar cifras

Nas cifras de substituição, ao substituirmos qualquer letra, há uma alta probabilidade de que a letra resultante seja uma consoante, pois há mais consoantes do que vogais em nosso alfabeto. Porém, a frequência de vogais nas palavras do português é próxima à de consoantes, apesar de existirem menos vogais no alfabeto. Portanto, conseguimos distinguir entre cifras de substituição e transposição. Se, no texto cifrado, aparecer muito mais consoantes do que vogais, concluímos que foi utilizada uma cifra de substituição; caso contrário, concluímos que foi utilizada uma cifra de transposição.

## Cifras da antiguidade.

### Atbash

Uma das primeiras cifras de substituição. É vista em passagens da bíblia como em \[Jeremias 25:26 - "O rei de Sheshach beberá depois deles" - Sheshach, que significa Babilônia em Atbash \(בבל bbl → ששך ššk\)\].

```text
Trata-se de uma substituição monoalfabética de deslocamento 0 com o alfabeto do texto cifrado na ordem inversa do alfabeto do texto plano. Exemplo com o alfabeto latino:
```

A \|B \|C \|D \|E \|F \|G \|H \|I \|J \|K \|L \|M \|N \|O \|P \|Q \|R \|S \|T \|U \|V \|W \|X \|Y \|Z

Z \|Y \|X \|W \|V \|U \|T \|S \|R \|Q \|P \|O \|N \|M \|L \|K \|J \|I \|H \|G \|F \|E \|D \|C \|B \|A

Ganesh -&gt; Tzmvhs

### Cifra de César

```text
Foi uma cifra de substituição monoalfabética utilizada pelo general Julio César em Roma. 
```

Exemplo com o alfabeto latino:

A\|B\|C\|D\|E\|F\|G\|H\|I\|J\|K\|L\|M\|N\|O\|P\|Q\|R\|S\|T\|U\|V\|W\|X\|Y\|Z

C\|D\|E\|F\|G\|H\|I\|J\|K\|L\|M\|N\|O\|P\|Q\|R\|S\|T\|U\|V\|W\|X\|Y\|Z\|A\|B

Deslocamento 2

Ganesh -&gt; Icpguj

### Polybius Square

Um dispositivo inventado por Cleoxenus e Democleitus e aperfeiçoado por Polybius, cujo propósito era dividir os símbolos do texto plano para que pudessem ser representados por um conjunto menor de símbolos.

Inicialmente, Polybius sugeriu que os símbolos poderiam ser usados para transmitir mensagens com pares de tochas. Além disso, também foi usada na forma de "knock code" para transmitir mensagens em prisões a partir de barulhos em canos e paredes.

A tabela a seguir é utilizada para encriptar e decriptar mensagens:

![](https://i.imgur.com/8C8J1Zx.jpg)

**Exemplo:**

Texto plano: G \|a \|n \|e \|s \|h \|

Texto cifrado: 22\|11\|33\|15\|43\|23\|

### Outras

Na Índia, há relatos de duas formas de cifras chamadas de Kautiliyam e Mulavediya. Na Kautiliyam, as substituições de letras da cifra são baseadas nas relações fonéticas, tais como vogais se tornando consoantes, e vice-versa. Na Mulavediya, o alfabeto da cifra consiste em pares de letras e a utilização de recíprocas.

## Medieval

Segundo David Kahn, a criptografia moderna teve origem com os árabes, que foram o primeiro povo a documentar sistematicamente métodos criptanalíticos. Al-Khalil \(717-786\) escreveu o primeiro livro com registros do primeiro uso de permutações e combinações para listar todas as possíveis palavras árabes com e sem vogais.

Textos cifrados feitos por uma cifra clássica podem revelar informações estatísticas sobre o plaintext, o que pode ser usado para quebrar a cifra usada. Com a descoberta da análise por frequência, pelo matemático árabe Al-Kindi no século IX, quase todas as cifras poderiam ser quebradas com métodos baseados nessa forma de análise. A frequência de uso de letras em um alfabeto, por exemplo, é uma forma de explorar a previsibilidade de tais cifras.

Ex no alfabeto da língua portuguesa:

![](https://i.imgur.com/LxBGNea.png)

A análise de frequência foi uma forma eficiente de quebrar a proteção de mensagens até a criação das cifras polialfabéticas, sendo descrita pela primeira vez no trabalho de Al-Qalqashandi \(1355–1418\), baseado nos estudos de Ibn al-Durayhim \(1312–1359\), descrevendo uma cifra polialfabética na qual cada plaintext é relacionado com mais de um substituto. Também foi descrita por Leon Battista Alberti em, aproximadamente, 1467, sendo que ele também inventou o que, possivelmente, foi o primeiro dispositivo automático para gerar cifras.

### A cifra de Vigenère

É uma cifra polialfabética cuja chave é uma palavra responsável por especificar o deslocamento, caractere a caractere, do texto cifrado.

Muitas pessoas tentaram quebrar a cifra, mas até 3 séculos depois de criada, ninguém havia obtido sucesso. No entanto, em 1863, Friedrich Kasiski foi o primeiro a publicar um método de ataque da cifra de Vigenère.

O ataque ocorre quando a chave é menor que o texto plano, ocasionando colisões \(deslocamentos iguais\) ao longo do texto cifrado, sendo plausível de análise criptográfica.

A tabela a seguir é utilizada para facilitar a encriptação e decriptação, dado um texto plano e uma chave.

![](https://i.imgur.com/FDqEB9w.png)

**Exemplo:**

Texto: SomosOGanesh

Chave: cripto

Encriptação: Para encriptar a primeira letra, olhamos a primeira linha e encontramos a coluna da letra S \(do texto plano\). Posteriormente, olhamos a primeira coluna e encontramos a linha da letra c \(da chave\). A primeira letra do texto cifrado será o cruzamento entre essa linha e essa coluna, com isso encontramos a letra U.

\|S\|o\|m\|o\|s\|O\|G\|a\|n\|e\|s\|h\|

\|c\|r\|i\|p\|t\|o\|c\|r\|i\|p\|t\|o\|

```text
Texto cifrado: UfudlCIrvtlv

Decriptação: O processo é semelhante ao da encriptação, porém utilizando o texto cifrado e a chave.
```

### A cifra AutoKey

```text
É uma melhoria da cifra de Vigenère de modo a garantir que a chave sempre tenha o mesmo tamanho do texto plano, a fim de prover maior segurança (com essa cifra não é possível realizar ataques estatísticos). Para isso, utilizamos uma palavra de C caracteres que será usada para compor o início da chave, sendo o restante da chave composta pelos primeiros N-C caracteres do texto plano (que possui tamanho N). 

**Exemplo:**

Texto: SomosOGanesh

Palavra: Key

Chave: KeySomosOGan

Encriptação:

               |S|o|m|o|s|O|G|a|n|e|s|h|

               |K|e|y|S|o|m|o|s|O|G|a|n|
```

Texto cifrado:\|C\|s\|k\|g\|g\|A\|U\|s\|b\|k\|s\|u\|

```text
Decriptação:

             |C|s|k|g|g|A|U|s|b|k|s|u|

             |K|e|y|[...]

 Texto plano:|S|o|m|[...]

Tendo acesso às primeiras 3 letras do texto plano, podemos continuar preenchendo a chave a fim de decriptar o texto cifrado.
```

## Cifras contemporâneas

Até o século XX, criptografia estava focada com linguística e padrões lexicográficos. Desde então, houve uma alteração na ênfase, pois, atualmente, criptografia utiliza de artifícios matemáticos para garantir a segurança de suas cifras, o que é possível devido ao grande desenvolvimento dos computadores, que são capazes realizar diversos processos em um curto intervalo de tempo.

Além disso, também há pesquisas baseadas no relacionamento entre problemas criptográficos e física quântica.

### Esteganografia.

A esteganografia \(do grego ‘escrita escondida’\) é o uso de de técnicas para ocultar a existência de uma mensagem dentro da outra, uma forma de segurança por obscurantismo. A diferença entre esteganografia e criptografia é que a primeira preocupa-se em ocultar a existência da mensagem, e a segunda o seu significado.

### Método NULL

A simples representação também remete à esteganografia, que é uma técnica para omitir uma mensagem dentro de outra, com o objeto de fazer com que uma forma escrita seja camuflada em outra a fim de mascarar sua própria existência. Uma técnica simples de esteganografia é o método NULL, no qual a letra do meio de cada palavra da mensagem original compõe a mensagem que se deseja esconder.

