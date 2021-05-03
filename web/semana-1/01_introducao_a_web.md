# Arquitetura de uma aplicação Web

## Internet e Web

Imagine que a Internet é uma imensa loja de livros e a Web é uma coleção de livros presente nessa loja...

De forma simples, a Internet é uma rede \(global\) de redes que conecta milhões de dispositivos através de: email eletrônico, compartilhamento de arquivos \(via FTP\), jogos online, aplicativos mobile, páginas web etc.

Já a Web \(World Wide Web\) representa um conjunto de informações acessadas via Internet por meio de _hyperlinks_ - referenciando URIs \([Uniform Resource Identifier](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier)\). Ou seja, a Web é uma das redes presente na Internet. Os recursos presentes na Web são normalmente acessados por meio de navegadores \(Chrome, Firefox, Safari etc.\), fazendo uso do protocolo HTTP ou HTTPS.

Os recursos na Web costumam ser apresentados na forma de _web pages_ - que formam _websites_. Essas páginas são criadas e estilizadas por meio de linguagens como HTML, CSS e Javascript - sendo possível utilizar também outras, como PHP e Python.

## A Arquitetura

![Arquitetura de um web app](../../.gitbook/assets/arquitetura_web_back_front.png)

Em uma aplicação Web, há dois tipos de "sub-programas", um _client-side_ e outro _server-side_. O código _client-side_ \(HTML, CSS e Javascript\) é o que está na página do navegador e que interage diretamente com as entradas do usuário. Já o código _server-side_ está em um servidor e responde às requisições HTTP que chegam até ele. Para o código _client-side_, pode-se utilizar C\#, Java, Javascript, Python, PHP, Ruby e mais - basicamente, qualquer linguagem que entenda e responda requisições HTTP.

### Componentes estruturais

Esses componentes são responsáveis pela funcionalidade da aplicação web \(com a qual o usuário interage\) e pelo controle, tratamento e armazenamento dos dados passados ao servidor.

Esses componentes englobam:

* Páginas web + navegador \(_browser_\) -&gt; _client-side_
* Servidor da aplicação web -&gt; _server-side_
* Servidor do banco de dados -&gt; _server-side_

  _Obs.: o servidor da aplicação e do banco de dados podem ser a mesma máquina._:w

#### Navegador e páginas web

O navegador recebe e processa o código das páginas web, geralmente desenvolvidas usando HTML, CSS e Javascript, e então mostrar o resultado para o usuário e permitir que ele interaja com a página já pronta.

#### Servidor da aplicação Web

O servidor da aplicação é responsável por: tratar as requisições que chegam dos clientes, "chamar" APIs, fazer requisições para bancos de dados e enviar respostas aos clientes \(na forma de páginas Web, arquivos, JSONs etc.\). Esse servidor pode ser desenvolvido em Node.js, PHP, Python, Java, .NET, Ruby...

#### Servidor do banco de dados

O banco de dados é responsável por armazenar dados - como informações de login de usuários ou itens de uma loja - no _server-side_ de forma persistente. Além de armazenar esses dados, ele é capaz de fazer buscas e retornar informações para que o servidor da aplicação Web utilize e possivelmente devolva ao cliente.

### Entendendo o "fluxo" de informação do front-end

Primeiramente, ao digitar a URL de um site, o navegador deve convertê-la em um endereço IP. Esse processo é chamado de "name resolution" e é realizado através de um DNS \(Domain Name System\), que faz a associação `hostname da URL:endereço IP`.

Em seguida, o navegador fará uma requisição para o servidor para o qual o endereço IP encontrado no primeiro passo aponta. Essa requisição, em geral, será um `GET`, solicitando a página web especificada na URL, ou um `POST`, enviando dados que serão usados pelo _back-end_ do servidor.

Como resposta, o servidor \(_back-end_\) enviará arquivos e informações do tipo HTML, CSS, JS, PHP, JSON, JPG e, possivelmente, outros. Esses arquivos são tratados pelo navegador, que é responsável por exibi-los ao usuário, e pelo código da página web presente no _front-end_. Além disso, podem haver _headers_ importantes nesses arquivos, contendo, por exemplo, informações sobre a sessão atual.

Vale destacar que o sistema operacional do cliente é responsável por fazer as requisições "saírem" do navegador em direção à Internet e por recuperar as respostas vindas do servidor \(pela Internet\). O sistema operacional expõe o computador à rede por meio de portas, que permitem a troca de informação via certos protocolos, como o HTTP \(comumente porta 80\) e o HTTPS \(comumente porta 443\).
