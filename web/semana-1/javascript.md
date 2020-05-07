# Introdução ao Javascript

Javascript \(ou ECMAScript\) é uma linguagem de programção muito utilizada no desenvolvimento Web. Com ela, é possível programar o comportamento das páginas HTML - alterar conteúdo e atributos HTML, CSS e mais.

O JavaScript nasceu como uma linguagem voltada para processamento no navegador. Entretanto, com a chegada do Node.js, que permite a execução de Javascript fora do navegador, _back-ends_ de websites e aplicações feitas majoritariamente em Javascript \(como o Discord\) também passaram a utilizar amplamente a linguagem.

Praticamente todas as páginas na internet usam Javascript para fazer operações _client-side_, como verificação de campos, envio de formulários, gerenciamento de cookies, solicitações de informações para o servidor etc.

```markup
<!DOCTYPE html>
<html>
    <body>
        <p id="teste">JavaScript pode mudar conteúdo HTML </p>
        <button type="button" onclick='document.getElementById("teste").innerHTML = "Viu? Modificado!"'> Ao clicar aqui, o texto do parágrafo irá mudar! </button>
    </body>
</html>
```

## Script interno e externo

O código Javascript pode estar dentro ou fora de um documento HTML. Em ambos os casos, o Javascript fica dentro de uma tag `<script></script>`.

* Externo:

  ```markup
  <!DOCTYPE html>
  <html>
    <head>
        <script src="/caminho/ate/arquivo/myScript.js"></script>
        <script src="https://www.sitecomscripttop.com/myScript.js"></script>
    </head>
    <body>
        <h1> Olá </h1>
    </body>
  </html>
  ```

* Interno \(no HEAD\):

  ```markup
  <!DOCTYPE html>
  <html>
    <head>
        <script>
            function myFunction() {
              document.getElementById("para1").innerHTML = "Parágrafo modificado";
            }
        </script>
    </head>
    <body>
        <h1> Página de teste </h1>
        <p id="para1"> Um parágrafo </p>
        <button type="button" onclick="myFunction()"> Mudar parágrafo </button>
    </body>
  </html>
  ```

## Estrutura e sintaxe do JS

### Variáveis e constantes:

**Variáveis** são usadas para armazenar dados que podem ser modificados a qualquer momento. Em JS, as variáveis são declaradas com `var` ou `let`e elas podem ser praticamente qualquer coisa: números, palavras, funções etc.

Ao usar `var`, se a variável for declarada fora de uma função, ela poderá ser acessada de qualquer ponto do código \(dentro e fora de funções\), ou seja, ela é de _scope_ global. Caso a variável seja declarada dentro de uma função, ela só poderá ser acessada de dentro dessa função. Esse tipo de variável pode ser redeclarado - além de atualizado - no meio do código.

```javascript
    var msg_introdutoria = 0.5; // declara a variável e atribui um real (float) a ela
    var msg_introdutoria = "Olá mundo!"; // redeclara a variável e atribui uma string a ela
    var contador = 0; // declara uma variável e atribui um inteiro (int) a ela

    console.log(msg_introdutoria); // exibirá "Olá mundo!"

    if (contador <= 0) {
        // bloco de código do IF
        var msg_introdutoria = "Oi mundo!";  // atualiza o valor da variável
    }

    console.log(msg_introdutoria) // exibirá "Oi mundo!"
```

Já ao usar `let`, a variável sempre será _block scoped_, ou seja, ela está limitada ao bloco de código em que foi declarada \(e aos blocos mais internos a ela\). Um bloco é definido por chaves \(`fora do bloco { dentro do bloco } fora do bloco`\). Além disso, variáveis declaradas com _let_ não podem ser redeclaradas \(mas podem ser atualizadas\).

```javascript
    let msg_introdutoria = "Olá mundo!";
    let contador = 4;

   if (contador > 3) {
        let msg_introdutoria_2 = "Oi mundo!";

        console.log(msg_introdutoria); // "Olá mundo!"
        console.log(msg_introdutoria_2); // "Oi mundo!"
    }
    console.log(msg_introdutoria); // "Olá mundo!"
    console.log(msg_introdutoria_2); // msg_introdutoria_2 não está definida
```

