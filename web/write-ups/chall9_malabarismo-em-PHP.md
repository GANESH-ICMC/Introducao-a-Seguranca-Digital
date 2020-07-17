## Chall 09 - Malabarismo em PHP (made by Guerra - PInG 2020)

**Flag:** `Ganesh{PHP_C0mp@r3_1s_W3!rd}`

Neste chall já iniciamos com o acesso a um arquivo php "vazado" e uma página de login. Fazendo alguns testes de login vemos que a mesma não parece vulnerável a injeções simples de SQL e portanto vamos parar pra analisar o arquivo php.

```:::php
<?php
$admin_user = "pr0_@dm1n";
$admin_pw = clean_hash("0e408306536730731920197920342119");

function clean_hash($hash) {
    return preg_replace("/[^0-9a-f]/", "", $hash);
}

function myhash($passwd) {
    return clean_hash(md5(md5($passwd) . "SALT"));
}
?>
```

Logo de primeira vista já conseguimos analizar que tanto o login quanto a hash da senha do administrador estão contidos no inicio do arquivo.

Vemos também que a aplicação parece estar utilizando uma espécie de md5 encadeada em conjunto com uma string `"SALT"` fixa.

A partir desse ponto, a primeira abordagem que talvez venha na nossa mente seria um **Ataque de Dicionário**, um **Ataque de Força Bruta** ou até verificar se o hash possui uma **Rainbow Table** pré-computada para analisar o hash (não é o caso nesse chall).

É nesse ponto que precisamos dar um passo para trás e tentarmos analisar os dados que foram "vazados" com um pouco de mais cuidado antes de gastarmos nosso tempo e recursos nessas tentativas... vamos?

```:::php
$admin_pw = clean_hash("0e408306536730731920197920342119");
```

Infelizmente, ao trabalhar com senhas no PHP, muitos desenvolvedores inexperientes acabam pecando ao não compreender como funciona as comparações na linguagem e acabam criando possíveis vulnerabilidades.

Uma das falhas que acontecem é a da utilização da **Loose Comparison** para a comparação de hashs de senhas do banco com as vindas do usuário.

```:::php
// Exemplo Loose (==)
if($a == $b) { ... }

// Exemplo Strict (===)
if($a === $b) { ... }
```

Não cabe à esse texto explicar porque o uso da Loose Comparison não é ideal nesse cenário, no momento basta compreender que ao utilizá-la o interpretador irá tentar analisar as variáveis de diferentes maneiras dependendo dos valores que forem utilizados (lembre-se que PHP é uma linguagem não tipada).

Vamos então testar algumas comparações

```:::php
echo ("0e408306536730731920197920342119" == "0e408306536730731920197920342119"); // 1
echo ("0e408306536730731920197920342119" == "abc"); // 0
echo ("0e408306536730731920197920342119" == "0abc"); // 0
echo ("0e408306536730731920197920342119" == "0e408"); // 1
```

Reparou algo estranho na última linha? De fato, o retorno da comparação é 1 mesmo que as strings sejam iguais. Isso se deve ao fato do hash do administrador possuir apenas números e, com muito azar, ter as mesmas características de um número em notação científica. 

Com isso, o interpretador PHP acredita que a string é, na verdade, um número e vai verificar se o segundo item da comparação é também algo numérico. Caso seja, ele irá então performar uma comparação do valor 0^4083... com 0^408.

OU SEJA... para conseguirmos burlar o login, podemos tentar buscar algum valor cuja hash possua a mesma propriedade de ser parecida com um valor numérico e cujo valor seja interpretado como 0.

Para isso, utilizei o seguinte script.

```:::php
$target = "0e408306536730731920197920342119";
$guess  = 1;   
while(true){
    echo $guess."\n";
    if(myhash(strval($guess)) == $target){
        echo myhash($guess)."\n";
        exit(0);
    }
    $guess++;
}
```

E agora você pode se perguntar "Mas o que você fez foi simplesmente uma força bruta, não?". 

De fato, o loop nada mais é do que um ataque offline que testa valores. No entanto, essa técnica apenas foi selecionada devido às propriedades da hash do administrador que eram propicias para este ataque pois caso contrário seria necessário buscar um valor cuja hash fosse 100% compatível com a $target e isso certamente seria muito mais demorado e custoso por parte do atacante.

Após a execução do script e aguardarmos alguns minutos até ele encontrar a colisão necessária, chegamos a valor `62778807` como possível senha e, por fim, com as credenciais em mãos basta utilizá-las para fazer o login e pegar a flag.