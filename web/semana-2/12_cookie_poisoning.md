# Cookie Poisoning:

## O que é cookie poisoning
Cookie poisoning é uma estratégia de ataque onde o atacante altera, forja, sequestra ou podemos dizer "envenena" um cookie válido e manda-o de volta para o servidor para poder roubar dados, evitar a segurança ou ambos.

## O por que o cookie poisoning é importante?
Cookie poisoning é relativamente fácil para atacantes os quais podem usar um cookie envenenado para roubar a identidade do usuário para fraude ou para ganhar acesso não autorizado ao servidor para futuras explorações.

## Como cookie poisoning funciona?
Cookies \(ou outros tokens de sessão\) não gerados ou transmitidos com segurança são vulneráveis a sequestro ou envenenamento. Cross-site scripting \(XSS\) é uma maneira comum de roubar cookies, mas vários métodos, incluindo detecção de pacotes e força bruta, podem ser usados para obter acesso não autorizado aos cookies. E como o envenenamento de cookies é um termo geral para inúmeras atividades maliciosas que envolvem cookies, um exploit de envenenamento de cookies também pode ser descrito com precisão como um ataque man-in-the-middle ou sequestro de sessão, fixação ou falsificação, entre outros termos.

## Diferentes tipos de cookie poisoning:
* ### Cookie poisoning pelo lado do cliente:
    A verdadeira forma de envenenamento de cookies é bastante rara porque os programadores de aplicativos hoje em dia raramente cometem esses erros básicos. Um ataque de envenenamento de cookie é iniciado por um usuário que manipula o conteúdo do cookie para sua vantagem antes que o cookie seja enviado ao servidor da web. Tudo o que o usuário precisa fazer é pressionar F12 e usar a GUI do navegador do usuário para modificar os cookies. Um usuário avançado pode, é claro, também criar uma solicitação HTTP adequada do zero, de acordo com suas necessidades.
    Por exemplo, um aplicativo web mal escrito pode armazenar o nome de usuário do usuário atualmente conectado em um cookie. Em seguida, o aplicativo pode usar o conteúdo do cookie para verificar qual usuário está executando uma determinada operação. Nesse caso, o usuário pode alterar o conteúdo do cookie para se passar por outra pessoa, por exemplo o adminstrador da aplicação.
* ### Man-in-the-middle Cookie Hijack:
    O termo envenenamento de cookies também é frequentemente usado para descrever o sequestro de cookies, que é uma forma de ataque man-in-the-middle \(MITM\). Nesse caso, o invasor usa alguma outra técnica de ataque para espionar a comunicação entre o navegador Web e o servidor Web e obtém acesso ao conteúdo do cookie que está sendo transmitido.
    Em um ataque MITM típico, o invasor não apenas escuta a comunicação, mas pode manipulá-la. Eles podem roubar informações confidenciais contidas no cookie transmitido ou modificá-las em seu próprio benefício.
* ### Cookie Hijacking using Buffer Overflow:
    O conteúdo dos cookies também pode ser acessado por terceiros não autorizados usando ataques de buffer overflow. Se o servidor Web executar um software vulnerável a ataques de buffer overflow, o invasor poderá ler a memória do servidor, que geralmente contém as informações de cookies mais recentes.
    No entanto, esse tipo de ataque é muito raro. Poucos aplicativos instalados em servidores web são vulneráveis a buffer overflow e, mesmo que sejam, deve ser uma rara coincidência que o invasor consiga encontrar e reconhecer cookies para um determinado site. Observe que erros de buffer overflow quase nunca acontecem em aplicativos da web porque as linguagens mais populares usadas para criar aplicativos da web, como PHP, Java e JavaScript, são imunes a buffer overflow.
* ### Cross-site Scripting and Cookie Hijacking:
    Os ataques de script entre sites \(XSS\) são uma maneira excelente de acessar o conteúdo do cookie, incluindo identificadores de sessão. Se o aplicativo da web for vulnerável até mesmo a XSS refletido simples, tudo o que o invasor precisa para receber o identificador de sessão é enganar a vítima para que clique em um link fornecido.
    Assim que a vítima clica no link, o conteúdo do cookie de sessão é enviado em uma solicitação ao site do invasor. No caso mais simples, o invasor precisa apenas analisar os logs do servidor da web para ver o conteúdo do cookie da sessão.

## Como se prevenir de cookie poisoning?
* ### F5 Advanced WAF \(Web Application Firewall\):
    O F5 Advanced WAF usa inspeção de dados full proxy, análise de comportamento e aprendizado de máquina para fornecer segurança de aplicativo de alto nível, incluindo gerenciamento de sessão sofisticado e criptografia de cookies SSL / TLS. Ao interceptar todo o tráfego de e para o servidor da web, ele pode descriptografar esse tráfego e compará-lo com as informações enviadas pelo servidor para evitar que cookies alterados cheguem ao servidor ou aplicativo.
    Caso queira um video que explique melhor sobre o F5 Advanced WAF veja [esse video](https://www.youtube.com/watch?v=HBbDKBV4QW0&ab_channel=F5DevCentral).
    
* Use apenas comunicação HTTPS, por exemplo, impondo HSTS. Isso reduz muito a ameaça de espionagem no conteúdo do cookie.
    
* Faça a varredura regularmente de seus aplicativos da web usando um scanner de vulnerabilidade para encontrar e eliminar todas as vulnerabilidades de segurança que podem levar ao envenenamento de cookies.
    
* Não use seus próprios geradores para criar identificadores de sessão. Confie no seu software de servidor da web para fazer isso por você.
    
* Nunca confie nos dados calculados do lado do cliente porque podem ser facilmente manipulados.
    
## Referências:
- https://www.f5.com/services/resources/glossary/cookie-poisoning
- https://www.acunetix.com/blog/web-security-zone/what-is-cookie-poisoning/
