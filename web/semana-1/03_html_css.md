# HTML e CSS:

## HTML:
HTML significa HyperText Markup Language → Não é uma linguagem de programação, mas sim uma linguagem de marcação, utilizada para que navegadores \(chrome, firefox, Explorer, opera\) interpretem suas marcações e transforme na página que será visualizada.

### DOM → Document Object Model

Basicamente a estruturação de documentos Web \(o padrão de formato\). 

Estruturado em 3 partes principais: Doctype, Head, Body

### TERMOS COMUNS EM HTML

- ELEMENTS

Designações. Definem a estrutura e o conteúdo em uma página.

Identificados entre "<" e ">"

Exemplo: <a\>

- TAGS

A utilização dos símbolos "<" e ">" ao redor do elemento criam a tag.

As tags mais comuns são abertas e fechadas em pares.

```html
<div>
Temos acima a abertura da tag div (divisão) e abaixo o fechamento da tag.
</div>
```

- ATRIBUTOS

Propriedades que providenciam maiores informações acerca do elemento.

```html
<a href="http://sitequalquer.com">Clique aqui para acessar um site qualquer</a>
	 |-----> atributo da tag 'a' (âncora)
```

## ESTRUTURAÇÃO DO HTML

```html
<!DOCTYPE html>
<html lang="pt-br">
	<head>
		<meta charset="UTF-8">
		<title> Hello, World!</title>
	</head>
	<body>
		<h1> Hello, my World!</h1>
		<p>Isso vai aparecer no site.</p>
	</body>
</html>
```

## SEMÂNTICA

Prática de fornecer conteúdo, sentido e estrutura, utilizando o elementos ideais para cada caso.

Desconsidera questões visuais, avaliando a estrutura semântica da página por meio de seus elementos.

## ARQUITETURA DE UM HTML

![arch-html](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fc0dcde4c-7f66-4a8d-b820-4b70ae285c88%2Farch-html.png?table=block&id=6a7acac2-819f-4e9a-8684-9af2b8f90dac&width=770&userId=6b906191-3739-42ff-bcbd-5448632e5695&cache=v2)

Outro elemento importante é o nav:

```html
<nav>
Utilizado aqui para navegar entre as informações do site, do servidor, etc.
</nav>
```

---
## CSS:
CSS significa Cascading Style Sheets.

Utilizado em conjunto com as outras linguagens HTML e JS, conferindo um conjunto de estilos como propriedades de cada elemento desejado na página HTML.

## TERMOS COMUNS EM CSS

- SELETOR

Seleciona qual elemento \(s\) está sofrendo alteração em seu estilo.

Pode sofrer especificações, identificando elementos específicos elementos específicos \(id, nomes, classes\).

- PROPRIEDADES

Estilos adicionados ao elemento selecionado 

- VALOR

Comportamento da propriedade

```css
|--> SELETOR
p {
	|--> PROPRIEDADE
	color : orange;
	font-size : 12px;
				  |-->VALOR
}
```

## REFINANDO OS SELETORES

- TYPE

Seleção por tipo do elemento

```css
div {...}
Todo elemento com tag <div>
```

- CLASSE

Selecionamos elementos a partir de sua classe

```css
div.suaclasse { ... }
.suaclase { ... }
```

Exemplo 1: elementos com tag <div> e classe "suaclasse".

Exemplo 2: elementos de qualquer tag, com classe "suaclasse".

OBS .: podemos determinam um objeto no HTML com várias classes, de modo a modularizar a escolha de estilo:

```html
<a class="btn btn-danger">...</a>
<a class="btn btn-success">...</a>
```

Neste caso, temos uma classe comum \(btn\), na qual a fonte de tamanho 16 pixels será padrão. Depois temos 2 especificações de modo a individualizar as outras 2 "sub-classes"

```css
.btn {
  font-size: 16px;
}
.btn-danger {
  background: red;
}
.btn-success {
  background: green;
}
```

- ID

Selecionamos, especificamente, um elemento a partir do seu ID.

```css
div#seuID { ... }
#seuID { ... }
```

Exemplo 1: elemento com tag <div> e id "seuID".

Exemplo 2:  elemento de qualquer tag, com id "seuID".

## REFERENCIANDO O CSS NO HTML

Dentro do HTML

```html
<head>
	<link rel="stylesheet" href="main.css">
</head>
```

---

# Referência:

- [Web Development](https://www.notion.so/WEB-DEVELOPMENT-5ea22e21aa9f47758e9cbecb2711a92c)
