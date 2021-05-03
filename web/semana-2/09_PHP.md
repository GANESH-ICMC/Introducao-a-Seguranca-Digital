# Introdução ao PHP

*Como vimos anteriormente, conteúdos gerados dinâmicamente geralmente executam alguma linguagem de programação por trás dos panos. Nesta aula iremos trazer um paradigma geral sobre as linguagens mais usadas para o desenvolvimento de aplicações Web dando enfoque à linguagem PHP.*

*Obs: se você já se sente confortável com desenvolvimento Web e PHP, sinta-se a vontade para avançar para os próximos tópicos.*

## 1. Quais linguagens de programação são utilizadas na Web?

Relembrando a aula anterior, servidores web são computadores que possuem alguma aplicação agindo como Servidor HTTP e processando as requisições.

Na teoria, portanto, você pode comandar essa aplicação para enviar requisições para um programa escrito em qualquer linguagem que você desejar (obviamente, você teria que se atentar às especificações ao integrar o servidor HTTP ao seu programa, garantindo que o mesmo recebesse e retornasse os dados corretamente).

Na prática, existem certas linguagens que costumam ser mais adotadas pelos desenvolvedores devido a alguns fatores. Vamos citar abaixo alguns deles.

* **Facilidade:** apesar de ser possível utilizar qualquer linguagem na hora de desenvolver um sistema web, algumas delas já possuem de antemão o ferramental necessário para lidar com as requisições recebidas do servidor. O [PHP](https://www.php.net/manual/pt_BR/intro-whatis.php), por exemplo, se tornou popular devido à baixa curva de aprendizado e à rapidez quando integrado ao Apache Web Server.

* **Frameworks:** muitas linguagens de próposito geral já possuem framewoks que facilitam no desenvolvimento web. Dentro vários, podemos citar, por exemplo, o framework [Django](https://www.djangoproject.com) para python e o [Rails](https://rubyonrails.org/) para Ruby.

* **Eficiência ou Segurança:** muitos sistemas precisam lidar com questões de desempenho e a escolha da linguagem muitas vezes impacta nesse fator. A linguagem [Rust](https://www.rust-lang.org/pt-BR), por exemplo, é muito empregada em sistemas cujo uso da memória precisa ser seguro e eficiente. Já o [Node.js](https://nodejs.org/en/) foi criado pensando em aplicações que necessitam de escalabilidade.

* **Gosto pessoal:** por fim, a zona de conforto do responsável pelo sistema também influencia muito na hora de escolher uma linguagem, uma vez que cada linguagem possui suas decisões de projeto, paradigmas, se é tipada/não tipada, se é compilada ou interpretada etc.

![Linguagens de Programação Web](https://i.imgur.com/c19QBDB.png)

Nos challs utilizados no Ping \(assim como em muitos outros CTF's pela web\) iremos utilizar, majoritariamente o PHP exatamente pelo fator de facilidade para principiantes de programação web. Vamos, portanto, dar uma breve olhada em como essa linguagem funciona na prática.

## 2. O que é o PHP?

O PHP se trata de uma linguagem de script de propósito geral criada em 1994 por Rasmus Lerdof. Ela nasceu nos primórdios da web como uma ferramenta voltada para a criação de sites e se tornou uma das mais conhecidas do meio. Essa linguagem é responsável por uma grande parcela dos sites que compõem a web e ainda recebe diversas atualizações. Vejamos então um exemplo de script utilizando essa linguagem.

```php
<html>
 <head>
  <title>Super Ultra Website</title>
 </head>
 <body>
     <?php echo "<p>Olá Mundo!</p>"; ?>
 </body>
</html>
```

Arquivo: index.php

Primeiramente podemos notar que há uma visível mistura de HTML com scripts PHP inseridos no meio, isso se deve a própria natureza da linguagem que nasceu para facilitar a criação de páginas dinâmicas para web. As tags `<?php ...código... ?>` permitem que o interpretador saiba diferenciar quais conteúdos devem ser de fato executados e quais devem apenas ser retornadas como estão.

Todos os arquivos devem terminar com o tipo `.php` e é comum que os Servidores HTTP sempre carreguem o arquivo `index` ao receberem uma requisição que aponte para uma pasta, como por exemplo:

```
GET / HTTP/1.1
Host: ganesh.icmc.usp.br

Apache irá carregar o arquivo /index.php ou /index.html se existirem...
```

## 3. Sintaxe, Variáveis e Operadores

O PHP se trata de uma linguagem não tipada e que também não exige que suas variáveis sejam previamente declaradas. Todas as variáveis devem iniciar com o símbolo `$` e há poucas restrições para os caractéres que podem ser utilizados em suas nomeações. Veja os exemplos:

```php
<?php
    $a = 1;
    $b = "5ej4 1m G4n3shEr!";
    $c = (2 * 2.5) + 3;
    $d = $a + $b + $c;

    echo $d;  // output: 14
```

Se você está estranhando o resultado 14 e não um erro por termos feito uma soma entre dois números e uma string, isso se deve à característica do PHP em tentar realizar a transformação automática da string para um número (que é bem sucedida pois a mesma inicia com o valor 5). 

Logo, linguagens de tipo dinâmico são fáceis de serem utilizadas mas podem apresentar comportamento não previsíveis aos desatentos do seu funcionamento.

Outro detalhe importante é o uso obrigatório do `;` ao fim de cada sentença mesmo que seja utilizado apenas um comando por linha.

Por fim, o PHP possui uma série de operadores lógicos e estruturas de controle como grande parte das linguagens, veja o exemplo a seguir:

```php
<?php
    for($i = 0; $i < 10; $i++){
        if($i % 2 == 0){ 
            echo "par";
        } else {
            echo "impar";
        } 
    }
```

Para saber mais detalhes das estruturas de controles, declaração de funções e criação de classes e objetos a [documentação do PHP](https://www.php.net/manual/pt_BR/langref.php) é bastante simples de se compreender, além de existir bastante material disponível na internet para iniciantes.

## 4. Acessando os dados da Requisição

Vamos relembrar o diagrama visto na aula de Servidores Web acerca do Apache HTTP Server:

![](https://s3.amazonaws.com/stillat/img/ch1_request_lifecycle.png)
Fonte: https://stillat.com/

Durante a etapa em que o servidor invoca o interpretador \(etapa 4\), as informações da requisição também são enviadas afim de ficarem disponíveis para o script `.php` e podem ser acessadas por meio de [variáveis globais pré-definidas](https://www.php.net/manual/pt_BR/reserved.variables.php). Vamos imaginar portanto, uma requisição para a seguinte url:

```
http://ganesh.icmc.usp.br/buscar.php?frente=web
```

Podemos acessar o parâmetro enviado pela URL utilizando a seguinte variável:

```php
<?php echo $_GET['frente']; ?>
```
 
Outras variáveis muito utilizadas também são: `$_POST`, `$_COOKIE`, `$_SERVER`, `$_REQUEST` e `$_SESSION`, tendo cada uma seu uso específico e que pode ser consultado na própria documentação.

## 5. De início quanto devo me aprofundar?

No âmbito de segurança web, compreender a linguagem utilizada é essencial para compreender a lógica implementada por trás de um sistema ou desafio. No geral, como a web utiliza o protocolo HTTP como meio de comunicação, uma vez que se compreenda o funcionamento de uma linguagem se torna um pouco mais simples a migração desses conceitos para novas linguagens.

Muitas das falhas que veremos nos websites não necessariamente estarão atreladas à uma linguagem em si mas sim às más decisões tomadas ao construir um determinada funcionalidade. Por outro lado, também haverá vulnerabilidades atreladas ao design de cada linguagem e possuir a capacidade de se adaptar dentre diferentes cenários é algo essencial (Exemplo: pesquise vulnerabilidades de PHP Type Juggling).

Logo, recomendamos que aproveite os desafios mais fáceis do Ping para se acostumar com a sintaxe do PHP e tentar compreender o que ocorre em cada código para então partir para outras linguagens.

*Menção Honrosa:* o Node.js é outra linguagem em ascenção e que já domina uma boa parcela das vagas de web atualmente, porém para evitar delongas deixamos seu estudo ao cargo do leitor.
