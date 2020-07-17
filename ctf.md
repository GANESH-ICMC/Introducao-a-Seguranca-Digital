# CTF

## O que é CTF? <a id="o-que-e-ctf"></a>

Se você chegou até aqui, é bem provável que já saiba o que é um CTF, mas explicarei de qualquer forma.

CTF, ou _Capture The Flag,_ é uma modalidade de competição, também sendo referido como um jogo, de segurança de informação. Nos CTFs são apresentados diversos desafios relacionados à segurança, cujo objetivo costuma ser explorar um sistema, descobrir uma falha ou algo do gênero.

### Modalidades de CTF <a id="modalidades-de-ctf"></a>

Existem diversos tipos de CTF, o mais comum \(e o que usamos no Ping\), é o **Jeopardy**, onde são apresentados desafios usualmente independentes entre si, onde o usuário completa o desafio, pega a flag, comprovando isso, e submete em uma plataforma, conseguindo pontos, mas essa não é a única modalidade da competição. Outra modalidade comum é o _**Attack & Defense**,_ onde usualmente cada time é "dono" de um sistema, que vem com vulnerabilidades, e o objetivo é consertar essas vulnerabilidades enquanto explora-se as dos outros times, ganhando pontos caso se explore uma falha de outro time e perdendo caso seja a vítima. Isso é mais comum em competições presenciais, por ser necessária toda uma infraestrutura que suporte as interações entre os diferentes times, apesar de não ser algo exclusivo. Ainda, outra modalidade é o _**Boot2Root**_, onde são disponibilizadas máquinas inteiras em que o objetivo do jogador é conseguir acesso e fazer a escalação de privilégios \(ou conseguir acesso root, daí o nome _Boot2Root\)._ Sites comuns dessa modalidade são o _Hackthebox_, que disponibiliza máquinas online para serem invadidas pelos usuários, e o _Vulnhub,_ que disponibiliza máquinas virtuais, as quais o usuário baixa e executa no seu computador. Nesse último caso normalmente não há submissão de flags online, o que faz com que não seja exatamente uma competição.

### Qual a importância do CTF para a segurança da informação? <a id="qual-a-importancia-do-ctf-para-a-seguranca-da-informacao"></a>

CTFs são um ótimo jeito de aprender sobre técnicas novas de segurança. É bem comum se deparar com um cenário que nunca viu antes e passar um bom tempo pesquisando para aprender a resolver o desafio. No fim, mesmo que não consiga, são liberadas as resoluções \(ou _write-ups\)_ pelos próprios jogadores, o que faz com que possa ler sobre e entender o que faltou.

Além disso, empresas de segurança costumam valorizar jogadores de CTF. Por adquirir uma certa experiência com as competições, jogadores conseguem demonstrar as suas habilidades ao resolver os desafios, o que pode ser colocado no currículo e ajudar bastante a conseguir aquela querida vaga de emprego. Fora o fato que várias empresas fazem desafios no estilo CTF para contratação de novos empregados, principalmente em níveis iniciais.

### O que preciso saber para jogar um CTF? <a id="o-que-preciso-saber-para-jogar-um-ctf"></a>

Nada! Existem CTFs de diversos níveis, desde aqueles feitos para escolas de ensino fundamental e médio, para faculdades e outros para os "melhores hackers" do mundo.

Se você está querendo começar nesse mundo e está perdido, a recomendação inicial é pegar algum CTF feito para iniciantes, como por exemplo o _picoCTF_, aberto o ano todo, ou os CTFs feitos para escolas de ensino fundamental/médio, como o _NeverlanCTF_ ou o _Angstrom CTF._

### Onde procurar por CTFs? <a id="onde-procurar-por-ctfs"></a>

