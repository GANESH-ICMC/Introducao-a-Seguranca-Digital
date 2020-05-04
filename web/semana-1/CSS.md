# CSS

CSS (Cascading Style Sheets) é uma linguagem usada para descrever o estilo de uma página HTML, ou seja, de que forma os elementos de um documento serão apresentados/exibidos.
O CSS pode ser usado para alterar fontes, cores, tamanhos, espacamentos, animações etc. de diferentes conteúdos. 

## Tipos e sintaxe
A estilização dos elementos de uma página pdoe ser feita de 3 formas diferentes:
- **Internal CSS**: a estilização fica dentro do documento HTML, no HEAD, entre tags `<style></style>`;
- **External CSS**: há um arquivo externo do tipo `.css` que é importado para o documento HTML através de uma tag `<link>`;
- **Inline CSS**: a descrição do estilo de um elemento é feito através de um parâmetro (style) dentro do próprio elemento (ex.: `<h1 style="color: blue; text-align: center;"> Oi </h1>`).

``` HTML
<!DOCTYPE html>
<html>
<head>
    <!-- CSS externo -->
    <link rel="stylesheet" type="text/css" href="arquivoExterno.css" />  
    
    <style> /* CSS interno */
    /* comentário dentro do CSS é feito assim */
        body {
          background-color: lightblue;
        }

        h1 {
          color: white;
          text-align: center;
        }

        p #idUnico {
          font-family: verdana;
          font-size: 20px;
        }
    </style>
</head>
<body>
    <h1> Olá mundo! </h1>
    <h2 style="color: blue; text-align: center;"> Estilização "inline" </h2>
    <p id="idUnico"> Há estilização nessa tag também :) </p>
</body>
</html>
```
A sintaxe utilizada para declarar um "rule-set" de CSS é a seguinte:
``` HTML
seletor(pode ser a tag , o id ou a classe de um elemento) {
    propriedade: valor;
    propriedade: valor;
}

p {
  color: red;
  text-align: center;
}
```
### Seletor 
O seletor aponta para o elemento que queremos estilizar. Dentro do bloco (delimitado por chaves), podemos escrever quantas declarações quisermos, alterando as propriedades do elemento definido pelo seletor. 

O tipos mais comuns de seletores são:
- **Seletor pelo nome do elemento (tag)**: seleciona o elemento HTML baseado em seu nome (tag), como `<p>`, `<h1>` ou `<img>`.
    - Exemplo:
    ``` HTML
    p {
      text-align: center;
      color: red;
    }
    ```

- **Seletor pelo id do elemento**: seleciona o elemento HTML pelo seu ID (um dos possíveis atributos de um elemento). O ID de um elemento é único. Para selecionar elementos pelo ID usa-se uma hashtag (#) antes do ID.
    - Exemplo:
    ``` HTML
    p #para1 {
      text-align: center;
      color: red;
    }
    ```

- **Seletor pela classe do elemento**: seleciona o elemento HTML por sua classe. A classe é um atributo dos elementos HTML que pode ser repetido. Para selecionar elementos pela classe usa-se um ponto (.) antes do nome da classe.
    - Exemplo:
    ``` HTML
    p .classe1 {
      text-align: center;
      color: red;
    }
    ```
    _O seletor pode vir acompanhado da tag de um elemento específico ou não_.

---
_Uma página interessante baseada em CSS + SASS (outra "stylesheet language") está disponível em "[CSS/SASS based single page application with CSS game AI built in](https://dmytsv.github.io/sass-spa/index.html#about)", associado ao seguinte repositório: https://github.com/dmytsv/sass-spa. Nela, não há código Javascript, somente HTML e CSS/SASS._

---

## Mais informações sobre CSS
- [W3Schools](https://www.w3schools.com/css/default.asp)
- [TutorialsPoint](https://www.tutorialspoint.com/css/index.htm)
- [Codecademy](https://www.codecademy.com/learn/learn-css)
- [Developer Mozilla](https://developer.mozilla.org/en-US/docs/Learn/CSS/First_steps)
- _Novamente, pesquisar por cursos no Youtube ou em sites como Alura, Udemy, Coursera também é muito bom. Só sair procurando que você acha._
