# Command Injection

## Como surge essa vulnerabilidade?

Por mais que não pareça, muitas vezes as aplicações precisam executar comandos do sistema. Alguns dos motivos dessa necessidade estão em: execução de código em outra linguagem de programação, acessar o sistema de arquivos do computador, se conectar com outro servidor, entre outros.  
Então linguagens como o PHP, por exemplo, possuem comandos que permitem ao usuário essa interação com o Shell da máquina. Porém, mesmo sendo muito útil essa funcionalidade pode trazer muitos riscos para a aplicação se utilizada incorretamente.

## O que é Command Injection?

Command Injection, ou Shell Injection é uma vulnerabilidade de sistemas Web que permite que o usuário execute comandos arbitrários no servidor onde o sistema web está hospedado. Isso é agravado porque geralmente as aplicações web rodam no servidor com privilégios do servidor \(por exemplo apache, ou tomcat\). Então, para o sistema é como se o apache estivesse executando algum comando que está dentro do seu escopo, o que faz com que o SO não bloqueie a execução do comando.  
Isso faz com que essa falha de segurança seja extremamente sensível, pois o atacante pode conseguir acesso completo do sistema por meio dessa falha \(o famoso _shell reverso_\).

## Exemplo

Um exemplo de aplicação desse comando é o seguinte código em PHP:

```php
<?php
    print("Please specify the name of the file to delete");
    print("<p>");
    $file=$_GET['filename'];
    system("rm $file");
?>
```

Ele basicamente pega o que é enviado no parâmetro "filename" do método GET e utiliza para rodar um comando no sistema. Porém não há nenhum tratamento nesse comando, o que faz com que o atacante possa inserir comandos juntos ao comando já existente. Por exemplo, ao fazer a seguinte requisição:

```text
http://127.0.0.1/delete.php?filename=bob.txt;id
```

Ao receber essa requisição o servidor vai pegar toda a string descrita no parâmetro "filename" e colocar na execução do comando, após o "rm". O comando que será executado fica da seguinte forma:

```text
rm bob.txt;id
```

Quando um separador como ";", "\|" ou "&&", por exemplo, é utilizado no shell, de maneira simplificada o que acontece é: ele trata o que vem antes do separador como um comando e o que vem depois como outro. Isso faz com que essa requisição HTTP possua a seguinte resposta do servidor:

```text
Please specify the name of the file to delete

uid=33(www-data) gid=33(www-data) groups=33(www-data)
```

Ele retorna o que script php mandou imprimir, além do retorno da execução do comando injetado \(no caso "id"\).

## Como evitar?

A solução para esse tipo de vulnerabilidade é bem simples: basta "limpar" \(do inglês _sanitize_\) as entradas do usuário, não permitindo que esses separadores ou executores de código sejam utilizados pelo usuário \($\(\), ;, \|, &&, etc\).

