# Ports e Serviços

*No texto de Servidores Web abordamos principalmente os serviços que são servidos por meio das requisições HTTP. Vamos comentar agora sobre outros serviços que, na maioria dos casos, também estão presentes em um servidor.*

## O que são Ports?

Em um computador agindo como servidor web, é comum que haja uma grande quantidade de serviços que precisam enviar e receber dados pela rede utilizando diferentes tipos de protocolos. Como saber, então, a qual serviço cada pacote recebido pertence?

Este é o objetivo das portas: uma sequência numérica de 16 bits que identifica e mapeia processos a endereços na rede de maneira exclusiva.

Não é o objetivo desse texto se aprofundar no funcionamento técnico das portas ou do modelo TCP/IP. Mas, caso seja do seu interesse, você poderá ler um pouco sobre isso nos links abaixo:

* O que são Portas TCP e UDP? (https://www.youtube.com/watch?v=SMU92puJxdU)
* Portas (https://pt.wikipedia.org/wiki/Porta_(redes_de_computadores)#Fun%C3%A7%C3%A3o_multiplexagem)
* TCP/IP (https://pt.wikipedia.org/wiki/TCP/IP)

## Convenções e Port Scanners

Com o crescimento da Internet e seus serviços, algumas convenções foram adotadas para facilitar a comunicação dentre usuários. Uma dessas convenções foi a de padronizar o uso de algumas portas para determinados serviços.

Um Servidor HTTP, por exemplo, é comumente executado na porta 80. Dessa forma, ao acessar um website por meio de um browser, não é necessário dizer ao navegador qual será a porta utilizada para enviar as requisições, uma vez que o navegador irá definir, por conta própria, a porta padrão a ser utilizada.

Você pode ver no link a seguir uma grande lista com diversos serviços e suas respectivas portas (lembre-se que tal convenção não é obrigatória, podendo esses serviços serem distribuidos em outras portas sob critério do administrador do servidor) https://pt.wikipedia.org/wiki/Lista_de_portas_dos_protocolos_TCP_e_UDP.

Mas como saber se um servidor web dispõe ou não de outros serviços? Para isso existem ferramentas chamadas de Port Scanners, cujo objetivo é verificar se a máquina do servidor está escutando por requisições para tais serviços. Essas ferramentas podem tanto fazer uma busca simples, baseando-se nas portas mais convencionais, quanto utilizar a força bruta para buscar serviços em portas não usuais.


## Exemplos de Serviços

* **Port 20/21 - File Transfer Protocol (FTP):** Protocolo que permite transferir arquivos entre dois computador conectados via Internet (Saiba mais: https://www.hostinger.com.br/tutoriais/ftp-o-que-e-como-funciona). Uma falha nesse serviço pode ocasionar livre acesso à injeção de arquivos (por vezes maliciosos).
* **Port 22 - Secure Shell (SSH):** Protocolo que permite acesso e controle remoto do servidor por meio de uma comunicação criptografada.
* **Port 25/587 - Simple Mail Transfer Protocol (SMTP):** Protocolo para envio de mensagens de correio eletrônico. É um serviço usado apenas para saída de pacotes.
* **Port 110 - Post Office Protocol version 3 (POP3)** Protocolo utilizado para acesso remoto a servidores de e-mail. Permite o download das mensagens para a máquina local.
* **Port 80 - HTTP**
* **Port 443 - HTTP Secure (HTTPS)**


## Qual a importância?

Servidores Web são instâncias visíveis e, no geral, bastante acessíveis para que qualquer um possa enviar e solicitar dados.

Sob a perspectiva de um agente malicioso, um Scan de Portas é geralmente um dos primeiros passos realizados contra um determinado endereço. Isso é utilizado como método de reconhecer quais serviços são oferecidos e quais portas estão abertas para comunicação pela rede.

Não é incomum, por exemplo, a existência de bots que vasculham a internet em busca de determinados serviços para, em seguida, realizar ataques automatizados por meio de vulnerabilidades já conhecidas.

Já sob a perspectiva de um administador da máquina, um Scan de Portas é interessante, pois pode denúnciar a existência de backdoors ou outros processos maliciosos - como de um servidor FTP em uma porta não convencional.

