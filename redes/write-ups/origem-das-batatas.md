# Origem das Batatas

## PARTE 1

Rodando o arquivo fornecido é informado que o programa está ouvindo \(listening\) em uma determinada porta, isso significa que a porta está aberta.

> Uma porta aberta é simplesmente uma porta que possui uma aplicação esperando por conexões nela. 

Se não houvesse uma aplicação ouvindo naquela porta, qualquer tentativa de conexão nela seria automaticamente rejeitada pelo sistema operacional.

As portas são identificadas por números e pelo protocolo de comunicação usado, como TCP ou UDP. No caso desse challenge, o protocolo é o TCP.

> Netcat é uma ferramenta utilizada para estabelecer conexões utilizando os protocolos TCP ou UDP como meio de tráfego.

Como já sabemos qual porta está sendo escutada \(dada pelo código\), rodamos o comando para se conectar a essa porta aberta:

$ nc localhost < NUMERO DA PORTA > 

Dessa forma obtemos a flag.

## PARTE 2.1

Nesta segunda etapa também temos um programa escutando em alguma porta, porém desta vez não é informado qual é o número dela. Para descobrir qual porta está escutando utilizaremos a ferramenta netstat.

> Netstat \(Network Statistics\) é uma ferramenta utilizada para monitorar redes e, como o próprio nome diz, gerar estatísticas.

Algumas informacoes que conseguimos obter com o netstat são, por exemplo, quais portas de comunicacão TCP e UDP estão abertas na nossa maquina e quais os programas ouvindo nessas portas.

Dessa forma, conseguimos utilizar alguns comandos como:

$ netstat -a Lista todas as conexões e portas abertas.

$ netstat -at Aplica um filtro \(-t\) no comando anterior, listando apenas as portas TCP.

$ netstat -at -p Mostra também o programa que está sendo executado em cada porta

Com esse último comando é possivel ver quais portas TCP estão abertas e verificar qual é a porta que esta ouvindo \(na qual o programa está rodando\).

Sabendo qual a porta que está ouvindo podemos fazer a mesma coisa que foi feita na parte 1 \(com o netcat\) para obtermos mais uma flag.

## PARTE 2.2

Agora, ao rodar o programa temos o seguinte saída do programa:

In: 8424

Out: 8903

Isso indica que a porta 8424 é a porta a qual devemos interagir com com o programa enviando algum input, no caso, a senha que nos foi fornecida (batatoso). Analogamente, a porta 8903 é a porta a qual receberemos a resposta do servidor, por isso precisamos usar o netcat pra ouví-la.

Porém, na camada de transporte, além do protocolo TCP também existe o UDP e a conexão que é estabelecida pelo programa utiliza justamente o UDP.

Para a primeira parte:

$ nc -u localhost < NUMERO DA PORTA In > 

Para a segunda parte:

$ nc -ul localhost < NUMERO DA PORTA Out > 

## PARTE 3

Se você chegou até aqui, a parte 3 será muito simples. 

Siga os mesmo passos feitos na parte 2.1

Agora interaja com o programa enviando 'por favor' ou 'svp' na conexão estabelecida com o netcat

