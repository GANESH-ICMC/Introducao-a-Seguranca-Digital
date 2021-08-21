# DNS

DNS (Domain Name System) é a razão pela qual não precisamos inserir o endereço IP quando vamos fazer uma simples busca na internet.
É um protocolo no qual pede-se um endereço IP baseado em um nome, ou domínio.

## Domínios e Subdomínios

Os domínios são os nomes que podem ser registrados, no contexto de DNS e Internet.
Consistem de duas partes, sendo o domínio de fato e a raiz de domínio. Por exemplo: usp.br é um domínio que pertence à raiz .br
Os subdomínios pertencem aos domínios, mas ao registrar um domínio, é possível criar um número infinito(virtualmente) de subdomínios.
Domínios e subdomínios podem corresponder a endereços distintos.
Por exemplo, o domínio [icmc.usp.br](https://icmc.usp.br), no qual o site do ICMC é hospedado, corresponde a um servidor, mas o domínio [ganesh.icmc.usp.br](https://ganesh.icmc.usp.br/) provavelmente não é servido no mesmo servidor.

## Servidores DNS

Os servidores DNS são máquinas acessíveis na rede que possuem tabelas de correspondência entre domínios (e subdomínios) e endereços de rede.
Mas agora, já se perguntou a quantidade de domínios que existem? Não seria muito viável ter todas essas relações em um único local. Imagina só como seria para uma máquina lidar com as requisições do mundo todo.
Para isso, o sistema de domínios é arquitetado de uma forma distribuída. Os servidores DNS têm uma lista de quais são outros servidores que podem ter o domínio procurado.
Ao fazer uma requisição DNS para o servidor, se ele não possui a entrada (par domínio:ip) ele delega para outro servidor que está em sua lista.

## Referências

- [Cloudflare](https://www.cloudflare.com/learning/dns/what-is-dns/)