**Constantes** também são usadas para armazenar dados, mas elas não podem ser modificadas durante a execução do programa. Uma vez declaradas com certo valor, elas não podem ser alteradas. Além disso, constantes são _block scoped_ e não podem ser redeclaradas \(nem alteradas - como foi dito logo acima\).

```javascript
    const saudacao = "Olá!";
    saudacao = "Oi!"; // Erro: (re)atribuição à constante

    // OBS.: se a constante for um objeto é possível fazer certas alterações:
    const saudacao2 = { // objeto com mais de um campo
        msg : "Olá!",
        countador : 3
    };

    saudacao2.msg = "Oi!"; // Isso é permitido! O campo msg é atualizado!

    const saudacao2 = {
        teste : "Aaaa",
        nome : "Marcelo Batata"
    }; // isso não é permitido! ERRO!!
```

### Operadores e comparadores:

* **Operadores aritméticos**: são os operadores que realizam operações aritméticas em números \(e variáveis com valores numéricos\). Entretanto, em certos casos, é possível usar esses operadores com outros tipos de variáveis, como no caso de "soma" de strings \(`"Nome " + "Sobrenome" -> "Nome Sobrenome"`\).

| Operador aritmético | Operação | Exemplo |
| :---: | :---: | :---: |
| + | Adição | `let x = 1 + 2; // x = 3` |
| - | Subtração | `let x = 5 - 7; // x = -2` |
| \* | Multiplicação | `let x = 3 * 5.2; // x = 15.6` |
| / | Divisão | `let x = 6 / 2; // x = 3` |
| \*\* | Pontenciação | `let x = 2**3; // x = 8` |
| % | Módulo \(resto\) | `let x = 10 % 3; // x = 1` |
| ++ | Incremento \(+1\) | `let x = 1; x++; // x = 2` |
| -- | Decremento \(-1\) | `let x = 1/ x--; // x = 0` |

* **Comparadores**:

| Comparador | Compração | Exemplo |
| :---: | :---: | :---: |
| == | Igual a \(em valor\) | `1 == 1.0 (true)` |
| === | Igual a \(em valor e tipo\) | `1 === 1.0 (false)` |
| != | Diferente de \("não igual"\) | `1 != 1.0 (false)` |
| !=== | Diferente de \("não igual" em valor e tipo\) | `1 !== 1.0 (true)` |
| &gt; | Maior que | `10 > 2 (true)` |
| &lt; | Menor que | `1 < 2 (true)` |
| &gt;= | Maior ou igual que | `5 >= 5 (true)` |
| &lt;= | Menor ou igual que | `4 <= 3 (false)` |

* Ainda há os **comparadores lógicos**. São eles:
  * `&&` \(and\): `(2 < 10 && 0 > 1)` --&gt; verdade **E** mentira é **mentira** 
  * `||` \(or\): `(5 == 5 || 3 == 5)` --&gt; verdade **OU** mentira é **verdade**    
  * `!` \(not\): `!(1 == 1)` --&gt; **NÃO** verdade é **mentira**
* E, por último, também é importante conhecer o **comparador ternário**, que atua como um comparador IF:

  \`\`\` javascript // Comparador ternário: variablename = \(condition\) ? value1 : value2; var voteable = \(age &lt; 18\) ? "Too young" : "Old enough";

// Isso é igual a:

voteable = \(\)\(age\) =&gt; { if \(age &lt; 18\) { return "Too young"; } else { return "Old enough"; } }

```text
### Tipos de dados:
De forma simplificada, podemos resumir os tipos de dados em primitivos e complexos. Os **tipos primitivos** são: *string* (basicamente, caractéres e palavras - sempre entre aspas), *boolean* (verdadeiro ou falso), *number* (número inteiro, real) e *undefined* (variáveis sem valor definido). Já os **tipos complexos** são: *object* (listas, JSON, XML, vetores, dados inexistentes etc.) e *function* (funções).
``` javascript
typeof "" // String
typeof "Marcelo Batata" // String

typeof 3 // Number
typeof 3.14 // Number
typeof (3 + 4) // Number

var x; // Declarada, mas sem valor atribuído
typeof x // Undefined

typeof true // Boolean
typeof false // Boolean

typeof { name:'John', age:34 } // Object
typeof [1, 2, 3, 4] // Object
typeof null // Object

typeof function myFunc(){ console.log("Testing..."); } // Function
```

