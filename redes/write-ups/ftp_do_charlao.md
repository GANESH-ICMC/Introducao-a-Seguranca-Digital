# FTP do Charlão
Conteúdo: ftp, pcap, wireshark

Nesse desafio, é disponibilizado um arquivo pcap (gravação dos pacotes que
passaram pela interface de rede do computador). Para analisar esse arquivo,
podemos usar o *wireshark*. Ao abrir o arquivo, vemos que temos vários pacotes
para analisar, mas a maioria é ruído e temos a indicação de que o que nos importa
é relacionado a FTP (um protocolo de compartilhamento de arquivos em rede).

Aplicando o filtro `ftp` no wireshark, vemos um conjunto de pacotes que mostram
a conexão com um servidor. Como o FTP não usa criptografia, podemos ver todas
as informações trocadas. Desta forma, descobrimos o usuário (`hiro`) e a senha
(`redes123`). Procurando um pouco sobre o FTP, conseguimos descobrir que ele
usa a porta 21 para mensagens de controle (login, comandos, etc) e a porta 20
para o envio de arquivos. Desta forma, podemos utilizar o filtro `tcp.port ==
20` para ver os dados enviados. Olhando o fluxo TCP, vemos um arquivo sendo
transferido e seu conteúdo nos dá a flag.

Flag: `Ganesh{pr0f3ss0r_ch4rl3s}`
