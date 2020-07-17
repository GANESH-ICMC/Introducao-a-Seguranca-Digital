# Proteções da stack

Agora que sabemos de alguns ataques, vamos olhar algumas das formas de proteção contra tais ataques.

Nos exemplos de buffer overflow, compilamos nossos programas com `-fno-stack-protector`. Isso evita que o GCC compile nosso programa com o `-fstack-protector`.

Essa proteção coloca todos os buffers entre as variáveis normais e os registradores salvos na stack (como o ebp). Dessa forma, ela evita que as variáveis normais sejam sobrescritas por um buffer overflow. Além disso, ela também coloca um espaço extra no fim do stack frame, chamado de stack canary, que é atribuido um valor secreto que muda toda vez que o programa é executado. No fim da função, esse valor será verificado e caso tenha sido alterado, a função `__stack_chk_fail()` será chamada, exibindo uma mensagem de erro de stack smashing e finalizará o programa.

Há também o NX bit, que previne a execução de certas áreas da memória, impedindo assim a execução de shellcodes nessas áreas. A stack costuma ser uma das regiões de memória protegidas pelo NX bit. Quando estavamos vendo shellcode, compilamos o programa com `-z execstack` e também usamos o `execstack -s` para removê-lo. Podemos habilita-lo explicitamente com `-z noexecstack` e `execstack -c`.

# PIC/PIE e ASLR

Além de delimitações de buffer que o programador pode colocar para evitar buffer overflow e proteções da stack, há algumas medidas de segurança para evitar execução de código arbitrário também. Uma delas é o **ASLR**. Mas antes de falar sobre ASLR, vamos falar sobre o **PIE**.

**Position-Independent Executable (PIE)** são binários executáveis que fazem o uso de **Position-Independent Code (PIC)** em todo seu código.

Position-Independent Code, como o nome diz, são códigos que não dependem de sua posição para serem executados, ou seja, seu endereço não é hard-coded no código do programa.

O ASLR, Address Space Layout Randomization, é uma técnica de segurança que aleatorializa as posições das regiões da memória, como por exemplo a stack, a heap e as bibliotecas compartilhadas. Isso deixa os endereços mais difíceis de serem adivinhados por um atacante, dificultando ataques envolvendo mudança do fluxo de execução e de escrita arbitrária. O PIE fornece uma maior eficácea para o ASLR, já que funções do executável principal também recebem o tratamento de bibliotecas compartilhadas e, portanto, podem ser randomizadas pelo ASLR.

O PIE pode ser habilitado com a flag de compilação `-pie` e desabilitado com `-no-pie`. O ASLR pode ser habilitado mudando o `/proc/sys/kernel/randomize_va_space` para 2 e desabilitado mudando para 0.
