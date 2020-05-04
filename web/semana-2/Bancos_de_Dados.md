# Bancos de Dados

### 1. O que são?
Bancos de dados são coleções organizadas de informações ou dados estruturados, que tipicamente são armazenados em sistemas computacionais. 
Resumindo, os bancos de dados podem ser entendidos como arquivos de um computador que são criados respeitando certas regras de escrita, de tal forma que seja possível a interpretação desses dados por um outro sistema computacional com essas mesmas regras de escrita, ou até mesmo por um ser humano (quando se utiliza o formato JSON por exemplo).

### 2. Como funcionam?
Geralmente os bancos de dados são gerenciados por um Sistema de Gerenciamento de Banco de Dados (SGBD). Existem alguns exemplo bem conhecidos, como MySQL, PostgreSQL, Oracle, etc. Cada um desses sistemas gerenciadores possui regras específicas de como montar um banco de dados, além de possui alguns recursos próprios, e vantagens uns sobre os outros. A grande maioria desses SGBDs possuem o conceito de usuários, onde cada usuário do sistema só possui acesso a um certo escopo do banco de dados, ou então só tem acesso a um determinado conjunto de comandos, por exemplo.

### 3. SGDB's
Os SGDB's (sistemas de gerenciamento de bancos de dados) são conjuntos de programas que fazem a interface entre os dados armazenados por uma DB e o usuário. Eles permitem o acesso e a manipulação dos dados. Eles visam armazenar organizadamente os dados, além de permitir busca e atualização eficiente dos mesmos.

### 4. Tipos de Bancos de dados
No geral os bancos de dados podem ser divididos em Bancos Relacionais ou Não-Relacionais (ou NOSQL - not only SQL).

### 4.1. Relacionais
Os bancos de dados relacional se refere aos bancos que tem seus dados gravados em forma de tabelas, onde cada coluna da tabela armazena um tipo de dado (strings, inteiros, etc). Nesse tipo de DB, toda a estruturação dos dados no banco devem ser definidas antes do seu uso. Caso uma tabela não seja definida (não possua um esquema definido), não é possível inserir dados nela.  
Alguns exemplos de SGDBs relacionais são:
- [Oracle DB](https://www.oracle.com/br/database/)
- [PostgreSQL](https://www.postgresql.org/)
- [MySQL](https://www.mysql.com/)

Os mais comuns em sistemas web são MySQL e PostgreSQL.

### 4.2. Não Relacionais
Os bancos de dados não relacionais não se tem a necessidade de fazer todo o esquema antes de começar a utilizá-lo, até porque todas as informações serão agrupadas em um registro. Não precisam das declarações dos relacionamentos, dado que tudo fica salvo no próprio registro. Um formato muito usual de armazenamento desse tipo de DB é o JSON, apesar de existirem outros formatos também.  
Alguns NOSQL são estruturados por meio de grafos, outros por meio de documentos, e ainda existem alguns outros tipos.
Exemplos de SGDBs NOSQL:

- [Neo4j](https://neo4j.com/) - graph database
- [MongoDB](https://www.mongodb.com/)

