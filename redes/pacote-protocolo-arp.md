# Ping - Pacote / Protocolo / ARP

## Introdução
Para explicarmos como funciona a transmissão de dados entre computadores, precisamos saber o que são **pacotes** e **protocolos**, conceitos fundamentais para compreender a lógica por trás da comunicação entre computadores, os quais serão explicados por analogia a uma carta.

## Protocolo
Analogamente, quando queremos escrever uma carta, o primeiro passo para isso é definir como o conteúdo da carta vai ser transmitido e como deve ser lido. Isso seria a língua, paragrafação, endereçamento, informações necessárias para compreender o conteúdo da carta.

Dessa maneira podemos definir protocolos como:

> Conjunto de normas de comunicação entre dois computadores

Além de ditar como um pacote deve ser interpretado, o protocolo vai muito além disso, ele pode ditar como um pacote deve ser recebido, que tipo de pacote deve ser esperado em determinada ocasião, como rearranjar os pacotes caso cheguem fora de ordem, etc. De maneira geral, é dele que surgem as soluções para problemas de comunicação em uma rede.

No exemplo abaixo, mostramos como um protocolo descreve um pacote de dados. Cada conjunto de bits do pacote representa alguma informação para compreender aquilo que está sendo transmitido.

<figure align="center">
  <img src="https://i.imgur.com/8NAiV0T.png">
  <figcaption>Imagem mostrando como seria a estrutura simples de um pacote</figcaption>
</figure>

<!---![](https://i.imgur.com/8NAiV0T.png)-->

## Pacote
Quando queremos transmitir uma informação através de uma rede, o que acontece é que temos que dividir essa informação em diversos fragmentos para que seja possível transmitir esses dados, pois existe um limite de dados que pode percorrer uma rede. Dessa forma, podemos definir pacote como:

>Unidade básica de informação em uma rede

<figure align="center">
  <img src="https://i.imgur.com/X39WHVB.png">
</figure>

A estrutura de um pacote é definida pelo tipo de pacote e pelo protocolo. Geralmente um pacote tem um cabeçalho e uma carga útil. O cabeçalho mantém informações gerais sobre o pacote, o serviço e outros dados relacionados à transmissão. Assim, contém diversas informações como a origem e destino do pacote, a numeração do pacote dentro de uma sequência, tipo de serviço, flags, entre outras informações técnicas.

<figure align="center">
  <img src="https://i.imgur.com/w3OmZ8S.jpg">
  <figcaption>Exemplo da estrutura do cabeçalho de um pacote IP (Internet Protocol)</figcaption>
</figure>

> Caso tenha se interessado, veja um vídeo acerca do envio dos dois primeiros pacotes da Internet: https://www.youtube.com/watch?v=uY7dUJT7OsU

Aprofundando no conceito de distribuição dos pacotes na rede, há dois conceitos importantes no que tange o envio de pacotes: **encapsulamento** e **comutação**.

### Encapsulamento
Agora que foi introduzido os conceitos básicos de pacotes e protocolos, deve-se olhar para como funciona o envio de dados através da rede como um todo. Toda camada do modelo OSI possui um protocolo que dita as regras de comunicação e de funcionamento para ela. Como um mesmo pacote passa por mais de uma camada, ou seja, mais de um protocolo é aplicado nele, é necessário haver uma forma desse pacote carregar os dados e informações relativas a cada protocolo sem interferir na integridade do resto do pacote. É aí que o conceito de **encapsulamento** aparece.

<figure align="center">
  <img src="https://i.imgur.com/cykFTSK.png">
  <figcaption>Exemplo do trajeto dos pacotes no modelo OSI</figcaption>
</figure>

Para cada protocolo, ele considera o pacote recebido como "data" e aplica um cabeçalho(header) do protocolo em cima do pacote, sem comprometer sua integridade. Na medida que o host receptor vai recebendo os pacotes por cada uma das camadas, o header relativo a ela é interpretado e retirado do pacote. Isso se chama desencapsulamento e é semelhante a uma cebola sendo descascada de cada uma das suas camadas.

<figure align="center">
  <img src="https://i.imgur.com/h7uTIt9.png">
  <figcaption>Demonstração do encapsulamento (payroll: carga útil)</figcaption>
</figure>

### Comutação de Pacotes
Comutação de pacotes se refere a tecnologia de comunicação utilizada no núcleo da rede em redes de computadores. Quando um computador deseja enviar uma informação a outro computador, ele encapsula a informação em vários **pacotes de dados**, encaminhando de roteador em roteador em função do endereço do destino. Nisso, ocorre um compartilhamento de recursos na forma de uma **multiplexação estatística** (os pacotes podem trafegar pela rede ocupando o mesmo espaço), ou seja, os pacotes trafegam pela rede por diversos equipamentos até chegarem ao seu destino, onde serão recolhidos e ordenados. 

<figure align="center">
  <img src="https://i.imgur.com/iXZssAh.jpg">
  <figcaption>Exemplo de Comutação de pacotes</figcaption>
</figure>

A comutação de pacotes existe em contraponto à comutação de circuitos onde uma conexão exclusiva é criada para cada comunicação, como por exemplo linha telefônica. Na de pacotes, não há reserva de recursos, mas sim um compartilhamento da estrutura da rede que é trafegada a partir do uso de pacotes endereçados.

## ARP (Address Resolution Protocol)
Na rede de computadores, por exemplo, utilizamos o protocolo IP (Internet Protocol, que vai ser visto numa próxima aula) na camada de rede para fazer o endereçamento dos pacotes que trafegam numa rede, como foi definido no tópico de comutação de pacotes. No entanto, na camada de enlace do modelo OSI, precisamos saber o endereço físico do dispositivo para ser possível se comunicar e interagir com tal dispositivo. A pergunta que se faz é: como conseguir fazer o vínculo entre o endereço IP e o endereço físico, também chamado de **endereço MAC**? É nesse contexto que o ARP (Protocolo de Resolução de Endereços) aparece.

### Funcionamento
Basicamente, para cada dispositivo na rede haverá uma tabela chamada de ARP Cache que conterá as seguintes informações:

* O endereço IP e o endereço MAC de cada dispositivo ouvido na rede;
* O endereço IP e o endereço MAC do próprio dispositivo;

Quando um host A deseja se comunicar com um host B de uma mesma rede local o que acontece?

1. O host A verifica se ele conhece o endereço MAC do host B em sua ARP Cache. Caso consiga, pronto. A comunicação é então encaminhada para a camada física.
2. Caso não tenha uma entrada em sua ARP Cache, ele faz um **ARP Request** em **Broadcast**. Isso significa basicamente que ele perguntará a seguinte pergunta para todos os dispositivos daquela rede ouvirem: **"Qual o endereço MAC do endereço IP {IP address do host B)? Diga ao  endereço MAC {MAC addess do host A) com endereço IP {IP address do host A}"**. Ou seja, ao perguntar o MAC address do host B, o host A informa seu IP address e seu MAC address para toda a rede local.
3. Caso o host B se encontre na rede, ele manda um **ARP Reply** para o host A informando seu MAC address. Lembre-se que o ARP Reply é em **Unicast**, ou seja, a mensagem enviada pelo host B é endereçada especificamente ao host A, logo os outros dispositivos na rede não tem acesso a ela.
4. Agora que o host A sabe o MAC address do host B, ele continua sua comunicação na camada física :)

