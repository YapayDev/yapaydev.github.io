---
title: Integração Simples
position: 3
menu: gateway
right_code: |
  ~~~ php
    <?php

        $username   = "diana@amazonas.com";
        $password   = "SEU_TOKEN";

        $data["transaction"]["number"] = "2429977";
        $data["transaction"]["installments"] = 1;      
        $data["transaction"]["amount"] = "1200";

        $data["transaction"]["payment"]["processor"] = "getnet";
        $data["transaction"]["payment"]["method"] = "visa";
        $data["transaction"]["payment"]["card"][reference] = "id99";
        $data["transaction"]["payment"]["card"][holder_name] = "Diana de Themyscira";
        $data["transaction"]["payment"]["card"][number] = "4916328365368562";
        $data["transaction"]["payment"]["card"][cvv] = "273";
        $data["transaction"]["payment"]["card"][expiration][month] = "09";
        $data["transaction"]["payment"]["card"][expiration][year] = "2018";

        $url = "https://gtw.sandbox.checkout.tray.com.br:443/api/v1/transactions.json?environment=test";

        ob_start();

        $ch = curl_init();
        curl_setopt($ch, CURLOPT_URL, $url);
        curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
        curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
        curl_setopt($ch, CURLOPT_HTTPHEADER, array(
            'Content-Type: application/json',        
            'Authorization: Basic ' . base64_encode("$username:$password"),
            'Content-Length: ' . strlen(json_encode($data)))
        );

        curl_exec($ch);

        // JSON de retorno  
        $resposta = json_decode(ob_get_contents());
        $code = curl_getinfo($ch, CURLINFO_HTTP_CODE);

        ob_end_clean();
        curl_close($ch);

        if($code == "201"){
            //Tratamento dos dados de resposta da consulta.
        }else{
            //Tratamento das mensagens de erro
        }
    ?>
  ~~~
  {: title="PHP" }
---

<span class="post">POST</span><span class="beforePost">/api/v1/transactions/</span>

1- O que contempla
{: .subtitulo }

Realizada na integração com **Adquirentes**.

Na **integração Simples** é necessário enviar pelo método **Criar Transação** o nó `payment` conforme necessidade. Abaixo você consegue visualizar os parâmetros para integração simples:

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

JSON Response 
{: .subtituloAzul }

~~~json
{
    "transaction": {
        "id": "072846c10e882b84cfab8bc542a0974e",
        "number": "12998",
        "status": "unpaid",
        "created_at": "2017-09-22T17:00:05.000-03:00",
        "tid": "1006993069000BD6446A",
        "nsu": "411974",
        "fingerprint": null,
        "free": null,
        "ip": null,
        "payment": {
            "method": "visa",
            "processor": "cielo",
            "installments": 1,
            "processing_type": "pre_authorized",
            "prices": {
                "total": 560,
                "additional": "0.0",
                "discount": "0.0"
            },
            "seller_settings": [
                {
                    "key": "affiliation",
                    "name": "Afiliação Cielo",
                    "description": "Afiliação Cielo",
                    "value": "23254866"
                }
            ],
            "card": {
                "number": null,
                "expiration": {
                    "month": null,
                    "year": null
                }
            },
            "billet": {
                "code": null,
                "due_date": null
            },
            "flag_url": "https://gtw.sandbox.checkout.tray.com.br/assets/payment_methods/701.png"
        },
        "customer": null,
        "urls": {
            "notification": null,
            "cancelation": null,
            "processing": null,
            "success": null
        },
        "shipping": {
            "type": null,
            "price": null
        },
        "products": [],
        "response": {
            "tid": "1006993069000BD6446A",
            "pan": "rTgjYLhJexlib7LSh69eYwDcaDdlpAkrD/dMUdF88c8=",
            "billet_bar_code": null,
            "url_payment": null,
            "status": {
                "id": 1,
                "name": "Aguardando Captura"
            },
            "authentication": {
                "code": "4",
                "message": "Transacao sem autenticacao",
                "eci": "7",
                "price": 560,
                "datetime": 2017
            },
            "authorization": {
                "lr": "00",
                "message": "Transação autorizada",
                "authorization_code": "4",
                "authorization_price": 560,
                "datetime": 2017
            },
            "cancellation": {
                "code": null,
                "message": null,
                "price": null,
                "datetime": 0
            }
        },
        "processor": {
            "transacao": {
                "versao": "1.2.1",
                "id": "1506110406",
                "xmlns": "http://ecommerce.cbmp.com.br",
                "tid": "1006993069000BD6446A",
                "pan": "rTgjYLhJexlib7LSh69eYwDcaDdlpAkrD/dMUdF88c8=",
                "dados_pedido": {
                    "numero": "12998",
                    "valor": "56000",
                    "moeda": "986",
                    "data_hora": "2017-09-22T17:00:07.097-03:00",
                    "descricao": null,
                    "idioma": "PT",
                    "taxa_embarque": "0"
                },
                "forma_pagamento": {
                    "bandeira": "visa",
                    "produto": "1",
                    "parcelas": "1"
                },
                "status": "4",
                "autenticacao": {
                    "codigo": "4",
                    "mensagem": "Transacao sem autenticacao",
                    "data_hora": "2017-09-22T17:00:07.111-03:00",
                    "valor": "56000",
                    "eci": "7"
                },
                "autorizacao": {
                    "codigo": "4",
                    "mensagem": "Transação autorizada",
                    "data_hora": "2017-09-22T17:00:07.114-03:00",
                    "valor": "56000",
                    "lr": "00",
                    "arp": "123456",
                    "nsu": "411974"
                }
            }
        }
    }
}
~~~

---

2- Adquirentes
{: .subtitulo }

Abaixo você consegue visualizar os Adquirentes que são suportadas:

| Adquirentes                                                                           | Integração |
|:-------------------------------------------------------------------------------------:|:-----------------------------------------------------------:|
| ![Cielo](/images/gateway/servicos/Cielo.png){: .imgLogoTable }                        | ![TrayCheckout](/images/checked-verde.svg){: .imgBtnTable } |
| ![Rede](/images/gateway/servicos/Rede.png){: .imgLogoTable }                          | ![TrayCheckout](/images/checked-verde.svg){: .imgBtnTable } |
| ![GetNet](/images/gateway/servicos/GetNet.jpg){: .imgLogoTable }                      | ![TrayCheckout](/images/checked-verde.svg){: .imgBtnTable } |

---

3- Sobre Autorização e Captura
{: .subtitulo }

A **autorização** da transação de cartão de crédito enviada para análise de limite de crédito e validação dos dados do cartão utilizado juntamente com o adquirente. Nessa etapa ainda não é gerada a cobrança na fatura para o usuário.

A **captura** de uma transação de cartão de crédito representa a cobrança realizada com o adquirente. Nessa etapa, o status "Aurotizado" é alterado para "Pago" e você tem a garantia de que o valor da transação será recebido.

---

4- Autorização e Captura
{: .subtitulo }

Texto

---

