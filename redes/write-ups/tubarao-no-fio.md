## Tubarão no Fio

Este é um chall introdutório ao uso da ferramenta Wireshark.

Para resolvê-lo basta abrir o .pcap que está anexado ao chall com o wireshark:

$ wireshark tubarao_no_fio

Após aberto, nota-se que há apenas um pacote capturado e é nele mesmo que a nossa flag está.

O Conteúdo do pacote pode ser visto clicando nele e depois em 'Data'.

O texto que representa a flag está entre os ...'s, porém está encriptogragado em base 64 (que é dado como dica no enunciado). Basta decodificá-lo que teremos a flag.
