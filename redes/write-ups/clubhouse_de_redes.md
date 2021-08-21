# Clubhouse de Redes
Conteúdos: `wireshark`, `espectrogramas`

Analisando no '.pcapng' as poucas streams que temos, não conseguimos achar
nada. Dado o tamanho do '.pcapng', provavelmente temos um arquivo dentro dele
e, portanto, vamos ver os objetos HTTP presentes nele.

Para isso, seguimos o caminho `File -> Export Objects -> HTTP` e vemos que há
um arquivo de áudio chamado `flag.wav`. A descrição do chall da uma dica para
usarmos o Audacity ("cidade de Auda") para vermos o espectrograma ("espectros")
do arquivo. Para a visualização ficar boa, configuramos com um rate de 16KHz
("km 16000") e logo de cara vemos uma imagem, onde podemos identificar a flag.

Flag: `Ganesh{entr4nd0_n4_fr3qu3nc1a}`
