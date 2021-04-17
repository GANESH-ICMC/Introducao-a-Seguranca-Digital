# Ping - Ferramentas: netcat, nmap, wireshark

## Introdução
Nessa aula iremos introduzir algumas ferramentas importantes usadas para
explorar redes e portas, IPs, fazer conexões, mapear pacotes de dados em
tráfego, etc.

## Netcat
Um dos softwares mais utilizados para testes de invasão, é um utilitário
UNIX capaz de ler e gravar dados através de conexões de rede, utilizando
protocolos TCP/UDP.

**TODO**: netcat relação cliente/servidor (deixar claro a parte do servidor)

#### Utilidades do NetCat:
- Estabelecer conexões UDP e TCP
- Transferencia de dados
- Reverse shells

#### Comandos básicos:
- **nc -help**: vai printar uma lista comandos possíveis.
- **nc [options] [host] [porta]**: executa um port scanning padrão.
    - nc -zv [host] 80: escaneia uma porta
    - nc -zv [host] 80 443: escaneia diversas portas
    - nc -zv [host] 80-443: escaneia um conjunto de portas
- **nc -l [host] [porta]**: inicia uma escuta na porta referida.
- **nc [host] [porta] > file_name.out**: envia um arquivo.
- **nc [host] [porta] < file_name.in**: recebe um arquivo.

#### Flags importantes:
- **nc -4**: usa IPv4 somente.
- **nc -6**: usa IPv6.
- **nc -u**: usa UDP ao invés de TCP.
- **nc -k -l**: continua a ouvir na porta mesmo após desconectado.
- **nc -n**: pula procura pelo DNS (Domain Name System).
- **nc -v**: verbose.
- **nc -z**: reporta se as portas estão abertas para conexão ao invés de
  conectar diretamente.

## Nmap
É um software livre de Port Scanning que utiliza de pacotes IP para identificar
todos os aparelhos conectados a uma rede e assim coletar informações sobre os
serviços e sistemas operacionais rodando.

Usos comuns:
- Encontrar IPs das máquinas da rede
- Encontrar portas abertas em um IP
- Identificar sistemas operacionais
- Identifica qual programa está rodando em qual porta (e a versão também)

**Instalação**: https://nmap.org/download.html

#### Comandos Básicos:
- **nmap -sp 192.168.1.1/24**: Ping scan - escaneia todos os dipositivos
  conectados na sua rede local
- **nmap <local ip>**: escaneia um host para as portas mais conhecidas

**Opções de flags:** https://nmap.org/man/pt_BR/man-briefoptions.html

## Wireshark
Software gratuito e open-source de análise de pacotes. A utilidade do Wireshark
consiste em captar o tráfego de dados numa rede local, capturando pacotes de
dados para serem analisados.

**Download**: https://www.wireshark.org/download.html

![](https://i.imgur.com/cGKrc8Z.png)

- **No.**: Número da ordem que o pacote foi capturado. Nesse caso, a linha
  significa que tal pacote faz parte de uma conversa.
- **Time**: Mostra o tempo que o pacote foi capturado após você começar a
  capturar pacotes.
- **Source**: Enredeço que enviou o pacote.
- **Destination**: IP de destino do pacote.
- **Protocol**: Tipo de pacote trafegando na rede, por exemplo, TCP, DNS,
  DHCPv6, or ARP.
- **Length**: Tamanho do pacote em bytes.
- **Info**: Coluna que mostra informações adicionais sobre o conteúdo do
  pacote, o qual varia dependendo do tipo de pacote.

## Bibliografia

### NetCat
- https://www.varonis.com/blog/netcat-commands/
- https://en.wikipedia.org/wiki/Netcat
- https://www.4security.com.br/o-poderoso-netcat/
- https://nmap.org/ncat/

### Nmap
- https://nmap.org/
- https://www.varonis.com/blog/nmap-commands/
- https://www.freecodecamp.org/news/what-is-nmap-and-how-to-use-it-a-tutorial-for-the-greatest-scanning-tool-of-all-time/
- https://pt.wikipedia.org/wiki/Nmap
- https://github.com/nmap/nmap

### Wireshark
- https://www.varonis.com/blog/how-to-use-wireshark/
- https://www.wireshark.org/
- https://en.wikipedia.org/wiki/Wireshark
