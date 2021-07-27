# Introdução ao Hardware Hacking

Esse tipo hacking, como o próprio nome já diz, lida com a manipulação e exploração de aparelhos físicos, sistemas embarcados, e tecnologias afins. Dentro desse tema vasto é possível destacar algumas áreas de interesse principais que são tratadas pela frente:

##  - IOT Hacking
O IOT, também conhecido em português como internet das coisas, é um conceito moderno dentro da área da tecnologia que se refere à interconexão digital dos objetos do dia-a-dia com a internet e até mesmo entre si.
O uso de dispositivos desse tipo tem se tornado muito comum nos dias de hoje, entretanto a segurança empregada na fabricação desses dispositivos deixa um pouco a desejar. Um exemplo famoso de exploits que usaram das vulnerabilidades desses aparelhos foi a Mirai Botnet (https://en.wikipedia.org/wiki/Mirai_(malware)).
Alguns dos ataques comuns aos dispositivos IOT incluem, mas não restritos a:

- Explorar pinos de debugging abertos para o usuário, como Interface serial ou JTAG
- Dessoldar chips e extrair a memória ou modificá-la

Em CTFs, esse tipo de hacking tem um enfoque em eletrônica e em challs de forensics que fornecem um dump de memória para ser analisado.

## - Telecomunicação
Essa área estuda a comunicação de dispositivos por ondas eletromagnéticas e transmissão de dados a longa distância, sendo essas possívelmente interceptáveis usando SDRs e técnicas de decodificação de sinais. É importante também o conhecimento de tecnologias novas como RFID, NFC, ZIGBEE e BLE.
Em CTFs os challs envolvem algum tipo de processamento e interpretação de sinais.

## - Eletrônica
Envolve um contato mais direto com circuitos eletrônicos e seu funcionamento, sendo algo bem comum a engenharia reversa e ataques diretamente à chips, PCBs e circuitos integrados na placa principal do aparelho. Um exemplo comum do comprometimento da segurança desses dispositivos são desbloqueios de videogame, e smart cards de TVs a cabo. Outros exemplos de ataque incluem a extração de segredos a partir do consumo de energia e as suas variações (https://en.wikipedia.org/wiki/Power_analysis), ou a pertubação do comportamento de um chip para obter um resultado conveniente ao atacante (https://en.wikipedia.org/wiki/Differential_fault_analysis).
Existem challenges que envolvem a engenharia reversa de projetos em Verilog, VHDL ou netlist.