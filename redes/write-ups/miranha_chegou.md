# O Miranha chegou
Conteúdos: port scanning, `nmap`, `netcat`

Ao executar o binário, recebemos uma mensagem pela metade - sabemos que o
binário está se comunicando com alguma porta, mas não sabemos qual.

Para encontrar a porta, precisamos fazer port scanning no próprio localhost.
Isso é possível com o nmap, usando `nmap -sS localhost -p 1-65535`. Dessa
forma, vamos olhar todas as portas `tcp` abertas no localhost.

Finalmente, é só abrir o netcat no modo client e receber a flag na porta
achada.

Flag: `Ganesh{sp1d3r_ag4in5t_w3b}`
