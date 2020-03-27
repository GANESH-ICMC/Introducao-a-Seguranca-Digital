# Registradores e tipos de dados

## Registradores e Tipos de Dados

Aqui estaremos estudando os registradores da arquitetura x86 e x86-64, seguindo principalmente o padrão da Intel.

Para guardar variáveis de forma no geral e passá-los de uma parte da memória para outra, a nossa principal ferramenta são os registradores.

### Registradores

Na arquitetura x86 temos 8 registradores de propósitos gerais \(ou GPR\) de 32-bits, alguns deles também podem ser divididos em registradores de 8 e 16 bits.

#### Registradores de propósito geral

Como o próprio nome diz, esses registradores são de propósito geral, ou seja, podem ser usados para "qualquer coisa", mas usualmente seguem algumas convenções

| Registrador | Convenção | 16 - Bits | 8 Bits |
| :--- | :---: | :---: | :---: |
| EAX | Acumulador, usado para operações aritméticas e para guardar resultados | AX | AH-AL |
| EBX | Registrador secundário, usado como "base" em operações de vetores | - | - |
| ECX | Contador em loops | - | - |
| EDX | Usado para guardar endereços de dados | - | - |

#### Registradores de Endereços

| Registrador | Propósito | 16 - Bits |
| :--- | :--- | :---: |
| ESI | Fonte em operações de memória/strings | SI |
| EDI | Destino em operações de memória/strings | DI |
| EBP | Registrador base para a stack/pilha \(frame atual\) | BP |
| ESP | Pointeiro da stack/pilha | SP |

#### Outros registradores

| Registrador | Propósito | 16 - Bits |
| :--- | :--- | :---: |
| EIP | Instruction Pointer \(Program counter\) - Indica em qual instrução a execução se encontra | - |
| EFLAGS | Guarda resultado de operações - Ex: Flag Zero | - |

### Set de Instruções

O conjunto de instruções x86 envolve o movimento de dados entre registradores e memória, classificados em 5 tipos:

* Imediato para registrador
* Registrador para registrador
* Imediato para memória
* Registrador para memória e vice-versa
* Memória para memória - Somente nas arquiteturas RISC.

#### x86

O foco aqui será a sintaxe da Intel.

**Intel vs AT&T**

A AT&T prefixa os registradores com `%` e imediatos com `$`, o que não acontece na Intel. Eles também adicionam um prefixo à instrução para indicar o tamanho do dado da operação  \(long, byte, etc. \). Na sintaxe da Intel, o destino vem e, em seguida, a fonte  \(op dest source \), na AT&T é o contrário. \(Pense em dest=fonte\) As instruções têm comprimento variável  \(1 a 15 bytes \).

x86 usa colchetes \( \[\] \) para indicar acesso à memória  \(semelhante ao asterisco \( \* \) em C / C ++ \) Para somar ou subtrair o endereço dentro de \[\] geralmente é usado hexadecimal, por exemplo: mov eax \[ecx + 10h\] - Onde h é usado para indicar notação hexadecimal.

**Instruções**

* MOV - mov ecx, \[eax\]
  * Seta ecx = \[eax\]  
* ADD - inc dword ptr \[eax\]
  * Incrementa o valor no endereço eax.  
* SUB - sub eax, 0x20
  * Subtrai eax por 0x20 \(32 em decimal\).
* PUSH - push eax
  * Coloca eax na stack.
* POP - pop eax
  * Tira o endereço do topo da stack e salva em eax.
* CMP - cmp eax, ebx
  * if \(eax == ebx\) seta eflags;
* JNE - jne 0x400086
  * Pula para o endereço dado se eflags foi setado como igual.
* CALL - call 0x400086
  * Pula para o endereço dado e salva a localização atual na stack. Equivalente às instruções:
    * push rip
    * jump 0x400086
* RET - ret
  * Tira o endereço da stack e retorna o controle para aquela localização.
    * pop rip
* LEA - lea eax, \[esp+0x1c\]
  * Move o endereço do registrador para outro. Usado para passar parâmetros para funções.
* LEAVE - leave
  * Move ebp para esp e tira ebp da stack.

