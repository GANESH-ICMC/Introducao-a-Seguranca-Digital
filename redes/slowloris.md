# Slow Loris

![](https://www.cloudflare.com/img/learning/ddos/ddos-slowloris-attack/slowloris-attack-diagram.png)

A ideia por trás do Slow Loris é abrir várias conexões TCP com um servidor web e, em cada uma delas, enviar de tempos em tempos uma parte de uma requisição GET. O servidor acha que as conexões estão lentas, mas que são legítimas, então ele as mantêm, impedindo outras conexões de usuários comuns.

Para esse ataque, vamos usar [esse código maravilindo](https://github.com/gkbrk/slowloris). Primeiro clonamos o repositório:

```
$ git clone https://github.com/gkbrk/slowloris
```


Depois entramos no repositório clonado:

```
$ cd slowloris
```
**Obs:** É possível que você precise especificar um caminho diferente ao `cd`, dependendo da pasta para onde o repositório foi clonado e da pasta onde você está.


Finalmente, basta usar o python para executar o código, passando o IP do alvo (nesse caso, nosso alvo é `10.10.10.10`):

```
$ python3 slowloris.py 10.10.10.10
```

Ou apenas o domínio, caso exista:

```
$ python3 slowloris.py example.com
```

**Obs:** Existe uma outra versão do Slow Loris que se chama R U Dead Yet, que envia requisições POST ao invés de GET.
