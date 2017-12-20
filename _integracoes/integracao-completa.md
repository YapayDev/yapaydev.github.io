---
title: Integração Completa
position: 1
menu: gateway
---

<span class="post">POST</span><span class="beforePost">/api/v1/transactions/</span>


1- O que contempla
{: .subtitulo }

Realizada na integração com **Adquirentes, Análise de Risco e Intermediador**.

Na **Integração Completa** é necessário enviar pelo método <a href="/gateway/criar-transacao/#criar-transacao" target="_blank" class="linkPadraoVerde">Criar Transação</a> os dados completos da transação, frete, produto e cliente. É enviado dentro do nó `transaction`os nós `payment`, `payment[card]` ou `payment[billet]`, `prices`, `shipping`, `products` e `customer`. Com o preenchimento de todos os campos, a anaáise de risco consegue ser realizada corretamente.




 Abaixo você consegue visualizar os parâmetros para integração simples:

| Parâmetro                                      | Formato  | Descrição                             |
|------------------------------------------------|----------|---------------------------------------|
| authorization                                  | Texto    | Token de autenticação                 |
| transaction[number]	                         | Texto    | Número do Pedido	                    |
| transaction[installments]	                     | Número   | Quantidade de Parcelas	            |
| transaction[amount]		                     | Número   | Valor                                 |
| transaction[payment][processor]	             | Número   | Processador do pagamento (Adquirente)	|
| transaction[payment][method]	                 | Número   | Meio de pagamento (Forma)	            |
| transaction[payment][card][reference]	         | Número   | Referência do cartão                  |
| transaction[payment][card][holder_name]        | Número   | Nome impresso no cartão               |
| transaction[payment][card][number]	         | Número   | Número do cartão                      |
| transaction[payment][card][cvv]	             | Número   | Código de segurança do cartão         |
| transaction[payment][card][expiration][month]	 | Número   | Mês de vencimento do cartão (mm)      |
| transaction[payment][card][expiration][year]	 | Número   | Ano de vencimento do cartão (YYYY)    |


Ao lado você consegue visualizar um exemplo de requisição.

2- Intermediadores, Adquirentes e Análise de Risco
{: .subtitulo }

Abaixo você consegue visualizar os Adquirentes, Análise de Risco e Intermediadores:

| Bancos                                                                                | Integração |
|:-------------------------------------------------------------------------------------:|:-----------------------------------------------------------:|
| ![Banrisul](/images/gateway/servicos/Banrisul.png){: .imgLogoTable }                  | ![Yapay Gateway](/images/checked-verde.svg){: .imgBtnTable } |
| ![Banco do Brasil](/images/gateway/servicos/BancoDoBrasil.png){: .imgLogoTable }      | ![Yapay Gateway](/images/checked-verde.svg){: .imgBtnTable } |
| ![Bradesco](/images/gateway/servicos/Bradesco.png){: .imgLogoTable }                  | ![Yapay Gateway](/images/checked-verde.svg){: .imgBtnTable } |
| ![Itaú](/images/gateway/servicos/Itau.png){: .imgLogoTable }                          | ![Yapay Gateway](/images/checked-verde.svg){: .imgBtnTable } |


| Adquirentes                                                                           | Integração |
|:-------------------------------------------------------------------------------------:|:-----------------------------------------------------------:|
| ![Cielo](/images/gateway/servicos/Cielo.png){: .imgLogoTable }                        | ![Yapay Gateway](/images/checked-verde.svg){: .imgBtnTable } |
| ![Rede](/images/gateway/servicos/Rede.png){: .imgLogoTable }                          | ![Yapay Gateway](/images/checked-verde.svg){: .imgBtnTable } |
| ![GetNet](/images/gateway/servicos/GetNet.jpg){: .imgLogoTable }                      | ![Yapay Gateway](/images/checked-verde.svg){: .imgBtnTable } |



| Análise de Risco                                                                      | Integração |
|:-------------------------------------------------------------------------------------:|:-----------------------------------------------------------:|
| ![ClearSale](/images/gateway/servicos/ClearSale.png){: .imgLogoTable }                | ![Yapay Gateway](/images/checked-verde.svg){: .imgBtnTable } |
| ![FControl](/images/gateway/servicos/FControl.png){: .imgLogoTable }                  | ![Yapay Gateway](/images/checked-verde.svg){: .imgBtnTable } |


| Intermediadores                                                                      | Integração |
|:-------------------------------------------------------------------------------------:|:----------------------------------------------------------:|
| ![PayU](/images/gateway/servicos/PayU.png){: .imgLogoTable }                         | ![Yapay Gateway](/images/checked-verde.svg){: .imgBtnTable } |
| ![Mercado Pago](/images/gateway/servicos/MercadoPago.png){: .imgLogoTable }          | ![Yapay Gateway](/images/checked-verde.svg){: .imgBtnTable } |
| ![MoIP](/images/gateway/servicos/MoIP.png){: .imgLogoTable }                         | ![Yapay Gateway](/images/checked-verde.svg){: .imgBtnTable } |
| ![PagSeguro](/images/gateway/servicos/PagSeguro.png){: .imgLogoTable }               | ![Yapay Gateway](/images/checked-verde.svg){: .imgBtnTable } |
| ![Elavon](/images/gateway/servicos/Elavon.jpg){: .imgLogoTable }                     | ![Yapay Gateway](/images/checked-verde.svg){: .imgBtnTable } |
| ![PayPal](/images/gateway/servicos/PayPal.png){: .imgLogoTable }                     | ![Yapay Gateway](/images/checked-verde.svg){: .imgBtnTable } |
| ![Peela](/images/gateway/servicos/Peela.jpg){: .imgLogoTable }                       | ![Yapay Gateway](/images/checked-verde.svg){: .imgBtnTable } |


3- Sobre Autorização e Captura
{: .subtitulo }

A **autorização** da transação de cartão de crédito enviada para análise de limite de crédito e validação dos dados do cartão utilizado juntamente com o adquirente. Nessa etapa ainda não é gerada a cobrança na fatura para o usuário.

A **captura** de uma transação de cartão de crédito representa a cobrança realizada com o adquirente. Nessa etapa, o status "Aurotizado" é alterado para "Pago" e você tem a garantia de que o valor da transação será recebido.

4- Autorização e Captura
{: .subtitulo }

Texto