Uma tecnologia usada para evitar que as ARP Caches fiquem demasiadamente grandes é a **TTL (Time To Live)**. Ela se baseia na ideia de que uma entrada na ARP Cache tem um tempo de validade. Ou seja, se o host A tem uma entrada em sua ARP Cache para o host B em algum momento, ele vai deixar de ter, devido ao TTL e vai ser novamente necessário fazer um ARP Request para reconquistar a entrada do host B.

>O protocolo ARP funciona em cooperação com o protocolo IPv4 e deixa de ser usado no IPv6 onde é substituído pelo protocolo NDP (Neighbor Discovery Protocol).

Basicamente esses são os conceitos básicos em relação a pacotes, protocolos e  ARP. Espero que tenham gostado e fiquem atentos para a próxima aula acerca de ARP Spoofing, ataque utilizando esse protocolo.

## Bibliografia
1. https://www.gta.ufrj.br/grad/silvia/silvia.htm
2. https://pt.wikipedia.org/wiki/Pacote
3. http://wiki.foz.ifpr.edu.br/wiki/index.php/Comuta%C3%A7%C3%A3o_de_pacotes_x_Comuta%C3%A7%C3%A3o_de_circuitos#:~:text=Na%20comuta%C3%A7%C3%A3o%20de%20pacotes%20n%C3%A3o,per%C3%ADodos%20de%20sil%C3%AAncio%20na%20comunica%C3%A7%C3%A3o.
4. http://www.inf.ufes.br/~zegonc/material/Redes_de_Computadores/O%20Protocolo%20ARP.pdf