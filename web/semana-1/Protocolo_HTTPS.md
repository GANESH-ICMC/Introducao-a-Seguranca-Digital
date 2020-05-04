# Procolo HTTPS (Hyper Text Transfer Protocol Secure)

O HTTPS é uma implementação do HTTP com uma camada adicional de segurança: o **protocolo SSL/TLS**. Isso permite que os dados sejam transmitidos por meio de uma conexão **criptografada** e que verifica a autenticidade do servidor e do cliente por meio de **certificados digitais**.

A porta TCP normalmente utilizada para o HTTPS é a 443, enquanto para o HTTP é a porta 80.

O HTTPS serve para criar um canal seguro sobre uma rede insegura - dado que o algoritmo de criptografia utilizado é bom e o certificado do servidor é confiável -, dificultando que pessoas "escutando" na rede (por meio de ataques como _man-in-the-midde_ ou algum tipo de _spoofing_) possam capturar e enteder pacotes que não são deles ou possam fingir ser quem não são.

A "confiança" fornecida pelo HTTPS é baseada em **autoridades de certificação** que vêm pré-instaladas no navegador.

## Protocolo TLS/SSL
O TLS (Transport Layer Security) é o sucesso do SSL (Secure Sockets Layer). Ambos são protocolos de segurança usado em comunicações sobre redes de computadores.

Em se tratando do TLS, o protocolo visa fornecer privacidade e integridade de dados entre duas aplicações que se comuniquem pela internet. Isso ocorre meio da **autenticação do servidor e/ou do cliente** e da **cifragem dos dados** transmitidos.

_Lembrando que isso não torna a conexão necessariamente segura, mas sim menos insegura..._

### Cifragem dos dados

O protocolo TLS usa [criptografia de chave simétrica](https://pt.wikipedia.org/wiki/Algoritmo_de_chave_sim%C3%A9trica) para criptografar os dados transmitidos. As chaves são únicas para cada conexão e trocadas por meio de um Handshake TLS no começo da comunicação (o handshake usa criptografia assimétrica).

#### Handshake TLS
Ao estabelecer uma comunicação cliente-servidor, a primeira operação que ocorre é o Handshake para determinar como o resto da comunicação será feita.

Esse handshake determina qual cifra de encriptação será usada, verifica a identidade/confiabilidade do servidor e, por fim, estabelece uma canal de comunicação criptografado.

O processo de handshake segue o fluxo abaixo:
1. Cliente manda uma mensagem para o servidor pedindo para estabelecer um canal de comunicação criptografado (passa nos _headers_ a lista de cifras a versão do protocolo TLS que ele aceita usar);
2. Servidor responde com a cifra e a versão do TLS que será usada. Ele também envia um certificado digital (que autentica sua confiabilidade e permite a comunicação por meio do HTTPS) junto de sua chave pública (criptografia assimétrica);
3. Cliente verifica o certificado do servidor e extrai sua chave pública. Em seguida, ele usa essa chave para encriptar uma "pre-master key" e a envia para o servidor;
4. Servidor usa sua chave privada para decriptar a "pre-master key";
5. Cliente e servidor usam a "pre-master key" para gerar uma chave secreta compartilhada;
6. Cliente envia uma mensagem criptografada (com a chave secreta compartilhada) e avisa que a partir daquele momento, toda a comunicação será feita dessa forma;
7. Servidor decripta a mensagem e, se tudo ocorrer conforme o esperado, ele envia uma última mensagem criptografada (com a chave secreta compartilhada) avisando que ele foi capaz de descriptografar a mensagem do cliente e que, a partir desse momento, todas as mensagem serão enviadas dessa forma (criptografas com essa chave);
8. Pronto! O resto da comunicação é feita usando a chave secreta compartilhada até o fim da sessão.

- A conexão é confiável porque cada mensagem transmitida inclui uma verificação de integridade de mensagem usando um código de autenticação de mensagem para evitar perda não detectada ou alteração dos dados durante a transmissão.

## Certificados digitais e autoridades cerificadoras

Autoridades certificadoras são companhias que analisam e validam a identidade de sites, emails, pessoas e outras companhias e vinculam-nas a chaves de criptografia por meio de certificados digitais.

Os certificados digitais buscam fornecer:
- Autenticidade, ao oferecer uma credencial para validar a identidade de certa entidade;
- Encriptação de informação, possibilitando comunicações mais seguras em redes inseguras (como a Internet);
- Integridade, assinando pacotes de informação com o certificado a fim de tentar impedir pessoas mal-intecionadas de alterá-los;

Para um certificado ser gerado, o aplicante:
1. Gera um par de chaves de criptografia, uma pública e uma privada;
2. Gera uma requisição de assinatura de certificado (CSR), que contém a recém gerada chave pública e dados como domínio, organização, email, endereço físico etc., e a envia para a autoridade certificadora;
3. A autoridade certificadora verifica as informações da entidade e, se tudo estiver correto, assina a CSR com uma chave privada e devolve-a;
4. Pronto! A entidade que aplicou para um certificado, enfim, tem um :) 

Existem vários tipos de certificados digitais e os mais simples - e piores - são facilmente adquiridos (por [aqui](https://letsencrypt.org/) por exemplo). O que reforça a ideia de que um site utilizar HTTPS, ou seja, ser certificado, não demonstra que ele é 100% confiável.

Para testes locais também é possível usar certificados "self-signed" por meio de certas ferramentas como o [OpenSSL](https://www.openssl.org/).

É possível verificar informações sobre o certificado de um site clicando no cadeado ao lado da URL do website.