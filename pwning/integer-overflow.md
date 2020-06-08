# Integer Overflow

Uma das anomalias mais simples que talvez possa ser explorada é o Integer Overflow.

Quando um inteiro é somado muitas vezes, seu número pode ultrapassar sua capacidade de representação. 

Por exemplo, um inteiro de 4 bytes pode representar do número `-2147483648` ao `2147483647`. Se somarmos 1 a um inteiro de 4 bytes com valor `2147483647`, ele se tornará `-2147483648` por causa da sua representação em complemento de 2 e esse comportamento é chamado de **Integer Overflow**. O comportamento oposto que acontece ao subtrair 1 de `-2147483648` é chamado de **Integer Underflow**.

Uma forma de explorar esse comportamento é caso esse inteiro esteja sendo usado como um _offset_ de alguma posição de memória ou uma expressão condicional (if). Fazendo um Integer Overflow, você pode ter acesso a uma posição de memória que o programa não permitia, ou ultrapassar alguma checagem de uma forma não pretendida.

Em geral, um Integer Overflow é uma vunerabilidade bem simples, e na maioria dos casos, não é possível explorar muito com ele. Mas uma forma de overflow bem mais perigosa que o Integer Overflow é o Buffer Overflow, que veremos a seguir.
