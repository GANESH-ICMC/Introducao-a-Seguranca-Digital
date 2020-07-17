# Linguagens de Programação \(Server Side\)

_Até agora vimos um pouco sobre a arquitetura dos servidores HTTP e como as portas são utilizadas para mapear os diferentes serviços que ela pode oferecer. Agora, iremos falar um pouco sobre as linguagens de programação utilizadas nos servidores para o desenvolvimento de sistemas._

_Obs: Vamos partir do pressuposto que você, neste momento, já tem um mínimo de conhecimento sobre alguma linguagem de programação \(C, C++, Java, python, etc\)._

## 1. Linguagens de programação Web são diferentes?

Reforçando o que já foi dito anteriormente, servidores web nada mais são do que computadores comuns que possuem alguma aplicação agindo como Servidor HTTP e processando as requisições.

Na teoria, portanto, você pode comandar essa aplicação para enviar requisições para um programa escrito em qualquer linguagem que você desejar \(obviamente, você teria que se atentar às especificações ao integrar o servidor HTTP ao seu programa, garantindo que o mesmo recebesse e retornasse os dados corretamente\).

Na prática, existem certas linguagens que costumam ser mais adotadas pelos desenvolvedores devido a alguns fatores. Vamos citar abaixo alguns deles.

* **Facilidade** apesar de ser possível utilizar qualquer linguagem na hora de desenvolver um sistema web, algumas delas já possuem de antemão o ferramental necessário para lidar com as requisições recebidas do servidor. O [PHP](https://www.php.net/manual/pt_BR/intro-whatis.php), por exemplo, se tornou popular devido à baixa curva de aprendizado e à rapidez quando integrado ao Apache Web Server.
* **Frameworks** muitas linguagens de próposito geral já possuem framewoks que facilitam no desenvolvimento web. Dentro vários, podemos citar, por exemplo, o framework [Django](https://www.djangoproject.com) para python e o [Rails](https://rubyonrails.org/) para Ruby.
* **Eficiência ou Segurança** muitos sistemas precisam lidar com questões de desempenho e a escolha da linguagem muitas vezes impacta nesse fator. A linguagem [Rust](https://www.rust-lang.org/pt-BR), por exemplo, é muito empregada em sistemas cujo uso da memória precisa ser seguro e eficiente. Já o [Node.js](https://nodejs.org/en/) foi criado pensando em aplicações que necessitam de escalabilidade.
* **Gosto pessoal** por fim, a zona de conforto do responsável pelo sistema também influencia muito na hora de escolher uma linguagem, uma vez que cada linguagem possui suas decisões de projeto, paradigmas, se é tipada/não tipada, se é compilada ou interpretada etc.

Nos challs utilizados no Ping \(assim como em muitos outros CTF's pela web\) iremos utilizar, majoritariamente, o PHP exatamente pelo fator de facilidade para principiantes de programação. Vamos, portanto, dar uma breve olhada em como essa linguagem funciona na prática.

## 2. PHP, como funciona?

O PHP se trata de uma linguagem de script de propósito geral criada em 1994 por Rasmus Lerdof. Ela nasceu nos primórdios da web como uma ferramenta voltada para a criação de sites e se tornou uma das mais conhecidas do meio.

Essa linguagem é responsável por uma grande parcela dos sites que compõem a web e ainda recebe diversas atualizações. Vejamos então um exemplo de script utilizando essa linguagem.

```php
<html>
 <head>
  <title>Super Ultra Website</title>
 </head>
 <body>
     <?php
         if( isset($_GET['admin']) && $_GET['admin'] == '1' ){
             echo "<p>Olá Administrador!</p>";
         } else {
             echo "<p>Olá Mundo!</p>";
         }
      ?>
 </body>
</html>
```

Arquivo: index.php

Primeiramente, é importante notar que todos os arquivos dessa linguagem são indentificados pelo tipo de arquivo `.php`. O nome do arquivo é importante, pois ele é utilizado pelo Servidor HTTP para decidir se o arquivo deve ou não ser executado ou retornado para o cliente.

Um comportamento bastante comum de diferentes servidores é o de buscar e carregar arquivos `index` ao receberem uma requisição que direciona para uma pasta.

Exemplo: um servidor Apache que recebe uma requisição para o seguinte caminho: `http://www.meusite.com/meu/diretorio` irá abrir o caminho desejado na máquina e verificar a existência de algum arquivo `index.html` ou `index.php`. Caso exista, o código do index é executado, senão é retornado um erro 404 \(ou a estrutura das subpastas, dependendo das configurações do servidor\).

Voltando agora ao exemplo, vemos que um arquivo `.php` permite a mistura do já conhecido HTML com estruturas dessa linguagem. Isso é possível graças às chaves `<?php args... ?>` que permitem ao interpretador decidir quais partes do arquivo precisam ser executadas.

```php
 <?php
     if( isset($_GET['admin']) && $_GET['admin'] == '1' ){
         echo "<p>Olá Administrador!</p>";
     } else {
         echo "<p>Olá Mundo!</p>";
     }

     $a = 1;
     $b = 2;
     echo $a + $b;
  ?>
```

Arquivo: index.php

Assim como qualquer outra linguagem, PHP também possui os operadores lógicos e condicionais básicos \(if, else, while etc.\). As variáveis em PHP são sempre iniciadas pelo símbolo `$` e o uso de `;` no final de cada comando é obrigatório. As variáveis no PHP não são tipadas, ou seja, qualquer tipo de valor pode ser atribuído a elas a qualquer momento \(assim como o valor `null`\).

Por fim, conforme visto nas aulas anteriores, a linguagem PHP também possui ferramentas para acessar os parâmetros recebidos na requisição utilizando as variáveis globais `$_REQUEST`,`$_GET`,`$_POST`,`$_COOKIE`, entre outras.

## 3. Qual a importância?

No âmbito de segurança web, é importante buscar entender a linguagem utilizada nos sistemas pois, em alguns casos, as escolhas tomadas nos projetos de algumas podem acarretar na má utilização por parte dos desenvolvedores e, por consequência, em vulnerabilidades nos sistemas.

Muitas das falhas cometidas na web são lógicas, isso é, não estão atreladas à linguagem em si, mas sim às más decisões ao construir um site.

Um SQL Injection, por exemplo, pode ser encontrado tanto em website PHP quanto em outro feito em Python e isso não está atrelado diretamente à linguagem e sim à implementação feita pelos desenvolvedores.

Há algumas vulnerabilidades, entretanto, que podem surgir devido às implementações da linguagem, podendo ser algo de baixo nível, como funções vulneráveis a buffer overflow ou coisas simples como uma conversão automática de tipos durante uma comparação \(_loose comparison_\).

