# Pwntools

## O que é

Pwntools é um framework para CTFs e desenvolvimento de exploits, escrito em python, com o objetivo principal de agilizar prototipagem e desenvolvimento, mas não tão útil assim caso seja algo mais "profissional".

##  Instalando

Instalar o pwntools é simples. O requisito básico é ter o python3 e o pip \(referente ao python 3\) instalado. Caso esteja usando alguma distribuição debian based \(ubuntu, kali, debian\), os comandos são os seguintes:

```bash
apt-get update
apt-get install python3 python3-pip python3-dev git libssl-dev libffi-dev build-essential
python3 -m pip install --upgrade pip
```

E, para instalar o pwntools em si:

```bash
python3 -m pip install --upgrade pwntools
```

## Utilização Básica

Para utilizar o pwntools, primeiro o importamos com `from pwn import *` e então utilizamos as suas funções como seria feito em python usualmente, por exemplo no código abaixo:

```python
from pwn import *

# Cria uma comunicação com um processo
p = process('./communication')

while True:
    # Recebe uma linha no formato byte array
    line = p.recvline()
    
    # Decoda-se essa linha em UTF-8 (transformando em string)
    line = line.decode("UTF-8")
    print(line)
    
    # Forma uma lista baseada nessa linha, dividindo no ' '
    line = line.split(' ')
    print(line)

    result = int(line[0]) * int(line[2])
    
    # Envia uma linha com o resultado obtido
    # No formato byte array (encodado)
    p.sendline(str(result).encode())
```

## Diferentes Módulos

O pwntools tem vários módulos para diferentes funções, no [vídeo ](https://www.youtube.com/watch?v=OAIvkINgCtQ)sobre comunicações focamos principalmente no módulo Tubes, que permite interação entre processos e algumas ferramentas de redes, mas existem outros que são tão utilizados quanto esse.

### Tubes

Módulo relacionado a comunicação e ferramentas de redes/interação entre processos.

Os principais comandos são:

```python
from pwn import *
# process(nomeprocesso) - cria um canal de comunicação com um processo
    p = process('sh')
    
# remote("ip", porta) - cria um canal de comunicação com um servidor
    r = remote('127.0.0.1', 1337)
    # a maioria dos comandos de remote e processos são iguais
    
# sendline(bytearray) - Envia um byte array para o servidor
    p.sendline(b'AAAAA')
    
# recvline() - Recebe uma linha (em bytes) do servidor
    line = p.recvline()

# recvuntil(b'bla') - Recebe e retorna tudo até a string especificada no argumento (inclusive)
    all = p.recvuntil(b': ')
    
# interactive() - Cria uma sessão interativa (como no terminal)
    p.interactive()
    
# ssh('user', 'ip', password='senha') - Cria uma sessao de ssh
    session = ssh('ganesh', 'gitbook.ganeshicmc.com', password='senha123')
    # p = session.process('sh')
    
```

### Utility

Utilitários no geral, como manipulação de bytes, hashing e manipulação de arquivos

#### Manipulação de números/bytes

```python
from pwn import *
# pack(inteiro) - transforma um número em bytearray
    pack(67305985) # retorna b'\x01\x02\x03\x04'
    
# unpack(bytearray) - transforma bytearray em inteiro
    unpack(b'\x01\x02\x03\x04') # retorna 67305985
    
# p32(numero) - transforma um número em um bytearray de 32 bits
# p64(numero) - transforma um número em um bytearray de 64 bits
    # levam em conta o contexto (bom para transformar endereços para little endian)
    p32(0x80044242) # retorna b'BB\x04\x80' (B é 0x42)
```

#### Arquivos

```python
from pwn import *

# write('nomearquivo', 'dados') # escreve em um arquivo
    write('oi.txt', 'tudobom')
# read('nomearquivo', quantidadeBytes) # lê X caracteres de um arquivo
    read('oi.txt', 5) # retorna 'tudob' 
```

#### Hashing e Encoding

```python
# Base64 (decoding e encoding)
    b64d(b64e('hello')) # retorna hello

# Hashes
    md5sumhex('hello') == '5d41402abc4b2a76b9719d911017c592'
    write('file', 'hello')
    md5filehex('file') == '5d41402abc4b2a76b9719d911017c592'
    sha1sumhex('hello') == 'aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d'

# URL Encoding
    urlencode("Hello, World!") == '%48%65%6c%6c%6f%2c%20%57%6f%72%6c%64%21'

# Hex Encoding
    enhex('hello') # retorna '68656c6c6f'
    unhex('776f726c64') # retorna 'world'
```

### Context

O módulo context serve para mudar especificações de arquitetura, log, timeout, endianness dos arquivos... que tal dar uma olhada [nele](https://github.com/Gallopsled/pwntools-tutorial/blob/master/context.md)?

### Outros

Outros módulos que não vamos falar sobre aqui estão na documentação oficial \(e no tutorial\) nos links extras.

## Links extras

A [documentação ](http://docs.pwntools.com/en/stable/)do pwntools não é muito clara apesar de ter bastante coisa, mas o repositório [pwntools-tutorial](https://github.com/Gallopsled/pwntools-tutorial) funciona como uma boa referência para a biblioteca.

