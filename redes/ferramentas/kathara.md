# Kathará

O [Kathará](https://www.kathara.org) é uma ferramenta que permite a simulação
de redes, máquinas e topologias inteiras através do docker. Ele é o sucessor
do [netkit](https://www.netkit.org) e permite que os laboratórios do netkit
sejam utilizados pelo kathará, somente em alguns casos específicos é necessário
adaptação.

## Instalação

### Debian e derivados

Para instalação no Debian, Ubuntu, Linux Mint, PopOS, Kali, etc, basta seguir
o [tutorial](https://github.com/KatharaFramework/Kathara/wiki/Linux) disponível
na [wiki do kathara](https://github.com/KatharaFramework/Kathara/wiki).
Basicamente será necessário instalar o `docker` e adicionar o repositório
(PPA) do kathará. Ambas as instalações podem ser feitas pelo `apt`.

### Arch e derivados

Para instalar no Arch e Manjaro, é necessário satisfazer as dependências do
kathará e baixar o arquivo *zip* do [repositório no github](https://github.com/KatharaFramework/Kathara).

As dependências principais são python 3, normalmente já instalado por padrão,
e o docker, que deve ser instalado com o `pacman`. A instalação do docker é
feita por:

```
sudo pacman -S docker
```

E a checagem do Python 3 pode ser feita por:

```
python3 --version
```

Se ele estiver instalado, irá imprimir na tela a versão.

Em seguida, você deve baixar o zip do [repositório](https://github.com/KatharaFramework/Kathara)
e, estando no mesmo diretório do arquivo zip, descompactá-lo com:

```
unzip Kathara-master.zip
```

Agora teremos que instalar as bibliotecas Python utilizadas. Vá para o
diretório com o código e digite:

```
sudo python -m pip install -r requirements.txt
```

Em seguida, você já poderá usar o kathará. Para testar a instalação, pode usar
o seguinte comando:

```
sudo python src/kathara.py check
```

E ele checará se consegue rodar um exemplo, pode demorar alguns minutos
a depender de sua conexão.

Se ele apresentar erro, pode ser que seja necessário habilitar e iniciar
o script responsável por iniciar o docker, para isso:

```
sudo systemctl enable docker.service
sudo systemctl start docker.service
```

Então execute o teste do kathará novamente.
