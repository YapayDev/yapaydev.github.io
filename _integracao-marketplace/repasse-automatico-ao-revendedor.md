---
title: Repasse automático ao revendedor
position: 2
menu: intermediador
---

Para que o repasse ao revendedor seja automático, utilizamos a API de Transação na integração com Marketplace informando os campos _affiliates[]_, esses campos quando são enviados são identificamos que é referente a transações Marketplace:

| Dados de Entrada                      |  Obrig.  | Formato / Tam. Max   | Descrição                             |
|---------------------------------------|----------|----------------------|---------------------------------------|
|   affiliates[][account_email]         |   Não    | Texto / 100	        | Email do afiliado da transação        |
|   affiliates[][percentage]            |   Não    | Número / 3	          | Percentual de repasse ao afiliado     |
|   affiliates[][commission_amount]     |   Não    | Decimal / 11	        | Valor de repasse ao afiliado          |


Para verificar a documentação completa da **API de Transação** <a href="/intermediador/apis/#api-transacao" target="_blank" class="linkPadraoVerde">clique aqui</a>.
{:.info}



<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>