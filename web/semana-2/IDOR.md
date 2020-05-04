# Insecure Direct Object Reference (IDOR)

*Como nossa última vulnerabilidade iremos citar o IDOR, um tipo de falha que apesar de ser muito simples de ser corrigida abre margem para vazamento ou manipulação indevida de dados.*

## O que é o IDOR?

O IDOR se trata de uma vulnerabilidade que ocorre quando um sistema web utiliza uma forma insegura para referênciar objetos e dados a serem retornados ou modificados sem garantir que a pessoa que esteja solicitando tenha o devido nível de acesso para executar tal ação. Confuso? Então vamos para alguns exemplos a seguir.

## Cenários de exemplos

#### Cenário 1 - IDOR via parâmetro GET

Neste cenário, vamos supor que você está navegando por um site como um usuário autenticado e, ao se deparar com a url, encontra algo da seguinte forma:

```
https://ga.nesh.com/profile/?userId=1337
```

Como um bom computeiro curioso, você decide então mudar o parâmetro e dar um refresh na página e... Feito! Seu perfil magicamente mudou para o de uma tal de Mariena com foto de perfil de gatinho.

Este é o exemplo mais simples de **Insecure Direct Object Reference** pois nesse caso os dados do usuário estão sendo referênciados pelo seu ID diretamente pelo parâmetro sem nenhuma outra validação sendo feita.

![Exemplo IDOR](https://i.imgur.com/mD3L5UU.png)


#### Cenário 2 - IDOR via Cookie

Similiar ao cenário anterior, porém desta vez ao invés de utilizar um parâmetro via URL é utilizado algum cookie que possui algum identificador.

#### Cenário 3 - IDOR via Input Hidden

Vamos agora para o cenário em que você é um usuário já cadastrado e online navegando pelo mesmo site do cenário 1 e decide editar alguns dados do seu perfil.

Uma tela de edição de nome, e-mail, endereço, etc é então carregada e você, por ser muito curioso, decide inspecionar o formulário e se depara com o seguinte campo no meio do formulário.

```html
<input type="hidden" name="userId" value="1337"/>
```

Novamente curioso, você decide mudar seu nome para `Smith` mas altera o valor do campo hidden para 1338. Ao recarregar a página nada acontece ao seu perfil mas ao voltar à página do cenário 1 e buscar os dados da Mariena vemos que os dados dela que foram alterados em seu lugar.

Este é um exemplo simples em que o IDOR foi utilizado não apenas para buscar dados mas também modificá-los de maneira indevida, e é por isso que tais vulnerabilidades abrem uma grande margem para problemas em uma aplicação real.

## Como descobrir

No geral, vulnerabilidades de IDOR podem ser descobertas mais facilmente com o auxílio de ferramentas de Proxy (como o Burp Suite, por exemplo), uma vez que tais vulnerabilidades geralmente ficam expostas à nível de requisição (Parâmetros Get, Post, Cookies).

A princípio, você vai querer testar como a modicação desses parâmetros irá afetar o retorno de cada requisição a fim de verificar se há ou não esse tipo de brecha em um website.

## Qual a importância?

No caso do IDOR, a gravidade desse tipo de vulnerabilidade é fortemente atrelada à onde ela se encontra. 

Por exemplo, se encontrassemos essa vulnerabilidade em uma [API's](APIS_e_Rest.md) cuja URL é responsável por retornar os dados dos usuário contendo `nome, cpf, rg, endereço`, e permitindo ainda a manipulação desses dados, essa seria uma falha gravíssima.

Agora, se a URL for feita para retornar dados que já são públicos por padrão, então não se trata de uma vulnerabilidade uma vez que não quebra nenhum tipo de autorização nem exibe dados sensíveis.

Acabamos esse artigo por aqui, mas caso queira ler mais, recomendamos as seguintes referências:

1. How-To: Find IDOR (Insecure Direct Object Reference) Vulnerabilities for large bounty rewards. (https://www.bugcrowd.com/blog/how-to-find-idor-insecure-direct-object-reference-vulnerabilities-for-large-bounty-rewards/)
2. PortSwigger: IDOR (https://portswigger.net/web-security/access-control/idor)
3. OWASP; IDOR (Broken Access Control) (https://owasp.org/www-chapter-ghana/assets/slides/IDOR.pdf)

