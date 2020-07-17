# Bataterro

Para completar esse desafio, era necessário achar a mensagem certa enviada no
bataterro. Ainda bem que sabemos qual é o hash MD5 dessa mensagem, ou seja,
podemos calcular os hashs de todas as mensagens e ver qual é a certa.

Há muitas maneiras diferentes de resolver esse desafio, eu vou mostrar um
jeito, mas quero saber depois como vocês resolveram!

Para calcular o hash MD5 de um arquivo, existe um programa no terminal,
é o `md5sum`.

Como queremos calcular o md5 de todos os arquivos do diretório,
podemos usar o *wildcard* (`*`), que é um caractere especial que o terminal
interpreta como "coloque aqui todos o nome de todos os arquivos desse
diretório".

Mas nós queremos encontrar só o correto fornecido pelo nosso informante.
Para isso, vamos usar um comando que filtra a entrada com base em um padrão
fornecido. Ele chama `grep` e, quando não informamos um arquivo junto com
o padrão, a leitura é feita na entrada padrão.

Agora o *gran finale* pra juntar todas essas coisas. Vamos usar outro
caractere especial, o *pipe* (`|`), ele redireciona a saída padrão do
comando executado (normalmente a tela do terminal) para outro programa
através da entrada padrão (que normalmente é o teclado).

Juntando tudo, temos:

```
md5sum * | grep e50522e94
```

A saída que você vai ver na tela é o hash do arquivo seguido do nome dele.
Pronto, agora já sabemos qual é a mensagem correta, é só copiar a flag para
o site do CTF. 

## Observação

Quando você baixar o arquivo executável, ele pode não ter permissão de
execução e você não vai conseguir dar `./programa`.

Se esse for seu caso, basta dar o seguinte comando:

```
chmod +x path/to/program
```

Em que `path/to/program` é o caminho do arquivo que você quer dar a
permissão de execução.
