# COMMAND INJECTION - SHELL INJECTION
Vulnerabilidade web que permite com que o atacante execute comandos de terminal arbitrariamente, utilizando comandos do sistema operacional no servidor no qual roda a aplicação, sendo assim, possibilitando alcançar e explorar a aplicação como um todo, assim como seus dados.

A falha ocorre quando a aplicação envia comandos para o sistema operacional a partir de dados fornecidos pelo usuário, enviados para a aplicaçào via formulários, cookies, HTTP headers, entre outros, sendo que tais informações não recebem um tratamento ou não são validadas.

Os dados fornecidos pelo usuário rodam em uma shell do sistema operacional da aplicação.

Ao não ocorrer uma validação do input realizado pelo usuário, um atacante poderá inserir comandos de linha de terminal/sistema operacional através do parâmetro vulnerável, utilizando os privilégios da aplicação web, possibilitando um exploit.

Ainda, em casos mais extremos, é possível executar um reverse shell a partir do command injection, evoluindo o risco e consequências do ataque.

## Comandos utilizados e seus propósitos

| Propósito | No Linux | No Windows |
|-----------|----------|------------|
|Descobrir o usuário atual| whoami|whoami|
|Descobrir o sistema em que roda a aplicação| uname -a| ver |
|Configuração da internet|ifconfig|ipconfig /all|
|Processos em execução| ps -ef|tasklist|

## Exemplos de Command Injection
### Exemplo 1
Consideremos o seguinte código PHP
``` php
<?php
    print("Please specify the name of the file to delete");
    print("<p>");
    $file=$_GET['filename'];
    system("rm $file");
?>
```
O código consiste em pegar o que é enviado pelo parâmetro filename do método GET do protocolo HTTP, utilizando para rodar um comando do sistema operacional, sendo ele o rm, que deleta um arquivo especificado como parâmetro.

Não existe tratamento ou validação do que é recebido pelo parâmetro, possibilitando um fácil ataque de um usuário malicioso, passando comandos junto ao já existente.

Realizando a seguinte requisição: enviar o nome do arquivo a ser removido pelo comando (rm bob.txt), mas acrescentando uma quebra de comando, com o caractere ";" e o comando id
```
https://127.0.0.1/delete.php?filename=bob.txt;id
```
Ao receber a requisição, o servidor utilizará a string enviado junto ao parâmetro get filename, executando o seguinte código:
```
rm bob.txt;id
```
Dessa forma, o arquivo bob.txt será de fato removido, mas teremos ainda a execução do comando seguinte (id), que nos retorna as informações acerca do usuário atual
```uid=33(www-data) gid=33(www-data) groups=33(www-data)```

### Exemplo 2
Consideremos uma aplicação web simples, que requisita a partir de um formulário de texto, um ip para que seja pingado, sem realizar nenhuma validação do que recebe do usuário.

Ao receber um ip como 127.0.0.1, o comando executado a partir do sistema operacional que roda a aplicação é o seguinte:
```ping -c 10 127.0.0.1```
Em um código PHP seria algo do tipo
``` php
$ip = $_GET['ip'];
system("ping -c 10 $ip");
```
Como não existe validação, um também válido seria
```127.0.0.1; id;```
Isso executaria o ping no ip desejado, e logo em seguida, resultaria na execução do comando id.

## Blind OS Command Injection \(Command Injection às cegas\)
Existem situações em que não é retornado para o usuário qual o resultado de sua interação, mesmo que a aplicação rode algum comando na shell do seu sistema operacional.

Dessa forma, é necessário encontrar outros modos de identificar que existe de fato uma shell rodando comandos a partir dos dados fornecidos pelo usuário.

Um exemplo é utilizando time delays: podemos inserir o comando ping com um número de determinado de pacotes ou de tempo para rodar, o que resulta em um delay da resposta da aplicação, resultante do tempo de execução do comando efetuado (ping com tempo ou pacotes delimitados).

## Redirecionado o output
Em algumas situações, podemos redirecionar o output de um comando que queremos verificar seu conteúdo, uma vez que não temos o retorno da aplicação, mas podemos manipular um arquivo e visualizar seu conteúdo.
```; whoami > /var/www/static/whoami.txt;```

## Principais comandos de OS injecting & como mitigar Command Injection

Os seguintes comandos são muito úteis para utilizar ao construir payloads de command injection
- &
- && 
- ;
- \n 
- | 
- ||  
- \`injected command\`
- $\(injected command\)

Dessa forma, a maneira mais precisa e eficiente de impossibilitar/mitigar ataques via command injection é realizar validações nos inputs realizados pelo usuário \(*data-sanitize*\), fazendo uma limpeza na string enviada a partir dos parâmetros, retirando os caracteres descritos acima.

## Fontes
[Owasp, uma das melhores fontes para aprender segurança web](https://owasp.org/www-community/attacks/Command_Injection)

[Portswigger: aprendendo segurança web de graça](https://portswigger.net/web-security/os-command-injection)

[Netsparker, artigo sobre Command Injection e sua mitigação](https://www.netsparker.com/blog/web-security/command-injection-vulnerability/)

[infosec, site brasileiro sobre segurança web](https://www.infosec.com.br/command-injection/)
