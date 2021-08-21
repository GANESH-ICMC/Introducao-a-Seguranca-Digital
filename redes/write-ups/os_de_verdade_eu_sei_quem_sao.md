# Os de verdade eu sei quem são
Conteúdo: wireshark

Inicialmente, temos um pcap com > 300 streams tcp. Para encontrar a flag,
precisamos achar em qual stream ela está sendo transmitida. Para isso,
vamos filtrar os pacotes que temos procurando usando o pedaço que sabemos
da flag.

`Edit -> Find Packet ( Marcando para procurar em Packet Bytes): Ganesh{`

Com isso, chegamos em um pacote com comunicação em texto plano! Basta
selecionar o pacote, clicar com botão direito e `Follow -> Tcp Stream`.

Chegamos na stream 22 onde ocorre a transação da flag em pequenos pedaços,
basta juntar e teremos a flag.

Flag: `Ganesh{k1b0n_4nd_br4ndt_x9s}`
