# Googlebot, não pegue!

## ＃ Marucs:

Flag: `Ganesh{W3B?_345Y_P345Y_L3M0N_5QU33ZY}`

Ao entrar no site, aparentemente não há nada para se ver, sem requisições especiais, nenhum link interno. Me chamou atenção não ter nenhuma página além da '/', então estava quase setando um dirbuster quando lembrei da existência do arquivo robots.txt, mas não achei que fosse realmente ter um.

### /robots.txt:

```text
# Pensando mais a longo prazo, a execuÃ§Ã£o dos pontos do programa nos obriga Ã  anÃ¡lise das regras de conduta normativas. 
# Acima de tudo, Ã© fundamental ressaltar que a contÃ­nua expansÃ£o de nossa atividade faz parte de um processo de gerenciamento das diretrizes de desenvolvimento para o futuro. 
# Assim mesmo, a consulta aos diversos militantes aponta para a melhoria dos mÃ©todos utilizados na avaliaÃ§Ã£o de resultados. 
# O cuidado em identificar pontos crÃ­ticos na estrutura atual da organizaÃ§Ã£o assume importantes posiÃ§Ãµes no estabelecimento do sistema de formaÃ§Ã£o de quadros que corresponde Ã s necessidades. 
# Do mesmo modo, a mobilidade dos capitais internacionais estende o alcance e a importÃ¢ncia das novas proposiÃ§Ãµes. 
# Todavia, o consenso sobre a necessidade de qualificaÃ§Ã£o ainda nÃ£o demonstrou convincentemente que vai participar na mudanÃ§a das direÃ§Ãµes preferenciais no sentido do progresso.
User-agent: *
Disallow: /
Disallow: /w/
Disallow: /api/
Disallow: /trap/
Disallow: /test/Special:
Disallow: /test/Spezial:
Disallow: /test/ganesh/flag.php
Disallow: /test/Spesial:
Disallow: /test/Special%3A
Disallow: /test/Spezial%3A
Disallow: /test/Spesial%3A
```

Lá tinha várias rotas proibidas. Uma delas era a /test/ganesh/flag.php, onde estava guardada a flag.

