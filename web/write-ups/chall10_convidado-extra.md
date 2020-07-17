# Convidado extra

## Alex:

**Flag:** `Ganesh{e@sy_3nc0nd!Ng}` Ao abrir o site, foi verificado que o site fazia a requisição de um arquivo javascript `defaultScript.js`:  


![req](https://i.imgur.com/vCOcU9R.png)

Ao abrir o arquivo JS foi percebido algo como uma TODO list em comentário, com uma dica de avaliar a senha:  


![file](https://i.imgur.com/JXzZ8Ja.png)

Então, ao olhar para a linha 4 do arquivo, foi percebido que se assemelha muito a uma codificação base64 \(o sinal de "=" no fim dá essa dica\). Ao decodar essa linha obtém-se o seguinte valor:

```text
ZGVmYXVsdF9wYXNzd29yZDo= 
          \/
    default_password:
```

Então, imagina-se que a linha abaixo seja a senha padrão do sistema. Ao olhar pra ela, sua codificação se assemelha com o URL encode. Ao reverter é obtido o seguinte valor:

```text
%66%39%33%66%63%31%30%34%37%32%61%33%31%62%62%33%30%36%31%61%61%30%62%34%35%65%32%32%38%63%35%61 
                                    \/
                    f93fc10472a31bb3061aa0b45e228c5a
```

Essa nova string obtida "f93fc10472a31bb3061aa0b45e228c5a" possui apenas caracteres hexadecimais, o que lembra um pouco a criptografia md5. Ao fazer o processo reverso do md5 é obtido o seguinte valor:

```text
f93fc10472a31bb3061aa0b45e228c5a
              \/
        strongpassword
```

Ao entrar com essa senha no site, é então mostrada a seguinte frase: 

![flag](https://i.imgur.com/6aPanxK.png)

E por consequência a flag é: Ganesh{e@sy\_3nc0nd!Ng}

