# WPA Cracking Attack

A principal ideia por trás  do WPA Cracking Attack é se aproveitar de
vulnerabilidades existentes na conexão Wi-Fi para brutar a senha de uma
rede. Ele consiste em 3 principais passos:

- Monitorar um ponto de acesso.
- Forçar uma desautenticação de um dos clientes da rede.
- Capturar a reautenticação/handshake desse cliente com o ponto de acesso.
- Crackear o handshake (bruteforce).

De forma que poderemos saber se alguma das chaves contidas numa `WORDLIST`
corresponde à senha da rede monitorada.

## Definições

### WPA/WPA2

Assim como seu antecessor WEP, são protocolo de segurança criados para proteger
redes WiFi.

### Interface de monitoramento

Normalmente, a interface wireless da sua placa de rede está responsável por
capturar apenas os pacotes destinados para o seu computador, ou seja, apenas
aqueles enviados pela rede Wifi na qual está conectado. Quando ativamos o
**modo monitoramento**, no entanto, conseguimos inspecionar os mais diversos
pacotes de todos os pontos de acesso ao seu redor.

### Ponto de Acesso (AP)

São os dispositivos que permitem hosts se conectarem a uma rede, como por
exemplo roteadores.

### BSSID e ESSID

**BSSID** diz respeito ao próprio endereço MAC do ponto de acesso; enquanto
**ESSID/SSID**, ao nome público desse.

### WORDLISTS

São listas de senhas em *plain text* geralmente conseguidas por meio de
vazamentos de grandes bancos de dados. Elas são comumente utilizadas para
testes de *password cracking*, e uma das mais famosas se trata da
[rockyou.txt](https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt).

## 4-Way Handshake

![4WayHandshake](https://upload.wikimedia.org/wikipedia/commons/a/ac/4-way-handshake.svg)

## Deauthentication Attack
![Deauth Attack](https://upload.wikimedia.org/wikipedia/commons/thumb/9/95/Deauth_attack_sequence_diagram.svg/800px-Deauth_attack_sequence_diagram.svg.png)

O protocolo IEEE 802.11 (WiFi) possui um *"pacote"*, o qual na verdade trata-se
de apenas um frame, de controle chamado **deauthentication frame** que avisa ao
cliente que ele foi desconectado da rede.

Como o protocolo não exige nenhuma encriptação desse frame, se "fingindo" de AP
(spoofing), o atacante pode manda-lo conhecendo apenas o endereço MAC da vítima
e do ponto de acesso.
