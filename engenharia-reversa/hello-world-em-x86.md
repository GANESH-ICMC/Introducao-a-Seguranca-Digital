---
description: Explicação de um Hello World em Assembly x86
---

# Hello World em x86

Usando códigos como exemplo, é recomendável antes de mais nada entender conceitos básicos do Assembly x86, como a instrução `mov`.

Usando por exemplo esse programa:

```text
;; Programa Hello World
section .text
global _start

_start:
        mov     edx,len                             ;comprimento da mensagem
        mov     ecx,msg                             ;mensagem a ser escrita
        mov     ebx,1                               ;descritor de arquivo (stdout)
        mov     eax,4                               ;número da system call
; (sys_write)
        int     0x80                                ;call kernel

        mov     eax,1                               ;numero da syscall
; (sys_exit)
        int     0x80                                ;call kernel

section     .data
        msg     db  'Hello, world!',0xa                 ;nossa string lindona
        len     equ $ - msg                             ;comprimento da lindona
```

### **Entendendo o código**

Inicia com um comentário, marcado a partir de um `;` como você pode ver.

É necessário especificar seções do código. Uma vez que o Assembly vai ser carregado diretamente na memória, você precisa especificar o que é o fragmento `text` \(instruções\) e o que é o fragmento `data` \(código não executável, usado para guardar strings e algumas variáveis, etc.\). Como vocẽ pode ver, define-se um rótulo \(label na forma culta\) global `_start`. Isso é necessário para ser possível definir o ponto de entrada do código \(É um rótulo padrão\).

Vamos olhar agora a seção `.data`. Primeiramente ela declara um "define byte" \(`db`\) que nós chamamos de `msg`, com a string que queremos imprimir, juntamente com `0xa`, que é o caractere de nova linha, \(equivalente ao `\n` no C, por exemplo\). Na próxima linha, definimos uma variável `len` que representa o comprimento da string, isto é, o endereço atual da memória onde está a instrução \(representado por `$`\) subtraído do começo da string \(`msg`\).

Voltando agora para o rótulo `_start` \(também chamado de função nesse caso\), nas primeiras 4 linhas nós acabamos de armazenar as variáveis nos registradores `edx` e `ecx`, depois nós colocamos o valor 1 em `ebx` e 4 em `eax`. Isso significa que, uma vez que queremos escrever alguma coisa na `stdout` \(ou saída padrão\), nós usamos a syscall `write`, que pede o argumento `fd` \(descritor de arquivo\) passado no registrador `ebx` como uma convenção, como visto em [System Calls Reference](https://syscalls.kernelgrok.com/). Então a `int`errupção 0x80 será chamada \(isso é uma _syscall_\), que irá imprimir "Hello, world!" no terminal.

No final, o registrador `eax` terá o valor 1, significando a _syscall_ "exit". Então será chamado através de `int 0x80`, saindo do programa.

No caso de nós quisermos colocar um `return 0` no final do código, nós poderíamos colocar apenas `mov ebx, 0` logo antes da syscall.

### **Compilando e testando o código**

Para montar códigos Assembly x86, uma boa maneira é usar o montador [nasm](https://nasm.us/).

Supondo que temos um código `hello.asm`, podemos montá-lo com

```bash
nasm -f elf hello.asm
```

Fazendo isso nós especificamos que o formato do arquivo será um `elf` \(32bits\) e um novo objeto `hello.o` será produzido.

Ainda assim, esse não é nosso arquivo executável. Para fazer um ainda precisamos utilizar o comando `ld` \(link-editor\) para ligar o objeto com as bilbiotecas do sistema, o que pode ser feito facilmente:

```bash
ld -s -o hello hello.o -m elf_i386
```

Isso simplesmente liga o objeto gerado para um executável `hello`, que tem o formato `elf_i386`. No caso de qualquer erro acontecer, verifique se você tem `32bits glibc` no seu sistema operacional.

Então, execute-o simplesmente usando

```bash
./hello
```

E é isso, temos nosso Hello World! OwO

### Referências

* [Linux System Calls Reference](https://syscalls.kernelgrok.com/)
* [x86 Hello World](http://asm.sourceforge.net/intro/hello.html)
* [nasm](https://nasm.us/)