A grande plataforma de CTFs mundial é o [ctftime](https://ctftime.org/), que possui listas de CTFs que acontecem quase todo fim de semana \(normalmente múltiplos CTFs por final de semana\), além de ranquear os melhores times e CTFs de acordo com um sistema de votação implementado pelo site \(o que facilita para os usuários reconhecerem quais são os melhores para que possam jogá-los\).

O site também é um bom lugar para procurar por _write-ups,_ dado que eles mesmos disponibilizam uma página para os usuários postarem os seus write-ups de cada CTF feito.

## Categorias comuns de CTFs <a id="categorias-comuns-de-ctfs"></a>

É comum que os desafios de um CTF Jeopardy sejam divididos em categorias, podendo cada desafio ser de uma ou mais. Existem também CTFs "exóticos" que costumam criar desafios de categorias não incluídas aqui, então nem sempre tudo se incluirá aqui.

Em ordem alfabética, as categorias mais comuns de CTF são as seguintes:

### Criptografia <a id="criptografia"></a>

Os desafios de criptografia se dividem em 2 categorias principais.

1 - Abordar os principais ataques conhecidos a criptografias: Usualmente esses desafios envolvem alguma criptografia já publicada, podendo ser amplamente conhecida ou não, e tem alguma falha que deve ser explorada para se obter a flag.

2 - Abordar falha em programação relacionada a criptografias: São dados códigos de uma determinada implementação não segura de alguma criptografia ou _hashing_ e o objetivo de jogador é conseguir entender o que está sendo feito, qual a falha e como quebrar esse código.

A categoria acaba sendo ótima para quem gosta de matemática e de programar soluções criptográficas.

### Engenharia Reversa <a id="engenharia-reversa"></a>

Os desafios giram em torno de entender como um programa funciona, qual a falha nele e como essas vulnerabilidades podem ser exploradas, de forma semelhante ao que se usa para "crackear" um programa ou fazer um hack para um jogo, por exemplo.

A categoria costuma ser muito relacionada a programação e sistemas de baixo nível, o que faz com que os jogadores precisem ter um conhecimento mais elevado sobre arquiteturas de computadores, assembly e programação C.

Os desafios relacionados a engenharia reversa costumam ter como vantagem que ajudam bastante a entender como os programas funcionam nos "bastidores", ou seja, como um sistema operacional interage com um programa e como ele na verdade é interpretado e executado, por exemplo.

### Miscellaneous <a id="miscellaneous"></a>

Miscellaneous, também conhecida como _misc._ é a categoria que usualmente não está relacionada com nenhuma das outras e aborda assuntos diversos, por exemplo conhecimento de softwares de rádio, decodificação de áudios/imagens, linguagens esotéricas, softwares com funcionalidades "fora do comum", e todo o resto que não se encaixa em outras categorias.

Se está realmente lendo, aqui a resposta do desafio do ping, submeta no formato usual: I\_c4n\_r3ad

### Networking/Redes <a id="networking-redes"></a>

Obviamente, envolvem conhecimentos de redes.

Giram em torno de ataques relacionados a redes, como ataques em proxy, análises de tráfego, _bypass_ de _firewall_, análises de protocolos e truques relacionados a ferramentas de redes.

Em diversos CTFs essa categoria acaba entrando como misc, por não se tratar tanto do conhecimento de uma vulnerabilidade específica mas sim o uso do conhecimento de redes para conseguir explorar alguma vulnerabilidade apresentada que não necessariamente é diretamente relacionada a redes.

### Professional Programming Competition \(PPC\) <a id="professional-programming-competition-ppc"></a>

São desafios de programação, semelhantes aos de programação competitiva, sem muita relação com segurança em si. Não é uma categoria tão comum, é bem característica de algumas competições específicas, como o _Hackaflag_, ctf brasileiro, que costuma contar com um desafio dessa categoria a cada edição.

É bom para praticar a criação de scripts e a programação em si, bastante usada em algumas áreas da segurança da informação.

### Pwning/Shellcoding <a id="pwning-shellcoding"></a>

O nome Pwning vem de um trocadilho com o verbo "_Owning_", que é, nesse contexto, "se tornar dono de".

Essa categoria usualmente vem combinada com engenharia reversa, em que é necessário entender uma aplicação e explorar ela para quebrar o sistema e/ou se tornar dono dele \(literalmente tomando posse da máquina\) e executar comandos arbitrários.

É uma categoria boa para quem quer começar a desenvolver os próprios exploits, sendo considerado um "algo a mais" na parte de engenharia reversa.

### Web <a id="web"></a>

É bastante relacionado a falhas de segurança web \(como sql injection, xss, entre outras\). Em CTFs mais voltados para iniciantes costuma ser exploração direta de vulnerabilidades, enquanto nos avançados o foco é maior em _bypass_ de _Web Application Firewalls_ \(WAF\) ou reconhecimento da aplicação para posterior exploração das vulnerabilidades.

Quanto mais se conhece de aplicações web, melhor, dado que novas vulnerabilidades estão sempre a aparecer.

É considerada uma das categorias mais fáceis de se começar, por não depender tanto de conteúdo prévio, apesar de que uma base forte de programação web é bastante útil para a exploração mais elaborada de vulnerabilidades com certo nível de proteção.

Uma das principais vantagens de _web_ é a existência grande de programas de _Bug Bounty_, onde profissionais de segurança podem reportar vulnerabilidades para companhias e receber pagamentos \(_bounties\)_ em troca. Algumas plataformas grandes são o _hackerone_ e _bugcrowd,_ que já pagaram milhões de dólares em bounties.

## Sugestões <a id="sugestoes"></a>

* Se especializar em menos áreas com um time diversificado é uma boa ideia: Segurança é praticamente sem fim, sendo impossível saber tudo de tudo, então o que é aconselhado é escolher algumas áreas e criar uma especialidade nela. Como CTFs usualmente são competições em time um time com vários especialistas em áreas distintas se torna mais forte.
* Ler writeups é uma ótima forma de aprender: Ver como são resolvidos desafios que não foram resolvidos pelo seu time acaba sendo um jeito bom de aprender o que não conseguiu.
* Pessoas diferentes criam soluções diferentes: Diversos desafios não tem uma só solução. O que faz com que seja bom ver resoluções mesmo de desafios que não foram resolvidos.

​

Boa sorte com os desafios :\)

