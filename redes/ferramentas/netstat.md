# Netstat

![](https://i.imgur.com/MHpXCfP.png)

> The Network statistics tool

 Netstat \(Network Statistics\) é uma ferramenta utilizada para monitorar redes e, como o próprio nome diz, gerar estatísticas.

Algumas informacoes que conseguimos obter com o netstat são, por exemplo, quais portas de comunicacão TCP e UDP estão abertas na nossa maquina e quais os programas ouvindo nessas portas.

## Funcionamento básico

`$ netstat -a` Lista todas as conexões e portas abertas.

`$ netstat -at` Aplica um filtro \(-t\) no comando anterior, listando apenas as portas TCP.

`$ netstat -au` Aplica um filtro \(-u\) , listando apenas as portas UDP.

`$ netstat -atp` Com o acréssimo do p mostra também o programa que está sendo executado em cada porta.

## Gerando Estatísticas sobre a rede

`$ netstat -i` Para obter informações de uso das interfaces de rede.

`$ netstat -ie` Para detalhar ainda mais as informações mostradas 

`$ netstat -s` Para obter estatísticas resumidas de cada um dos protocolos de rede (por exemplo, TCP, UDP, ICMP).

`$ netstat -rn` Para visualizar a tabela de routing da máquina.
