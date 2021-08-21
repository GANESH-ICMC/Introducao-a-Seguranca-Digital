# Consulta Marcada
Conteúdos: portas, `nmap` e `netcat`

Ao executarmos o binário, ele pede que passemos alguma porta pela linha de
comando. Em seguida, passando uma porta, obtemos que essa porta está trancada.

Para resolver isso, precisamos abrir a porta - podemos usar o netcat no modo
servidor para ficar escutando em uma porta, com `nc -l -p <alguma_porta>`. Em
seguida, vemos que a conexão não vai acontecer na porta que passamos, mas sim
na porta `1337`.

Então, precisamos conectar na porta `1337` do localhost. Vamos abrir outro
netcat, agora no modo cliente, para estabelecer essa comunicação. Usando `nc
127.0.0.1 1337` conseguimos fazer isso. 

Por fim, é só escrever a mensagem pedida pelo binário e receberemos a flag.

Flag: `Ganesh{d3nt4dur4_d3_r3de5}`
