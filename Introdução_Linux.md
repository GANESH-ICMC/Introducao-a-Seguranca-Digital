##O que é um sistema operacional?
O sistema operacional do seu computador é o software encarregado de realizar a comunicação entre o  hardware e os demais softwares a serem executados no seu pc. Sua função é administrar e gerenciar os recursos do sistema, desde os elementos de baixo nível (os componentes de hardware como dri) até os de alto nível (programas de terceiros e interface gráfica), fornecendo uma **interface entre o usúario e hardware.**

Entre as diversas funções do sistema operacional, poedmos citar:
1. Gerenciamento dos processos (execução de programas);
2. Gerenciamento da memória;
3. Gerenciamento de recursos;
4. Entrada/Saída de dados;
5. Sistema de arquivos;
6. Definir interface com o usúario;
7. Tratamento de erros;

#### Interfaces de uso:
* Interface Gráfica (GUI)
* Interface de terminal (CLI)
* Interface textual
* Interface de voz (VUI)

#### Sistemas de Arquivos
[SistemaArquivosLinux]: https://www.rs-online.com/designspark/rel-assets/dsauto/temp/uploaded/linux-filesystem.png?w=815 "Sistema de Arquivos Linux"
[Introdução ao Sistema de Arquivos do Linux](https://www.rs-online.com/designspark/an-intro-to-linux-file-system-management)

[Gnu/LinuxDistros]: linux_distros "Distribuições GNU/Linux"
[Sistemas Operacionais: Crash Course Computer Science (EN)](https://youtu.be/26QPDBe-NB8)
[A mente por trás do Linux | Palestra com Linus Torvalds (EN)](https://youtu.be/o8NPllzkFhE)

## Utilizando a linha de comando (CLI)	
Todos os comandos estão no formato `comando [-flags] <argumentos>`

### Comandos para Ajuda e Documentação
* `man <comando>`: Manual com informações acerca de todos os comandos
* `info`: Outra ferramenta de documentação
* `uname`: Mostra informações do sistema

### Comandos de Controle e Acesso
* `exit`: Terminar a sessão, ou seja, a shell
* `logout`: Deslogar/terminar sessão atual
* `passwd`: Mudar a senha do usuário logado

### Comandos para Gestão de Arquivos e Diretórios
* `ls [-l] [-a] <diretorio>`: Listar o conteúdo de um diretório, a flag `-l` exibe o resultado em forma de lista e a `-a` exibe também o conteúdo oculto
* `cd <diretorio>`: Mudar diretório atual
	* `/`: Vai para diretório Root
	* `~`: Vai para diretóorio Home
	* `..`: Vai para diretório anterior
* `pwd`: Mostra nome do diretório atual
* `touch <arquivo>`: Cria arquivo
* `cp <arquivo1> <arquivo2>`: Copia conteúdo do aqrquivo1 para arquivo2
	* Se o arquivo2 já existir, ele é sobrescrito
* `cat <arquivo>`: Mostra o conteúdo de um arquivo e pode ser usado também para concatenar arquivos, como por exemmplo utilizando "a.txt b.txt > c.txt" para juntar o conteúdo dos aquivos `a.txt` e `b.txt` em um único chamado `c.txt`
* `mv`: Move ou renomeia arquivos ou diretórios
* `mkdir <diretorio>`: Cria um diretório
* `rm [-r|-R]`: Remove um arquivo
* `rmdir <diretorio>`: Remove um diretório
* `chmod`: Muda permissões de arquivo ou diretório
	user:group:everyone
	4	:	read (r)
	2	:	write (w)
	1	:	execute (x)
* `file`: Determina tipo de arquivo
* `grep <'pesquisa'> <arquivo>`: Procura por um padrão em um arquivo
* `strings`: Retorna as strings identificadas em um arquivo
* `unzip`: Ferramenta para descompactar arquivos zipados

### Comandos de Edição de Texto
* `emacs`: Editor de texto
* `nano`: Editor de texto
* `vim`: Editor de texto do terminal

### Comandos de Rede
* `ping`: Pingar um determinado host ou verificar existência de conexão; envia pacotes icmp para host específicado e mede tempo de resposta, entre outras coisas  
* `ifconfig`: Configurar a interface de uma rede; utilizado para visualizar os ips da nossa máquina
* `ssh`: Cria sessão segura (Secure Shell) e permite-nos conectar num servidor remoto através do protocolo ssh
* `netcat`: Criar conexão TCP/UDP
* `netstat`: Mostra o estado da rede
* `nmap`: Ferramenta de port-scan para visualização de portas abertas num dado host

### Processos:
* `ps`: Mostra os processos em execução
* `pstree`: Mostra processos atuais em forma de árvore
* `kill`: Mata um processo, como por exemplo `kill -9 100`

### Comandos de Informação de Estado
* `date`: Exibe data e hora
* `ps`: Lista os processos em execução
* `pwd`: Mostra o caminho inteiro do diretório atual, ou seja, o pathname
* `whoami`: Diz quem é o dono da shell
* `who`: Mostra quem está logado no sistema 

[Cheatsheet de Comandos Linux](https://cheatography.com/davechild/cheat-sheets/linux-command-line/pdf/)
[Bandit - OverTheWire](https://overthewire.org/wargames/bandit/)
[CmdChallenge](https://cmdchallenge.com/)
[Tutorial Vim](https://www.openvim.com/tutorial.html)
