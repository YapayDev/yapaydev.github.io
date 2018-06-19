---
title: API de Cancelar Transação
position: 6
menu: intermediador
right_code: |
  ~~~ php
    <?php
        $data['access_token'] = '### Access Token do Vendedor ###';

        $data["transaction_id"] = 79717;
        $data["reason_cancellation_id"] = 6;       

        $url = "https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/cancel";

        ob_start();

        $ch = curl_init();
        curl_setopt($ch, CURLOPT_URL, $url);
        curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "PATCH");
        curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
        curl_setopt($ch, CURLOPT_HTTPHEADER, array('Content-Type: application/json'));

        curl_exec($ch);

        // JSON de retorno  
        $resposta = json_decode(ob_get_contents());
        $code = curl_getinfo($ch, CURLINFO_HTTP_CODE);

        ob_end_clean();
        curl_close($ch);

        if($code == "200"){
            //Tratamento dos dados de resposta da consulta.
        }else{
            //Tratamento das mensagens de erro
        }
    ?>
  ~~~
  {: title="PHP" }

  ~~~ javascript
    var http = require("https");

    var options = {
    "method": "PATCH",
    "hostname": "api.intermediador.sandbox.yapay.com.br",
    "path": "/api/v3/transactions/cancel",
    "headers": {
        "content-type": "application/json"
    }
    };

    var req = http.request(options, function (res) {
    var chunks = [];

    res.on("data", function (chunk) {
        chunks.push(chunk);
    });

    res.on("end", function () {
        var body = Buffer.concat(chunks);
        console.log(body.toString());
    });
    });

    req.write(JSON.stringify({ 
        access_token: 'SEU_ACCESS_TOKEN', 
        transaction_id: '83584', 
        reason_cancellation_id: '6' 
    }));

    req.end();
  ~~~
  {: title="NodeJS" }    

  ~~~ java
    ...
    String url = "https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/cancel";
     
    HttpClient client = new HttpClient();
    PostMethod method = new PostMethod(url);
    
    method.getParams().setParameter(HttpMethodParams.RETRY_HANDLER, 
        new DefaultHttpMethodRetryHandler(3, false));
    byte[] responseBody = null;

    try {
        NameValuePair[] data = {
            /* Token da Conta do Lojista */
            new NameValuePair("access_token", "### Access Token do Vendedor ###"),
            
            new NameValuePair("transaction_id", "79717"),
            new NameValuePair("reason_cancellation_id", "6")           
            
        };

        method.setRequestBody(data);

        // Execute the method.
        int statusCode = client.executeMethod(method);

        if (statusCode != HttpStatus.SC_OK) {
            System.err.println("Method failed: " + method.getStatusLine());
        }
        
        responseBody = method.getResponseBody();
        
    } catch (HttpException e) {
        e.printStackTrace();
    } catch (IOException e) {
        e.printStackTrace();
    } finally {
        method.releaseConnection();
    }

    String jsonResponse = new String(responseBody);

    ... 
  ~~~
  {: title="Java" }

  ~~~ c#
    ...
    
    var client = new RestClient("https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/cancel");
    var request = new RestRequest(Method.PATCH);
    
    request.AddHeader("content-type", "application/json");
    request.AddParameter("application/json", "{\"access_token\":\"ACCESS_TOKEN_VENDEDOR\",\"transaction_id\":\"79717\",\"reason_cancellation_id\":\"6\"}", ParameterType.RequestBody);
    IRestResponse response = client.Execute(request);
    
    ... 
  ~~~
  {: title="C#" }    


  ~~~ json
    {  
        "access_token":"SEU_ACCESS_TOKEN",
        "transaction_id": 79717,
        "reason_cancellation_id": "6"
    }
  ~~~  
  {: title="JSON" }    
---

<span class="patch">PATCH</span><span class="beforePost">/api/v3/transactions/cancel</span>


O Yapay disponibiliza uma versão transparente para cancelamento de transações, permitindo que seja cancelada a transação de forma transparente. 

Através do access_token e o id da transação, é possivel realizar um <span class="patch">PATCH</span> na API de Cancelamento de Transação. Lembrando que o access_token você pega utilizando a API de Autorização.


| Endereço para Integração                                                                          |
|--------------------------|------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/cancel   |
| Ambiente de Produção     | http://api.intermediador.yapay.com.br/api/v3/transactions/cancel           |
| Protocolo                | Rest                                                              |



Para a integração via <span class="patch">PATCH</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada                       |  Obrig.  | Descrição                                  |
|----------------------------------------|----------|--------------------------------------------|
| access_token                           |   Sim    |  Access Token de identificação do vendedor |
| transaction_id                         |   Sim    |  ID da Transação                           |
| message_cancellation                   |   Não    |  Mensagem de Cancelamento                  |
| reason_cancellation_id                 |   Sim    |  Motivo Cancelamento<sup>1</sup>           |

<sup>1</sup> Essa opção é necessário informar o motivo `6`. O Motivo 6 é relacionado ao **CANCELAMENTO PELA LOJA**, as outras opções são relacionadas ao cancelamento feito pelo cliente.
{:.info}



Veja ao lado uma chamada de API de exemplo.

JSON de Resposta
{: .subtitulo }

A API de Cancelar de Transações retorna a resposta em JSON.


Exemplo de resposta com sucesso baseando no envio do exemplo acima:

```json
    {
        "message_response": {
            "message": "success"
        },
        "data_response": {
            "transaction": {
                "order_number": "79717",
                "free": "Campo Livre",
                "transaction_id": 79717,
                "status_name": "Cancelada",
                "status_id": 7,
                "token_transaction": "4101779e6b84332c8a31dd730c00b0dc",
                "payment": {
                    "price_original": "142.0",
                    "price_payment": "142.0",
                    "payment_response": "",
                    "url_payment": "https://tc.intermediador.sandbox.yapay.com.br/payment/billet/774b33dd8d4a10809cb370b21d3bd",
                    "tid": null,
                    "split": 1,
                    "payment_method_id": 6,
                    "payment_method_name": "Boleto Bancario",
                    "linha_digitavel": "123123123123123131232131232131313211231321321"
                },
                "customer": {
                    "name": "Diana Prince",
                    "cpf": "37573138792",
                    "email": "dianaprince9834347522@amaf4343sdfdsfdszonas1587.com",
                    "company_name": "",
                    "trade_name": "",
                    "cnpj": "",
                    "addresses": [
                        {
                            "street": "Av Themyscira",
                            "number": "1001",
                            "neighborhood": "Jd das Rochas",
                            "postal_code": "17000000",
                            "completion": "A",
                            "city": "Themyscira",
                            "state": "SP"
                        }
                    ],
                    "contacts": [
                        {
                            "value": "11999999999",
                            "type_contact": "M"
                        },
                        {
                            "value": "4113096901",
                            "type_contact": "H"
                        }
                    ]
                }
            }
        }
    }
```


Mensagens de Erro
{: .subtitulo }

No caso de erro, a API retorna uma mensagem de erro. Assim é possível identificar o erro ocorrido e realizar o tratamento através do código e/ou mensagem retornada.

Abaixo segue o JSON de resposta:


```json
{
    "message_response": {
        "message": "error"
    },
    "error_response": {
        "general_errors": [
            {
                "code": "003005",
                "message": "Transação inválida ou inexistente"
            }
        ]
    }
}
```


As mensagens de erros retornados pela API estão listadas na tabela abaixo:

| Código    |  Mensagem                                        |
|-----------|--------------------------------------------------|
|  003005   |     Transação inválida ou inexistente            |



<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>