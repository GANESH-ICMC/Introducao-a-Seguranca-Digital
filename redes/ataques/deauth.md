# Ataque de desautenticação

Esse ataque consiste em utilizar uma operação presente na especificação do
802.11. É o comando de desautenticação. Ele permite que os AP's enviem esse
comando para os clientes se desconectarem da rede wifi, contudo é possível
fraudar esse comando e desconectar um cliente maliciosamente.

Para realizar esse ataque, precisaremos de um adaptador wireless capaz de
entrar em modo *monitor* (i.e. capaz de ler frames não endereçados a ele). Além
disso, também precisa ser capaz de injetar pacotes fraudados - especialmente
pacotes *deauth*. Tendo satisfeito essas duas condições, será possível realizar
o ataque utilizando a suíte *aircrack-ng*. Para testar a viabilidade do ataque
com seu adaptador wi-fi, siga os passos abaixo.

## Teste de compatibilidade
Precisaremos inicialmente baixar a suíte de aplicações *aircrack-ng*, ela
contém todos os programas necessários para testar sua placa de rede (i.e.
adaptador wi-fi) e para executar o ataque. Para distros baseadas em Debian
(i.e. usam o gerenciador de pacotes `apt`), basta executar (com `sudo` ou como
usuário `root`):

```bash
apt install aircrack-ng
```

Bem, a partir de agora, as coisas ficam um pouquinho mais complicadas.
Precisamos encontrar o nome da sua interface de rede dado pelo sistema
operacional. Execute:

```bash
ip a
```

E verifique a saída procurando por `wlanX` ou `wlpXsYfZ`, em que X, Y e Z são
números. Segue abaixo um exemplo.

```bash
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: wwan0: <POINTOPOINT,NOARP> mtu 1500 qdisc noop state DOWN group default qlen 1000
    link/none 
3: enp0s31f6: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc fq_codel state DOWN group default qlen 1000
    link/ether 00:2c:37:a4:88:02 brd ff:ff:ff:ff:ff:ff
4: wlp0s20f3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether f9:e4:e3:e3:a5:ce brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.6/24 brd 192.168.1.255 scope global dynamic noprefixroute wlp0s20f3
       valid_lft 83560sec preferred_lft 83560sec
    inet6 fe80::e7c:e4bd:fa21:ac21/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```

Neste caso, a interface de interesse é `wlp0s20f3`. Sabendo disso, já podemos
iniciar os testes.

**A partir de agora, você vai ficar sem conexão wi-fi**

Primeiramente é necessário matar os processos que podem interferir no processo
de troca para o modo de monitoramento:

```bash
airmon-ng check kill
```

Guarde quais processos foram mostrados como saída do comando, pois precisaremos
reativá-los depois.

Agora já é possível trocar para o modo de monitoramento com:

```bash
airmon-ng start wlpXsYfZ
```

Será criada uma nova interface com o mesmo nome da sua original, mas com *mon*
adicionado ao fim. A partir deste exemplo, será criada a interface
`wlpXsYfZmon`. Agora já é possível verificar se o seu adaptador de rede permite
o modo de monitoramento. Isto pode ser feito com:

```bash
airodump-ng wlpXsYfZ
```

Se várias redes wi-fi aparecerem no terminal, seu adaptador de rede permite o
modo monitoramento!

Por fim, o último passo é verificar se o adaptador permite a injeção de
pacotes. Para isso, execute:

```bash
aireplay-ng --test wlpXsYfZ
```

A saída desse comando vai indicar o sucesso ou fracasso da injeção de pacotes.

Pronto, se você passou por todos esses passos e foi bem-sucedido, será possível
executar o ataque de desautenticação.

### Recuperando a conexão wi-fi
Para recuperar a conexão wi-fi, precisamos sair do modo monitoramento e
reativar os processos que foram mortos. O primeiro passo é:

```bash
airmon-ng stop wlpXsYfZ
```

Para sistemas baseados em Debian (pode funcionar para outros também - se você
usa uma distro que necessita de uma solução diferente, faça um MR para colocar
ela nesse tutorial :-), execute os comandos abaixo.

```bash
systemctl restart wpa_supplicant
systemctl restart NetworkManager
```
