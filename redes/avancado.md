# Avançado

## Aulas Ganesh Redes 2019

### Sumário

* [Aula 1: Introdução – Protocolos, TCP/IP, NAT, Endereçamento](https://hackmd.io/ssK5SvdFTTWNXeYR8kyHTw?both#Aula-1-Introdu%C3%A7%C3%A3o-%E2%80%93-Protocolos-TCPIP-NAT-Endere%C3%A7amento)
* [Aula 2: Bettercap, MITM e Spoofing](https://hackmd.io/ssK5SvdFTTWNXeYR8kyHTw?both#Aula-2-Bettercap-MITM-e-Spoofing)
* [Aula 3: DoS, DDoS, ADoS e Slow Lorris](https://hackmd.io/ssK5SvdFTTWNXeYR8kyHTw?both#Aula-3-DoS-DDoS-ADoS-e-Slow-Lorris)
* [Aula 4: SSL/TLS, HTTP/HTTPS e HSTS](https://hackmd.io/ssK5SvdFTTWNXeYR8kyHTw?both#Aula-4-SSLTLS-HTTPHTTPS-e-HSTS)
* [Aula 5: Coisas importantes que você precisa saber sobre a Internet](https://hackmd.io/ssK5SvdFTTWNXeYR8kyHTw?both#Aula-5-Coisas-importantes-que-voc%C3%AA-precisa-saber-sobre-a-Internet)
* [Aula 6: Deauthentication Attack em Redes Wi-Fi](https://hackmd.io/ssK5SvdFTTWNXeYR8kyHTw?both#Aula-6-Deauthentication-Attack-em-Redes-Wi-Fi)
* [Aula 7: WPS, PIN codes, Reaver e Pixie Dust](https://hackmd.io/ssK5SvdFTTWNXeYR8kyHTw?both#Aula-7-WPS-PIN-codes-Reaver-e-Pixie-Dust)
* [Aula 8: DHCP Exhaustion/Starvation](https://hackmd.io/ssK5SvdFTTWNXeYR8kyHTw?both#Aula-8-DHCP-ExhaustionStarvation)

#### Ficando Atualizado \(ou "Sempre na Crista da Onda"\)

* [Blog de segurança da Mozilla](https://blog.mozilla.org/security/)

#### MISC

* Diferença entre Roteador e Access Point

#### ATAQUES

* **MITM**
* **Spoofing**
  * Mac changer
  * IP spoofing
  * ARP spoofing
  * DNS spoofing/poisoning
* **DoS**
  * SYN flood
  * ICMP flood
  * DHCP starvation
  * Rogue DHCP
* **Botnet**
  * Malwares
  * LOIC
  * HOIC
* **Wifi**
  * WPS PIN brute forcing
  * Deauth
* **Website cloning**

#### FERRAMENTAS

* Nmap
* Bettercap
* Wifi Pumpkin
* Reaver, Wash, Pixie Dust
* Linset
* Fake ap
* Wi-filax

## Aula 1: Introdução -- Protocolos, TCP/IP, NAT, Endereçamento

* Protocolos
  * Walkie talkie \("câmbio", "copiei"\)
  * SUS \(coleta de dados &gt; triagem &gt; médico\)
  * Protocolos vs Protocolos de comunicação
  * Protocolo Walkie talkie: independente da pessoa/equipamento de walkie talkie
  * Ideia: hardwares/softwares diferentes mas que conseguem se comunicar
  * RFC \(Request For Comments\): IETF \(Internet Engineering Task Force\)
    * Documento
    * Dúvida: Qualquer um pode fazer parte da IETF?
      * [https://www.ietf.org/about/participate/](https://www.ietf.org/about/participate/)
      * [https://www.ietf.org/about/participate/get-started/](https://www.ietf.org/about/participate/get-started/)
      * [https://www.ietf.org/about/participate/tutorials/](https://www.ietf.org/about/participate/tutorials/)
* IP: Internet Protocol
  * Host to Host \(máquina a máquina\)
  * Semântico \(!= do MAC\) e hierárquico \(País &gt; Estado &gt; Cidade &gt; Rua &gt; Número\)
  * Semântica ajuda nos protocolos de roteamento
  * Octeto
  * Máscaras de Sub-rede
    * Classes
    * Historinha dos IPs perdidos
    * Ex: calcular máscara
    * Ex: calcular número de hosts/redes
    * Dúvida: Por que preciso de mais bits pra rede?
  * Endereço de Rede \(192.168.32.2/24 =&gt; 192.168.32.0\)
    * Bits de host zerados
    * Dúvida: Pra que serve isso?
  * Endereço de Broadcast \(192.168.32.2/24 =&gt; 192.168.32.255\)
    * Bits de host settados
    * Dúvida: Pra que serve isso? Fazer Broadcast!
    * Ex: Ping broadcast
  * IP não garante que o destino recebeu o pacote!!
  * IPv5
  * DHCP
  * Alternativas ao IP
  * Tooling: nmap \(network scan =&gt; descobrir hosts ativos na rede\), IP spoofing

192 .168 .254 .128 /24 11000000 10101000 11111110 11111110 RRRRRRRR RRRRRRRR RRRRRRRR HHHHHHHH \(24\) 11111111 11111111 11111111 00000000 255 .255 .255 .0 /??

* TCP
  * Processo a processo/Inter-process communication \(programa a programa\)
  * Portas
  * Conexão \(definida por um par de sockets\)
  * Socket \(???\)
  * Número de série \(garantir recebimento do pacote\)
  * Dúvida: o que é um socket 'listening'? \(netcat\)
  * Three-way handshake \(limite de conexões, hping3\)
    * Todo pacote do TCP deve ter um ACK correspondente \(INCLUSIVE O SYN\)
    * SYN, SYN/ACK, ACK
    * Outros tipos de pacotes: FIN, RES, etc.
    * Curiosidade: Four-way handshake
  * NAT \(Network Address Translation\)
    * Várias máquinas atrás do mesmo endereço
    * Diferenciação pela porta
    * Ex: Call of Duty
  * Tooling: nmap \(portscan\), hping3 \(connection flood\), netcat \(nc, ncat,...\)

#### Segurança

* IP spoofing
* MITM/MITMA/MIM \(Man in the Middle Attack\)
* Connection flood
* Portscanning

#### Exercícios

* Nmap: Descobrir hosts conectados em alguma rede \([https://resources.infosecinstitute.com/nmap/](https://resources.infosecinstitute.com/nmap/)\) e fazer um SYN flood nele com hping3
* Echo Server \(python, socket.socket\)/Client
* Xtra2: Ip spoofing
* Xtra3: Traceroute \(o que é, como fazer\)

## Aula 2: Bettercap, MITM e Spoofing

* What is monitor mode? How do I read packets of networks I don't have access to?
* Interactive vs Non-interactive
  * '-eval'
  * '-caplets'
* Ticker: deamonizing commands
  * ticker. 
  * ticker.period
* ARP spoofing
  * Spoofs gateway by default \(can be deactivated\)
  * 
* Sniffer
  * 
* HTTP proxy \(redirect http traffic\)
* SSLStrip

### MITM \(Man in the middle\)

Um ataque man in the middle \(lit. homem no meio\) é feito visando a enganar o computador da vítima a pensar que o atacante é o roteador \(ou outro dispositivo / serviço pelo qual passem informações sensíveis\) e também enganar o roteador \(ou dispositivo / serviço... sensíveis\) e fazê-lo pensar que o atacante é a vítima. Desse modo, todo o tráfego de dados passará pelo computador do atacante, e a conexão não será rompida. Portanto, o ataque é transparente ao uso cotidiano.

* Materiais:
  * Bettercap cheat sheet: [https://www.cyberpunk.rs/bettercap-usage-examples-overview-custom-setup-caplets](https://www.cyberpunk.rs/bettercap-usage-examples-overview-custom-setup-caplets)
  * Bettercap tutorial \(gostei mais\): [https://www.kalitut.com/2019/04/how-to-install-and-use-bettercap.html\#point3](https://www.kalitut.com/2019/04/how-to-install-and-use-bettercap.html#point3)

## Aula 3: DoS, DDoS, ADoS e Slow Lorris

#### DoS \(Denial of Service\)

Um ataque DoS visa impedir o acesso a determinado recurso ou serviço.

* Exemplos: excluir um arquivo \(negação de acesso ao arquivo\); impedir conexões em um servidor

No caso de impedir conexões em um servidor alvo, deve-se inundar \("floodar"\) o tráfico de Internet dele. Normalmente, isso é feito por meio do envio de muitas requisições ao servidor, superando sua capacidade de receber novas conexões. Nesse sentido, podemos pensar que o servidor é uma grande avenida que se encontra com um trânsito de carros muito grande. Esse excesso de tráfego torna a entrada de outro veículo na avenida praticamente impossível.

Um jeito simples de fazer tal ataque é mandar uma requisição de conexão ou um ping com frequência superior a capacidade de processamento dessas requisições por parte do servidor.

* Resolver esse ataque é simples: basta fazer blacklist do IP do atacante.

#### DDoS \(Distributed DoS\)

Enquanto o ataque DoS parte de uma única máquina, o DDoS faz uso de múltiplos dispositivos conectados à Internet \(computadores, dispositivos IoT, celulares etc.\). Dessa forma, o ataque torna-se mais eficiente. Os dispositivos utilizados no ataque podem estar participando por boa vontade ou podem ser parte de uma **botnet**.

* Os dispositivos que formam uma botnet foram infectados por algum malware que dá ao atacante \("dono" do malware\) controle remoto sobre cada um deles.

Resolver um DDoS já bem mais difícil, pois as requisições estão vindo de diversos dispositivos \(IPs diferentes\), fazendo com que o ataque pareça tráfego normal.

#### \(D\)DoS Refletido \(Reflection DoS\)

O atacante envia pacotes \(ping ou alguma outra requisição\) para um servidor \(chamado de refletor\) pedindo que o pacote seja repassado para outro IP, o do verdadeiro alvo.

* Esse ataque spoofa o IP do atacante, pois passa pelos servidores refletores.

Caso o ataque parta de uma máquina, resolvê-lo é simples, pois a banda de um servidor tende a ser muito maior do que a de um computador pessoal. Entretanto, esse ataque também pode ser um DDoS.

#### ADoS \(Amplified DoS\)

Nesse ataque, faz-se uso de requisições spoofadas para servidores mal-configurados. Uma certa quantidade de pequenas requisições com o IP spoofado do servidor alvo é enviada para servidores acessíveis. Os servidores respondem para o IP do alvo com pacotes muito maiores \(amplificados\), floodando o serviço de forma muito mais fácil.

Pode-se amplificar o ataque usando um comando de EDNS0, que aumenta o tamanho do pacote de resposta \(até 70 vezes maior\), ou usando o comando mullist do protocolo NTP, que aumenta o tamanho do pacote de 20 a 200 vezes.

ADoS não são triviais de serem resolvidos, o melhor jeito é blacklist todos os servidores envolvidos no ataque e esperar passar.

#### Memcached DDoS

**O sistema memcached:**

Memcached é um cache "in-memory" bem veloz usado para acelerar aplicações web dinâmicas, aliviando o carregando a partir de bases de dados. Por exemplo, uma aplicação manda uma requisição para o servidor memcached antes de mandar para um bando de dados. O servidor memcached armazena respostas de requisiões comuns, portanto, se ele tem a resposta para a requisição feita, o banco de dados sequer é acessado. Do contrário, o memcached responde que não tem o conteúdo e uma requisição é enviada ao banco de dados. Além disso, a memória "sobrando" em certas partes do sistema Memcached é disponibilizada para áreas nas quais falta memória \(isso aumenta virtualmente a quantidade de cache disponível\)

**O ataque:**

O ataque funciona da mesma forma que um ADoS. Ele só é possível pois os servidores memcached, por padrão, operam usando o protocolo UDP. Logo, como não há handshake, dados podem ser enviados ao servidor alvo sem o real consentimento dele.

São enviadas requisições spoofadas \(com o IP do servidor alvo\) para o servidor memcached, que responderá com pacotes de tamanhos muito maiores ao alvo, floodando-o e impedindo que ele processe outras requisições.

Para defender-se: desabilite UDP no servidor memcached e use firewall.

#### Slow Lorris e R.U.D.Y.

Outra maneira de atacar servidores é usando ataques de protocolo \(camadas 3 e 4 do modelo OSI\), como o Slow Lorris e o R.U.D.Y.

Ambos esses ataques consistem no estabelecimento de conexões com o servidor e no envio extremamente lento \(e constante\) dos bytes de cada pacote, utilizando pouca banda e mantendo todas as conexões abertas.

* Slow Lorris faz uso de requisições do tipo HTTP GET
* R.U.D.Y. faz uso de requisições do tipo HTTP POST

Se feito corretamente, um computador "caseiro" pode parar um servidor comercial sozinho.

#### SYN Flood

É o ataque explora o funcionamento do TCP para estabelecer conexões\(o three-way handshake\).

No handshake, o servidor fica esperando um pacote de confirmação \(ACK packet\) para estabelecer a conexão. Portanto, o atacante envia muitos pacotes SYN \(e nenhum pacote ACK!\), fazendo com que o servidor fique esperando a confirmação de cada conexão \(que nunca chega\). Assim, o servidor torna-se incapaz de abrir uma conexão real pelo número de requisições em aberto.

Uma possível solução é realizar uma filtragem dos pacotes.

#### ICMP \(Ping\) Flood

É o ataque que utiliza ping \(echo\) requests. Use-se o protocolo ICMP, que exige um consumo de banda para envio e para resposta. O objetivo é sobrecarregar o alvo por meio do envio de muitas requisições ICMP - obrigando o servidor a responder a todas -, superando sua capacidade de responder a conexões.

Para evitar esse ataque, é possível desativar a funcionalidade ICMP do servidor, impedindo o envio de requisições ping ou traceroute.

#### DNS Flood

Esse ataque visa floodar servidores DNS \(os "DNS resolvers"\), impedindo que haja resoluções DNS - comprometendo, portanto, a capacidade do servidor alvo de responder à tráfego legítimo \(a não ser que a pessoa utilize IPs para conectar-se a algum endereço\).

Esse ataque requer muita banda para ser efetivo.

#### Materiais Adicionais

* [Material geral sobre DDoS \(Cloudflare\)](https://www.cloudflare.com/learning/ddos/what-is-a-ddos-attack/)
* [Como fazer DDoS \(Cloudflare\)](https://www.cloudflare.com/learning/ddos/ddos-attack-tools/how-to-ddos/)
* [Código pra fazer Slow Loris](https://github.com/gkbrk/slowloris)
* [Outro código pro Slow Loris, em Go](https://github.com/valyala/goloris)
* [SYN Flood \(Phrack Magazine\)](http://phrack.org/issues/48/13.html#article)
  * **Obs:** Se você não conhece a Phrack, é muito importante tanto para cultura hacker/histórico quanto sobre conteúdo de primeira em geral
* [SYN Flood \(RFC 4987\)](https://tools.ietf.org/html/rfc4987)
* [Memcached](https://memcached.org/about)
  * [Vídeo explicando o funcionamento do memcached ](https://www.youtube.com/watch?v=1MAgt0bFdwM)

## Aula 4: SSL/TLS, HTTP/HTTPS e HSTS

#### HTTP: HyperText Transfer Protocol

* Protocolo usando para transmitir HTML via internet
* Não usa criptografia alguma \(tudo em texto plano\)
* HTTPS: HTTP uasndo criptografia \(SSL/TLS\)

#### Certificados e Unidades Certificadoras \(CAs\)

HTTPS funciona primariamente baseado em **confiança**, ou seja, é preciso confiar no servidor com o qual você está falando. Para isso, SSL/TLS são equipados com _certificados_.

Certificados são documentos assinados por instituições em quem o cliente confia _a priori_: as **Autoridades Certificadoras \(CAs\)**. Esses documentos garantem que o servidor com o qual um determinado cliente está falando é confiável e, mais, que é ele mesmo \(não uma cópia feita por um atacante\).

Para ilustrar isso melhor imagine que Merindrola é o site que quer "provar" para o cliente Marcelo \(popularmente conhecido como 'Batatinha'\) que ela é um site leígitimo e não uma cópia. Batatinha é grande amigo do Carlos \(a Autoridade Certificadora\), e confia 100% nele. O que acontece quando uma Autoridade Certificadora assina um certificado de um servidor é equivalente a Carlos dizendo a Batatinha que Merindrola é parça \(morô?\).

**CSR \(Certificate Signing Request\):** Requisição feita do servidor para a CA para que seja emitido um certificado para o a aplicação.

**Self-Signed Certificate:** Certificado assinado por uma "Autoridade Certificadora" criada pelo próprio site/app \(nada seguro, deve ser usado somente para testes\)

**Obs.:** Veja o vídeo nos materiais adicionais sobre Certificados e Autoridades Certificadoras.

#### HSTS: HTTP Strict Transport Security

* Política de segurança para garantir obrigatoriedade no uso de HTTPS
* Na prática, HSTS é nada mais que um header contido na resposta do servidor ao cliente
* Quando um cliente recebe alguma resposta do servidor com o header `Strict-Transport-Security` significa que todos os requests feitos para o servidor após aquele deverão usar HTTPS \(nunca HTTP\) por um certo período de tempo
* Header `Strict-Transport-Security`
  * `max-age`: tempo em segundos da validade do HSTS \(em segundos\)
  * `includeSubDomains`: todos os subdomínios também só poderão ser acessados por HTTPS

#### Vulnerabilidades no HSTS

* O primeiro pacote mandado pelo cliente ainda usa HTTP, pois é o servidor que deve especificar, através do header HSTS, a obrigatoriedade do HTTPS. Portanto, é ainda possível estabelecer o SSL Stripping, mas somente na interceptação do primeiro request feito em HTTP pelo cliente.
* _"Because HSTS is time limited, it is sensitive to attacks involving shifting the victim's computer time e.g. using false NTP packets."_ \(Wikipedia\)

#### Atacando HSTS

* [NSE script \(script do Nmap\) para verificar o uso de HSTS em domínios](https://github.com/icarot/NSE_scripts/blob/master/http-hsts-verify.nse)
* [BlackHat Conf: Bypass HSTS](https://www.youtube.com/watch?v=eLhb4jZuv6M)
* [Ferramenta MITM para alterar o relógio do SO através do NTP \(fazer parecer que o HSTS expirou\)](https://github.com/PentesterES/Delorean)
* [Modern MITM attacks](https://maxpl0it.com/modern-man-in-the-middle-attacks/)

#### Materiais Adicionais:

* [Vídeo sobre certificados e CAs em HTTPS](https://www.youtube.com/watch?v=T4Df5_cojAs)
* [Página da Wikipedia sobre HSTS](https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security)
* [Vídeo básico HSTS e HTTP](https://www.youtube.com/watch?v=zEV3HOuM_Vw)
* [OWASP HSTS Guide](https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Strict_Transport_Security_Cheat_Sheet.html)
* [Como funciona a Preload list do Firefox \(Mozilla sec blog\)](https://blog.mozilla.org/security/2012/11/01/preloading-hsts/)
* \[Listas de Preload do Firefox\]\([https://wiki.mozilla.org/SecurityEngineering/HTTP\_Strict\_Transport\_Security\_\(HSTS\)\_Preload\_List](https://wiki.mozilla.org/SecurityEngineering/HTTP_Strict_Transport_Security_%28HSTS%29_Preload_List)\)
* [Teste de sites que contêm HSTS Preload](https://hstspreload.org/)
* [Definição do header HSTS \(Mozilla Developer Network\)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Strict-Transport-Security)
* [RFC do HSTS \(RFC 6797\)](https://github.com/GANESH-ICMC/Introducao-a-Seguranca-Digital/tree/903dd7e9d77755234289ef3c8e78dceeec70ce48/Redes/tools.ietf.org/html/rfc6797/README.md)
* [OWASP Transport Layer Protection Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Protection_Cheat_Sheet.html)

## Aula 5: Coisas importantes que você precisa saber sobre a Internet

#### Internet vs Web

A primeira coisa que precisamos entender é que Internet e Web são coisas diferentes. Acredite se quiser, existiu um tempo em que a Internet existia mas a Web não -- mais precisamente, de 1969 até 1989.

Internet é a rede mundial de computadores, trata-se da _infraestrutura_: cabos, roteadores, protocolo IP \(_Internet_ Protocol\). Tudo isso forma a internet.

A Web, ou World Wide Web, é uma _aplicação distribuída que usa a infraestrutura da internet_. É o conjunto de servidores web \(servidores HTTP/HTTPS\) e clientes web \(browsers, curl, etc.\) que trocam páginas HTML. Quando ouvir falar de Web, pense em páginas HTML \(hoje em dia vêm acompanhadas de JavaScript e CSS\), protocolos HTTP e HTTPS.

#### Protocolos na prática

* sockets
* portas TCP
* portas UDP

#### APIs \(Application Programming Interfaces\)

São interfaces, conjuntos de padrões de ações, entradas e saídas, para interação de clientes com servidores. A grande vantagem das APIs é que elas abstraem chamadas de funções em um servidor.

Por exemplo, imagine que a Merindrola quer fazer um site para mostrar informações sobre o clima na cidade dela: São Carlos \(SP\). Ela então vai no site do INPE e descobre como funciona a API deles. A [API do INPE](http://servicos.cptec.inpe.br/XML/) é razoavelmente simples, vamos pegar como exemplo a previsão do tempo dos próximos 4 dias: 1. Você manda para eles [uma requisição](http://servicos.cptec.inpe.br/XML/#req-previsao-4-dias) com o código da localidade \([encontrado aqui](http://servicos.cptec.inpe.br/XML/listaCidades)\):

```text
    http://servicos.cptec.inpe.br/XML/cidade/codigo_da_localidade/previsao.xml
```

1. Achado o código, que no caso da Merindrola é 4774, fazemos uma requisição GET na url \(aqui, vamos usar o `wget` para exemplificar\):

   ```text
    $ wget http://servicos.cptec.inpe.br/XML/cidade/4774/previsao.xml
   ```

2. Temos como retorno um arquivo, nesse caso é `XML`, mas poderia ser `JSON`, que é mais comum atualmente:

   ```text
    <?xml version='1.0' encoding='ISO-8859-1'?><cidade><nome>S�o Carlos</nome><uf>SP</uf><atualizacao>2019-10-02</atualizacao><previsao><dia>2019-10-02</dia><tempo>ps</tempo><maxima>33</maxima><minima>17</minima><iuv>11.0</iuv></previsao><previsao><dia>2019-10-03</dia><tempo>ps</tempo><maxima>32</maxima><minima>20</minima><iuv>10.0</iuv></previsao><previsao><dia>2019-10-04</dia><tempo>ps</tempo><maxima>32</maxima><minima>17</minima><iuv>11.0</iuv></previsao><previsao><dia>2019-10-05</dia><tempo>ps</tempo><maxima>33</maxima><minima>20</minima><iuv>11.0</iuv></previsao></cidade>
   ```

3. O arquivo pode parecer confuso, mas como tudo relacionado a APIs, ele segue um _padrão_ e, claro, esse padrão está especificado também na [página do INPE](http://servicos.cptec.inpe.br/XML/#res-previsao-4-dias).
4. Finalmente, Merindrola pode _parsear_ esses dados e fazer seu site lindamente.

Existem vários jeitos de se fazer uma API, vamos falar sobre dois padrões famosos de APIs: SOAP e REST.

#### SOAP vs REST

* **SOAP \(Simple Object Access Protocol\)** é um protocolo de troca de informações para serviços web. APIs que fazem uso desse protocolo utilizam XML para se comunicar. Uma característica do SOAP é que ele pode ser utilizado com a maioria dos protocolos de transporte, como HTTP, SMTP, TCP etc.
* **REST \(Representational State Transfer\)** é uma estilo de arquitetura para serviços web. APIs que fazem o uso dessa arquitetura são chamados APIs RESTful. Seu protocolo de transporte é necessariamente HTTP/HTTPS e APIs RESTful podem utilizar diferentes formas de transferncia de dados, como JSON, XML e YAML. Ela segue 6 princípios:
  * Arquitetura cliente-servidor
  * Sem monitoramento de estado
  * Capacidade de cache
  * Sistema em camadas
  * Código sob demanda \(opcional\)
  * Interface uniforme

#### Materiais adicionais

* [Post do medium super legal com introdução a flask](https://medium.com/@onejohi/building-a-simple-rest-api-with-python-and-flask-b404371dc699)
* [Palestra sobre decorators em Python \(PyData\)](https://www.youtube.com/watch?v=cKPlPJyQrt4)
* [Mais sobre APIs](https://www.redhat.com/pt-br/topics/api/what-are-application-programming-interfaces)
* [Mais sobre SOAP vs REST](http://www.matera.com/blog/post/rest-usa-json-e-soap-usa-xml-certo)
* [Especificações do SOAP v1.2](https://www.w3.org/TR/soap12/)
* [Sobre REST e JSON](http://www.matera.com/blog/post/rest-nao-e-json)

## Aula 6: Deauthentication Attack em Redes Wi-Fi

#### Protocolo 802.11

O protocolo 802.11 é o que se conhece por wifi. Ele especifica como a informação deve ser organizada ao ser transmitida de uma placa de rede para outra.

![](https://community.cisco.com/legacyfs/online/legacy/7/2/1/90127-2.png)

Esse ataque se utiliza de uma falha de segurança \(ou feature ?\) nos pacotes 802.11 onde os pacotes do tipo "Deauthenticate"

#### Informações importantes

É importante estar familiarizadx com a maneira pela qual as interfaces de rede, bem como os modos de operação de placas de rede sem fio \(managed e monitor\).

#### O ataque

Primeiramente devemos iniciar uma interface em modo monitor.

```text
# iw list
```

O comando

```text
# iw dev wlan0 interface add mon0 type monitor
```

irá adicionar uma interface virtual funcionando em modo monitor. Podemos comprovar isso com

```text
# ifconfig
```

que agora deve listar a nova interface.

Agora utilizaremos alguns programas da suite -ng.

```text
# airodump-ng mon0
```

faz uma varredura dos canais suportados atualmente pela placa de rede \(de acordo com a configuração de país ???\), e mostra um sumário de cada BSS e suas respectivas estações conectadas. É possível utilizar argumentos de filtro caso necessário.

Com nosso alvo escolhido, isto é, seu BSS ou BSS + MAC encontrados, podemos começar o ataque. O seguinte comando irá enviar pacotes de desautenticação como se fosse o BSSID especificado. É possível passar o MAC da estação de destino também, com a flag -c

```text
# aireplay-ng -0 0 -a xx:xx:xx:xx:xx:xx -c xx:xx:xx:xx:xx:xx
```

#### Troubleshooting

* "Meu aireplay não vai"

  Verifique se o canal da interface é o mesmo do BSS

* "Device is busy ou algo do tipo"

  Se você adicionou uma interface virtualmente, ela funciona de modo mutex com a interface real. Desative a wlan0 da vida com

  ```text
  # ifconfig wlan0 down
  ```

#### Materiais adicionais

* [Pacotes 802.11](https://www.liveaction.com/docs/glossary/wireless-lan-802-11-wlan/packet-types/)

## Aula 7: WPS, PIN codes, Reaver e Pixie Dust

Um mecanismo ainda razoavelmente comum em redes wi-fi é a presença de **Wi-fi Protected Setup \(WPS\)**. No entanto, essa técnica permite fazer ataques muito simples para se quebrar a senha de uma rede Wi-fi.

#### WPS: Wi-fi Protected Setup

O WPS foi criado com o intuito de facilitar configuração e conexão de hosts em redes wi-fi usando apenas um código numérico de 8 dígitos: o **PIN code**. Cada rede wi-fi com WPS habilitado \(WPS-enabled wi-fi\) possui um único PIN code, e é possível se conectar nela ou pela senha \(normalmente\), ou passando o PIN code para o Access Point.

Existem três agentes importantes no WPS, são eles: **o Access Point \(ou AP\)**, o **Enrollee** \(quem quer se conectar\), e o **Registrar** \(a entidade responsável por dar ou revogar acesso à rede\). Em geral, o Registrar nada mais é do que um software rodando no AP, mas é importante salientar que ele pode estar em um outro dispositivo.

**Obs:** WPS independe do método de autenticação da rede wi-fi. Por exemplo, é possível ter uma rede WPA cujo método de autenticação é Pre-Shared Key \(PSK\), ou seja, uma rede WPA/PSK, que mesmo assim utilize WPS para facilitar a configuração e futuras conexões na rede.

#### O problema com WPS

O PIN code é composto por 8 dígitos numéricos, sendo que o último desses dígitos é um _checksum_ dos 7 anteriores. Quando um Enrollee quer se conectar na rede usando um PIN code, ele precisa seguir todo o protocolo WPS, que em geral envolve 7 mensagens \(de M1 a M7\):

![](https://i.imgur.com/ehdAIZT.png)

![](https://i.imgur.com/LIrh2zP.png)

Se, apos enviarmos a mensagem M4, a primeira metade do PIN code estiver incorreta, recebemos um NACK. Da mesma maneira, se enviarmos a primeira metade do PIN correta mas a segunda incorreta, recebemos um NACK após M6. Isso torna possível fazer um ataque de força bruta em que enviamos todas as possibilidades da primeira metade do PIN \(de 0000 até 9999\). Depois de acertarmos a primeira metade do PIN, repetimos o processo para a segunda metade. No entanto, como o último dígito do PIN é um checksum \(ou seja, apenas uma conta feita com os primeiros 7\), basta chutarmos 3 dígitos nessa parte \(de 000\[checksum\] até 999\[checksum\]\).

#### Primeiro ataque: Reaver

O `reaver` é uma ferramenta que vem por padrão junto com o Kali e serve justamente para realizar o brute force \(_online_\) descrito acima. No pacote do `reaver` do Arch vem também o `wash`, que nos permite listar todas as redes wi-fi próximas com WPS habilitado.

```text
$ sudo wash -i <sua interface wireless>
$ sudo wash -i wlan0

BSSID               Ch  dBm  WPS  Lck  Vendor    ESSID
--------------------------------------------------------------------------------
7C:05:07:F6:EE:84    1  -90  2.0  No   Broadcom  HAL_9000
D4:B9:2F:2B:9D:2A    1  -92  2.0  No   Broadcom  2.4G_gobbs
```

Nesse exemplo, encontramos duas redes: `HAL_9000` e `2.4G_gobbs`. Vamos agora atacar a primeira delas \(`HAL_9000`\) usando o `reaver`:

```text
$ sudo reaver -i <sua interface wireless> -b <BSSID do alvo> -vv
$ sudo reaver -i wlan0 -b 7C:05:07:F6:EE:84 -vv
```

#### Segundo ataque: Pixie Dust

A implementação desse ataque se baseia em uma falha de implementação da geração de números pseudo aleatórios \(PRNG\) em vários APs, gerando PRN inseguros.

Na mensagem M1, que o Enrolee envia para o quem quer se conectar, um número \(Nonce\) é passado. E na mensagem M3, é enviado E-Hash1 \(hash para a primeira mensagem do pin\) e a E-Hash2 \(hash para segunda metade do pin\).

O problema nessa implementação é que Nonce, e as chaves que geram E-Hash1 e E-Hash2 \(chamadas, E-S1 e E-S2\) são geradas em sequência. Nesse sentido, se usarmos força bruta para descobrir o state do PRNG, poderemos gerar E-S1 e E-S2 a partir de Nonce. Em seguida, chutamos Pin1 e Pin2.

Utilizaremos o `reaver` novamente para o Pixie Dust. Para isso, basta usar o comando anterior, mas com a flag `-K 1` \(note o espaço entre `-K` e `1`.

```text
$ sudo reaver -i wlan0 -b 7C:05:07:F6:EE:84 -vv -K 1
```

#### Materiais adicionais

* [Ataque Pixie Dust \(Dominique Bongard\)](https://web.archive.org/web/20160320164624/https://passwordscon.org/wp-content/uploads/2014/08/Dominique_Bongard.pdf)
* [Wi-fi Protected Setup \(Wikipedia\)](https://en.wikipedia.org/wiki/Wi-Fi_Protected_Setup)
* [Hostapd e WPS](https://w1.fi/cgit/hostap/plain/hostapd/README-WPS)
* [Especificação do WPS \(Wi-fi Alliance\)](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=12&ved=2ahUKEwjRmPuH_pTlAhXkDrkGHb-mAjoQFjALegQIARAC&url=http%3A%2F%2Fcfile28.uf.tistory.com%2Fattach%2F16132E3C50FCFFCB3EC74E&usg=AOvVaw1qku-2deouZtsbCKevTQPP)
* [Melhores práticas em WPS \(Wi-fi Alliance\)](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=2ahUKEwixorfz_5TlAhWgGLkGHVJvDGsQFjAAegQIARAC&url=https%3A%2F%2Fwww.wi-fi.org%2Ffile%2Fwi-fi-simple-configuration-protocol-and-usability-best-practices-for-the-wi-fi-protected-setup&usg=AOvVaw3-aY3gcJUGkQBmuFaJw2Od)

## Aula 8: DHCP Exhaustion/Starvation

Imagine que nossa heroína, Merindrola, acabou de chegar na sua casa e quer conectar o celular dela na rede Wi-Fi. Você então ajuda a nossa nobre salvadora dos exemplos didáticos e dá a senha da rede, ela digita no celular e...

E daí? O que acontece depois?

Você deve saber que a grande maioria das redes atualmente usam o protocolo IP, seja ele v4 ou v6, e que para que dois _hosts_ consigam conversar usando esse protocolo cada um deles dever ter um endereço IP, mesmo que privado \(tipo `192.168...`\). Então, o que acontece quando a Merindrola se conecta na sua rede é que ela precisa saber **\(1\)** qual o IP do roteador, que chamaremos de _gateway_, para o qual ela vai encaminhar pacotes para redes externas, **\(2\)** qual o endereço do servidor DNS que ela deve usar quando quiser resolver nomes e, finalmente, **\(3\)** qual o endereço IP que o celular dela deve usar, de maneira que seja único e respeite as restrições da rede \(máscara, bits de rede e de host, etc.\).

#### DHCP: Dynamic Host Configuration Protocol

O DHCP é o protocolo que facilita tudo isso, de forma que não seja preciso que cada um dos usuários da rede configurem manualmente todas essas variáveis. Se houver um servidor DHCP na rede, qualquer host conseguirá informações básicas de configuração automaticamente.

A figura abaixo, retirada do RFC da especificação do DHCP, ilustra o processo de descoberta do servidor DHCP e aquisição das configurações de um cliente em uma rede onde há dois servidores DHCP.

**1. DHCP DISCOVER:** O cliente recentemente conectado na rede envia um pacote no endereço de _broadcast_ procurando algum servidor DHCP.

**2. DHCP OFFER:** Dois servidores localizados na rede geram configurações para o cliente e as enviam diretamente para ele. Daqui em diante mais nenhuma mensagem é trocada no endereço de broadcast.

**3. DHCP REQUEST:** Cliente responde para apenas um dos servidores, indicando que ele escolheu as configurações daquele servidor.

**4. DHCP ACK:** Servidor escolhido responde ao DHCP REQUEST, indicando que ele o recebeu e reservou as configurações para aquele cliente.

**5. DHCP RELEASE:** Finalmente, ao se desconectar, o cliente responde com uma mensagem liberando aquelas configurações, para que outro _host_ consiga usá-las no futuro.

![](https://i.imgur.com/Qd8uNIk.png)

#### DHCP Pools

Nos servidores DHCP existem _pools_, ou piscinas, de endereços IP. Estas contêm todos os IPs da faixa de endereços que o servidor pode distribuir para os clientes.

A vantagem de se ter diferentes _pools_ é que é possível reservar faixas de IPs para determinados tipos de dispositivos. Por exemplo, todos os celulares ocuparão uma determinada faixa, ou todos os dispositivos da gerência ocuparão uma faixa específica.

### O ataque

Como vimos, a faixa de IPs de uma DHCP pool é limitada. O ataque que faremos, o **DHCP Starvation/Exhaustion/Depletion**, busca fazer com que o computador do atacante se passe por diversos clientes distintos e, dessa forma, faz com que ele seja capaz de reservar toda a faixa de IPs disponíveis na DHCP pool. Os demais clientes ficarão sem conseguir obter um endereço IP e não conseguirão se comunicar na rede.

Se você está pensando que esse ataque é muito parecido com o DoS \(Denial of Service\), é porque ele é, de fato, um tipo de DoS.

_Se não sabe o que é um DoS, leia a_ [_Aula 4: DoS, DDos, ADoS e Slow Lorris_](https://hackmd.io/ssK5SvdFTTWNXeYR8kyHTw?both#Aula-3-DoS-DDoS-ADoS-e-Slow-Lorris)_._

#### Motivação

Em sequência a esse ataque, geralmente o atacante fará outro ataque, e esse sim pode causar danos reais.

Um ataque que comumente segue após o **DHCP Starvation** é um do tipo **MITM \(Man In The Middle\)** chamado **Rogue DHCP** \(Se não sabe o que é MITM, leia a aula [Aula 2: Bettercap, MITM e Spoofing](https://hackmd.io/ssK5SvdFTTWNXeYR8kyHTw?both#Aula-2-Bettercap-MITM-e-Spoofing)\).

O ataque Rogue DHCP \(DHCP intruso\) consiste em, após esgotar todos os IPs livres no servidor DHCP legítimo, subir outro servidor DHCP, dessa vez controlado pelo atacante.

Como o servidor legítimo não possui IPs livres, pode ser que a implementação dele não responda com **DHCP OFFER** os **DHCP DISCOVERs** enviados, deixando o caminho livre para o atacante oferecer o "serviço de DHCP" dele.

Nesse cenário, o servidor malicioso pode oferecer uma configuração em que o endereço do _gateway_ seja o computador do atacante. Desse modo, o ataque segue justamente como um MITM tradicional visto na _Aula 2_ \(usando ARP Spoof\).

A fins de ilustração, uma das possíveis consequências é a leitura de pacotes sem protocolo de criptografia, de modo a expor dados como nomes de usuário, senhas, números de cartão de crédito, etc... \(por exemplo, uma conexão com um site por HTTP em vez de HTTPS não possui criptografia e pode ser lida por um MITM\).

OBS: Se você quiser saber mais sobre HTTP ou HTTPS, leia a [Aula 4: SSL/TLS, HTTP/HTTPS e HSTS](https://hackmd.io/ssK5SvdFTTWNXeYR8kyHTw?both#Aula-4-SSLTLS-HTTPHTTPS-e-HSTS).

#### Na prática

Para realizar o ataque, vamos usar o **DHCPig**. Para rodar o DHCPig é preciso ter instalado o **Python 2**, **Pip** e a biblioteca **Scapy** para o Python 2. Um problema conhecido é que a versão mais recente do Scapy para o Python 2 não funciona com o DHCPig. Então, é preciso instalar a versão `2.3.3`:

```text
$ pip2 install scapy==2.3.3
```

Clonamos o respositório do GitHub do DHCPig e entramos nele:

```text
$ git clone https://github.com/kamorin/DHCPig.git
$ cd DHCPig
```

Finalmente, rodamos o programa:

```text
$ sudo python2 pig.py <IP do servidor DHCP>
```

#### Materiais adicionais

* [RFC 2131 \(DHCP\)](https://tools.ietf.org/html/rfc2131)
* [RFC 2132 \(adição ao DHCP\)](https://tools.ietf.org/html/rfc2132)
* [RFC 951 \(BOOTP\)](https://tools.ietf.org/html/rfc951)
* [DHCPig \(GitHub\)](https://github.com/kamorin/DHCPig)

## Aula 9: IPv6 Neighbor Cache Exhaustion

## Aula 10: IPv6 Neighbor Cache Exhaustion

### IPv6 Subnetting

### NDP: Neighbor Discovery Protocol

### Neighbor Cache

```text
sudo atk6-ndpexhaust6 <dev> <link-address>
```

#### Referências

* [Blog post](https://insinuator.net/2013/03/ipv6-neighbor-cache-exhaustion-attacks-risk-assessment-mitigation-strategies-part-1/)
* ["Classic Paper"](http://inconcepts.biz/~jsw/IPv6_NDP_Exhaustion.pdf)
* [Mitigation techniques](https://tools.ietf.org/html/rfc6583)
* [RFC 6583](https://tools.ietf.org/html/rfc6583)
* [THC-IPv6 Tools](https://github.com/vanhauser-thc/thc-ipv6)
* [RFC 4861: Neighbor Discovery Protocol](https://tools.ietf.org/html/rfc4861#section-7.3.2)
* [RFC 5157](https://tools.ietf.org/html/rfc5157)
* [Código do NDPExhaust](https://github.com/vanhauser-thc/thc-ipv6/blob/master/ndpexhaust26.c)
* [Código do Ndisc \(Kernel do Linux\)](https://github.com/torvalds/linux/blob/master/net/ipv6/ndisc.c)

## Aula ?: Packet capturing, APs e servidores -- Montando ambientes de teste

* Hostapd
* Nginx
* goloris
* Wireshark

## Aula ?: Redes Peer-to-Peer \(Matrix, BitTorrent, Kademlia, IPFS\)

## Aula ?: Virtual Private Network: Conceitos básicos, funcionamento, segurança e exemplos com Wireguard

