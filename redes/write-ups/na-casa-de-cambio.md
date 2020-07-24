## Na Casa de Câmbio

Esse chall é basicamente uma continuação do Tubarão no Fio aprofudando um pouco mais no uso da ferramento Wireshark.

Para resolvê-lo basta abrir o .pcap que está anexado ao chall com o wireshark:

$ wireshark na_casa_de_cambio

Dessa vez, ao abrir o pcap temos diversos pacotes, então teremos que analisar o que está acotecendo.

Existem apenas 2 ip's que se intercalam entre source e destination. Ou seja, está acontecendo um dialogo com comutação de pacotes, basicamente como funciona qualquer conexão em redes.

Para facilitar a leitura desse diálogo, iremos aplicar um filtro:

Clique com botão direito > Follow > TCP Stream

OBS: Se tivessem diversos diálogos acontecendo nessa rede esse filtro seria ainda mais útil, pois trocando as streams conseguimos ver esses diferentes 'canais'.

O conteúdo dos pacotes aparecem da seguinte maneira:

Al.., Capit..o Cruz buscando comunica....o. C..mbio.

Comunica....o aceita soldado, onde voc.. est..? C..mbio.

Consegui me livrar do imp..rio Tuberculoso e agora estou pr..ximo daquela casa de cambio.

Casa de que soldado? Acho que cortou o final. C..mbio.

N..o importa capit..o, conseguimos roubar uma bandeira do imp..rio Tuberculoso com o seguinte escrito: Iazfav{e4s4_pf_k4ad10_c4yc10}

Essa .. a bandeira que est.. criptografada, mas eu tenho certeza que a chave .. cambio.

A chave .. o que capit..o? Acho que aqui cortou tamb..m.

O texto nos fornece a flag (Iazfav{e4s4_pf_k4ad10_c4yc10}) e também a chave para descriptografar a flag ('cambio').

Uma das cifras mais famosas que utiliza chave é a de Vigenere, justamente a que é preciso utilizar para se chegar à flag correta.
