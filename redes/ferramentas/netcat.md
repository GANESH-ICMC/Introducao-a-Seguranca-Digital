# Netcat

![](https://i.imgur.com/JVCnnF0.png)

> The Swiss army knife of hacking tool

O Netcat é uma ferramenta capaz de receber e enviar dados em conexões usando TCP e UDP. Se você é responsável pela segurança de uma rede ou de um sistema, é essencial que você saiba utilizar os recursos que o Netcat proporciona. O Netcat pode ser usado como scanner, redirecionador e ouvinte de portas além de muitas outras coisas.

## Flags de comando \(Essenciais\)

-l -&gt; Coloca no netcat em estado de escuta \(listening\)

-p -&gt; Especifica a porta a ser usada \(sujeito a disponibilidade e a restrições de privilégio\)

-u -&gt; Usar UDP ao invés de TCP

-n -&gt; Força o netcat a usar apenas endereços de IP numéricos, sem fazer consultas a servidores DNS

-e -&gt; Especifica o programa a ser executado depois de a conexão acontecer, ligando entradas e saídas ao programa

-s -&gt; Especifica o endereço IP da interface usada para enviar os pacotes. Pode ser usado para spoofing de IPs.

-v -&gt; Controla o nível de mensagens mostradas na tela

-w -&gt; Limita o tempo máximo para que uma conexão seja estabelecida;

## Funcionamento básico

`$ nc <ip alvo> <porta>` Conecta-se em uma  arbitrária no 

`$ nc -l -p <porta local>` Cria um "ouvinte netcat" na 

## Enviar arquivo do cliente para o ouvinte

`$ nc -l -p <porta local> > <arquivo de saida>` ouve na porta  e armazena resultado no 

`$ nc -w3 <ip alvo> <porta> < <arquivo de entrada>` envia o  para o  em uma \`

## Receber arquivo do ouvinte para o cliente

`$ nc -l -p <porta local> > <arquivo de entrada>` ouve em uma  e prepara para enviar o arquivo de entrada\`

`$ nc -w3 <ip alvo> <porta> > <arquivo de saida>` conecta com o  em uma  e envia o \`

