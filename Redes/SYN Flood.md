# SYN Flood

Quando sua máquina conversa com outra através da internet ela quase sempre usa o protocolo TCP. Esse protocolo permite que duas máquinas abram uma conexão, ou seja, um canal de comunicação preestabelecido. Para que essa conexão seja feita é realizado um procedimento chamado [Three-way handshake](https://hackmd.io/O-7Oa6cKQ3aShXYMGavR2w?both), ou, numa tradução livre, Aperto de mão em três vias.

O ataque SYN Flood toma vantagem justamente de um comportamento inusitado desse procedimento.

Imagine que a máquina A manda o SYN, mas ela não recebe um SYN/ACK como resposta. Isso pode acontecer por diversos fatores: problemas na rede, firewals mal configurados, quedas de energia, etc. É por isso que o protocolo TCP tem os pacotes ACK, trata-se de um mecanismo de confirmação de recebimento de mensagens. Nesse caso, a máquina A entenderia que algo de errado aconteceu e ela reenviaria o pacote SYN. Da mesma forma, se a máquina B envia o SYN/ACK mas recebe um SYN novamente de A, ela entende que A não recebeu o seu SYN/ACK e reenviou o SYN.

O ataque então faz o seguinte: nós enviamos pacotes SYN sem parar, não importando qual seja a resposta do alvo. Ele pensará que nós realmente não estamos recebendo suas respostas e manterá várias conexões abertas por um tempo considerável. Isso faz com que a tabela de conexões do alvo fique lotada com as nossas conexões, impedindo-o de abrir conexões com outras máquinas.

Para isso, usaremos uma ferramenta chamada Hping3:

```
sudo hping3 -c <quantidade de pacotes> -d <tamanho do pacote> -S -p <porta alvo> -i u<tempo> --flood <ip do alvo>
```
---
-c <quantidade> : Quantidade de pacotes a serem enviados
-d <tamanho do pacote> : Tamanho de cada pacote a ser enviado -S: Usar a flag SYN do TCP
-p <porta alvo> : Porta da máquina destino (em geral não importa, desde que seja uma porta onde há um socket em modo LISTEN) 
-i u <tempo> : tempo entre envios (em milissegundos: u100 == 100 milissegundos entre pacotes) --flood: Envia pacotes o mais rápido possível

---

Referências:

[RFC sobre SYN flood](https://tools.ietf.org/html/rfc4987)
[Arigo sobre SYN Flood da Phrack Magazine](http://phrack.org/issues/48/13.html#article)
[Repositório do Hping3 no Github](https://github.com/antirez/hping)
[Wiki do Hping3](http://wiki.hping.org/)