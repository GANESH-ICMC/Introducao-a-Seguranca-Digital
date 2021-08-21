# Calculadora Python
Conteúdos: python, netcat

Ao conectar na porta do chall, recebe-se uma sessão interativa com o
interpretador do Python.  Após testar alguns comandos simples, percebe-se que é
possível importar módulos externos - e executar comandos fora da sessão
interativa que estamos.

Dessa forma, com a payload `exec("import os") or os.system("ls")`, conseguimos
listar os arquivos na pasta que a calculadora está sendo executada, e achamos um
`flag.txt`.

Por fim, usamos a payload `exec("import os") or os.system("cat flag.txt")` e
recebemos por netcat a nossa flag.

Flag: `Ganesh{th3_m1lksh4k3_1s_4_l13}`
