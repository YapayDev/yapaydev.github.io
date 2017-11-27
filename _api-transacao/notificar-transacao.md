---
title: Notificar a transação
position: 5
menu: gateway
right_code: |
  ~~~ php
    <?php

    $username   = "diana@amazonas.com";
    $password   = "SEU_TOKEN";

    $url = "https://gtw.sandbox.checkout.tray.com.brapi/v1/transactions/8b1195bba1e2993777e1f71f18530f2d";

    $ch = curl_init();

    curl_setopt($ch, CURLOPT_URL, $url);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($ch, CURLOPT_SSLVERSION, 1);
    curl_setopt($ch, CURLOPT_HTTP_VERSION, CURL_HTTP_VERSION_1_1);
    curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");   
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

        url = URI("https://gtw.sandbox.checkout.tray.com.br/api/v1/transactions/8b1195bba1e2993777e1f71f18530f2d")


        http = Net::HTTP.new(url.host, url.port)

        http.use_ssl = true

        request = Net::HTTP::Post.new(url)
        request["Accept"] = 'application/json'
        request["Content-Type"] = 'application/json'
        request["Authorization"] = 'Basic SEU_TOKEN'


        response = http.request(request)

        puts response.read_body
  ~~~
  {: title="Ruby"}

  ~~~java
    var client = new RestClient("https://gtw.sandbox.checkout.tray.com.br/api/v1/transactions/8b1195bba1e2993777e1f71f18530f2d");
    var request = new RestRequest(Method.POST);
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

<span class="post">POST</span><span class="beforePost">/api/v1/transactions/</span>

O método de **Notificar Transação** possui os seguintes parâmetros:

| Parâmetro    | Formato  | Descrição                      |
|---------------------|----------|-------------------------|
| authorization       | Texto    | Token de autenticação   |
| id                  | Número   | ID do pedido            |

Ao lado você consegue visualizar um exemplo de requisição.

Observe que na URL está sendo informado o parâmetro `ID DO PEDIDO`. 

Exemplo de URL: `https://gtw.sandbox.checkout.tray.com.br/api/v1/transactions/f862781748917fba108cd7b1fb17014e`
