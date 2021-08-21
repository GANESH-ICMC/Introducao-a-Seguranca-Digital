# Espionagem FTP
Conteúdo: ftp, terminal

As anotações do Guerra indicam que temos que nos conectar a um servidor FTP do
Hiro. Também comentam sobre ele ter faltado em algumas aulas de segurança.
Temos dois caminhos para resolver esse desafio, o primeiro dizrespeito à
primeira informação. Se nos lembrarmos do **FTP do Charlão**, perceberemos que
lá é vazada uma credencial de um servidor FTP..., basta usá-las para nos
conectarmos ao servidor. Um `ls` lista o conteúdo do diretório FTP e um `get`
faz o download do arquivo com a flag.

O segundo caminho faz uso da segunda informação. Se procurarmos um pouquinho
sobre vulnerabilidades do FTP, encontraremos, além da falta de criptografia,
algo relacionado ao usuário `anonymous` habilitado. Esse usuário permite a
conexão sem senha e, muitas vezes, pode compremeter o sistema. Fazendo login
com esse usuário no servidor FTP, veremos um arquivo com a flag. Seguindo o
mesmo procedimento do método 1, teremos o arquivo com a flag no nosso
computador.

Flag 1: `Ganesh{H1r0_1s_g0d}`

Flag 2: `Ganesh{An0nym0us_f0r_th3_w1n}`