Obs.: Ainda há **null**, que é similar ao _undefined_, mas seu tipo é objeto, Por mais contraditório que isso seja, esse objeto _null_ represta um dado que não existe.

```javascript
typeof undefined // retorna undefined
typeof null // retorna object

null === undefined // retorna false
null == undefined // retorna true (loose comparison)
```

### Funções:

Funções são blocos de códigos que executam uma tarefa. Algo deve invocar a função para ela ser executada \(ela precisa de algum "gatilho", nem que seja outra parte do código "chamando" ela - ou até ela própria se invocando\). Ou seja, a execução do código dentro da função ocorre quando:

* Um evento ocorre \(ex.: usuário pressiona um botão\);
* A função é invocada por outro trecho de código Javascript;
* A própria função invoca-se e é executada automaticamente.

#### Sintaxe:

```javascript
function nome_funcao(parametro1, parametro2, parametro3) {
  // código a ser executado quando a função for chamada
  console.log("A função foi executada!");

  return {"mensagem" : "OK"};
}

// --- Outra alternativa, em certos casos, é a "Arrow Function": ---
// O trecho abaixo pode ser escrito de forma mais concisa
var multiplicacao = function(x, y) {
  return x * y;
};
// Arrow function: (param1, param2, paramN) => { expressão / bloco da função }
const multiplicacao2 = (x, y) => { return x * y };
```

### Exemplo comentado:

Para ajudar no entendimento da sintaxe da linguagem é bom analisar um trecho de código comentado: _Obs.: `//` representa um comentário._

```javascript
// o bloco de código da função 'requisitarDadosPessoais()' começa aqui e quando ela for chamada, tudo que está aqui dentro será executado (linha por linha, de cima para baixo)
// userID é um parâmetro que deve ser passado ao chamar essa função. userId funciona como uma varíavel
async function requisitarDadosPessoais(userID) { 
    // a variável 'dados' recebe o retorno da função 'httprequest', ou seja, o que essa função trouxer como resposta sera guardado em 'dados'
    var dados = await httprequest(`http://site-exemplo.com/usuarios/${userID}`); // a função é executada e em seguida sua resposta é armazenada em 'dados'

    if (!dados) { // se 'dados' estiver vazio (for nulo), a condição é verdade e o código dentro desse bloco (delimitado por chaves) é executado
        alert(`O usuário ${userID} não existe!`); // emite um alerta na tela avisando que o usuário com o nome armazenado em 'userID' não existe
        return null; // a função 'requisitarDadosPessoais()' termina aqui e retorna o valor 'null' (nulo)
    } // fim do bloco de código referente ao 'if'

    if (dados.sucesso == true){ // 'dados' é um objeto com vários campos (atua como um JSON) e ele tem um parâmetro 'sucesso'. Se 'sucesso' for igual 'true', a condição é satisfeita e o código dentro desse bloco é executado
        alert(`Bem vindo, ${dados.nome}, faz ${dados.tempoDesdeUltimoLogin} horas que você conectou pela última vez`); // emite uma mensagem de boas-vindas na tela, fazendo uso de outros parâmetros dentro de 'dados' ('nome' e 'tempoDesdeUltimoLogin')
        redirecionar_usuario('http://site-exemplo.com/profile/${userID}', dados.cookies); // Executado uma função chamada 'redirecionar_usuario()' que está em outra parte do arquivo Javascript
    } // fim do bloco de código referente ao 'if'
    else { // caso a condição nos parênteses do 'if' não seja satisfeita, esse bloco de código é executado
        alert(`${dados.nome}, a senha digitada está incorreta`); // emite um alerta na tela, avisando que a senha referente ao usuário digitado está incorreta
    } // fim do bloco de código referente ao 'else'

    return dados; // caso a função não tenha terminado antes, ela termina aqui, retornando o conteúdo de 'dados' (variável) para onde foi feita a chamada à essa função
}
```

