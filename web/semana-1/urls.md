# Entendendo as URLs

URL é a sigla para "Uniform Resource Locator". Cada URL aponta para algum conteúdo único na Web \(como uma página web, um documento CSS, uma imagem etc.\) - desde que a URL seja válida, claro.

## Estrutura das URLs

Toda URL segue a seguinte estrutura: **`Protocolo` + `Domínio` \(+ `Porta`\) + `Caminho até arquivo/recurso`** Ex.: [**https://**](urls.md)[**www.example.com**](urls.md)[**:443**](urls.md)[**/path/to/resource.html**](urls.md)

A porta costuma estar omitida. Nesses casos, o browser considera que serão utilizadas portas padrões de acordo com o tipo de protocolo \(ex.: HTTP: 80, HTTPS: 443\).

Além disso, é possível que a URL também contenha parâmetros que serão passados para o servidor - que seguem a forma: `param1=teste&param2=123` - e tags que identificam certo ponto de um documento HTML - vêm ao final da URL, após `#`. Ex.:  [https://www.example.com:3000/file\_path/resource?user=admin&passwd=1234](urls.md)[\#anchor](urls.md)&lt;/a&gt;

![URL Structure](https://media.gcflearnfree.org/content/55784768317faa316096bef2_06_10_2015/fullurlending_image2.png)

### Protocolo \(Scheme\)

**https://**www.example.com:3000/file\_path/resource?user=admin&passwd=1234\#anchor

Define o tipo de protocolo que será usado na comunicação entre o navegador e o servidor, ou seja, como os dados serão enviados e recebidos. Alguns deles \(os que mais aparecem\) são: 1. **http://** \(Hypertext Transfer Protocol\) 2. **https://** \(Hypertext Transfer Protocol Secure\) 3. **file://** \(indica um arquivo local - no seu HD ou compartilhado em LAN\) 4. **ftp://** \(File Transfer Protocol\)

### Domínio \(Host Name\)

[https://](urls.md)[www.example.com](urls.md)[:3000/file\_path/resource?user=admin&passwd=1234\#anchor](urls.md)

Representa aonde o website pode ser encontrado. Ele pode ser tanto o endereço IP do servidor \(IPv4: 32 bits ou IPv6: 128 bits\) quanto um nome de domínio mais "human-friendly". O Google, por exemplo pode ser acessado por `www.google.com` ou por `216.58.205.46` \(IPv4 do Google\). No primeiro caso, servidores DNS convertem `www.google.com` em `216.58.205.46`, pois só assim ele será encontrado na rede.

### Porta

[https://www.example.com:3000/file\_path/resource?user=admin&passwd=1234\#anchor](urls.md)

É o número da porta do servidor Web. Representa em que porta da máquina está "rodando" o recurso buscado. Uma mesma máquina \(ou servidor\) pode rodar diversos serviços em diferentes portas. Por padrão, a porta do protocolo HTTP é 80 e a do protocolo HTTPS é 443.

### Caminho até o arquivo/recurso

[https://www.example.com:3000](urls.md)[/file\_path/resource](urls.md)[?user=admin&passwd=1234\#anchor](urls.md)

Representa o caminho dentro do servidor até o recurso buscado. Ele começa sempre com um "forward slash" \(`/`\) e pode passar por diversas "pastas" - todas separadas por `/` ao descrever o caminho. Por fim, tem-se o nome do recurso procurado. Por exemplo: em `www.teste.com/2019/usuarios/usuario_1.html`, buscamos a página `usuario_1.html`, que está dentro de `usuarios` que está dentro de `2019`. A palavra "pasta" está entre aspas porque, atualmente, esse caminho **não necessariamente** representa uma sequência de pastas que existe no servidor. Frequentemente, isso é só uma abstração criada para ajudar no server-side.

Obs.: No caso desse caminho ser uma sequência de pastas, as vezes é possível voltar para pastas externas da mesma forma que fazemos em sistemas UNIX ou no próprio Windows:

```text
www.sitebemvulneravelmesmo.com/../../../../../etc/passwd
```

### Parâmetros de requisição \(Query Strings\)

[https://www.example.com:3000/file\_path/resource](urls.md)[?user=admin&passwd=1234](urls.md)[\#anchor](urls.md)

Esses parâmetros são informações que serão passadas ao servidor. Eles vem na forma chave-valor: `nome_parametro=valor`. Caso haja mais de um parâmetro, usa-se como separador o `&`. Na URL, os parâmetros vêm após um ponto de interrogação \(`?`\).

### "Âncoras" \(Fragment identifiers\)

[https://www.example.com:3000/file\_path/resource?user=admin&passwd=1234](urls.md)[\#anchor](urls.md)

Esse elementos da URL é utilizado para indicar um ponto específico na página para o qual o navegador deve ir imediatamente. Esse identificador pode apontar para um elemento no HTML \(como um `<a name="anchor_reference_name">`\) ou para um momento específico de um vídeo/aúdio. Esses identificadores não são enviados para o servidor em requisições.

## URL Encoding

Existem caractéres chamados de reservados, os quais têm algum significado especial nas URLs. A barra \(`/`\), por exemplo, separa elementos na URL \(como o caminho até o recurso buscado\). De forma similar, existem caractéres considerados inseguros, os quais, apesar de não terem significado especial nas URLs, podem significar algo no contexto em que a URL está escrita \(ex.: dentro de um elemento HTML, em trechos de código Javascript/PHP etc.\) - é o caso das aspas duplas \(`"`\). O tratamento incorreto/descuidado desses elementos pode levar a brechas de segurança.

Em ambos os casos, a saída para utilizar esses caractéres sem confundir o browser \(ou às vezes querendo confundí-lo\) é encodá-los. Para isso serve URL Enconding. A barra, por exemplo, torna-se `%2F` e as aspas duplas tornam-se `%22`. Em geral, os caractéres encodados seguem a forma: `%` + `número em hexadecimal` \(dois digitos para UTF-8\).

Apesar de isso ser utilizado para esses caractéres "especiais", muitos outros podem ser encodados, como podemos ver [nessas tabelas](https://www.tutorialspoint.com/html/html_url_encoding.htm).

