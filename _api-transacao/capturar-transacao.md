---
title: Capturar Transação
position: 4
menu: gateway
---

<span class="patch">PATCH</span><span class="beforePost">/api/v1/transactions/{id}</span>

Para realizar a captura da transação, deve estar no status **Aguardando Captura**. Dessa forma quando é chamado o método **Captura de Transação**, é verificado o nó `response`, `authentication` e `cancellation`.


Abaixo você consegue visualizar os parâmetros para integração simples:

| Dados de Entrada    | Formato  | Descrição               |
|---------------------|----------|-------------------------|
| authorization       | Texto    | Token de autenticação   |
| id                  | Número   | ID do pedido            |

Abaixo você consegue visualizar um exemplo de requisição:

~~~php
    <?php

        $username   = "diane@amazonas.com";
        $password   = "SEU_TOKEN";

        $url = "https://gtw.sandbox.checkout.tray.com.br/api/v1/transactions/072846c10e882b84cfab8bc542a0974e";

        ob_start();

        $ch = curl_init();
        curl_setopt($ch, CURLOPT_URL, $url);
        curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "PATCH");
        curl_setopt($ch, CURLOPT_HTTPHEADER, array(
            'Content-Type: application/json',        
            'Authorization: Basic ' . base64_encode("$username:$password"))
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

JSON Response 
{: .subtituloAzul }

Abaixo você consegue visualizar o JSON Response:

~~~json
{
    "transaction": {
        "id": "01003302f8cbb8dfb6103d0543d54915",
        "number": "122998",
        "status": "paid",
        "created_at": "2017-09-22T17:03:24.000-03:00",
        "tid": "1006993069000BD6451A",
        "nsu": "411985",
        "fingerprint": null,
        "free": null,
        "ip": null,
        "payment": {
            "method": "visa",
            "processor": "getnet",
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
            "tid": "1006993069000BD6451A",
            "pan": "rTgjYLhJexlib7LSh69eYwDcaDdlpAkrD/dMUdF88c8=",
            "billet_bar_code": null,
            "url_payment": null,
            "status": {
                "id": 2,
                "name": "Capturada"
            },
            "authentication": {
                "code": "6",
                "message": "Transacao sem autenticacao",
                "eci": "7",
                "price": 560,
                "datetime": 2017
            },
            "authorization": {
                "lr": "00",
                "message": "Transação autorizada",
                "authorization_code": "6",
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
        "processor": null
    }
}
~~~