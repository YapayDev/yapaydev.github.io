---
title: API de Consulta de Transação
position: 8
menu: intermediador
right_code: |
  ~~~ php
    <?php
        /* Token da Conta do Lojista */
        $data['token_account'] = 'SEU_TOKEN_AQUI';

        /* Token da Transação */
        $data['token_transaction'] = '### Token da Transação ###';

        $url = "https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/get_by_token";

        ob_start();

        $ch = curl_init();
        curl_setopt($ch, CURLOPT_URL, $url);
        curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "GET");
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
    "method": "GET",
    "hostname": "api.intermediador.sandbox.yapay.com.br",
    "port": null,
    "path": "/api/v3/transactions/get_by_token?token_account=SEU_TOKEN&token_transaction=67601a9a50b90e05187d602ecb1f12",
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

    req.write(JSON.stringify({}));
    req.end();

  ~~~
  {: title="NodeJS" }    

  ~~~ ruby
    require 'uri'
    require 'net/http'

        url = URI("https://api.sandbox.yapay.com.br/api/v3/transactions/get_by_token?token_account=TOKEN&token_transaction=87408ed3f0a5a98790aa00fba90c03eb")


        http = Net::HTTP.new(url.host, url.port)

        http.use_ssl = true

        request = Net::HTTP::Get.new(url)
        request["Accept"] = 'application/json'
        request["Content-Type"] = 'application/json'

        response = http.request(request)

        puts response.read_body
  ~~~
  {: title="Ruby" }


  ~~~ java
    HttpResponse<String> response = Unirest.get("https://api.sandbox.yapay.com.br/api/v3/transactions/get_by_token?token_account=TOKEN&token_transaction=87408ed3f0a5a98790aa00fba90c03eb")
        .body("{}")
        .asString();    
  ~~~
  {: title="Java" }

  ~~~ c#
    var client = new RestClient("https://api.sandbox.yapay.com.br/api/v3/transactions/get_by_token?token_account=TOKEN&token_transaction=87408ed3f0a5a98790aa00fba90c03eb");
    var request = new RestRequest(Method.GET);
    request.AddParameter("undefined", "{}", ParameterType.RequestBody);
    IRestResponse response = client.Execute(request);
  ~~~
  {: title="C#" }

  ~~~ shell
    curl --request GET \
        --url 'https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/get_by_token?token_account=SEU_TOKEN&token_transaction=cb22c716c80ddbaa16f8b8dbc49302a2' \
        --data '{}'
  ~~~
  {: title="Shell - cURL" }  
---

<span class="get">GET</span><span class="beforePost">/api/v3/transactions/get_by_token</span>

O Yapay disponibiliza um recurso para a consulta da transação. Com este recurso, você poderá realizar a consulta para obter as informações detalhadas da transação, e assim comparar as informações e atualizar o status do pedido com segurança.

Para esta integração, deverá ser feito uso da API a seguir:

| Endereço para Integração                                                                            |
|--------------------------|--------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/get_by_token |
| Ambiente de Produção     | http://api.intermediador.yapay.com.br/v3/transactions/get_by_token             |
| Protocolo                | Rest/HTTP                                                                |


Para a integração via <span class="get">GET</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada                       |  Obrig.  | Formato / Tam. Max   | Descrição                                                |
|----------------------------------------|----------|----------------------|----------------------------------------------------------|
| token_account                          |   Sim    |  Texto / 15          |  Token de identificação do vendedor                      |         
| token_transaction                      | Sim      |  Texto / 32          |  Token de identificação da transação                     |


Veja ao lado uma chamada de exemplo da API de Consulta de Transação.

Exemplo de resposta com sucesso baseando no envio do exemplo:

```json
{
    "message_response": {
        "message": "success"
    },
    "data_response": {
        "transaction": {
            "order_number": "79690",
            "free": "Campo Livre",
            "transaction_id": 79690,
            "status_name": "Aprovada",
            "status_id": 6,
            "token_transaction": "cb22c716c80ddbaa16f8b8dbc49302a2",
            "payment": {
                "price_original": "142.0",
                "price_payment": "147.69",
                "payment_response": "Autorização aprovada",
                "url_payment": "",
                "tid": "10347871500026BF1001",
                "split": 3,
                "payment_method_id": 4,
                "payment_method_name": "Mastercard",
                "linha_digitavel": null
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
                        "value": "1133221122",
                        "type_contact": "H"
                    },
                    {
                        "value": "11999999999",
                        "type_contact": "M"
                    }
                ]
            }
        }
    }
}

```



Exemplo de um retorno com erro:

```json
{
    "message_response": {
        "message": "error"
    },
    "error_response": {
        "general_errors": [
            {
                "code": "001001",
                "message": "Token inválido ou não encontrado"
            }
        ]
    }
}
```

As mensagens de erros retornados pela API estão listadas na tabela abaixo:

| Código    |  Mensagem                                        |
|-----------|--------------------------------------------------|
| 001001    | Token inválido ou não encontrado                 |
| 003041    | O Token da Transação não pode ficar em branco    |
| 003042    | Transação não encontrada                         |


Tabelas Auxiliares
{: .subtitulo }

Na integração existem alguns campos com informações pré-definidas, onde deverão ser enviadas conforme o padrão existente, se for necessário enviar o campo na requisição, ou poderá tratar a informação conforme retorno recebido.

Abaixo segue tabelas com essas informações pré-definidas:


| Tabela 1 – Formas de Contato  |
|--------------|------|
| Residencial  | H    |
| Celular      | M    |
| Comercial    | W    |


| Tabela 2 – Formas de Pagamento       |
|---------------------------------|----|
| Cartões de Crédito              |    |
| Diners Club                     | 2  |
| Visa                            | 3  |
| Mastercard                      | 4  |
| American Express                | 5  |
| Discover                        | 15 |
| Elo                             | 16 |
| Aura                            | 18 |
| JCB                             | 19 |
| Hipercard                       | 20 |
| Hiper (Itaú)                    | 25 |
| Transferências Online           |    |
| Itaú Shopline                   | 7  |
| Peela                           | 14 |
| Transf. Online Bradesco         | 22 |
| Transf. Online Banco do Brasil  | 23 |
| Boleto Bancário                 |    |
| Boleto Bancário                 | 6  |


| Tabela 3 – Status da Transação       |
|---------------------------------|----|
| Aguardando Pagamento            | 4  |
| Em Processamento                | 5  |
| Aprovada                        | 6  |
| Cancelada                       | 7  |
| Em Contestação                  | 24 |
| Em Monitoramento                | 87 |
| Em Recuperação                  | 88 |
| Reprovada                       | 89 |

<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>