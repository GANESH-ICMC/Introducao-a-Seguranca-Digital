# O Castelo de 10000 Portas

```
Esta porta está trancada, ouça ela para destrancá-la
```

Droga! Bem quando pensamos que conseguiríamos escapar, parece que não vai
ser tão fácil.

Melhor fazer o que o narrador está falando. Para ouvir uma porta, podemos
usar o `netcat` (ou `nc` dependendo da sua distribuição) com a opção `-l`
(de *listen*) para ficar ouvindo.

```
nc -l localhost 7331
```

Agora precisaremos de outra janela para invocar o programa.

```
Parabens, você destrancou a porta
Vá até a porta 1337 e diga o nome da melhor frente do ganesh
```

Gostei do narrador, me faz lembrar dos tempos de Super Mario 64. Precisamos
abrir uma nova janela de terminal para ir até a porta 1337. Aí podemos usar
mais uma vez o *netcat* para iniciar uma conexão com a porta 1337 e é só
digitar o nome da melhor frente do ganesh. Dica: não somos tendenciosos ;).

```
nc localhost 1337
```

## Observação

Quando você baixar o arquivo executável, ele pode não ter permissão de
execução e você não vai conseguir dar `./programa`.

Se esse for seu caso, basta dar o seguinte comando:

```
chmod +x path/to/program
```

Em que `path/to/program` é o caminho do arquivo que você quer dar a
permissão de execução.
