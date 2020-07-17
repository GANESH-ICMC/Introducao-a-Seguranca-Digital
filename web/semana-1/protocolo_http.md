# Protocolo HTTP

O protocolo HTTP é a base da troca de dados na Web, sendo responsável por transmitir documentos de hipertexto - como o HTML -, imagens, vídeos e resultados de formulários entre cliente e servidor.

O HTTP é um protocolo _stateless_ \(comunicação feita por meio de mensagens individuais\) cliente-servidor que segue o seguinte modelo de comunicação: um cliente \(geralmente o _browser_\) abre uma conexão por meio de uma requisição feita ao servidor, que recebe a requisição e envia uma resposta ao cliente. Entretanto, entre o navegador que faz a requisição e o servidor que envia a resposta existem vários dispositivos tratando e retransmitindo a mensagem \(roteadores, modems, computadores e outras máquinas\).

## Etapas de comunicação - Fluxo HTTP

Conforme dito anteriormente, a comunicação entre cliente e servidor ocorre por meio de mensagens individuais. Porém, quando um cliente quer comunicar-se com um servidor ele realiza os seguintes passos: 1. **Abrir uma conexão TCP**: essa conexão é utilizada para enviar uma ou várias requisições e receber respostas.

1. **Enviar uma mensagem HTTP**: um detalhe **importantíssimo** do protocolo HTTP é que essa mensagem **não é criptografada**, ou seja, ela pode ser lida por qualquer um que esteja monitorando o fluxo de pacotes da rede. A mensagem segue esse padrão:

![](https://i.imgur.com/OxDXcP7.png)

1. **Ler a mensagem de resposta do servidor**: após enviar uma requisição, se não houver problemas, o servidor enviará uma resposta. Essa resposta também **não é criptografada** e segue esse padrão:

![](https://mdn.mozillademos.org/files/13691/HTTP_Response.png)

1. **Fechar ou reutilizar a conexão TCP que foi aberta**.

## Requisições

Conforme mostrado nas duas últimas imagens, as requisições e as respostas são compostas de certos elementos.

Os **elementos das requisições** são:

* Método HTTP: operação que o cliente deseja fazer;
* O caminho do recurso a ser buscado: em outras palavras, a parte da URL que vem após o ".com", ".br", ".org" etc. \(ou seja, a URL sem os _elementos de contexto_\*\), indicando a localização do recurso no servidor;
* A versão do protocolo HTTP;
* _Headers_ opcionais: são cabeçalhos que contém informações adicionais para os servidores, como cookies, data, linguagem aceita, tamanho da requisição e outros. Headers padrões podem ser encontrados [aqui](https://flaviocopes.com/http-request-headers/);
* Corpo de dados: contém recursos requisitados \(ou enviados\). Normalmente, eles vêm em respostas, mas também se fazem presentes, geralmente, em requisições do tipo `POST` por exemplo.

E os **elementos das respostas** são:

* Versão do protocolo HTTP utilizada pelo servidor;
* Código de status: indica se a requisição foi bem sucedidade ou não \(e o porquê\);
* Mensagem de status: breve descrição do código de status;
* _Headers_ \(cabeçalhos\) HTTP: iguais aos da requisição;
* Corpo com dados do recurso requisitado \(se algo foi requisitado\).

 \* Elementos de contexto são coisas como: protocolo \(`http://`\), domínios e subdmínios \(`www.google.com`\) e a porta da conexão TCP \(após a URL pode vir um`:80` por exemplo\)

### Tipos de requisições \(métodos HTTP\)

As requisições HTTP podem ser de vários tipos, indicando a ação que deve ser realizada com determinado conteúdo. Os principais tipos são **`GET`** e **`POST`**, mas também há: **`HEAD`**, **`PUT`**, **`DELETE`**, **`CONNECT`**, **`OPTIONS`**, **`TRACE`**, **`PATCH`** e outros.

* **`GET`** é utilizado para requisitar certo conteúdo \(normalmente a apresentação desse conteúdo no navegador\). Esse método serve para reaver/solicitar dados.
* **`POST`** é utilizado para enviar algum conteúdo para o servidor \(como os dados de um formulário preenchido ou uma tentativa de login\).

  Obs.: Esses métodos podem ser usados em outros contextos, pois o servidor decide como interpretar as requisições. O servidor pode esperar um `POST` que simplesmente solicite conteúdo, sem enviar nada para o próprio servidor.

### Respostas HTTP \(status codes\)

Os códigos de status presentes em respostas HTTP \(_HTTP responses_\) indicam se a requisição foi realizada com sucesso ou não. Esses códigos são divididos em:

* Informational responses \(100–199\),
* Successful responses \(200–299\),
* Redirects \(300–399\),
* Client errors \(400–499\),
* Server errors \(500–599\).

### Os códigos que mais aparecem são:

* **`200` `OK`**: a requisição foi um sucesso, ou seja, o conteúdo da requisição foi obtido ou transmitido sem erros.
* **`301` `Moved Permanently`**: código de redirecionamento indicando que a recurso solicitado  foi movido permanentemente para outro local - indicado no _header_ `Location`. O _browser_ é redirecionado para lá automaticamente. O código 308 funciona da mesma forma.
* **`302` `Found`**: código de redirecionamento indicando que o conteúdo procurado está temporáriamente em outro local - também indicado no _header_ de resposta `Location`. O _browser_ é redirecionado para lá automaticamente. O código 307 funciona da mesma forma.
* **`400` `Bad Request`**: erro de sintaxe na requisição, ou seja, o servidor não conseguiu processar bem a requisição.
* **`401` `Unauthorized`**: requisição não autorizada. O cliente precisa se autenticar \(ex.: fazer login\) para conseguir o acesso ao que foi requisitado.
* **`403` `Forbidden`**: o cliente não pode acessar o conteúdo solicitado, ou seja, ele não está autorizado a ver certa informação \(mesmo que autenticado, já que o servidor sabe a identidade do cliente\).
* **`404` `Not Found`**: o servidor não encontrou o que foi requisitado - e o conteúdo buscado provavelmente não existe. Em _browsers_, isso significado que a URL passada não foi reconhecida.
* **`500` `Internal Server Error`**: erro interno do servidor, ou seja, o servidor está com problemas para lidar com certa situação.
* **`502` `Bad Gateweay`**: erro que indicado que o servidor, atuando como gateway \(buscando a resposta para retransmitir ao cliente\), recebeu uma resposta inválida.
* **`503` `Service Unavailable`**: o servidor não está pronto para processar a requisição. Normalmente, isso indica que o servidor está desligado ou sobrecarregado.

