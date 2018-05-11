---
title: API de Consulta de Cliente
position: 11
menu: intermediador
right_code: |
  ~~~ php
    <?php
        
        $params['cpf'] = '';         

        $urlPost = "https://api.intermediador.sandbox.yapay.com.br/v1/people/get_person_by_cpf_and_email"; 

        ob_start(); 

        $ch = curl_init(); 
        curl_setopt($ch, CURLOPT_URL, $urlPost); 
        curl_setopt($ch, CURLOPT_POST, 1); 
        curl_setopt($ch, CURLOPT_POSTFIELDS, $params); 
        curl_exec($ch); 

        /* XML de retorno */ 
        $resposta = simplexml_load_string(ob_get_contents()); 

        ob_end_clean(); 
        curl_close($ch); 

        if ($resposta->message_response->message == "success"){ 
           //Tratamento dos dados de resposta da consulta. 
        }else{ 
           //Tratamento das mensagens de erro 
        } 
    ?>
  ~~~
  {: title="PHP" }

  ~~~ java
        ...
        String url = "https://api.intermediador.sandbox.yapay.com.br/v1/people/get_person_by_cpf_and_email";
        
        HttpClient client = new HttpClient();
        PostMethod method = new PostMethod(url);
        
        method.getParams().setParameter(HttpMethodParams.RETRY_HANDLER, 
            new DefaultHttpMethodRetryHandler(3, false));
        byte[] responseBody = null;

        try {
            NameValuePair[] data = {
            
                /* Dados do Cliente */
                new NameValuePair("cpf", "CPF")

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
        String xmlResposta = new String(responseBody);
    ... 
        
  ~~~
  {: title="Java" }

  ~~~ c#
    ...
        string URLAuth = "https://api.intermediador.sandbox.yapay.com.br/v1/people/get_person_by_cpf_and_email";
        
        NameValueCollection queryParameters = new NameValueCollection();
        
        queryParameters.Add("cpf", "CPF");
        
        List<string> items = new List<string>();
        
        foreach (String name in queryParameters)
            items.Add(String.Concat(name, "=", System.Web.HttpUtility.UrlEncode(queryParameters[name])));
        
        string postString = String.Join("&", items.ToArray());
        
        const string contentType = "application/x-www-form-urlencoded";
        System.Net.ServicePointManager.Expect100Continue = false;
        
        CookieContainer cookies = new CookieContainer();
        HttpWebRequest webRequest = WebRequest.Create(URLAuth) as HttpWebRequest;
        webRequest.Method = "POST";
        webRequest.ContentType = contentType;   
        webRequest.CookieContainer = cookies;
        webRequest.ContentLength = postString.Length; 
        webRequest.Accept = "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8";
        
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

<span class="post">POST</span><span class="beforePost">/v1/people/get_person_by_cpf_and_email</span>

O Yapay permite a consulta de contas para auxiliar no processo de integração.

Através da API de Consulta de Cliente é possível criar clientes do tipo Pessoa Física ou Pessoa Jurídica, onde são retornados os dados do cliente para integração.

| Endereço para Integração                                                                          |
|--------------------------|------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/v1/people/get_person_by_cpf_and_email  |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/v1/people/get_person_by_cpf_and_email           |
| Protocolo                | Rest/HTTP                                                              |


Para a integração via <span class="post">POST</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada           |  Obrig.         | Formato / Tam. Max   | Descrição                      |
|----------------------------|-----------------|----------------------|--------------------------------|
| cpf                        | Sim             | Texto                | CPF<sup>1</sup>                |
| email                      | Sim             | Texto                | E-mail<sup>1</sup>             |




<sup>1</sup> Um dos parâmetros é obrigatório, `cpf` ou o `email`.
{:.info}


Veja ao lado uma chamada de API de exemplo.

JSON de Resposta
{: .subtitulo }

A API de Consulta de Clientes simples retorna a resposta em XML.


Exemplo de resposta com sucesso baseando no envio do exemplo acima:

```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <people>
        <data_response>
            <name>Diane Prince</name>
            <cpf>231.XXX.X65-XX</cpf>
            <email>anava@tray.net.br</email>
            <has_card type="boolean">true</has_card>
            <company nil="true"/>
        </data_response>
        <message_response>
            <message>success</message>
        </message_response>
    </people>
```


Mensagens de Erro
{: .subtitulo }

No caso de erro, a API retorna uma mensagem de erro. Assim é possível identificar o erro ocorrido e realizar o tratamento através do código e/ou mensagem retornada.

Abaixo segue os detalhes de cada nó do XML de resposta:


```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <people>
        <error_response>
            <errors type="array">
                <error>
                    <message>Cliente não encontrado</message>
                    <code>036004</code>
                </error>
            </errors>
        </error_response>
        <message_response>
            <message>error</message>
        </message_response>
    </people>
```


As mensagens de erros retornados pela API estão listadas na tabela abaixo:

| Código    | Mensagem                |
|-----------|-------------------------|
|  036004   | Cliente não encontrado  |


<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>