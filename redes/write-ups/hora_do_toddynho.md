# Hora do Toddynho
Conteúdos: `port scanning`, `nmap`, `netcat`

Novamente, temos um chall que, ao executar o binário, vemos que o programa está
se comunicando com alguma porta: 

```bash
localhost ouvindo na porta XXXX
Diga-me o nome da melhor frente do Ganesh 
```

Agora, então, precisamos fazer um `port scanning` no localhost:

```
nmap -sU locahost -p 1-65535
```

Percebam que estamos buscando por portas `UDP`. Se procurarmos por portas
`TCP`, não iremos achar nada e, portanto, o próximo tipo a ser checado é o que
de fato estamos procurando.

Com a porta em mãos, basta ouvi-lá com o netcat (`nc -u localhost <PORT>` e
então enviar a resposta **óbvia** da perguntinha: `redes`.

Flag: `Ganesh{m0nic1_c0uldnt_r3fu5e}`
