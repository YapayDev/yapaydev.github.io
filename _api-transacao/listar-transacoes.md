---
title: Listar Transações
position: 2
menu: gateway
right_code: |
  ~~~ php
    <?php

    $headers = array(
        "accept: application/json",
        "content-type: application/json",      
        "Authorization: Basic SEU_TOKEN"      
        );

    $url = "https://gtw.sandbox.checkout.tray.com.br/api/v1/transactions";

    $ch = curl_init();

    curl_setopt($ch, CURLOPT_URL, $url);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($ch, CURLOPT_SSLVERSION, 1);
    curl_setopt($ch, CURLOPT_HTTP_VERSION, CURL_HTTP_VERSION_1_1);
    curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "GET");   
    curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);


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

        url = URI("https://gtw.sandbox.checkout.tray.com.br/api/v1/transactions")


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
    var client = new RestClient("https://gtw.sandbox.checkout.tray.com.br/api/v1/transactions");
    var request = new RestRequest(Method.GET);
        request.AddHeader("Accept", "application/json");
        request.AddHeader("Content-Type", "application/json");
        request.AddHeader("Authorization", "Basic SEU_TOKEN");
        request.AddParameter("undefined", "{}", ParameterType.RequestBody);
        IRestResponse response = client.Execute(request);
  ~~~
  {: title="Java"}  

  ~~~c#
    HttpResponse<String> response = Unirest.get("https://gtw.sandbox.checkout.tray.com.br/api/v1/transactions")
        .header("Accept", "application/json")
        .header("Content-Type", "application/json")
        .header("Authorization", "Basic SEU_TOKEN")
        .body("{}")
        .asString();
  ~~~
  {: title="C#"}  
---

<span class="get">GET</span><span class="beforePost">/api/v1/transactions/</span>

O método de **Listar Transações** possui os seguintes parâmetros:

| Parâmetros                | Formato  | Descrição                 |
|---------------------------|----------|---------------------------|
| Authorization             | Header   | Token de autenticação     |
| q[number]                 | query    | Número do Pedido          |
| q[status]                 | query    | Status                    |
| q[payment][method]        | query    | Forma de Pagamento        |
| q[payment][processor]     | query    | Processador de Pagamento  |
| q[customer]               | query    | Nome ou Email do Cliente  |
| q[initial_created_date]   | query    | Data de Criação Inicial   |
| q[final_created_date]     | query    | Data de Criação Final     |
| q[initial_price]          | query    | Valor Inicial             |
| q[final_price]            | query    | Valor Final               |
| q[installments]           | query    | Quantidade de Parcelas    |
| current_page              | query    | Página Atual              |
| per_page                  | query    | Quantidade Por Página     |

Ao lado você consegue visualizar um exemplo de requisição

Para utilizar o método com parâmetros é necessário informar a URL com os parâmetros que desejar. Exemplo de URL:

`https://gtw.sandbox.checkout.tray.com.br/api/v1/transactions?q%5Bnumber%5D=1200877`

JSON Response
{: .subtituloAzul }

Abaixo você consegue visualizar o JSON Response:

```json
{  
   "transactions":[  
      {  
         "id":"9704874bb3f5a781aa69c2d8b3300142",
         "number":"112233",
         "status":"unpaid",
         "created_at":"2017-09-20T12:12:12.000-03:00",
         "tid":null,
         "nsu":null,
         "fingerprint":null,
         "free":null,
         "ip":"127.0.0.1",
         "payment":{  
            "method":"visa",
            "processor":"cielo",
            "installments":1,
            "processing_type":"authorized",
            "prices":{  
               "total":230.0,
               "additional":"0.0",
               "discount":"0.0"
            },
            "seller_settings":[  
               {  
                  "key":"affiliation",
                  "name":"Vendedor",
                  "description":"Username do vendedor na operadora",
                  "value":"hti_tray"
               },
               {  
                  "key":"establishment",
                  "name":"Codigo vendedor",
                  "description":"Codigo de EC cadastrado na Cielo",
                  "value":"1122334"
               }
            ],
            "card":{  
               "number":"4111111111111111",
               "expiration":{  
                  "month":"05",
                  "year":"2020"
               }
            },
            "billet":{  
               "code":null,
               "due_date":null
            },
            "flag_url":"https://gtw.sandbox.checkout.tray.com.br/assets/payment_methods/894.png"
         },
         "customer":{  
            "id":1234,
            "name":"Diana de Themyscira",
            "customer_document":"84352522139",
            "created_at":"2012-02-29T14:47:22.000-03:00",
            "updated_at":"2015-11-21T15:46:56.000-02:00",
            "email":"diana@amazonas.com",
            "birth_date":"1942-05-01",
            "gender":"F",
            "seller_document":null,
            "company_name":null
         },
         "urls":{  
            "notification":"",
            "cancelation":"",
            "processing":"",
            "success":""
         },
         "products":[  
            {  
               "id":44556,
               "transaction_id":77885,
               "code":"00",
               "description":"Tansação: 77885",
               "quantity":"1.0",
               "price_unit":"230.0",
               "weight":"0.0",
               "shipping_cost":"0.0",
               "created_at":"2017-09-20T21:43:27.000-03:00",
               "updated_at":"2017-09-20T21:43:27.000-03:00",
               "url_img":null
            }
         ]
      }      
   ],
   "meta":{  
      "current_page":1,
      "per_page":20,
      "total_pages":953,
      "total_count":19043
   }
}
```