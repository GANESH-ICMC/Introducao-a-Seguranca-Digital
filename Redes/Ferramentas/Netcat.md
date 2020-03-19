# Netcat

![](https://i.imgur.com/JVCnnF0.png)
> The Swiss army knife of hacking tool


O Netcat é uma ferramenta capaz de receber e enviar dados em conexões usando TCP e UDP. Se você é responsável pela segurança de uma rede ou de um sistema, é essencial que você saiba utilizar os recursos que o Netcat proporciona. O Netcat pode ser usado como scanner, redirecionador e ouvinte de portas além de muitas outras coisas.

### Flags de comando (Essenciais)

-l -> Coloca no netcat em estado de escuta (listening)

-p -> Especifica a porta a ser usada (sujeito a disponibilidade e a restrições de privilégio)

-u -> Usar UDP ao invés de TCP

-n -> Força o netcat a usar apenas endereços de IP numéricos, sem fazer consultas a servidores DNS

-e -> Especifica o programa a ser executado depois de a conexão acontecer, ligando entradas e saídas ao programa

-s -> Especifica o endereço IP da interface usada para enviar os pacotes. Pode ser usado para spoofing de IPs.

-v -> Controla o nível de mensagens mostradas na tela

-w -> Limita o tempo máximo para que uma conexão seja estabelecida;

### Funcionamento básico

`$ nc <ip alvo> <porta>`
Conecta-se em uma <porta> arbitrária no <ip alvo>

`$ nc -l -p <porta local>`
Cria um "ouvinte netcat" na <porta local>

### Enviar arquivo do cliente para o ouvinte

`$ nc -l -p <porta local> > <arquivo de saida>`
ouve na porta <porta local> e armazena resultado no <arquivo de saida>

`$ nc -w3 <ip alvo> <porta> < <arquivo de entrada> `
envia o <arquivo de entrada> para o <ip alvo> em uma <porta>`

### Receber arquivo do ouvinte para o cliente

`$ nc -l -p <porta local> > <arquivo de entrada>`
ouve em uma <porta local> e prepara para enviar o arquivo de entrada`

`$ nc -w3 <ip alvo> <porta> > <arquivo de saida> `
conecta com o <ip alvo> em uma <porta> e envia o <arquivo de saída>`





