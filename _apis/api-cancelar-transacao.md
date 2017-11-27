---
title: API Cancelar Transação
position: 6
menu: intermediador
right_code: |
  ~~~ php
    <?php
        $data['access_token'] = '### Access Token do Vendedor ###';

        $data["transaction_id"] = 79717;
        $data["reason_cancellation_id"] = 6;       

        $url = "https://api.sandbox.traycheckout.com.br/api/v3/transactions/cancel";

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

        if($code == "201"){
            //Tratamento dos dados de resposta da consulta.
        }else{
            //Tratamento das mensagens de erro
        }
    ?>
  ~~~
  {: title="PHP" }

  ~~~ java
    ...
    String url = "https://api.sandbox.traycheckout.com.br/api/v3/transactions/cancel";
     
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
    
    string URLAuth = "https://api.sandbox.traycheckout.com.br/api/v3/transactions/cancel";
    
    NameValueCollection queryParameters = new NameValueCollection();
    
    queryParameters.Add("token_account", "### Access Token do Vendeor ###");
        
    queryParameters.Add("transaction_id", "79717");
    queryParameters.Add("reason_cancellation_id", "6");
    
    List<string> items = new List<string>();
    
    foreach (String name in queryParameters)
        items.Add(String.Concat(name, "=", System.Web.HttpUtility.UrlEncode(queryParameters[name])));
    
    string postString = String.Join("&", items.ToArray());
    
    const string contentType = "application/json";
    System.Net.ServicePointManager.Expect100Continue = false;
    
    CookieContainer cookies = new CookieContainer();
    HttpWebRequest webRequest = WebRequest.Create(URLAuth) as HttpWebRequest;
    webRequest.Method = "PATCH";
    webRequest.ContentType = contentType;   
    webRequest.CookieContainer = cookies;
    webRequest.ContentLength = postString.Length; 
    webRequest.Accept = "text/html,application/json;q=0.9,*/*;q=0.8";
    
    StreamWriter requestWriter = new StreamWriter(webRequest.GetRequestStream());
    requestWriter.Write(postString);
    requestWriter.Close();
    
    StreamReader responseReader = new StreamReader(webRequest.GetResponse().GetResponseStream());
    string responseData = responseReader.ReadToEnd();
    
    responseReader.Close();
    webRequest.GetResponse().Close();
    
    ... 
  ~~~
  {: title="C#" }    

---

<span class="patch">PATCH</span><span class="beforePost">/api/v3/transactions/cancel</span>


O Yapay disponibiliza uma versão transparente para cancelamento de transações, permitindo que seja cancelada a transação de forma transparente. 

Através do access_token e o id da transação, é possivel realizar um PATCH na API de Cancelamento de Transação. Lembrando que o access_token você pega utilizando a API de Autorização.


| Endereço para Integração                                                                          |
|--------------------------|------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.sandbox.traycheckout.com.br/api/v3/transactions/cancel   |
| Ambiente de Produção     | https://api.traycheckout.com.br/api/v3/transactions/cancel           |
| Protocolo                | Rest                                                              |


Para a integração via POST, segue abaixo os dados necessários para envio:

| Dados de Entrada                       |  Obrig.  | Descrição                                  |
|----------------------------------------|----------|--------------------------------------------|
| access_token                           |   Sim    |  Access Token de identificação do vendedor |
| transaction_id                         |   Sim    |  ID da Transação                           |
| reason_cancellation_id                 |   Sim    |  Motivo Cancelamento<sup>1</sup>           |

<sup>1</sup> Essa opção é necessário informar o motivo `6`. O Motivo 6 é relacionado ao **CANCELAMENTO PELA LOJA**, as outras opções são relacionadas ao cancelamento feito pelo cliente.
{:.info}



Veja ao lado uma chamada de API de exemplo.

JSON de Resposta
{: .subtitulo }

A API de Processamento de Transações retorna a resposta em JSON.


Exemplo de resposta com sucesso baseando no envio do exemplo acima:

```json
{  
   "access_token":"SEU_ACCESS_TOKEN",
   "transaction_id": 79717,
   "reason_cancellation_id": "6"
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

