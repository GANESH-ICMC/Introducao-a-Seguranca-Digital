# Nmap

![](https://i.imgur.com/VmXeG64.png)

> The Network Mapper

Você já logou numa rede que não era a sua \(ou a sua mesmo\) e queria saber quais os dispositivos ligados naquela rede? Ou melhor, qual o IP do access point ao qual você está conectado? Quais as portas abertas naquele servidor safado que você tá tentando invadir. Nmap is here for you.

## Comandos básicos

### Host Discovery

Vamos começar com um básico, descobrir todos os IPs dos dispositivos conectados à rede local \(supondo que você sabe o endereço da rede e a máscara de subrede\):

```text
# nmap <ip da rede>/<máscara> -sn
nmap 192.168.15.0/24 -sn
```

### Scan Básico

Beleza, agora você já sabe quem são todos os hosts na sua rede. Digamos que a Merindrola, seu alvo, está no `192.168.15.40`. Mas o que está rodando na máquina dela? O que podemos tentar atacar? Para isso podemos usar um _port scanning_:

```text
# nmap <ip do alvo>
nmap 192.168.15.40
```

Isso vai nos dar informações básicas sobre as portas mais importantes

### Scan em mais portas

O scan básico que fizemos anteriormente vai focar em portas famosas, ou _well-known ports_. Mas e se a Merindrola foi sapeca e "escondeu" seus serviços em portas bizarras \(por exemplo a HTTP na 7890 ao invés da 80\)? Nmap neles:

```text
# nmap <ip do alvo> -p [<portas>, <range de portas>]
nmap 192.168.15.40 -p 7890 # scan na porta 7890 (como o protocolo não foi especificado, vai ser na TCP)
nmap 192.168.15.40 -p 2000-8000 # scan nas portas 2000 até 8000
nmap 192.168.15.40 -p- # scan em TODAS as portas
```

### Serviços e Versões

Beleza, agora sabemos o IP da Merindrola e as portas abertas na máquina dela. Mas o que tem atrás dessas portas? O nmap geralmente por padrão tenta mandar uma série de pacotes especiais que, de acordo com a resposta da aplicação, ele consegue adivinhar qual é o serviço rodando numa porta. Mas para economizar tempo, o nmap não tenta todas as possibilidades de payload em todas as portas \(até porque isso nunca acabaria rs\).

Digamos que nós encontramos um servidor web rodando na porta 80 da Merindrola. O nmap tem payloads que nos permitem adivinhar qual exatamente é o servidor web \(apache, nginx, etc.\):

```text
# nmap <ip do alvo> -sC
nmap 192.168.15.40 -sC
```

...e até a versão dele:

```text
# nmap <ip do alvo> -sV
nmap 192.168.15.40 -sV
```

Melhor já ir direto nos dois!

```text
# nmap <ip do alvo> -sC -sV
nmap 192.168.15.40 -sC -sV
```

## Dicas e Hacks

Geralmente a saída do nmap é grande e você provavelmente quer salvá-la. Usar o redirecionador `>` para um arquivo é geralmente uma boa ideia:

```text
nmap 192.168.15.40 > nmap.txt
```

Mas olhar a saída do nmap enquanto ele faz o scan é ainda mais legal. Você pode fazer as duas coisas ao mesmo tempo usando o comando `tee`:

```text
tee nmap.txt nmap 192.168.15.40
# ou, outra forma de fazer a mesma coisa
nmap 192.168.15.40 | tee nmap.txt
```

## NSE: Nmap Scripting Engine

Talvez você encontre um desses aqui pela internet, mas quando você for um verdadeiro mago do nmap, você vai ser capaz de _fazer_ os seus e nunca mais depender de ninguém muahahaha.

```text
# nmap --script=<nome do script> <ip do alvo>
nmap --script=my-evil-script.nse 192.168.15.40

# ou

# nmap --script <nome do script> <ip do alvo>
nmap --script my-evil-script.nse 192.168.15.40
```

O nmap possibilita que seus usuários criem scripts para automatizar tarefas mais específicas e complexas. Esses scripts são códigos mesmo, que você escreve na linguagem Lua e o nmap roda eles. Sabe quando a gente mandou o nmap fazer umas bruxarias mais complexas mais cedo para descobrir o tipo do servidor web e a sua versão? Adivinha? Ele nada mais fez do que rodar alguns desses scripts que são bem conhecidos e vêm instalados:

Em pentests e em máquinas do Hack The Box, situações em que você precisa ser bem preciso no seu trabalho de reconhecimento, talvez valha à pena procurar na internet por scripts customizados e mais específicos. Todo trabalho de invasão começa com um bom reconhecimento ;\)

## Links Úteis

* [Nmap Reference Guide](https://nmap.org/book/man.html)
* [StationX Cheatsheet](https://www.stationx.net/nmap-cheat-sheet/)
* [NSE Guide](https://nmap.org/book/man-nse.html)

