# Definições

## Cifras de substituição

É uma forma de criptografia do qual os símbolos do alfabeto do texto plano são substituídas por símbolos do alfabeto do texto cifrado de acordo com uma regra de deslocamento. A forma de decriptação é a substituição inversa.

Nas cifras em que a chave é o deslocamento, frequentemente temos um valor de deslocamento maior do que a quantidade de letras do alfabeto. Neste caso, utilizamos o conceito de módulo. Por exemplo, deslocamento de 29 em um alfabeto de 26 letras corresponde ao valor 29 mod 26, que resulta em um deslocamento de 3 letras.

Ex 1. \[_Alfabetos não coincidentes_\]

Alfabeto texto plano: A\|\*\|C\|D\|&\|F\|%\|$\|I\| \(...\)

Alfabeto texto cifrado: 1\|2\|3\|4\|5\|6\|7\|8\|9\| \(...\)

Ex 2. \[_Alfabetos coincidentes_\]

```text
Alfabeto texto plano:         A|B|2|D|4|F|5|H|I| (...)
```

Alfabeto texto cifrado: A\|B\|2\|D\|4\|F\|5\|H\|I\| \(...\)

## Monoalfabética ou simples

Cada unidade do texto plano é substituída por uma única unidade do texto cifrado em uma razão de deslocamento constante para todas unidades.

**A**\|B\|C\|D\|**E**\|F\|**G**\|**H**\|I\|J\|K\|L\|M\|**N**\|O\|P\|Q\|R\|**S**\|T\|U\|V\|W\|X\|Y\|Z\|

**3**\|4\|E\|F\|**G**\|H\|**I**\|**J**\|K\|L\|M\|N\|O\|**P**\|Q\|R\|S\|T\|**U**\|V\|W\|X\|Y\|Z\|1\|2\|

_Deslocamento 2_

Ganesh -&gt; I3pguj

## Polialfabética

Cada unidade do texto plano é substituída por uma única unidade do texto cifrado em uma razão de deslocamento variável para pelos menos uma unidade. Comumente utiliza-se outra palavra \(chave\) para indicar o deslocamento de cada símbolo do texto plano.

Texto plano: O\|X\|I\|N\|T\|A\|

Cifra: G\|A\|N\|E\|S\|H\|

Texto cifrado: U\|X\|V\|R\|L\|H\|

Um exemplo famoso é a cifra de Vigenere.

## Homófona

Cada símbolo do alfabeto do texto plano é correspondida pra mais do que um símbolo. É utilizado para dificultar uma análise estatística baseada na frequência.

Alfabeto do texto plano: ABCDEFGHIJKLMNOPQRSTUVWXYZ

Alfabeto 1 do texto cifrado: 1234EFGHIJKLMNOPQRSTUVWXYZ

Alfabeto 2 do texto cifrado: @\#$ABCDEFGHIJKLMNOPQRSTUV

Alfabeto 3 do texto cifrado: ZWYKLMNSPQ234FDJV=-915678CX

Texto cifrado: ‘Cifra curta’ -&gt; 3JGS1 $VSU@

## Poligráfica

A substituição se dá mapeando um caractere para um grupo de símbolos.

Alfabeto do texto plano: A; B; C; E\[...\]

Alfabeto do texto cifrado: &A, 789; CVD; ZDFG\[...\]

