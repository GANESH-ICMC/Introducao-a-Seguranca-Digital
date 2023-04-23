Dois tipos principais de cifra abrangeram a história da criptografia clássica: as cifras de substituição e as de transposição. Nas cifras de substituição os símbolos do alfabeto do texto plano são substituídos por um ou mais símbolos do alfabeto do texto cifrado de acordo com uma regra, gerando o texto cifrado. Já nas cifras de transposição os símbolos do alfabeto do texto plano são permutados, também de acordo com uma regra, gerando o texto cifrado.

# Cifras de Substituição

## Cifra de substituição simples (monoalfabética)

Trata-se de uma cifra em que cada unidade do texto plano é substituída por uma única unidade do texto cifrado, de acordo com um mapeamento entre os alfabetos do plaintext e do ciphertext, por exemplo:

Alfabeto do plaintext: </br>
A|B|C|D|E|F|G|H|I|J|K|L|M|N|O|P|Q|R|S|T|U|V|W|X|Y|Z

Alfabeto do ciphertext: </br>
D|G|U|A|S|M|Z|E|R|B|C|I|H|V|Y|P|K|X|Q|N|T|F|W|L|O|J

Ex: GANESH -> ZDVSQE

Para decriptar, basta deslocar cada letra do ciphertext no sentido contrário. Uma das cifras mais utilizadas na antiguidade, a Cifra de César era uma cifra monoalfabética em que o alfabeto do ciphertext era o mesmo que o do plaintext, porém deslocado

### Quebrando a Cifra de substituição simples

É possível quebrar as cifras de substituição monoalfabética por meio da análise de frequência das letras do ciphertext, desde que se conheça o idioma utilizado. Acontece que nas cifras monoalfabéticas cada letra do plaintext é encriptada sempre para a mesma letra do ciphertext. No exemplo que vimos acima, a letra L será sempre encriptada para a letra I, a letra M será sempre encriptada para a letra H, e assim sucessivamente.

Por exemplo, no idioma inglês a letra E é a mais frequente de todas, aparecendo em 12,70% do total de letras em um texto, seguida dela vem a letra T, que aparece 9,05% das vezes. Sabendo disso, em posse de um ciphertext escrito em inglês, se a letra mais frequente encontrada for a letra K, provavelmente ela corresponde à letra E do plaintext. E se a segunda letra mais frequente for a letra W, provavelmente ela corresponde à letra T do plaintext.

## Cifra de Vigenère

Trata-se de uma cifra de substituição polialfabética em que a palavra chave é responsável por especificar o deslocamento de cada letra do plaintext. Desse modo, é impossível realizar diretamente um ataque de frequência como o utilizado nas cifras de substituição monoalfabética, já que uma mesma letra do plaintext pode ser encriptada para diferentes letras no ciphertext, a depender do seu “match” com a palavra chave ao longo do texto.

Quando a palavra chave for menor do que o plaintext, ela deve ser repetida até completar o tamanho do plaintext. A encriptação pode ser descrita algebricamente: se as letras A-Z correspondem aos números 0-25, soma-se o valor numérico da letra no plaintext com o valor numérico de sua letra pareada na chave e aplica-se o resto da divisão por 26, encontrando o valor numérico da letra do ciphertext. Exemplo de encriptação com a chave LEMON:

Plaintext:</br>
A|T|T|A|C|K|A|T|D|A|W|N</br>
Chave:</br>
L|E|M|O|N|L|E|M|O|N|L|E</br>
Ciphertext:</br>	
L|X|F|O|P|V|E|F|R|N|H|R
