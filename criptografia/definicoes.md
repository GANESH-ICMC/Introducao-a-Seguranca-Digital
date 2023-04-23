# Definições

Na literatura, é muito comum encontrarmos três personagens que representam o cenário da comunicação dentro da Criptografia: **Alice**, **Bob** e **Eve**. Estes personagens foram adotados por diversos autores em livros, artigos e publicações acadêmicas e acabaram sendo padronizados para fins didáticos. O papel de cada um deles é o seguinte:

> * **Alice:** é o emissor da mensagem, possui o texto original (plaintext) e aplica um algoritmo de encriptação para torná-lo secreto, obtendo o texto cifrado (ciphertext).
> * **Bob:** é o receptor da mensagem, recebe o ciphertext de Alice e aplica um algoritmo de decriptação para recuperar o plaintext.
> * **Eve:** é o atacante, não é o distinatário legítimo da mensagem, mas deseja conhecer seu conteúdo ou alterá-lo antes que a mensagem chegue a Bob.

![cenario](https://user-images.githubusercontent.com/96321435/233815814-5f1d1312-7069-4891-9dc7-382d56e5bbc6.png)

# Objetivos

À medida que as exigências de segurança avançaram, o campo da criptografia também se aperfeiçoou, buscando atingir uma gama mais ampla de objetivos de segurança, sendo eles:

> * **Confidencialidade** da mensagem: só o destinatário autorizado deve ser capaz de extrair o conteúdo da mensagem da sua forma cifrada. Além disso, a obtenção de informação sobre o conteúdo da mensagem (como uma distribuição estatística de certos caracteres) não deve ser possível, uma vez que, se o for, torna mais fácil a análise criptográfica;
> * **Integridade** da mensagem: o destinatário deverá ser capaz de verificar se a mensagem foi alterada durante a transmissão;
> * **Autenticação** do remetente: o destinatário deverá ser capaz de verificar se o remetente é realmente quem diz ser;
> * **Não repúdio** do remetente: não deverá ser possível ao remetente negar a autoria de sua mensagem.
