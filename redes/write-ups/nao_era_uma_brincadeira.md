# Não era uma brincadeira
Conteúdos: wireshark

Esse chall nos dá um `.pcap` para analizar e encontrar a flag. Começamos
analizando as diferentes streams presentes, pela aba `Analyze -> Follow ->
UDP`. Vemos que, das diversas streams UDP presentes, temos algumas em http.

Como o `.pcap` tem um bom tamanho, é possível que algum tipo de arquivo tenha
sido captado. Podemos usar a aba `File -> Export Objects -> HTTP`.

Um dos arquivos encontrados pelo Wireshark é o `hiro.jpg`. Ao abri-lo, obtemos
a flag.

Flag: `Ganesh{h1r0_1s_0ur_le4d3r}`
