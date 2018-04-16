---
title: Recebendo as notificações de status
position: 1
menu: intermediador
---

O Yapay pode comunicar com sua aplicação a cada alteração de status de uma transação, fazendo com que seu sistema acompanhe todo o fluxo de status e esteja sempre atualizado quanto a situação da transação.

![Fluxo de notificação automática](/images/intermediador/conteudo/Notificacao_automatica.png "Fluxo de notificação automática"){: width="70%" height="auto"}

Integração com Notificação Automática de Status
{: .subtitulo }

Para a integração com a notificação automática de status, é necessário configurar uma URL que receberá a chamada, processará os dados recebidos, e em seguida irá obter mais detalhes da transação através de uma API específica. Esse parâmetro está disponível em ambas as integrações (POST ou API) e chama-se **transaction[url_notification]**.

O Yapay irá realizar o POST com a seguinte informação:

| Parâmetros enviados via Post                                                      |
|--------------------------------------------------|--------------------------------|
| token_transaction                                | Token da transação             |
| transaction[products][][extra]                   | Informação Extra               |
| transaction[products][][description]             | Descrição                      |
| transaction[products][][quantity]                | Quantidade do produto          |
| transaction[products][][code]                    | Código do produto              |
| transaction[products][][price_unit]              | Valor unitário do produto      |
| transaction[customer][email]                     | e-mail do cliente              |
| transaction[customer][address][postal_code]      | CEP                            |
| transaction[customer][address][city]             | Cidade                         |
| transaction[customer][address][street]           | Rua                            |
| transaction[customer][cpf]                       | CPF                            |
| transaction[customer][address][state]            | Estado                         |
| transaction[customer][address][number]           | Número                         |
| transaction[customer][address][completion]       | Complemento                    |
| transaction[customer][token]                     | Token do cliente               |
| transaction[customer][address][neighborhood]     | Bairro                         |
| transaction[customer][name]                      | Nome do Cliente                |
| transaction[payment][payment_response]           | Response do Pagamento          |
| transaction[payment][date_approval]              | Data de Aprovação do pagamento |
| transaction[payment][price_payment]              | Valor do pagamento             |
| transaction[payment][number_of_voucher_sales]    | Número do comprovante          |
| transaction[payment][selling_message]            | Mensagem do Vendedor           |
| transaction[payment][url_payment]                | url do pagamento               |
| transaction[payment][payment_method_id]          | ID do Meio de Pagamento        |
| transaction[payment][card_id]                    | ID do cartão de crédito        |
| transaction[payment][number_proccess]            | Número do processamento        |
| transaction[payment][date_payment]               | Data do pagamento              |
| transaction[payment][payment_method_name]        | Meio de pagamento              |
| transaction[payment][split]                      | Split do pagamento             |
| transaction[company][name]                       | Nome do Vendedor               |
| transaction[company][contact]                    | Número do contato do cliente   |
| transaction[company][cnpj]                       | CNPJ do Vendedor               |
| transaction[company][url]                        | URL da Empresa                 |
| transaction[company][cpf]                        | CPF do Vendedor                |
| transaction[company][token]                      | Token do Vendedor              |
| transaction[seller_token]                        | Token do Vendedor              |
| transaction[free]                                | Camo Free                      |
| transaction[price_seller]                        | Valor do Vendedor              |
| transaction[price_payment]                       | Valor                          |
| transaction[date_payment]                        | Data do Pagamento              |
| transaction[price_discount]                      | Valor de desconto              |
| transaction[status_id]                           | ID do Status                   |
| transaction[shipping_price]                      | Valor do Frete                 |
| transaction[price_additional]                    | Valor adicional                |
| transaction[payment_method_name]                 | Meio de pagamento              |
| transaction[status_name]                         | Nome do Status                 |
| transaction[payment_method_id]                   | ID do Meio de pagamento        |
| transaction[split]                               | Parcelas                       |
| transaction[transaction_token]                   | Token da Transação             |
| transaction[order_number]                        | Número do pedido               |
| transaction[date_transaction]                    | Data da Transação              |
| transaction[shipping_type]                       | Tipo de Frete                  |
| transaction[transaction_id]                      | ID da Transação                |
| transaction[price_original]                      | Valor                          |


A notificação será realizada através de um POST, que espera receber o retorno **“HTTP 200”** de sua aplicação. Caso a página esteja fora do ar ou com algum outro erro e não retorne “HTTP 200”, **serão feitas novas tentativas a cada 12 horas durante 3 dias**.

Após receber esta informação, deverá ser feita a consulta pelas informações completas da transação, através da <a href="/intermediador/apis/#api-consulta-transacao" target="_blank" class="linkPadraoVerde">API de Consulta de Transação</a>.
{:.info}


<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>