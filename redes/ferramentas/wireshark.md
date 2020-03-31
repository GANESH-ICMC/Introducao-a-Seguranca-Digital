# Wireshark

Estamos sempre falando dos protocolos e camadas de rede, mas os vimos na teoria, ou com algumas ferramentas que não mostram o que ocorre por baixo dos panos. O [wireshark](https://www.wireshark.org/) é uma ferramenta que permite analisar os protocolos e dados trafegando, por exemplo, entre seu computador e a internet.

## Instalação

Geralmente o wireshark não vem instalado no sistema operacional por padrão - exceções são distribuições GNU/Linux voltadas para segurança da informação como o Kali. Portanto, se você quiser utilizar a ferramenta, terá que instalá-la no seu computador.

Na maioria das distribuições, o programa está nos repositórios padrões, então basta utilizar o gerenciador de pacotes da sua distro para instalar. Vocês também podem olhar o [guia oficial de instalação do wireshark](https://www.wireshark.org/download.html), ou perguntarem no grupo de Telegram do Ping se tiverem mais dúvidas.

### Debian/Ubuntu

Aqui é o exemplo de instalação no Debian:

```
# apt install wireshark
```

No caso do Ubuntu, temos que utilizar o `sudo`:

```
$ sudo apt install wireshark
```

