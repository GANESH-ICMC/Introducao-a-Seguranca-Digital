# Guia de Python para criptografia

## **Introdução**

Python está entre as linguagens de programação mais utilizadas da atualidade, dentre os principais motivos estão: legibilidade, simplicidade e flexibilidade. Especialmente para criptografia, Python inclui, por padrão, muitas funções e ferramentas que facilitam o trabalho do programador/aventureiro.

O objetivo deste guia será introduzir os principais conceitos dessa linguagem tendo como público-alvo pessoas que já possuam experiência em outras linguagens, como C/C++. Para informações mais detalhadas e ferramentas não mencionadas neste guia, favor consultar a documentação oficial do Python em: [https://docs.python.org/3/](https://docs.python.org/3/)

## **Executando códigos**

Comandos do Python podem ser executados de três formas: fornecendo um arquivo \(de extensão .py\) que já contém o código a ser executado, inserindo comandos interativamente pelo terminal do Python, ou combinando as duas técnicas ao importar um arquivo já existente através do terminal e utilizar as variáveis e funções declaradas nesse arquivo, interativamente.

No primeiro caso, utilizando um terminal localizado no mesmo diretório onde se encontra o arquivo, executamos:

```bash
python nomedoarquivo.py
```

No segundo caso, simplesmente executamos `python` e inserimos os comandos desejados no terminal, os quais são interpretados em tempo real. Neste caso, funções e variáveis chamadas mas não atribuídas imprimem seu conteúdo diretamente no terminal.

No terceiro caso, executamos:

```bash
python -i nomedoarquivo.py
```

e inserimos comandos da mesma forma do modo anterior, porém com a vantagem de já possuirmos disponível todo o código declarado no referido arquivo.

**Observação**: No Ubuntu e distribuições Linux derivadas dele, a versão padrão do Python é a 2, portanto os comandos acima executariam o Python 2. Para utilizar a versão 3 \(mais recomendada\) é necessário utilizar o comando “python3”. Muitos dos exemplos listados neste guia não funcionarão caso executados na versão 2!

## **Escopos**

Diferentemente de outras linguagens, Python não utiliza colchetes para determinar os escopos do código, ele obtém essa informação através da indentação. Ou seja, linhas de código que estão no mesmo “nível” horizontal estarão no mesmo escopo de execução. Exemplo:

```python
if 2 == 3:
    print("escopo interno")
print("escopo externo")
```

Esse código imprime apenas “escopo externo”, pois o primeiro print, que foi chamado no escopo do if, não é executado.

## **Tipos de dados**

Python difere de linguagens como C ao possuir tipagem dinâmica. Em outras palavras, o tipo de uma variável pode ser alterada, sem qualquer restrição, em tempo de execução. Essa regra também vale para estruturas complexas que armazenam outros tipos, que serão descritas abaixo.

Além disso, Python possui tipagem forte, ou seja, ele não permite fazer operações entre tipos de dados diferentes. Por exemplo, em C a operação ‘b’ - 1 retorna o inteiro pertencente ao código ASCII de ‘a’ \(97\), porém em Python essa operação gera um erro de execução. Para isso é necessário utilizar as funções chr\(\) e ord\(\) que retornam, respectivamente, o caractere de um código ASCII e o código ASCII de um caractere.

### Mutaveis

Tipos de dados mutáveis permitem que o valor de seus elementos e sua própria estrutura sejam alterados em qualquer momento da execução do código. Os exemplos mais usados para criptografia são:

#### **Listas**

Listas são caracterizadas como uma sequência ordenada de elementos de qualquer tipo. São análogas ao array \(vetor\) do C/C++, porém, assim como tudo em Python, listas permitem misturar tipos diferentes dentro da mesma estrutura.

```python
l1 = ['cripto', 2, True]

# imprime True
print(l1[2])

# concatena um novo elemento ao final da lista
l1.append('novo elem')

# imprime 'novo elem'
print(l1[3])

# estende a lista com os elementos de uma nova lista
l1.extend([1.2, 4])

# imprime ['cripto', 2, True, 'novo elem', 1.2, 4]
print(l1)

# sintaxe alternativa para o extend
l1 += [1.2, 4]

# obs: utilizar o append com uma lista concatena a lista em si, e não seus elementos
exemplo = [1, 2]
exemplo.append([3, 4])

# imprime [1, 2, [3, 4]]
print(exemplo)

# imprime 3 (o tamanho da lista) pois a lista interna é um único elemento
print(len(exemplo))

# deleta o primeiro elemento da lista l1
del(l1[0])

# imprime [2, True, 'novo elem', 1.2, 4]
print(l1)

# imprime 5 (novo tamanho da lista)
print(len(l1))

# operador "slice" do Python:
# [i:j] retorna os elementos entre i e j-1
print(l1[0:2])     # imprime [2, True]
print(l1[2:5])     # imprime ['novo elem', 1.2, 4]

# também é possível acessar na ordem inversa (de trás pra frente)
print(l1[-1])      # imprime 4
print(l1[-2])      # imprime 1.2

# sintaxe alternativa para criar listas, utilizando o construtor
# os parênteses duplos são necessários pois essa função recebe apenas um argumento, que neste caso é uma tupla (explicada adiante)
l2 = list((2.3, 'a'))

# também aceita outros tipos iteráveis como argumento
l3 = list('abc')

# imprime ['a', 'b', 'c']
print(l3)

l4 = []        # listas vazias
l5 = list()    #

# l6 = concatenação de l1 e l2
l6 = l1 + l2

# imprime [2, True, 'novo elem', 1.2, 4, 2.3, 'a']
print(l5)
```

Neste exemplo, criamos uma lista L com os tipos String, Integer e Boolean. Qualquer posição da lista pode ser alterada dinamicamente, similarmente ao C. Para informações detalhadas sobre tipos iteráveis, ler a seção 8 deste guia.

#### **Dicionários**

Dicionários são análogos ao map do C++, ou seja, é um tipo que associa pares chave-valor. As chaves devem ser únicas, porém os valores podem se repetir.

```python
d1 = {'grupo': 'Ganesh', 'membros': 54}

# imprime 'Ganesh'
print(d1['grupo'])

# imprime 54
print(d1['membros'])

# imprime 2 (o tamanho de d1)
print(len(d1))

# incrementa em 1 a quantidade de membros
d1['membros'] += 1

# imprime {'grupo': 'Ganesh', 'membros': 55}
print(d1)

# novo elemento adicionado ao dicionário
d1['melhor frente'] = 'cripto'

# imprime 'cripto'
print(d1['melhor frente'])

# sintaxe alternativa para criar dicionários
d2 = dict([(2, 'dois'), (3, 'tres')])

d3 = {}           # dicionários vazios
d4 = dict()    #
```

#### **Bytearrays**

Juntamente com o tipo bytes \(explicado na seção 4.2.c\), o bytearray é especialmente importante para criptografia por facilitar o processo de encriptação e decriptação de mensagens e exibição de ciphertexts. Um bytearray pode ser visto como uma “lista de bytes”, onde cada elemento assume um valor entre 0 e 255 \(um byte\).

Sua representação na função print\(\) é feita através de caracteres de “byte puro” em hexadecimal quando estes não são imprimíveis, ou de caracteres ascii quando são; ou seja, “\x02” é o terceiro caractere não imprimível \(incluindo o zero\), “\x03” é o quarto, etc. A seção 6 deste guia tratará com mais detalhes esse tipo de representação. Porém, ao ser referenciado individualmente, um elemento de bytearray é exibido como inteiro decimal entre 0 e 255 \(um byte\).

```python
# cria um bytearray com os elementos da lista
# caso fossem utilizados valores acima de 255, o Python produziria um erro
b1 = bytearray([2,89,100,254])

# imprime bytearray(b'\x02Yd\xff')
print(b1)

# imprime 2
print(b1[0])

# modifica o primeiro byte
b1[0] = 5

# imprime bytearray(b'\x05Yd\xff')
print(b1)

# inicializa b2 com a string 'ganesh' em formato de bytes
b2 = bytearray(b'ganesh')

# imprime 97 (código ascii do caractere 'a')
print(b2[1])

# representação hexadecimal de b2 em uma string
h = b2.hex()

# imprime '67616e657368'
print(h)

# convertendo de volta a bytearray
b3 = bytearray.fromhex(h)

# imprime bytearray(b'ganesh')
print(b3)
```

A habilidade de transformar bytearrays em uma string de hexadecimais é interessante quando se deseja imprimir um ciphertext na tela. A maioria dos bytes de um ciphertext não se encontram no intervalo de caracteres imprimíveis da tabela ASCII, portanto a representação hexadecimal ajuda nessa tarefa. Além disso, a operação de xor entre duas strings é facilitada utilizando esse tipo, e será ensinada com mais detalhes na seção 8.2 deste guia.

O construtor \(função que cria o objeto\) do tipo bytearray necessita receber um objeto iterável ou um inteiro como argumento. No primeiro caso, cria-se um bytearray com todos os elementos do iterável. No segundo caso, cria-se um bytearray com n elementos iguais a zero, onde n é o inteiro fornecido como argumento. Portanto caso se deseje criar um bytearray com um único elemento, é necessário incluí-lo dentro de uma lista ou tupla:

```python
# cria um bytearray com 1 único elemento de valor 42
b1 = bytearray([42])

# utilizando uma tupla, produz o mesmo resultado
b2 = bytearray((42,))

# cria um objeto com 4 bytes iguais a zero
b3 = bytearray(4)

# imprime bytearray(b'\x00\x00\x00\x00')
print(b3)
```

### **Imutáveis**

Tipos imutáveis são caracterizados pelo fato de não permitirem alterações em seus elementos após terem sido declarados, com exceção do método extend\(\) ou do operador += \(ambos realizam a inclusão de novos elementos\), a qual é permitida irrestritamente. A vantagem da utilização de tipos imutáveis é que eles são os únicos tipos que permitem o cálculo de hash, de forma que, por exemplo, somente tipos imutáveis podem ser a chave de um dicionário; além disso, elas apresentam uma maior confiabilidade e um maior desempenho de execução em comparação aos mutáveis, por motivos que fogem ao escopo deste guia.

#### **Strings**

Strings em Python são semelhantes às strings de qualquer linguagem de programação de alto nível, sendo a principal diferença para outras linguagens o fato de elas serem imutáveis. Em outras palavras, podemos concatenar novas strings ao final de outra já existente, mas não podemos alterar qualquer parte dela diretamente; para isso é necessário convertê-la em uma lista e realizar as operações desejadas sobre a lista, e em seguida convertê-la de volta a uma string utilizando o método ''.join\(lista\).

Simplificadamente, o método join de uma string s que recebe como argumento uma lista l retorna uma nova string com os elementos de l separados por s; neste caso, como s é uma string vazia, obteremos uma nova string apenas com os elementos de l. Esse método será mais explorado no exemplo a seguir.

Strings literais em Python podem ser representadas por aspas duplas ou simples, portanto a string ‘exemplo’ é exatamente igual à string “exemplo”.

```python
s = "one-time pad"

# concatena uma nova string à original
s += " tem perfect secrecy"

# imprime "one-time pad tem perfect secrecy"
print(s)

# imprime 'one-time pad'
print(s[0:12])

# cria uma lista com os caracteres de s
l = list(s)

# deleta os 11 primeiros caracteres ('one-time pad')
del(l[0:12])

# insere 'stream-ciphers' ao começo da lista
l = list('stream-ciphers') + l

# concatena 'não ' à lista formada pelos 14 primeiros elementos
# ou seja, insere um 'não ' após a palavra 'stream-ciphers'
l[0:15] += list('não ')

# substitui 'tem' por 'têm'
l[20] = 'ê'

# s recebe l em formato de string
s = ''.join(l)

# imprime 'stream-ciphers não têm perfect secrecy'
print(s)

# mais exemplos do funcionamento do método join
s1 = ' '.join(['1', '2', '3'])

# imprime '1 2 3'
print(s1)

s2 = ','.join(['1', '2', '3'])

# imprime '1,2,3'
print(s2)

s3 = ' - '.join(['1', '2', '3'])

# imprime '1 - 2 - 3'
print(s3)
```

**Tuplas**

Tuplas são os equivalentes imutáveis das listas, ou seja, podem ser vistas como listas cujos elementos não podem ser alterados.

```python
# declara uma tupla formada por 2 inteiros, 1 string e 1 lista
t = 1, 2, 'b', [5, 3]

# sintaxe alternativa para tuplas
# as aspas duplas são necessárias pois essa função recebe apenas 1 elemento como argumento
t = tuple((1, 2, 'b', [5,3]))

# imprime 'b'
print(t[2])

# concatena a tupla (5.2) à tupla t
# somente tuplas podem ser concatenadas a outras tuplas
# a vírgula ao final é necessária e serve para indicar que trata-se de uma tupla com 1 elemento
t += 5.2,

# cria uma nova tupla com os elementos da lista presente na última posição da tupla t
t2 = tuple(t[3])
```

#### **Bytes**

Bytes é o equivalente imutável do bytearray. Ao contrário do bytearray, o tipo bytes possui uma representação literal.

```python
# representação literal do tipo bytes
x = b'isso eh uma string de bytes puros e somente aceita caracteres ascii'

# imprime o byte correspondente ao caractere "s"
x[1]

# também é possível transformar strings utf-8 em bytes, para isso utiliza-se o segundo argumento da função:
x = bytes('isso é uma string com caracteres não ascii', 'utf-8')

# imprime b'isso \xc3\xa9 uma string com caracteres n\xc3\xa3o-ascii'
# ou seja, os caracteres especiais (não-ascii) são representados pelos seus valores em byte puro e codificados em hexadecimal
print(x)

# assim como no bytearray, também é possível representar os strings de bytes em hexadecimal
print(x.hex())

# converte um tipo bytes para bytearray
b = bytearray(x)

# converte um tipo bytearray para bytes
y = bytes(b)
```

As mesmas regras de construção do bytearray também se aplica ao tipo bytes:

```python
# cria um bytes com 1 único elemento de valor 42
b1 = bytes([42])

# utilizando uma tupla, produz o mesmo resultado
b2 = bytes((42,))

# cria um objeto com 4 bytes iguais a zero
b3 = bytes(4)

# imprime b'\x00\x00\x00\x00'
print(b3)
```

## **Conversões entre bases**

Dada uma string representando um número em uma base qualquer, é possível convertê-la em decimal utilizando a função int\(\), onde o primeiro argumento é a string e o segundo argumento indica a base onde essa string está codificada:

```python
# converte o hexadecimal '2e' ou '0x2e' em decimal
dec = int('2e', 16)

# imprime 46
print(dec)

# produz o mesmo resultado
dec = int('0x2e', 16)

# converte o binário '010' ou ‘0b010’ em decimal
dec = int('010', 2)

# imprime 2
print(dec)
```

Também é possível representar números de diversas bases de forma literal no Python. Para binário utilizamos o prefixo 0b, para octal utilizamos o prefixo 0o, para hexadecimal utilizamos o prefixo 0x, e assim por diante. Porém, esses literais são sempre automaticamente convertidos em decimal ao armazenarmos seus valores numa variável ou imprimirmos eles na tela:

```python
# armazena na variável o hexadecimal '2e', convertendo em decimal
dec = 0x2e

# é possível utilizar valores de qualquer tamanho
dec = 0x2e578a

# literal em octal
dec = 0o4261

# literal em binário
dec = 0b01001110
```

Também podemos utilizar as funções bin\(\), oct\(\) e hex\(\) para converter decimais em binário, octal e hexadecimal, respectivamente. Porém todas essas funções retornam uma string, visto que o Python não armazena valores literais em outras bases:

```python
# armazena a string '0b100'
binario = bin(4)

# armazena a string '0o12'
octal = oct(10)

# armazena a string '0x14'
hexa = hex(20)
```

Como visto anteriormente, dado um objeto do tipo bytearray ou bytes, é possível convertê-lo em uma sequência de hexadecimais, e vice-versa:

```python
# armazena '142d' (0x14 = 20 e 0x2d = 45)
hexa = bytes([20, 45]).hex()

# converte a mesma sequência de volta a bytes
b = bytes.fromhex(hexa)
```

## **Codificação e decodificação**

Por padrão, o Python utiliza a codificação utf-8, isso significa que podemos armazenar strings com caracteres especiais \(incluindo acentuação, por exemplo\).

Os caracteres de uma string que estão contidos na tabela ascii são codificados como ascii \(pois eles coincidem com o utf-8\) e utilizam apenas 1 byte por caractere, porém os caracteres especiais necessitam de mais bytes para serem representados. Por conta disso, se armazenarmos uma string com caracteres especiais em um objeto do tipo bytes e utilizarmos a função print\(\) nesse objeto, esses caracteres não serão imprimidos na tela, ao invés disso os seus bytes individuais serão imprimidos com o prefixo ‘\x’, isso indica que eles são caracteres fora da tabela ascii e possuem o valor em hexadecimal representado após o ‘\x’.

```python
# armazena a string 'é' em um objeto do tipo bytes, é necessário indicar que a string está codificada em utf-8 no segundo argumento
b = bytes('é', 'utf-8')

# o caractere 'é' é representado pelos bytes 0xc3 e 0xa9 e ambos não estão na tabela ascii, portanto o comando a seguir imprime b'\xc3\xa9'
print(b)

# também podemos utilizar o método encode() das strings, que produz o mesmo resultado
b = 'é'.encode('utf-8')

# também é possível representar o objeto acima de forma literal utilizando o formato b''
s = b'\xc3\xa9'

# a decodificação de bytes para utf-8 é feita utilizando o método decode() do bytes
b = s.decode('utf-8')

# imprime 'é'
print(b)
```

Como dito anteriormente, a fim de obtermos o código ascii ou unicode de um caractere no Python devemos utilizar a função ord\(\). Analogamente, para obtermos o caractere correspondente a um código unicode devemos utilizar a função chr\(\).

```python
# imprime o código unicode do 'a' (97)
print(ord('a'))

# imprime o código unicode do 'é' (233)
print(ord('é'))

# imprime o caractere cujo código unicode é 199 ('Ç')
print(chr(199))

# atribui 'b' à uma variável e subtrai seu valor de 1, obtendo 'a'
c = 'b'
c = chr(ord(c) - 1)
```

## **Operadores**

Os operadores mais usados em criptografia são o XOR e o módulo. O primeiro é muito utilizado para encriptar e decriptar mensagens, e o segundo é utilizado para garantir que um cálculo específico não ultrapasse determinado valor, geralmente o intervalo de um byte \(de 0 a 255\).

### **XOR**

Assim como em C, o operador XOR \(^\) opera sobre dois inteiros e retorna o resultado de aplicar ou-exclusivo \(eXclusive-OR\) sobre eles, bit a bit \(bitwise\).

```python
# xor entre 4 (100) e 6 (110), que resulta em 2 (010)
print(4 ^ 6)
```

### **Módulo**

Assim como em C, o operador módulo \(%\) opera sobre dois inteiros e retorna o resto da divisão do primeiro pelo segundo, ou seja, X % Y retorna o resto da divisão de X por Y.

```python
# imprime 257 módulo 256, que resulta em 1
print(257 % 256)
```

## **Loops e iteradores**

### **For**

O for do Python difere consideravelmente do for da linguagem C pois, no Python, este deve sempre iterar sobre outros objetos “iteráveis” \(o nome genérico para esse tipo de loop é for each\).

Todos os tipos apresentados na seção 4 e os generators, explicados na seção 8.3, são iteráveis, ou seja, seus elementos podem ser acessados invidualmente, em ordem, portanto todos podem ser utilizados no for.

A sintaxe do for é, de forma genérica, for {variável} in {iterador}, sem os colchetes, e como resultado faz com que, a cada iteração, “variável” receba o valor de cada elemento presente no objeto “iterador”.

Para utilizar o for do Python da mesma forma que utilizamos em C, fazemos uso da função range\(\) que recebe como argumento 3 valores \(start, stop e step\) e retorna um iterador contendo todos os valores entre start e \(stop - 1\), separados por step. Então ao executarmos for i in range\(0, 10, 1\), o valor de i receberá, a cada iteração, os valores de 0 a 9, separados de 1 em 1. Contudo, os argumentos start e step são opcionais e, caso não sejam fornecidos, são definidos como 0 e 1, respectivamente.

```python
# imprime todos os números de 0 a 9
for i in range(10):
    print(i)

# imprime os números de 5 a 9
for i in range(5, 10):
    print(i)

# imprime os valores 5, 7 e 9
for i in range(5, 10, 2):
    print(i)

# itera a variável 'elem' sobre os elementos de uma lista e imprime todos, um a um
for elem in [5, 'string', 8.9, True]:
    print(elem)

s = 'criptografia'

# itera sobre cada caractere da string s ('criptografia')
for char in s:
    print(char)

# a função range() também pode ser atribuída a uma variável e, neste caso, armazena um iterador sobre os elementos requisitados
t = range(2, 5)

# imprime 3
print(t[1])
```

A iteração também pode ser feita em dois ou mais objetos simultaneamente utilizando a função zip\(\). Essa função retorna n tuplas, onde cada tupla contém os elementos de mesma posição dos objetos que foram fornecidos à função, e “n” é o tamanho do menor desses objetos. Caso um dos objetos seja maior do que o outro, os elementos restantes do maior objeto serão ignorados.

```python
# declarando duas listas com valores diferentes
l1 = [1,2,3]
l2 = [4,5,6]

# iterando sobre cada par de mesma posição de l1 e l2, simultaneamente
for elem1, elem2 in zip(l1, l2):
    print(elem1, elem2)

# o código acima imprime:
# 1 4
# 2 5
# 3 6
```

Outro método de iteração simultânea é utilizando a função enumerate\(\) que recebe apenas 1 objeto de tamanho n e retorna n tuplas, cada uma contendo a posição e o valor de cada elemento do objeto.

```python
# a cada iteração, i recebe a posição e elem recebe o valor da lista
for i, elem in enumerate([7, 8, 9])
    print(i, elem)

# o código acima imprime:
# 0 7
# 1 8
# 2 9
```

### **Xor entre bytes**

Agora que sabemos o funcionamento do for e do bytes, podemos finalmente implementar um código que realiza a operação xor entre dois objetos bytes quaisquer. Operação essa que é muito útil para diversos algoritmos de criptografia. Lembrando que o operador xor é representado pelo circunflexo \(^\) e sempre opera sobre dois decimais inteiros.

```python
# xor entre dois bytes (12 e 30)
result = 12 ^ 30

# imprime o resultado (18)
print(result)

# agora vamos encriptar um plaintext em formato de bytes
plaintext = b'um plaintext muito bonito'
chave = b'uma chave maior do que o plaintext'

# o ciphertext começa como um bytes vazio
ciphertext = bytes()
for p, c in zip(plaintext, chave):
    # realiza o xor e incrementa o ciphertext com o resultado
    xor = p ^ c
    ciphertext += bytes([xor])

# imprime o ciphertext em formato de bytes
print(ciphertext)

# imprime o ciphertext em formato hexadecimal (melhor visualização)
print(ciphertext.hex())
```

### **Generators**

Generators são um tipo especial de iterador. Além de possuírem uma sintaxe bastante compacta, sua principal característica que os diferem de outros iteradores é que eles não armazenam elementos em sua estrutura e portanto quase não consomem espaço na memória RAM, ao invés disso, ao se solicitar o próximo elemento de um generator ele faz o cálculo e devolve o resultado requisitado sob demanda.

Existem 2 tipos principais de generators:

O primeiro utiliza a sintaxe {expressão} for {variável} in {iterador}, sem os colchetes. Nesse caso, “variável” itera sobre cada elemento do “iterador”, e este generator retorna o resultado de “expressão” \(possui acesso ao conteúdo de “variável”\), sob demanda, a cada requisição de uma nova iteração. Essa sintaxe pode ser atribuída a uma variável, a qual será do tipo generator e poderá ser utilizada para solicitar novos valores, ou pode ser utilizada para construir outros tipos, como listas, tuplas e bytes.

O segundo tipo utiliza funções e será explicado na seção 9.1.

```python
# cria uma variável generator que retorna o dobro de todos os números entre 0 e 5
# os parênteses são necessários
g = (2 * n for n in range(6))

# a função next() recebe um generator e retorna o resultado da próxima iteração sobre ele
# imprime 0
print(next(g))

# imprime 2
print(next(g))

# cria uma lista com os próximos elementos do generator (4, 6, 8 e 10), pois os 2 primeiros já foram consumidos
l1 = list(g)

# reinicia o mesmo generator
g = 2 * n for n in range(6)

# cria uma segunda lista com todos os elementos originais do generator
l2 = list(g)

# cria uma nova lista utilizando um generator
# armazena o xor entre os elementos de l1 e l2
l3 = [p ^ c for p, c in zip(l1, l2)]
```

Agora somos capazes de reescrever o mesmo código da seção 8.2 \(xor entre bytes\) utilizando apenas 1 linha:

```python
# faz o xor entre plaintext e chave e armazena no ciphertext
ciphertext = bytes([p ^ k for p, k in zip(plaintext, chave)])
```

### **Slices**

Slice é um recurso do Python que permite acessar “pedaços” de objetos iteráveis \(exceto generators\). Seu formato é \[começo:fim:passo\], onde começo indica a posição inicial que se deseja obter, \(fim - 1\) é a posição final que se deseja obter, e passo é a diferença entre elementos consecutivos. Caso o passo não seja fornecido, seu valor é definido como 1. Caso o começo não seja fornecido, seu valor é definido como a posição inicial do objeto. Caso o fim não seja fornecido, seu valor é definido como a posição final do objeto.

```python
# cria uma lista com os elementos de 0 a 9
l1 = list(range(10))

# imprime os elementos de 4 a 8
print(l1[4:9])

# imprime do começo da lista até a 5ª posição
print(l1[:6]

# imprime da 5ª posição até o final da lista
print(l1[5:]

# imprime os elementos de 2 a 8, pulando de 2 em 2
print(l1[2:9:2]

# imprime todos os elementos da lista, pulando de 2 em 2
print(l1[::2]
```

## **Funções**

As funções no Python são semelhantes às funções de outras linguagens, com diferença de que o tipo de retorno, assim como tudo Python, não precisa ser especificado.

Para definir uma função utilizamos a keyword def, seguidos pelos parâmetros entre parênteses, e utilizamos a mesma regra de escopo da seção 3 para definir todo o código que pertence à função:

```python
# função que recebe um plaintext e uma chave, faz o xor entre ambas e retorna o ciphertext
def xor(plaintext, chave):
    ciphertext = bytes([p ^ k for p, k in zip(plaintext, chave)])
    return ciphertext
```

### **Generator**

Como foi citado na seção anterior, é possível criar funções do tipo generator, as quais realizam um cálculo e devolvem a expressão após a keyword yield a cada requisição de uma nova iteração do gerador:

```python
# cria um gerador que recebe um número e, a cada requisição, devolve o número anterior incrementado de 1, e pode ser utilizada infinitamente (por conta do “while True”)
def gerador(num):
    while True:
        num += 1
        yield num

g = gerador(5)

# imprime 6
print(next(g))

# imprime 7
print(next(g))

# imprime 8
print(next(g))

# etc
```

## **Bibliotecas de criptografia**

* PyCryptodome

PyCryptodome é uma biblioteca que surgiu para substituir a PyCrypto, que foi descontinuada. Atualmente ela possui diversas cifras simétricas e assimétricas \(Salsa20, ChaCha, RSA, entre outras\), funções de Hash e de Assinatura Digital, chaves públicas, gerador de números pseudoaleatórios, entre outros.

Para instalar essa biblioteca no Python, execute no terminal `pip install --user pycryptodome`, a flag `--user` realiza a instalação apenas para o usuário logado é importante para garantir que ela não seja instalada em todo o sistema, o que possivelmente pode causar problemas futuros. **Obs:** Caso você esteja utilizando o comando `python3` para executar códigos, utilize `pip3` para instalar módulos.

A API com todas as ferramentas dessa biblioteca está disponível em [https://www.pycryptodome.org/en/latest/src/api.html](https://www.pycryptodome.org/en/latest/src/api.html).

Exemplos de uso dessa biblioteca podem ser encontrados em [https://www.pycryptodome.org/en/latest/src/examples.html](https://www.pycryptodome.org/en/latest/src/examples.html).

