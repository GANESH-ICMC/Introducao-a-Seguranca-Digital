# Directory Traversal

## O que é "Directory traversal"?

Directory traversal é uma vulnerabilidade em que o atacante consegue acesso a arquivos arbitrários do server que está rodando um programa. Então, nesta vulnerabilidade é possível acessar documentos do diretório raíz.

![https://upload.wikimedia.org/wikipedia/commons/d/df/Directory_traversal.png](https://upload.wikimedia.org/wikipedia/commons/d/df/Directory_traversal.png)

## Lendo arquivos com directory traversal:

Para carregar uma imagem em uma página web, pode ser usado HTML:

```html
<img src="loadImage?filename=ganesh.png">
```

É possível ver que há um parâmetro *filename*, que é o nome do documento da imagem que será mostrada na página.

Para acessar a imagem, o programa percorre um caminho até a imagem, um exemplo seria:

```jsx
*/var/www/images/ganesh.png*
```

Caso não haja medidas de defesa contra esta vulnerabilidade, alguém mal intencionado pode requisitar outros arquivos da seguinte forma:

```jsx
[https://icmc.com.br/loadImage?filename=../../../etc/passwd](https://insecure-website.com/loadImage?filename=../../../etc/passwd)
```

Com esta requisição, ao invés de seguir o caminho anterior, a máquina seguirá o seguinte caminho:

```jsx
/var/www/images/../../../etc/passwd
```

Assim como no terminal, \(`../`\) indica que a máquina acessará o diretório pai ao atual, e por ter três \(`../`\), o computador acessará a root, e o que realmente é lido é:

```jsx
/etc/passwd
```

Esta localização acima, em sistemas operacionais baseados em Unix, contém informações privadas do usuário, por isso o exemplo contém estes nomes.

No Windows, pode ser usado tanto \(`../`\) quanto \(`..\`\) e ao invés de `/etc/passwd` seria `\windows\win.ini` 

## Obstáculos contra essa vulnerabilidade

- **Bloqueio de directory traversal sequences**:
    - Para evitar a vulnerabilidade, a página pode bloquear sequencias de \(`../`\), então duas coisas podem ser feitas:
        - Ao invés de usar \(`../`\), usar \(`....//`\), pois é equivalente ao anterior e dependendo do filtro, conseguiria passar por ele \(Ex: [https://icmc.com.br/loadImage?filename=]\(https://insecure-website.com/loadImage?filename=../../../etc/passwd\)....//....//....//etc/passwd \);
        - testar se é possível usar o caminho absoluto, desde a root \(Ex: [https://icmc.com.br/loadImage?filename=]\(https://insecure-website.com/loadImage?filename=../../../etc/passwd\)/etc/passwd\);
- **Bloqueio de chars ou URL-encoding:**

    Alguns caracteres podem ser limitados por filtros, para impedir a exploração desta vulnerabilidade, porém é possível burlar estes filtros com versões codificadas dos caracteres proibidos:

    **Encoding and double encoding:**

    - `%2e%2e%2f` representa `../`;
    - `%2e%2e/` representa `../`;
    - `..%2f` representa `../`;
    - `%2e%2e%5c` representa `..\`;
    - `%2e%2e\` representa `..\`;
    - `..%5c` representa `..\`;
    - `%252e%252e%255c` representa `..\`;
    - `..%255c` representa `..\`;

    Entre outros exemplos;

    **URL encoding:**

    - `..%c0%af` representa `../`;
    - `..%c1%9c` represents `..\`;

    ### Referências:

    [What is directory traversal, and how to prevent it? | Web Security Academy](https://portswigger.net/web-security/file-path-traversal)

    [Path Traversal](https://owasp.org/www-community/attacks/Path_Traversal)
