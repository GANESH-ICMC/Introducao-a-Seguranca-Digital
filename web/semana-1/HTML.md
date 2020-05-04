## O que é HTML?
HTML significa Hyper Text Markup Language, ou seja, ele atua como uma linguagem de marcação. Podemos considerá-lo o "esqueleto" de uma página Web, pois ele descreve a estrutura da página.
O HTML é composto por uma série de elementos (representados por tags) que dizem para o browser como o conteúdo deve ser disposto na página.
As tags HTML podem ser aninhadas (uma torna-se filha de outra) e elas não são renderizadas na página.

Um exemplo básico da estruturação de uma página HTML é:
``` HTML
<!DOCTYPE html> <!-- explicita que é um documento HTML -->
<html> <!-- tag raiz de uma página HTML -->
    <head> <!-- tag que contém informações do documento como título, scripts externos/internos e outros metadados -->
        <title> Título da página </title> <!-- título do documento (aparece na aba do browser) -->
    </head> <!-- fechando uma tag: </nome_da_tag> -->
    <body> <!-- contém os elementos visíveis da página -->
        <h1> Cabeçalho da página </h1> <!-- define um "heading" -->
        <p> Parágrafo </p> <!-- (obviamente) representa um parágrafo -->
    </body>
</html> <!-- fim do documento HTML -->
```
_Obs.: <!-- oi --> representa um cometário_

## Tags
A estrutura de uma tag segue o padrão abaixo:
``` HTML
<nome_da_tag> conteúdo dentro da tag </nome_da_tag>
<!-- Em certos casos, a tag pode ser escrita também da seguinte forma: -->
<nome_da_tag/>
```
Nota-se, portanto, que as tags HTML vêm em pares: `<tag>` + `</tag>`, indicando seu início e seu fim, respectivamente. Em alguns casos, elas também podem ser escritas com somente uma tag: `<tag/>`.

### "Principais" tags 
- `<!--...-->`: define um comentário dentro do HTML.
- `<a></a>`: define um hyperlink para outro ponto da página - âncora - ou para um endereço externo.
- `<b></b>`: texto em negrito.
- `<body></body>`: define o corpo do documento HTML.
- `<button></button>`: cria um botão, que pode ser de 3 tipos: button, reset e submit.
- `<div></div>`: define uma seção dentro do documento HTML - é literalmente um "bloco" vazio que pode ser trabalhado individualmente.
- `<footer></footer>`: define o footer da página (parte inferior do documento).
- `<form></form>`: cria um formulário HTML vazio - os campos para inserir dados e os botões devem ser inseridos dentro dele com outras tags.
- `<h1></h1>` até `<h6></h6>`: define textos de cabeçalho ("headings") da página - são como "títulos".
- `<head></head>`: contém informações sobre o documento/página.
- `<header></header>`: define a parte superior da página.
- `<html></html>`: tag raiz de um documento HTML.
- `<i></i>`: texto em itálico.
- `<iframe></iframe>`: define um iframe dentro do documento. Um iframe é uma janela para um documento HTML no meio do corpo de um outro documento (principal).
- `<img></img>`: define uma imagem.
- `<input></input>`: Define algum tipo de controle de entrada do usuário, ou seja, nele o usuário passará algum valor, condição, opção etc. Pode assumir vários tipos, conforme mostrado [aqui](https://www.w3schools.com/tags/att_input_type.asp). 
- `<label></label>`: define um espaço para texto dentro de elemento do tipo `<form>`.
- `<link></link>`: define um link entre o documento atual e algum outro recurso externo (como arquivos de estilo - css). O arquivo externo é "importado" para o documento atual, afetando-o de alguma forma.
- `<meta></meta>`: define metadados de um documento HTML (se quiser saber sobre metadados é só dar um Google).
- `<ol></ol>`: define uma lista ordenada, ou seja, os itens da lista tem numeração (a priori).
- `<p></p>`: define um parágrafo.
- `<script></script>`: define um script que será executado no "client-side" (não é executado no servidor), como um código Javascript por exemplo.
- `<style></style>`	Define informações de estilização da página (CSS). Também pode ser definido em um arquivo externo referenciado por um `<link>`.
- `<table></table>`: define uma tabela (as linhas e colunas são definidas por outras tags).
- `<textarea></textarea>`: define um campo de texto de várias linhas (uma caixa de texto).
- `<title></title>`: define um título para o documento.
- `<ul></ul>`: define uma lista desordenada, ou seja, ela não tem numeração.

Para explicações mais detalhadas sobre as tags, acesse: [Código Fonte](https://www.codigofonte.com.br/artigos/principais-tags-de-html) e [W3Schools](https://www.w3schools.com/tags/ref_byfunc.asp).

## Atributos
Todos os elementos HTML apresentam atributos. Eles normalmente vêm dentro da tag inicial que define o elemento. Os atributos, em geral, tem a forma: `nome_atributo="valor"`.
Esses atributos detalham o elemento, definindo atributos específicos como nome, classe, ID, tamanho, referências externas e internas etc.

Alguns exemplos de tags com atributos são:
``` HTML
<a href="https://theuselessweb.com/"> Clique para acessar um site top. </a>
<img src="test_img.jpg" alt="imagem de teste" />
<p style="color: red; background-color: #FFFFFF"> Olá mundo! </p>
```
- `href="www.google.com"`: href define para onde elemento está "apontando" - um link HTML. Na tag `<a>`, ele é usada para definir para que lugar o link levará o usuário que nele clicar.
- `src="test_img.png"`: define o nome do arquivo que será inserido naquele elemento - normalmente num elemento do tipo `<img>`.
- `style="color: black; text-align: center;"`: especifica o estilo do elemento, ou seja, define características como alinhamento, tamanho, cor, bordas etc. Funciona como um CSS (explicado adiante) dentro do próprio elemento HTML.
- `alt="nome_referencia"`: define um nome que será exibido caso o conteúdo do elemento não possa ser carregado (usado em imagens). Além disso, esse atributo é imporatnte para deficientes visuais navegando pela página, pois esse "alt" é lido para eles pelo browser ou um software de auxílio (como o Chrome Speak).

Além desses, há uma infinidade de atributos para diferentes elementos. Para saber mais sobre os atributos de algum elemento basta pesquisar por sua tag.

### Inspecionando páginas
Para acessar o código-fonte de um site, basta pressionar `ctrl`+`U` (para visualizar o source-code) ou `ctrl`+`shift`+`I` (para entrar no modo de inspeção).

---
### Mais informações sobre HTML aqui!
- [Developer Mozilla](https://developer.mozilla.org/en-US/docs/Web/HTML)
- [W3Schools](https://www.w3schools.com/html/)
- [GeeksForGeeks](https://www.geeksforgeeks.org/html-introduction/)
- _Pesquisar por cursos no Youtube ou em sites como Alura, Udemy, Coursera também é muito bom :)_
