# Wireshark

![The network protocol analyzer](https://www.sololinux.es/wp-content/uploads/2014/07/Logo-de-Wireshark.png)

Estamos sempre falando dos protocolos e camadas de rede, mas os vimos somente na teoria, ou com algumas ferramentas que não mostram o que ocorre por baixo dos panos. O [wireshark](https://www.wireshark.org/) é uma ferramenta que permite analisar os protocolos e dados trafegando, por exemplo, entre seu computador e a internet.

## Instalação

Geralmente o wireshark não vem instalado no sistema operacional por padrão - exceções são distribuições GNU/Linux voltadas para segurança da informação como o Kali. Portanto, se você quiser utilizar a ferramenta, terá que instalá-la no seu computador.

Na maioria das distribuições, o programa está nos repositórios padrões, então basta utilizar o gerenciador de pacotes da sua distro para instalar. Vocês também podem olhar o [guia oficial de instalação do wireshark](https://www.wireshark.org/download.html), o [guia do usuário no capítulo de instalação](https://www.wireshark.org/docs/wsug_html_chunked/ChapterBuildInstall.html), ou perguntarem no grupo de Telegram do Ping se tiverem mais dúvidas.

### Debian/Ubuntu

Aqui é o exemplo de instalação no Debian (execute o comando como superusuário - root):

```text
# apt install wireshark
```

No caso do Ubuntu, temos que utilizar o `sudo`:

```text
$ sudo apt install wireshark
```

## Funcionamento Básico

Para ver as informações que estão saindo do seu computador, basta iniciaro wireshark e selecionar de qual interface de rede capturará as informações. Essa \[a interface de rede\] é a porta de saída para os programas enviarem informações para a rede, ela pode ser cabeada \(normalmente chamada de `eth0` ou `enp3s0`\), ou wireless \(então é `wlan0` ou `wlp3s0`\), mas cada SO pode atribuir um nome específico. Para checar as interfaces, digite o seguinte comando:

```text
ip address show
```

Depois de selecionar a interface da qual capturará as informações, você deve iniciar a captura clicando no botão mostrado abaixo \("Start"\), ou utilizando o atalho de teclado _Ctrl+E_. A partir de agora você estará gravando todos os pacotes trafegando entre a rede e o computador por a interface definida anteriormente. Se você apertar _Ctrl+E_ novamente, ou clicar no botão de parada \("Stop"\), a captura será encerrada e todos os pacotes capturados permanecerão na tela.

![](https://www.wireshark.org/docs/wsug_html_chunked/wsug_graphics/ws-capture-menu.png)

Agora que todos os pacotes estão na tela, você pode querer analisá-los, ou deixar para um outro momento. Caso opte pela segunda opção, poderá salvar os pacotes capturados como um arquivo com formato _pcap_. Esse é um ponto importante porque também é possível inicializar o wireshark lendo diretamente um arquivo _pcap_, isto também pode ser feito do terminal executando o seguinte comando:

```text
wireshark file.pcap
```

## Lendo pacotes

Agora que já capturamos alguns pacotes, está na hora de analisá-los. Vamos ver juntos um exemplo de pacote, no caso, o primeiro pacote enviado quando há uma conexão SSL \(faz a criptografia dos dados enviados\). Nesse pacote inicial, o cliente envia um "oi" para o servidor dizendo que quer iniciar a conexão.

Nós temos duas opções de visualizações de pacotes, a primeira é a mostrada abaixo. Nela o programa nos mostra as camadas do pacote e os respectivos dados de cada uma de uma maneira bastante organizada e simples. Vemos que este conjunto de dados é um _frame_, o quadro da camada de enlace. Ele engloba os dados e cabeçalhos de todas as outras camadas, mas o wireshark permite ver as informações de cada cabeçalho separadamente. Isto é, podemos ver que temos o protocolo Ethernet com os MAC's de origem e destino, em seguida, o protocolo IP com os ip's de origem e destino, então o protocolo TCP com as portas de origem e destino e algumas outras informações do protocolo e finalmente o protocolo TLS que envia o `"Client Hello"`.

![](https://jvns.ca/images/wireshark_packet_details_list.png)

A segunda maneira de visualizar os dados é mostrando os bytes crus. Temos acesso aos bytes de dados enviados ao lado esquerdo e aos valores decodificados para caracteres à direita. Então é possível passar o mouse sobre os caracteres e o wireshark indica os bytes correspondentes e vice-versa, e ainda indica a qual campo o dado pertence. No exemplo abaixo, `tiles.services.mozilla.com` corresponde ao campo "Server Name".

![](https://jvns.ca/images/wireshark_packet_details.png)

## Seguindo uma única conexão

Muitas vezes aparecem dados de diversas conexões TCP, mas estamos querendo ver somente uma. Para isso, o wireshark fornece uma forma simples de acompanhar uma conexão específica, basta clicar com o botão direito no pacote e selecionar "Conversation filter" -&gt; "TCP".

![](https://jvns.ca/images/wireshark_filter.png)

## Aplicando filtros

O wireshark também permite que você utilize filtros para especificar aspectos dos pacotes mostrados. Alguns exemplos são mostrados abaixo, mas existem muitos outros que vocÊ aprenderá conforme for utilizando o wireshark.

* `frame contains "mozilla"`: filtra por pacotes que contenham a string "mozilla";
* `tcp.port == 443`: filtra por pacotes cuja porta de destino é a 443 \(https\);
* `dns.resp.len > 0`: mostra todas as respostas DNS;
* `ip.addr == 192.168.15.1`: mostra todos os pacotes com _ip_ de origem ou destino igual a `192.168.15.1`.

## Links extras

* [Página oficidial do wireshark](https://www.wireshark.org/)
* [Guia do usuário oficial em PDF](https://www.wireshark.org/download/docs/user-guide.pdf)
* [FAQ oficial](https://www.wireshark.org/faq.html)
* [Publicação em que este tutorial foi baseado](https://jvns.ca/blog/2018/06/19/what-i-use-wireshark-for/) 

