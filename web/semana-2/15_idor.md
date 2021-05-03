# Insecure Direct Object Reference \(IDOR\)

_Como última vulnerabilidade apresentada aqui, iremos falar sobre o IDOR, um tipo de falha que, apesar de ser muito simples de corrigir, abre margem para vazamento ou manipulação indevida de dados._

## O que é o IDOR?

O IDOR \(ou _Insecure Direct Object Reference_\) é uma vulnerabilidade que ocorre quando um sistema web utiliza uma forma insegura para referenciar objetos e dados que serão retornados ao usuário ou que serão modificados por ele sem garantir que tal pessoa, ao realizar essas ações, tenha o nível de acesso adequado para isso. Um pouco confuso? Então vamos para alguns exemplos...

## Cenários de exemplos

### Cenário 1 - IDOR via parâmetro GET

Neste cenário, vamos supor que você está navegando por um site como um usuário autenticado e, ao se deparar com a URL, encontra algo da seguinte forma:

```text
https://ga.nesh.com/profile/?userId=1337
```

Como um bom computeiro curioso, você decide mudar o parâmetro `userId` para 1338 e solicitar ao servidor novamente aquela página, ou seja, enviar uma requisição com esse novo parâmetro. Com isso, você ganha acesso aos dados da conta de uma tal de Mariena - com foto de perfil de gatinho.

Este é o exemplo mais simples de **Insecure Direct Object Reference**, pois nesse caso os dados do usuário estão sendo referênciados diretamente pelo seu ID passado via parâmetro sem que haja qualquer outra validação \(como cookies de sessão\).

![Exemplo IDOR](https://i.imgur.com/mD3L5UU.png)

#### Código vulnerável de exemplo:
Esse trecho de código em Python foi retirado de um post no medium [acesse-o aqui](https://medium.com/@aysebilgegunduz/everything-you-need-to-know-about-idor-insecure-direct-object-references-375f83e03a87). 
Esse código é vulnerável pois um usuário pode passar qualquer `‘order_id’` em uma requisição GET que ele receberá as informações da ordem com aquele ID. Não há qualquer verificação que valide se o dono daquela ordem (com o `order_id` passado) é quem está fazendo a requisição, portanto, qualquer pessoa pode acessar qualquer ordem - basta saber o ID dela.

``` python
from flask import request

@app.route(‘/order_details’, methods=[‘GET’])

def order_details():
 order_id = request.args.get(‘order_id’) # aqui o "order_id" passado na requisição é pego
 order = Orders.query.filter_by(id=order_id).first_or_404() # não há qualquer verificação no order_id!
 # As informações são buscadas sem que haja uma validação de quem está pedindo essas informações
 # Não há controle de "ownership" da ordem (só quem fez a ordem deveria poder vê-la)
 return render_template(‘order_details.html’, order=order)
```

### Cenário 2 - IDOR via Cookie

Esse cenário é similiar ao anterior, porém ao invés de utilizar um parâmetro via URL, usa-se algum cookie que atua como identificador na página.

### Cenário 3 - IDOR via "Hidden Input"

Vamos agora para o cenário em que você é um usuário já cadastrado e logado. Enquanto você navega pelo mesmo site do cenário 1, você decide editar alguns dados do seu perfil.

Uma tela de edição de nome, e-mail, endereço etc. é exibida. Então, você decide inspecionar o formulário de edição dos dados e se depara com o seguinte campo no meio do formulário:
``` html
<input type="hidden" name="userId" value="1337"/>
```

Você decide mudar seu nome para `Smith`, mas também altera o valor do campo _hidden_ para 1338, muito curioso para ver o que acontece. Ao enviar o formulário e recarregar a página, nada acontece no seu perfil. Porém, ao voltar à página do cenário 1 e buscar os dados da Mariena \(agora Smith\), vê-se que os dados dela foram alterados no seu lugar.

Este é outro exemplo simples de IDOR. Todavia, nesse caso, a vulnerabilidade foi utilizada não apenas para buscar dados, mas também para modificá-los de maneira indevida. É por isso que tais vulnerabilidades abrem uma grande margem para problemas em uma aplicação real.

## Como descobrir essa vulnerabilidade?

No geral, IDORs podem ser descobertos mais facilmente com o auxílio de scanners automáticos e ferramentas de Proxy \(como o Burp Suite ou o Zap Proxy\), tendo em vista que tais vulnerabilidades geralmente ficam expostas a nível de requisição \(Parâmetros GET, POST, Cookies\).

A princípio, você vai querer testar como a modicação de parâmetros suspeitos \(possivelmente vulneráveis\) afetará o retorno de cada requisição a fim de verificar se há ou não esse tipo de brecha em um website.

## Qual a importância do IDOR?

No caso do IDOR, a gravidade desse tipo de vulnerabilidade é fortemente atrelada a onde ela foi encontrada.

Por exemplo, se encontrassemos essa vulnerabilidade em uma [API](apis_e_rest.md) cuja URL é responsável por retornar os dados dos usuário, contendo `nome, CPF, RG, endereço etc.` e quem sabe até permitindo a manipulação desses dados, haveria uma falha gravíssima no sistema.

Já se a URL retornasse dados que já são públicos por padrão, então a vulnerabilidade seria de gravidade leve ou inexistente uma vez que dados sensíveis não seriam exibidos nem nenhum processo de autenticação seria burlado.

## Para saber mais...

Caso tenha interesse em saber mais sobre IDORs, recomendamos as seguintes referências:

1. [How-To: Find IDOR \(Insecure Direct Object Reference\) Vulnerabilities for large bounty rewards.](https://www.bugcrowd.com/blog/how-to-find-idor-insecure-direct-object-reference-vulnerabilities-for-large-bounty-rewards/)
2. [PortSwigger: IDOR](https://portswigger.net/web-security/access-control/idor)
3. [OWASP: IDOR \(Broken Access Control\)](https://owasp.org/www-chapter-ghana/assets/slides/IDOR.pdf)
4. [Owasp IDOR Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Insecure_Direct_Object_Reference_Prevention_Cheat_Sheet.html)
