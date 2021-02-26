# DHCP

O DHCP(Dynamic Host Configuration Protocol) é um protocolo de gerenciamento utilizado para facilitar a configuração de um dispositivo numa rede.
Ao invés de serem necessárias configurações manuais (e que exigem conhecimento da estrutura da rede), a configuração é feita entre o cliente e o **Servidor DHCP**.

## O servidor DHCP

O servidor DHCP é uma máquina que internamente tem os parâmetros da rede, como servidores DNS e uma relação de endereços IP disponíveis.
Em redes domésticas, tipicamente o roteador assume todas as funções possíveis, para reduzir espaço e complicações.
Portanto, o que chamamos de roteador é, ao mesmo tempo: modem(no caso de o dispositivo que se conecta à fibra óptica ou cabo coaxial e ele prover a conexão WAN), roteador, servidor DHCP, entre outros.
No entanto, não há problema nenhum em utilizar um outro servidor DHCP na rede, o que geralmente é necessário quando se tem uma rede mais complexa ou customizada, como é o caso do [Pi-hole](https://pi-hole.net/), que permite ser tanto um servidor DHCP quanto um servidor DNS.

## Processo de configuração.

O processo é realizado através de pacotes UDP. As portas padrão para isso são 67
no servidor e 68 no cliente.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e4/DHCP_session.svg/260px-DHCP_session.svg.png)

1. Discovery: O cliente envia um pacote de descoberta para toda a rede.
2. Offer: Um (ou mais) servidores DHCP oferecem a configuração, consistindo
   tipicamente de endereço IP, servidores DNS, lease time e gateway padrão.
3. Request: O cliente pede a oferta ao servidor DHCP.
4. Acknowledgement: O servidor reconhece a oferta, e envia a mensagem encerrando
   o processo.

