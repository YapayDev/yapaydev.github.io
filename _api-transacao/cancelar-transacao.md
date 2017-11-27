---
title: Cancelar a transação
position: 6
menu: gateway
---

<span class="delete">DELETE</span><span class="beforePost">/api/v1/transactions/</span>

Para realizar o cancelamento da transação, você utiliza o método com o parâmetro:




| Dados de Entrada     | Formato   | Descrição                   |
|----------------------|-----------|-----------------------------|
| authorization        |  Texto    |  Token de autenticação      |
| id                   |  Número   |  ID do pedido               |


Abaixo você consegue visualizar um exemplo de requisição:

~~~php
    <?php

        $username   = "diane@amazonas.com";
        $password   = "SEU_TOKEN";

        $url = "https://gtw.sandbox.checkout.tray.com.br:443/api/v1/transactions/6d8bb0d98bff79274c050a36fa6972ad.json";

        ob_start();

        $ch = curl_init();
        curl_setopt($ch, CURLOPT_URL, $url);
        curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "DELETE");
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
    "id": "6d8bb0d98bff79274c050a36fa6972ad",
    "number": "1229100",
    "status": "returned",
    "created_at": "2017-09-22T18:09:47.000-03:00",
    "tid": "1006993069000BD6605A",
    "nsu": "412421",
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
      "tid": "1006993069000BD6605A",
      "pan": "rTgjYLhJexlib7LSh69eYwDcaDdlpAkrD/dMUdF88c8=",
      "billet_bar_code": null,
      "url_payment": null,
      "status": {
        "id": 4,
        "name": "Estornada"
      },
      "authentication": {
        "code": "9",
        "message": "Transacao sem autenticacao",
        "eci": "7",
        "price": 560,
        "datetime": 2017
      },
      "authorization": {
        "lr": "00",
        "message": "Transação autorizada",
        "authorization_code": "9",
        "authorization_price": 560,
        "datetime": 2017
      },
      "cancellation": {
        "code": "9",
        "message": "Transacao cancelada com sucesso",
        "price": 560,
        "datetime": 2017
      }
    },
    "processor": {
      "transacao": {
        "versao": "1.2.1",
        "id": "1506114624",
        "xmlns": "http://ecommerce.cbmp.com.br",
        "tid": "1006993069000BD6605A",
        "pan": "rTgjYLhJexlib7LSh69eYwDcaDdlpAkrD/dMUdF88c8=",
        "dados_pedido": {
          "numero": "1229100",
          "valor": "56000",
          "moeda": "986",
          "data_hora": "2017-09-22T18:09:48.416-03:00",
          "idioma": "PT",
          "taxa_embarque": "0"
        },
        "forma_pagamento": {
          "bandeira": "visa",
          "produto": "1",
          "parcelas": "1"
        },
        "status": "9",
        "autenticacao": {
          "codigo": "9",
          "mensagem": "Transacao sem autenticacao",
          "data_hora": "2017-09-22T18:09:48.431-03:00",
          "valor": "56000",
          "eci": "7"
        },
        "autorizacao": {
          "codigo": "9",
          "mensagem": "Transação autorizada",
          "data_hora": "2017-09-22T18:09:48.435-03:00",
          "valor": "56000",
          "lr": "00",
          "arp": "123456",
          "nsu": "412421"
        },
        "captura": {
          "codigo": "9",
          "mensagem": "Transacao capturada com sucesso",
          "data_hora": "2017-09-22T18:10:12.122-03:00",
          "valor": "56000"
        },
        "cancelamentos": {
          "cancelamento": {
            "codigo": "9",
            "mensagem": "Transacao cancelada com sucesso",
            "data_hora": "2017-09-22T18:10:24.955-03:00",
            "valor": "56000"
          }
        }
      }
    }
  }
}
~~~