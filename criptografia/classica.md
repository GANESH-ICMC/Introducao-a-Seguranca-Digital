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

Note que a primeira letra T foi encriptada para X, enquanto que a segunda letra T foi encriptada para F. Ou seja, a mesma letra do plaintext resultou em letras diferentes no ciphertext. Para decriptar, basta subtrair o valor numérico de cada letra do ciphertext do valor numérico do seu par na chave. Caso resulte em um número negativo, basta somar 26. O resultado dessa operação será o valor numérico da letra no plaintext.

A tabela a seguir é utilizada para facilitar a encriptação e a decriptaçao, dado um plaintext e uma chave.

![tableau_vigenere](https://user-images.githubusercontent.com/96321435/233817957-ed57a13f-fc6d-4260-b8bf-56f37dc89a77.png)

### Quebrando a Cifra de Vigenère (Teste de Kasiski)

Como já vimos anteriormente, a Cifra de Vigenère foi considerada inquebrável por três séculos, até que em 1863 Friedrich Kasiski propôs um ataque que funciona quando o tamanho da chave é menor do que o do plaintext. Para entendermos o Teste de Kasiski, vamos utilizar o mesmo exemplo anterior e considerar que o atacante já saiba o tamanho da chave:

Plaintext:
A|T|T|A|C|K|A|T|D|A|W|N
Chave:	
L|E|M|O|N|L|E|M|O|N|L|E
Ciphertext:	
**L**|X|F|O|P|**V**|E|F|R|N|**H**|R

Como o tamanho da chave já é conhecido (5 letras), sabemos que a cada cinco letras do ciphertext o deslocamento realizado para obter tais letras foi exatamente o mesmo. Note que as letras L, V e H, destacadas acima, foram todas obtidas a partir de um mesmo deslocamento. Agora, se temos um conjunto de letras e todas foram obtidas a partir de um mesmo deslocamento, temos diante de nós uma cifra de substituição simples, que é passível de ataque por análise de frequência.

Suponha que o texto do exemplo acima seja muito maior, logo o conjunto que possui as letras L, V e H possui ainda muito mais letras, muitas delas vão se repetindo dentro do conjunto. Como o texto é escrito em inglês, é provável que a letra que mais se repetir dentro desse conjunto foi obtida a partir da encriptação da letra E. Logo, em posse de uma letra do plaintext e de uma letra do ciphertext, é possível descobrir qual a letra da chave que gerou tal deslocamento.

Assim, descobrimos a primeira letra da chave. Para descobrir a próxima letra, basta repetir o processo para formar um novo conjunto (formado pelas letras X, E, R...) e supor que a letra mais abundante desse conjunto foi obtida a partir da encriptação da letra E. Note que isso tudo só é possível quando soubermos o tamanho exato da chave. Na prática, para descobrirmos o tamanho da chave é preciso encontrar padrões de repetições ao longo do ciphertext e a partir do distanciamento dessas repetições obter o tamanho da chave.

Observe a imagem com o ciphertext a seguir e repare na repetição da sequência U-S-E diversas vezes ao longo do texto.




