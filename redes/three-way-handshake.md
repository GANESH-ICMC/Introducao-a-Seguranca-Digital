# Three-way Handshake

![](https://i.imgur.com/xO66AX7.jpg)

O Three-way Handshake \(que pode ser traduzido como "aperto de mão de três vias"\) é um mecanismo especificado na documentação do protocolo TCP para o estabelecimento de conexões TCP.

> Notas: ACK = Acknowledgement flag \(Flag de reconhecimento\) SYN = Synchronize flag \(Flag de sincronização\)

**Flags** são nada mais do que bits em um pacote TCP. Por exemplo, é convencionado que 2 bits são, respectivamente, as flags ACK e SYN. Se você recebe um pacote e esses bits são 10 então esse pacote tem a flag ACK ativa, se eles são 11 então o pacote é SYN/ACK, e assim por diante \(o TCP tem mais flags além dessas duas, como FIN e RST\).

Uma conexão TCP é [geralmente](https://tools.ietf.org/html/rfc793#section-3.4) estabelecida em 3 etapas:

1. O cliente envia um pacote com a flag SYN ativa.
2. O servidor responde com um pacote com as flags SYN + ACK.
3. O cliente reponde com um pacote com a flag ACK.

Em outras palavras, a conexão entre cliente e servidor a partir do Three-way Handshake pode ser explicada da seguinte maneira:

**1. Cliente:** Servidor, estou enviando a mensagem com número de sequência 100 \(SEQ=100\). Dá pra sincronizar \(SYN\)?

Cliente **--------SYN----&gt;** Servidor

**2. Servidor:** Claro \(ACK\), sincroniza a mensagem 200 \(SEQ=200\) que estou enviando \(SYN\). Prossiga com a mensagem 101 \(ACK=101\).

Cliente **&lt;------------SYN----** Servidor

**3. Cliente:** Ok, recebi a mensagem 200 \(ACK=201\), estou enviando a mensagem 101 \(SEQ=101\).

Cliente **------------&gt;** Servidor

O cliente e o servidor, possuem números de sequência distintos, por este motivo é necessária a sincronização \(SYN\) em ambos os sentidos.

Feita a sincronização, começam a troca de pacotes com base em números de sequência, que tem o objetivo de enumerar os pacotes de cada um.

### Demonstração com o Wireshark:

#### Primeira via

![](https://i.imgur.com/wr0iFMS.png)

O cliente \(192.168.43.64\) envia uma solicitação de sincronização \(SYN\) para o servidor \(186.192.81.25\). Esta solitação parte da porta 33080 com destino a porta 443, com número de sequência 0 \(Seq=0\).

Repare que a porta do cliente \(33080\) e do servidor \(443\) não precisam ser iguais. Repare ainda que a porta 443 é a [well-known port](http://web.mit.edu/rhel-doc/4/RH-DOCS/rhel-sg-pt_br-4/ch-ports.html) para o protocolo HTTPS.

#### Segunda via

![](https://i.imgur.com/Sdj1YGe.png)

O servidor envia ao cliente uma solicitação de sincronização \(SYN\) com número de sequência 0 \(Seq=0\), juntamente com a confirmação \(ACK=1\) da solicitação de sincronização enviada anteriormente pelo cliente.

#### Terceira via

![](https://i.imgur.com/P9Z4x2Q.png)

O cliente \(192.168.43.64\) então confirma a solicitação de sincronização \(SYN\) para o servidor \(186.192.81.25\). Esta confirmação parte da porta 33080 com destino a porta 443, com número de sequência 1 \(Seq=1\).

## Referências

* [Descrição do three-way handshake \(RFC\)](https://tools.ietf.org/html/rfc793#section-3.4)
* [Primeira versão do protocolo TCP](https://tools.ietf.org/html/rfc793)
* [Resumo da IETF do TCP \(original e mudanças feitas até agora\)](https://tools.ietf.org/html/rfc7414)

