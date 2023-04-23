Até o momento, todas as cifras que descrevemos eram utilizadas com o objetivo de se garantir a confidencialidade, e os plaintexts eram compostos basicamente por sequencias de letras. Contudo, com a entrada da computação no cenário e a chegada da era moderna, a criptografia expandiu seus campos de atuação, de modo que hoje lidamos com sequencias de bits, que podem significar letras, pixels de uma imagem, áudios, entre outros.

Por exemplo, a sequência de bits 01000001 em um arquivo de extensão (.txt) significa a letra A, conforme [tabela ASCII](https://www.asciitable.com/). Já a sequencia 00000000 em um arquivo (.jpg) significa um pixel preto e a sequencia 11111111 significa um pixel branco.


# Simétrica

No sistema de criptografia simétrica apenas uma chave é utilizada, tanto para encriptar quanto para decriptar a mensagem.

## One Time Pad

Para estudar a cifra One Time Pad (OTP), é preciso primeiro compreender as propriedades do operador lógico XOR (ou exclusivo). Trata-se de uma operação sobre dois ou mais valores lógicos que produz um valor verdadeiro apenas se a quantidade de operadores verdadeiros for ímpar. A Tabela-verdade para o XOR de duas entradas é a seguinte:

