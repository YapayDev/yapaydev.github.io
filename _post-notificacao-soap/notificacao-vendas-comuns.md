---
title: Notificação vendas comuns
position: 1
menu: gateway
right_code: |
  ~~~ text
  POST HTTP
  Content-Type: application/x-www-form-urlencoded
  Content-Length: 125
  numeroTransacao=123&codigoEstabelecimento=1000000000000&campoLivre=A&campoLivre2=B&campoLivre3=C&campoLivre4=D&campoLivre5=E
  ~~~
  {: title="Exemplo de chamada" }

---

O sistema de campainha existe para notificar o estabelecimento sobre uma atualização de status na transação. Toda vez que ocorre qualquer alteração de status em uma transação, é feita uma chamada via POST ao campo “urlCampainha” (enviada como parâmetro junto da transação), essa chamada enviará alguns dados que identificarão a transação, e assim o estabelecimento saberá em qual transação houve uma mudança de status.

Importante lembrar que a chamada de campainha não informa qual o status atual da transação e apenas que houve uma alteração, sendo assim, o estabelecimento deve realizar uma consulta (através da função de <a href="/gateway/consultas/#consultando-uma-transacao" target="_blank" class="linkPadraoVerde">consultarTransacao</a>) para verificar com mais detalhes a situação atual da transação.

_Caso a URL de campainha estiver em HTTPS, informar ao Suporte Yapay, servicedesk@superpay.com.br_

Detalhamento dos campos retornados:

| Campo                 | Descrição                                               | Tipo          |
|-----------------------|---------------------------------------------------------|---------------|
| numeroTransacao       | Código que identifica a transação dentro do Yapay       | Numérico      |
| codigoEstabelecimento | Código que identifica o estabelecimento dentro do Yapay | Numérico      |
| campoLivre1           | Campo Livre 1                                           | Alfa Numérico |
| campoLivre2           | Campo Livre 2                                           | Alfa Numérico |
| campoLivre3           | Campo Livre 3                                           | Alfa Numérico |
| campoLivre4           | Campo Livre 4                                           | Alfa Numérico |
| campoLivre5           | Campo Livre 5                                           | Alfa Numérico |



<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>