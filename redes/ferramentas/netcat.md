# Netcat

![](https://i.imgur.com/JVCnnF0.png)

> The Swiss army knife of hacking tools

Se você é responsável pela segurança de uma rede ou de um sistema, é essencial que você saiba utilizar os recursos que o Netcat proporciona. O Netcat é um ferramenta simples (mas poderosa) que lê e envia dados através de conexões de rede, usando o protocolo TCP ou UDP.<br /><br />
Ele foi projetado para ser uma ferramenta de "back-end" compacta que pode ser usada direta e facilmente por outros programas e scripts. Ao mesmo tempo, é uma ferramenta de exploração de redes com muitas funcionabilidades, pois pode criar praticamente qualquer tipo de conexão necessária e possui vários recursos internos interessantes.

## Funcionamento básico

O uso mais simples (e mais frequente) do netcat cria uma conexão TCP com a porta especificada no host de destino também especificado. Sua entrada padrão (STDIN) é então enviada ao host e tudo o que retorna através da conexão é enviado à sua saída padrão (STDOUT). Isso continua indefinidamente, até que a conexão seja desligada.

`$ nc <ip alvo> <porta>`

Conecta-se em uma porta arbitrária no ip alvo.

O Netcat também pode funcionar como um servidor, escutando possíveis conexões em portas arbitrárias e, em seguida, fazendo a mesma leitura e escrita descrita acima. 

`$ nc -l -p <porta local>`

Cria um ouvinte na porta local.

## Algumas flags de comando

`-l` : Coloca no netcat em estado de escuta \(listening\)

`-p` : Especifica a porta a ser usada \(sujeito a disponibilidade e a restrições de privilégio\)

`-u` : Usar UDP ao invés de TCP

`-n` : Força o netcat a usar apenas endereços de IP numéricos, sem fazer consultas a servidores DNS

`-e` : Especifica o programa a ser executado depois de a conexão acontecer, ligando entradas e saídas ao programa

`-s` : Especifica o endereço IP da interface usada para enviar os pacotes. Pode ser usado para spoofing de IPs.

`-v` : Controla o nível de mensagens mostradas na tela

`-w` : Limita o tempo máximo para que uma conexão seja estabelecida

## Enviar arquivo do cliente para o ouvinte

`$ nc -l -p <porta local> > <arquivo de saida>`

Ouve na porta porta local e armazena resultado no arquivo de saida.

`$ nc -w3 <ip alvo> <porta> < <arquivo de entrada>`

Envia o arquivo de entrada para o ip alvo em uma porta.

## Receber arquivo do ouvinte para o cliente

`$ nc -l -p <porta local> > <arquivo de entrada>`

Ouve em uma porta local e prepara para enviar o arquivo de entrada.

`$ nc -w3 <ip alvo> <porta> > <arquivo de saida>`

Conecta com o ip alvo em uma porta e envia o arquivo de saída.

