# Introdução aos Servidores Web

*Até o momento atual vimos como o protocolo HTTP(S) atua como o protocolo de comunicação da Web, permitindo que os navegadores possam solicitar diferentes tipos de conteúdos pela Internet. A partir de agora, iremos nos focar em entender um pouco da arquitetura que permite que a web ofereça tantos serviços e sites tal como conhecemos nos dias atuais.* 

![Servidores Web](https://i.imgur.com/m9D1tgU.jpg)

# 1. O que é um Servidor Web?

Podemos definir um Servidor Web simples como um computador com uma série de mecanismos capazes de: 

 1. **Receber** requisições HTTP dos clientes,
 2. **Processar** as requisições uma a uma,
 3. **Retornar** uma resposta HTTP aos clientes.

Apesar de poucas etapas, o processamento muitas vezes pode ser algo simples, como o conteúdo de uma imagem, ou algo complexo como uma busca em um conjunto de bases de dados com milhares de registros.

Qualquer computador com acesso à uma rede pode agir como um Servidor Web e o objetivo dos próximos tópicos será de dar um breve vislumbre de quais são esses mecanismos e como eles atuam para que o servidor entregue o conteúdo esperado para cada requisição.

## 2. Servidor HTTP e Tipos de Conteúdos

O mecanismo responsável por estabelecer as conexões e processar as mensagens HTTP recebidas é chamado de **Servidor HTTP**, e a sua função é mapear, por meio das informações recebidas pelos cabeçalhos, qual tipo de conteúdo o cliente deseja receber do servidor. 

![Estrutura Servidor HTTP](https://i.imgur.com/HHyYUgW.png)

Fonte: developer.mozilla.org

Podemos dividir os tipos de conteúdos em duas categorias principais:

-   **Conteúdos Estáticos:** são arquivos que não necessitam de nenhum tipo de processamento do servidor, bastando que o processo apenas leia e retorne uma cópia do mesmo para o cliente (Ex: arquivos de imagens, CSS, JS, HTML, PDF, ZIP).

-   **Conteúdos Dinâmicos:** são conteúdos que demandam algum tipo de processamento para retornar o conteúdo. Uma pesquisa, por exemplo, necessita que haja uma busca em um banco de dados e que a resposta seja construída de acordo com a requisição.

Geralmente no segundo caso, o servidor HTTP irá invocar a execução de algum código escrito em alguma linguagem de programação (Ex: PHP, Python, Javascript) seja na mesma máquina ou em um Servidor de Aplicação externo e este será responsável por realizar toda a carga de trabalho necessária. Nas aulas futuras iremos abordar com mais detalhes como esses outros mecanismos funcionam.  

Vamos ver então dois exemplos de servidores web amplamente utilizados atualmente: o Apache HTTP Server e o Nginx. Mas antes, caso queira se aprofundar nos tópicos visto até o momento recomendamos os seguintes links:

1. Uma visão geral do HTTP. \([https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Overview](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Overview)\)
2. O que é um Servidor Web? \([https://developer.mozilla.org/pt-BR/docs/Learn/Common\_questions/o\_que\_e\_um\_web\_server](https://developer.mozilla.org/pt-BR/docs/Learn/Common_questions/o_que_e_um_web_server)\)
3. Servidor Web: Hardware ou Programa? \([https://tudosobrehospedagemdesites.com.br/servidor-web/\#servidor-web-programa](https://tudosobrehospedagemdesites.com.br/servidor-web/#servidor-web-programa)\)
4. What Is an Application Server vs. a Web Server? \([https://www.nginx.com/resources/glossary/application-server-vs-web-server/](https://www.nginx.com/resources/glossary/application-server-vs-web-server/)\)

## 3. Apache HTTP Server

![](https://s3.amazonaws.com/stillat/img/ch1_request_lifecycle.png)
Fonte: https://stillat.com/

O projeto Apache é um servidor web criado em 1995 e é, desde então, um dos servidores mais utilizados para a hospedagem de websites \([https://news.netcraft.com/archives/category/web-server-survey/](https://news.netcraft.com/archives/category/web-server-survey/)\). O core da sua aplicação é bastante enxuto e focado principalmente na tarefa de buscar e transmitir os dados requisitados via HTTP. No entanto, graças a uma grande comunidade de desenvolvedores e a sua arquitetura que permite a integração de módulos externos, ele se tornou uma ferramenta poderosa e muita utilizada ainda hoje.

Uma das vantagens do Apache é a sua alta integração com com outros projetos Open Source como o PHP e o MySQL. O uso dessas tecnologias em conjunto é muito comum e **recomendada como porta de entrada para aqueles que querem saber mais sobre desenvolvimento web**. Há diversos projetos que permitem a instalação dos três de maneira rápida, permitindo a criação de um servidor web local em conjunto com um banco de dados \(ex: XAMP, WAMP, LAMP\).

Para saber mais sobre, veja os seguintes links:

1. An Introduction to Apache \([https://code.tutsplus.com/tutorials/an-introduction-to-apache--net-25786](https://code.tutsplus.com/tutorials/an-introduction-to-apache--net-25786)\)
2. How Does PHP Work With The Web Server And Browser? \([https://stillat.com/blog/2014/04/02/how-does-php-work-with-the-web-server-and-browser](https://stillat.com/blog/2014/04/02/how-does-php-work-with-the-web-server-and-browser)\)
3. Apache tutorial \([https://www.guru99.com/apache.html](https://www.guru99.com/apache.html)\)

## 4. NGINX Web Server

![](https://www.aosabook.org/images/nginx/architecture.png)
Fonte: https://www.aosabook.org

O NGINX se trata de um sistema Open Source que atua como Web Server, foi lançado em 2004 com o objetivo de ser um servidor com alta escalabilidade e eficiência e é atualmente o servidor mais utilizado para servir conteúdos web.

Assim como o Apache, o NGINX também possui alta integração com muitos outros projetos Open Source, além de possui muitos outros serviços além do de HTTP Server como Proxy Reverso, Load Balancer e Web application Firewall. Caso queira se aprofundar mais em como ele funciona, veja os links a seguir

1. What is NGINX? \([https://www.nginx.com/resources/glossary/nginx/](https://www.nginx.com/resources/glossary/nginx/)\)
2. Inside NGINX \([https://www.nginx.com/blog/inside-nginx-how-we-designed-for-performance-scale/](https://www.nginx.com/blog/inside-nginx-how-we-designed-for-performance-scale/)\)
3. NGINX \([https://www.aosabook.org/en/nginx.html](https://www.aosabook.org/en/nginx.html)\)
4. Beginner's Guide \([http://nginx.org/en/docs/beginners\_guide.html\#control](http://nginx.org/en/docs/beginners_guide.html#control)\)

## 5. Arquitetura da Web na vida real

![](https://media.prod.mdn.mozit.cloud/attachments/2016/08/09/13677/d031b77dee83f372ffa4e0389d68108b/Fetching_a_page.png)

Fonte: developer.mozilla.org

Até o momento, tratamos o Servidor Web como uma instância simples que é executada em uma única máquina. No entanto, isso nem sempre é verdade. Grandes websites precisam lidar com problemas de disponibilidade e performance em alta escala e isso, muitas vezes, demanda uma arquitetura muito maior do que um simples servidor HTTP.

Caso você queira se aprofundar mais no tema, recomendamos a video aula do link a seguir. Nela, você poderá entender um pouco melhor sobre a arquitetura e funcionamento de serviços que precisam lidar com uma grande quantidade de requisições, assim como citar outros intermediários que podem estar inseridos entre o cliente e o servidor final.

1. Lecture 9 - Scalability - Harvard Web Development \([https://youtu.be/-W9F\_\_D3oY4](https://youtu.be/-W9F__D3oY4)\)
2. Reverse Proxy vs Load Balancer \([https://www.nginx.com/resources/glossary/reverse-proxy-vs-load-balancer/](https://www.nginx.com/resources/glossary/reverse-proxy-vs-load-balancer/)\)
3. Web Application Firewall \([https://pt.wikipedia.org/wiki/Web\_Application\_Firewall](https://pt.wikipedia.org/wiki/Web_Application_Firewall)\)
