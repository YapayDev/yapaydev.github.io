---
title: Detalhes da Transação
position: 3
menu: gateway
right_code: |
  ~~~ php
    <?php

    $username   = "diana@amazonas.com";
    $password   = "SEU_TOKEN";

    $url = "https://gtw.sandbox.checkout.tray.com.br/api/v1/transactions/f862781748917fba108cd7b1fb17014e";

    $ch = curl_init();

    curl_setopt($ch, CURLOPT_URL, $url);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($ch, CURLOPT_SSLVERSION, 1);
    curl_setopt($ch, CURLOPT_HTTP_VERSION, CURL_HTTP_VERSION_1_1);
    curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "GET");   
    curl_setopt($ch, CURLOPT_HTTPHEADER, array(
        'Content-Type: application/json',        
        'Authorization: Basic ' . base64_encode("$username:$password"),
        'Content-Length: ' . strlen(json_encode($data)))
    );


    $resposta = curl_exec($ch);
    $erro = curl_error($ch); //Salva o erro na variavel 

    curl_close($ch);

    if ($erro) { // Se der erro, mostra na tela
        echo "Retornou o error :" . $erro;
    } else { // Senão mostra o conteúdo JSON
        echo $resposta;
    }

    ?>
  ~~~
  {: title="PHP" }

  ~~~ruby
    require 'uri'
    require 'net/http'

        url = URI("https://gtw.sandbox.checkout.tray.com.br/api/v1/transactions/f862781748917fba108cd7b1fb17014e")


        http = Net::HTTP.new(url.host, url.port)

        http.use_ssl = true

        request = Net::HTTP::Get.new(url)
        request["Accept"] = 'application/json'
        request["Content-Type"] = 'application/json'
        request["Authorization"] = 'Basic SEU_TOKEN'


        response = http.request(request)

        puts response.read_body
  ~~~
  {: title="Ruby"}

  ~~~java
    var client = new RestClient("https://gtw.sandbox.checkout.tray.com.br/api/v1/transactions/f862781748917fba108cd7b1fb17014e");
    var request = new RestRequest(Method.GET);
        request.AddHeader("Accept", "application/json");
        request.AddHeader("Content-Type", "application/json");
        request.AddHeader("Authorization", "Basic SEU_TOKEN");
        request.AddParameter("undefined", "{}", ParameterType.RequestBody);
        IRestResponse response = client.Execute(request);
  ~~~
  {: title="Java"}  

  ~~~c#
    HttpResponse<String> response = Unirest.get("https://gtw.sandbox.checkout.tray.com.br/api/v1/transactions/f862781748917fba108cd7b1fb17014e")
        .header("Accept", "application/json")
        .header("Content-Type", "application/json")
        .header("Authorization", "Basic SEU_TOKEN")
        .body("{}")
        .asString();
  ~~~
  {: title="C#"}  
---

<span class="get">GET</span><span class="beforePost">/api/v1/transactions/</span>

O método de **Consultar Transação** possui os seguintes parâmetros:

| Parâmetro    | Formato  | Descrição                      |
|---------------------|----------|-------------------------|
| authorization       | Texto    | Token de autenticação   |
| id                  | Número   | ID do pedido            |


Ao lado você consegue visualizar um exemplo de requisição.

Observe que na URL está sendo informado o parâmetro `ID DO PEDIDO`. 

Exemplo de URL: `https://gtw.sandbox.checkout.tray.com.br/api/v1/transactions/f862781748917fba108cd7b1fb17014e`


JSON Response
{: .subtituloAzul }

Abaixo você consegue visualizar o JSON Response:

~~~json
{
    "transaction": {
        "id": "f862781748917fba108cd7b1fb17014e",
        "number": "102059",
        "status": "paid",
        "created_at": "2017-09-15T14:20:50.000-03:00",
        "tid": "1006993069000B0F3E9A",
        "nsu": "596777",
        "fingerprint": "",
        "free": null,
        "ip": null,
        "payment": {
            "method": "visa",
            "processor": "cielo",
            "installments": 1,
            "processing_type": "pre_authorized",
            "prices": {
                "total": 20,
                "additional": "0.0",
                "discount": "0.0"
            },
            "seller_settings": [
                {
                    "key": "affiliation",
                    "name": "Afiliação Cielo",
                    "description": "Afiliação Cielo",
                    "value": "00000001"
                }
            ],
            "card": {
                "number": "4111111111111111",
                "expiration": {
                    "month": "02",
                    "year": "2019"
                }
            },
            "billet": {
                "code": null,
                "due_date": null
            },
            "flag_url": "https://gtw.sandbox.checkout.tray.com.br/assets/payment_methods/701.png"
        },
        "customer": {
            "id": 9955,
            "name": "Diana de Themyscira",
            "customer_document": "84352522139",
            "created_at": "2017-08-30T08:52:06.000-03:00",
            "updated_at": "2017-09-14T15:29:03.000-03:00",
            "email": "diana@amazonas.com",
            "birth_date": null,
            "gender": "F",
            "seller_document": null,
            "company_name": ""
        },
        "urls": {
            "notification": null,
            "cancelation": "",
            "processing": "",
            "success": ""
        },
        "shipping": {
            "type": "",
            "price": null
        },
        "products": [
            {
                "id": 11445,
                "transaction_id": 11225,
                "code": "9201",
                "description": "Camiseta DC Comics",
                "quantity": "1.0",
                "price_unit": "20.0",
                "weight": "10.0",
                "shipping_cost": "0.0",
                "created_at": "2017-09-15T14:20:50.000-03:00",
                "updated_at": "2017-09-15T14:20:50.000-03:00",
                "url_img": null
            }
        ],
        "response": {
            "tid": "1006993069000B0F3E9A",
            "pan": "mTEIeZkc4vsrJjJLF42avRp9CqB9muz+BHc57k5trDg=",
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
                "price": 20,
                "datetime": 2017
            },
            "authorization": {
                "lr": "00",
                "message": "Transação autorizada",
                "authorization_code": "6",
                "authorization_price": 20,
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
                "id": "1506013715",
                "xmlns": "http://link.com.br",
                "tid": "1003333033000A0G2A8E",
                "pan": "nTTIgZcc4vsrJjJLF42avRp9CqB9muz+BHc57k5trDg=",
                "dados_pedido": {
                    "numero": "102059",
                    "valor": "2000",
                    "moeda": "986",
                    "data_hora": "2017-09-15T14:20:52.352-03:00",
                    "idioma": "PT",
                    "taxa_embarque": "0"
                },
                "forma_pagamento": {
                    "bandeira": "visa",
                    "produto": "1",
                    "parcelas": "1"
                },
                "status": "6",
                "autenticacao": {
                    "codigo": "6",
                    "mensagem": "Transacao sem autenticacao",
                    "data_hora": "2017-09-15T14:20:52.383-03:00",
                    "valor": "2000",
                    "eci": "7"
                },
                "autorizacao": {
                    "codigo": "6",
                    "mensagem": "Transação autorizada",
                    "data_hora": "2017-09-15T14:20:52.386-03:00",
                    "valor": "2000",
                    "lr": "00",
                    "arp": "123456",
                    "nsu": "596777"
                },
                "captura": {
                    "codigo": "6",
                    "mensagem": "Transacao capturada com sucesso",
                    "data_hora": "2017-09-15T14:21:07.225-03:00",
                    "valor": "2000"
                }
            }
        }
    }
}
~~~