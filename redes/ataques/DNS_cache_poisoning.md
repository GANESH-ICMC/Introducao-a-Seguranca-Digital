# DNS Cache Poisoning
---

### Relembrando o DNS

Quando a gente acessa, por exemplo, o *https://ganesh.icmc.usp.br/*, o nosso navegador precisa saber, na verdade, o endereço IP do site que estamos tentando acessar. Para isso, ele manda uma requisição para o DNS Server - que faz um match da URL com o IP. Com isso em mãos, o resultado fica guardado temporariamente na DNS Cache do navegador, ou até do sistema operacional, para que o IP daquele domínio fique salvo e possa ser reutilizado.

![](imgs/dns.png)
<span style="color:grey">Resolução do domínio pelo DNS Server</span>

### Fazendo uma resolução DNS manual

O ```dig``` é um comando do Linux utilizado para coletar informações de DNS: ele faz pesquisas de domínio e retorna os IPs dos nomes consultados. 

```bash
spider@ganesh:~$ dig google.com.br

; <<>> DiG 9.11.5-P4-5.1+deb10u3-Debian <<>> google.com.br
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 9066
;; flags: qr rd ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;google.com.br.                 IN      A

;; ANSWER SECTION:
google.com.br.          0       IN      A       216.58.202.195

;; Query time: 18 msec
;; SERVER: 172.17.27.241#53(172.17.27.241)
;; WHEN: Thu Mar 25 15:58:54 -03 2021
;; MSG SIZE  rcvd: 60
```

Observe que no campo ```QUESTION``` está o domínio do qual queremos saber o IP e no campo ```ANSWER``` temos o próprio IP do domínio que estamos consultando.

### Como funciona o DNS Cache Poisoning

**Uma breve intuição de como funciona**

PARABÉNS!! Você acabou de passar na faculdade :). No seu primeiro dia, você pisa no ICMC e precisa ir para a sala 5-001 ter aula de Cálculo. Mas onde ela fica???

Para se achar lá dentro, você abre o Guia dos Bixos e vai rever como funciona a numeração das salas. Chegando lá, você vê tudo vazio e volta pra casa sem entender nada. A questão é: quem te falou que a aula seria nessa sala foi um veterano chatão que só quer ver fogo no parquinho e falou qualquer número.

O DNS Cache Poisoning funciona mais ou menos dessa forma. O atacante (veterano chatão) "envenena" o DNS Cache (nesse caso, a informação que você recebe), podendo redirecionar a vítima para qualquer site que ele quiser, normalmente malicioso.

**Como envenenam o DNS Cache**

Quando um usuário acessa um site, o navegador precisa realizar toda resolução do endereço IP. Ele faz o request, com um Transaction ID específico (um inteiro de 16 bits aleatório) utilizado para validar a resposta daquele request (só é aceita uma resposta com o mesmo ID). Essa requisição chega até o DNS Server que responde com o respectivo endereço IP utilizando o mesmo Transaction ID.

O atacante, então, precisa estabelecer um Man-In-The-Middle (MITM) para que ele possa interceptar os requests de resolução de domínio, verificar o Transaction ID, forjar uma response maliciosa (válida) e enviar para a vítima.

A vítima salva essa resposta em sua DNS Cache, até que ela expire depois de um tempo definido pelo time-to-live. Então, o domínio precisa ser resolvido novamente.

---
### Referências
1. <a href="https://www.youtube.com/watch?v=Rck3BALhI5c">DNS as Fast As Possible</a>
2. <a href="https://www.youtube.com/watch?v=Rck3BALhI5c">O que é envenenamento do cache de DNS?</a>
3. <a href="https://www.youtube.com/watch?v=Rck3BALhI5c">DNS Cache Poisoning - Computerphile</a>