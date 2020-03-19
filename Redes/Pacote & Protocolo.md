# Pacote & Protocolo

## PACOTE
Basicamente tudo o que você faz na Internet envolve pacotes. Por exemplo, todas as paginas Web que você acessa chegam como uma série de pacotes e todos os emails que você envia saem como uma série de pacotes.

Na Internet, a rede divide uma mensagem de email em partes com um de terminado tamanho em bytes, esses são os pacotes. Cada pacote carrega as informações que o ajudarão a chegar ao seu destino - o endereço IP do remetente, o endereço IP do destinatário pretendido, algo que informa à rede em quantos pacotes essa mensagem de email foi dividida e o número desse pacote específico.

Os pacotes transportam os dados nos protocolos que a Internet usa: TCP / IP (Transmission Control Protocol / Internet Protocol). Cada pacote contém parte do conteúdo da sua mensagem.

---

## PROTOCOLO

Protocolo de rede é um conjunto de regras utilizadas pelos computadores de uma rede para estabelecer a comunicação entre eles. Assim como na linguagem falada, a qual duas pessoas somente se comunicam se falarem a mesma língua, dois computadores só conseguem se comunicar se utilizarem o mesmo protocolo.
O protocolo, em outros palavras, define como você opera: o que fazer, como fazer e de que maneira o pacote está organizado/especificado.

#### IP 

O IP (Internet Protocol) é responsável pelo roteamentro e entrega dos pacotes de informação. O endereço utilizado  neste processo é o endereço IP, portanto, deve conter a identificação da rede à qual o host pertence ( endereço de rede) e o seu endereço dentro dessa rede (endereço de host).

#### TCP

O protocolo TCP (Transmission Control Protocol) é um serviço de entrega de pacotes que garante a entrega e a integridade do pacote e funciona baseado numa conexão entre dois computadores. Nesse tipo de conexão, ambas as partes entram em acordo sobre a forma de trocarem informações. Quando uma informação é transmitida, mecanismos de verificação de erros e controle de fluxo garantem que a informação seja recebida.

Antes de transmitir os dados, o protocolo TCP estabelece uma conexão entre os computadores, num processo chamado “three-way handshake”.