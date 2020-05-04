# API's e Serviços Rest

*Em um mundo cada vez mais conectado, a web já não funciona apenas como um meio de distribuição de conteúdo mas também como provedora de diversos serviços que se tornaram essenciais ao cotidiano. Com a popularização dos dispositivos móveis, é cada vez necessário permitir que um mesmo sistema seja acessível tanto via browser quanto via aplicativos mobile.*

*Tendo em mente a problemática acima, iremos começar conversando sobre assíncronismos, API's,  e padrões REST, mostrando no fim a importância desse conhecimento na área de segurança web.*

## 1. Requisições Assíncronas

Vamos fazer uma viagem no tempo e lembrar um pouco como eram os websites no início dos anos 2000. O protocolo HTTP já existia (em uma versão mais nova) e alguns websites já serviam serviços aos usuários como redes sociais ou webmails.

Naquela época, toda vez que o usuário quisesse visualizar um novo conteúdo ou enviar algum formulário era necessário realizar uma nova requisição e recarregar uma nova página do servidor.

Mas hoje em dia as coisas não funcionam desta maneira. O feed do facebook, por exemplo, não necessita que o usuário realize um refresh em toda a página para carregar novas postagens e isso é possível devido às requisições assíncronas.

O **AJAX** (Asynchronous Javascript and XML) é um recurso da linguagem Javascript que foi adicionado em 2005 e é o responsável pelos comportamentos descritos acima, pois ele permite ao website enviar e receber dados do servidor sem a necessidade de toda a pagina ser recarregada.

```javascript
var xhttp = new XMLHttpRequest();
xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
 document.getElementById("demo").innerHTML = this.responseText;
    }
  };
xhttp.open("GET", "ajax_info.txt", true);
xhttp.send();
```
<p style="text-align: center;">Exemplo AJAX (fonte w3schools)</p>

No exemplo acima, uma requisição GET assíncrona é disparada para buscar um arquivo `ajax_info.txt` do servidor e, caso o servidor ache o arquivo e o retorne com sucesso, carrega seu conteúdo em uma tag cujo atributo é `id="demo"`.


## 2. Application Programming Interface (API)

Caso você já tenha ouvido falar sobre alguns frameworks web como React, Angular.js, Vue.js ou outros, muitos deles são voltados para a criação de sistemas que separam a aplicação que irá consumir os dados (front-end) com a responsável pelo armazenamento e execução das funcionalidades (back-end). Uma das vantagens de fazer essa separação é a de economizar o tempo de desenvolvimento e centralizar o código para futuras manutenções. 

Continuando a usar o Facebook como exemplo, o código central dele seria o responsável por buscar novos feeds, cadastrar uma nova postagem etc, enquanto o aplicativo mobile, browser ou desktop teria apenas a função de garantir a exibição desses dados em uma interface e disparar as requisições assíncronas com o servidor conforme o usuário interage com o sistema.

Alguns sistemas grandes, como o Twitter, possuem API's públicas cujo objetivo é permitir que desenvolvedores possam criar soluções que sejam integradas com seus sistemas, mas no geral em aplicações de médio e pequeno porte as API's são voltadas para o uso interno e exclusivo via algum client mobile ou front-end[.](https://youtu.be/BxV14h0kFs0)

## 3. REST e Serviços RESTful

Ao pesquisar sobre API's e requisições assíncronas, é bastante comum se deparar com os termos REST e RESTful. Apesar de não ser algo tão importante para segurança em si, é interessante saber do que se trata, uma vez que ela permite alguns insights durante um teste de invasão e segurança.

No geral, o REST se trata de um conjunto de boas práticas feitas para garantir que uma API seja estruturada de maneira semântica e organizada.

Esse modelo foi proposto por um dos criadores do protocolo HTTP, Roy Fielding, e é muito utilizado nos dias atuais devido aos fatos que já foram citados no início desse texto.

Um exemplo simples de boa prática seria o uso correto dos métodos HTTP ao enviar uma requisição assíncrona.

```
GET https://meu.website.com/usuarios/13
DELETE https://meu.website.com/usuarios/13
```

No exemplo acima, ambas as requisições são mapeadas para uma mesma url na API. A primeira, no entanto, se trata de um GET e teria o sentido semântico de buscar os dados do usuário 13, enquanto o segundo seria uma ação de exclusão do mesmo.

## 4. XML, JSON, YAML

Quando uma requisição assíncrona é enviada ao servidor, é necessário que os dados sejam retornados de uma maneira estruturada e que possa ser processada pela aplicação do cliente.

Vamos supor, por exemplo, que queremos consumir os dados usados no exemplo anterior:

```
GET https://meu.website.com/usuarios/13
```

Existem diferentes formatos que o servidor pode utilizar para servir esses dados, sendo os mais famosos:

* **XML (Extensible Markup Language):** é uma linguagem de marcação que utiliza de TAG's e se assemelha muito ao HTML. É visualmente menos legível porém permite a criação de atributos dentro das tags.
* **JSON (JavaScript Object Notation):** é uma estrutura baseada em chave-valor bastante utilizada devido à sua legibilidade e clareza para transmitir os dados.
* **YAML (YAML Ain't Markup Language)**

Dando um exemplo do possível retorno da nossa API em JSON e em XML, poderiamos ter algo como

```xml
<usuario role="administrador">
    <id>13</id>
    <nome>João</nome>
    <sobrenome>da Silva</sobrenome>
    <nascimento>10/03/1992</nascimento>
</usuario>
```
<p style="text-align: center;">Exemplo XML</p>

```json
{    
    "usuario": {
        "role":"administrador",
        "id":13,
        "nome":"João",
        "sobrenome":"da Silva",
        "nascimento":"10/03/1992"
    }
}
```
<p style="text-align: center;">Exemplo JSON</p>

Como se pode ver, ambos os casos expressam os dados do mesmo usuário de maneira eficiente, cabendo aos desenvolvedores decidir qual é o melhor formato a ser utilizado no retorno das requisições.


## 5. E qual a importância?

A web está muito mais presente nos sistemas do que muitas pessoas acreditam. Seja um site, um aplicativo mobile ou até mesmo algum [dispositivo IoT](https://pt.wikipedia.org/wiki/Internet_das_coisas), geralmente há uma API sendo consumida por cada um desses itens e é importante que a mesma seja construída de maneira segura pois, caso contrário, sempre haverá alguém disposto a tentar se aproveitar das vulnerabilidades dessa aplicação.

A existência de API's inseguras muitas vezes permite o vazamento de dados sensíveis  e este é o 3º tópico abordado no [OWASP Top 10 ](https://owasp.org/www-project-top-ten/). Um bom exemplo desse tipo de vulnerabilidade por ser visto [neste caso da Nissan](https://www.troyhunt.com/controlling-vehicle-features-of-nissan/) ou nesse da [Sky](https://www.zdnet.com/article/sky-brasil-exposes-data-of-32-million-subscribers/) em que ambos possuiam uma API que permitia o retorno de dados sem qualquer verificação ou senha por parte do solicitante.

