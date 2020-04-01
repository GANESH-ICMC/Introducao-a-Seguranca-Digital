# Wireshark

Estamos sempre falando dos protocolos e camadas de rede, mas os vimos somente na teoria, ou com algumas ferramentas que não mostram o que ocorre por baixo dos panos. O [wireshark](https://www.wireshark.org/) é uma ferramenta que permite analisar os protocolos e dados trafegando, por exemplo, entre seu computador e a internet.

## Instalação

Geralmente o wireshark não vem instalado no sistema operacional por padrão - exceções são distribuições GNU/Linux voltadas para segurança da informação como o Kali. Portanto, se você quiser utilizar a ferramenta, terá que instalá-la no seu computador.

Na maioria das distribuições, o programa está nos repositórios padrões, então basta utilizar o gerenciador de pacotes da sua distro para instalar. Vocês também podem olhar o [guia oficial de instalação do wireshark](https://www.wireshark.org/download.html), o [guia do usuário no capítulo de instalação](https://www.wireshark.org/docs/wsug_html_chunked/ChapterBuildInstall.html), ou perguntarem no grupo de Telegram do Ping se tiverem mais dúvidas.

### Debian/Ubuntu

Aqui é o exemplo de instalação no Debian:

```
# apt install wireshark
```

No caso do Ubuntu, temos que utilizar o `sudo`:

```
$ sudo apt install wireshark
```

## Funcionamento Básico

Para ver as informações que estão saindo do seu computador, basta iniciaro wireshark e selecionar de qual interface de rede capturará as informações. Essa [a interface de rede] é a porta de saída para os programas enviarem informações para a rede, ela pode ser cabeada (normalmente chamada de `eth0` ou `enp3s0`), ou wireless (então é `wlan0` ou `wlp3s0`), mas cada SO pode atribuir um nome específico. Para checar as interfaces, digite o seguinte comando:

```
ip address show
```

Depois de selecionar a interface da qual capturará as informações, você deve iniciar a captura clicando no botão mostrado abaixo ("Start"), ou utilizando o atalho de teclado *Ctrl+E*. A partir de agora você estará gravando todos os pacotes trafegando entre a rede e o computador por a interface definida anteriormente. Se você apertar *Ctrl+E* novamente, ou clicar no botão de parada ("Stop"), a captura será encerrada e todos os pacotes capturados permanecerão na tela.

![](https://www.wireshark.org/docs/wsug_html_chunked/wsug_graphics/ws-capture-menu.png)

Agora que todos os pacotes estão na tela, você pode querer analisá-los, ou deixar para um outro momento. Caso opte pela segunda opção, poderá salvar os pacotes capturados como um arquivo com formato *pcap*. Esse é um ponto importante porque também é possível inicializar o wireshark lendo diretamente um arquivo *pcap*, isto também pode ser feito do terminal executando o seguinte comando:

```
wireshark file.pcap
```


