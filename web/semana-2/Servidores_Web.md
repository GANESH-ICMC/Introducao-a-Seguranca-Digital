# Servidores Web

*No conteúdo da primeiro aula, abordamos um pouco sobre os processos que ocorrem sob o alcance do usuário ao requisitar o conteúdo de uma página web. Logo, no ponto atual, já sabemos o que são os protocolos HTTP, HTTPS além de sabermos o que são as requisições que o browser realiza e os tipos de conteúdos que o mesmo solicita para o servidores.*

*A partir de agora, iremos começar a explorar um pouco da arquitetura que permite que a web ofereça tantos serviços e websites tal como conhecemos nos dias atuais.*

## 1. O que é um Web Server 

![](https://media.prod.mdn.mozit.cloud/attachments/2016/08/09/13677/d031b77dee83f372ffa4e0389d68108b/Fetching_a_page.png) 
<p style="text-align: center;">Fonte: developer.mozilla.org</p>


Um servidor web pode ser compreendido de maneira sucinta como um computador que possui uma série de mecanismos capazes de receber, processar e responder as requisições que são enviadas pelos clientes.

O objetivo da segunda aula será o de introduzir quais são esses mecânismos e como eles atuam para que o servidor possa entregar ao cliente o conteúdo esperado para sua requisição.

*Tópicos que serão visitados: Servidores HTTP e de aplicação; Conteúdo estático vs Conteúdo Dinâmico; Apache Server; Nginx; Bancos de Dados; Portas e Serviços; etc.*

## 2. Servidores HTTP e Tipos de conteúdos

Dentre os diferentes tipos de protocolos de comunicação que funcionam na internet, iremos nos focar principalmente nos Hypertext Transfer Protocol (HTTP), uma vez que eles são os responsáveis por solicitar documentos e recursos do servidor.

*Obs: A forma utilizada para processar tais requisições irá variar dependendo da arquitetura e também do servidor utilizado, iremos então discutir em um nível abstrato e caso queira se aprofundar basta utilizar os links disponibilizados nas referências.*

![Estrutura Servidor HTTP](https://i.imgur.com/HHyYUgW.png)
<p style="text-align: center;">Fonte: developer.mozilla.org</p>

O mecanismo responsável pelo gerenciamento dessas requisições é chamado de Servidor HTTP e a sua função é mapear, por meio das informações recebidas pelo cabeçalho, qual tipo de documento o cliente deseja receber do servidor. Podemos dividir os tipos de conteúdos em duas categorias principais:

* **Conteúdos Estáticos:** são arquivos que não necessitam de nenhum tipo de processamento do servidor, bastando que o processo apenas leia e retorne uma cópia domesmo para o cliente (ex: arquivos de imagens, .css, javascript, .html, .pdf).
* **Conteúdos Dinâmicos:** são conteúdos que demandam algum tipo de processamento para retornar o conteúdo. Uma pesquisa, por exemplo, necessita que haja uma busca em um banco de dados e que a resposta seja construída de acordo com a requisição.

Vamos ver então dois cases de servidores web amplamente utilizados: o Apache HTTP Server e o Nginx. Mas antes, caso queira se aprofundar nos tópicos visto até o momento recomendamos os seguintes links:

1. Uma visão geral do HTTP. (https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Overview)
2. O que é um Servidor Web? (https://developer.mozilla.org/pt-BR/docs/Learn/Common_questions/o_que_e_um_web_server)
3. O que é um servidor Web (https://tudosobrehospedagemdesites.com.br/servidor-web/#servidor-web-programa)
4. What Is an Application Server vs. a Web Server? (https://www.nginx.com/resources/glossary/application-server-vs-web-server/)

## 3. Apache HTTP Server

![](https://s3.amazonaws.com/stillat/img/ch1_request_lifecycle.png) 
<p style="text-align: center;">Fonte: https://stillat.com/</p>

O projeto Apache é um servidor web criado em 1995 e é, desde então, um dos servidores mais utilizados para a hospedagem de websites (https://news.netcraft.com/archives/category/web-server-survey/). O core da sua aplicação é bastante enxuto e focado principalmente na tarefa de buscar e transmitir os dados requisitados via HTTP. No entanto, graças a uma grande comunidade de desenvolvedores e a sua arquitetura que permite a integração de módulos externos, ele se tornou uma ferramenta poderosa e muita utilizada ainda hoje.

Outra das vantagens do Apache é a sua alta integração com com outros projetos Open Source como o PHP e o MySQL. O uso dessas tecnologias em conjunto é muito comum e recomendada como porta de entrada para aqueles que querem saber mais sobre desenvolvimento web. Há diversos projetos que permitem a instalação dos três de maneira rápida, permitindo a criação de um servidor web local em conjunto com um banco de dados (ex: XAMP, WAMP, LAMP).

Para saber mais sobre, veja os seguintes links:

1. An Introduction to Apache (https://code.tutsplus.com/tutorials/an-introduction-to-apache--net-25786)
2. How Does PHP Work With The Web Server And Browser? (https://stillat.com/blog/2014/04/02/how-does-php-work-with-the-web-server-and-browser)
3. O que são Virtual Hosts? (https://revista.devall.com.br/apache-http-server-para-devs-o-que-sao-virtual-hosts/)
4. Apache tutorial (https://www.guru99.com/apache.html)

## 4. NGINX Web Server

![](https://www.aosabook.org/images/nginx/architecture.png) 
<p style="text-align: center;">Fonte: https://www.aosabook.org</p>

O NGINX se trata de um sistema Open Source que atua como Web Server, foi lançado em 2004 com o objetivo de ser um servidor com alta escalabilidade e eficiência e é atualmente o servidor mais utilizado para servir conteúdos web.

Assim como o Apache, o NGINX também possui alta integração com muitos outros projetos Open Source, além de possui muitos outros serviços além do de HTTP Server como Proxy Reverso, Load Balancer e Web application Firewall. Caso queira se aprofundar mais em como ele funciona, veja os links a seguir

1. What is NGINX? (https://www.nginx.com/resources/glossary/nginx/)
2. Inside NGINX (https://www.nginx.com/blog/inside-nginx-how-we-designed-for-performance-scale/)
3. NGINX (https://www.aosabook.org/en/nginx.html)
4. Beginner's Guide (http://nginx.org/en/docs/beginners_guide.html#control)

## 5. Qual a importância?

Compreender o básico sobre a arquitetura e funcionamento de servidores web é importante pois, como qualquer software, eles estão sujeitos a bugs e vulnerabilidades. Um HTTP Server mal implementado ou muito antigo, por exemplo, pode ser facilmente sobrecarregado por meio de um Ataque de Negação de Serviço (DoS) e possuir falhas de configuração que permitam acesso à arquivos indevidos.

## 6. Muito além do Servidor HTTP

Até o momento, tratamos o Servidor Web como uma instância simples que é executada em uma única máquina. No entanto, isso nem sempre é verdade. Grandes websites precisam lidar com problemas de disponibilidade e performance em alta escala e isso, muitas vezes, demanda uma arquitetura muito maior do que um simples servidor HTTP.

Caso você queira se aprofundar mais no tema, recomendamos a video aula do link a seguir. Nela, você poderá entender um pouco melhor sobre a arquitetura e funcionamento de serviços que precisam lidar com uma grande quantidade de requisições.

1. Lecture 9 - Scalability - Harvard Web Development (https://youtu.be/-W9F__D3oY4)
2. Reverse Proxy vs Load Balancer (https://www.nginx.com/resources/glossary/reverse-proxy-vs-load-balancer/)
3. Web Application Firewall (https://pt.wikipedia.org/wiki/Web_Application_Firewall)

