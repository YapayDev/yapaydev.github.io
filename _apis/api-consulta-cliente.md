---
title: API de Consulta de Cliente
position: 11
menu: intermediador
right_code: |
  ~~~ php
    <?php
        /* Tipo de Conta */ 
        $params['access_token'] = 'SEU ACCESS_TOKEN';

        
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
                /* Tipo de Conta */
                new NameValuePair("access_token", "SEU ACCESS_TOKEN"),
            
                /* Dados do Cliente */
                new NameValuePair("cpf", "CPF"),

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
        
        /* Tipo de Conta */
        queryParameters.Add("access_token", "SEU ACCESS_TOKEN");
        
        /* Dados do Cliente */
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


Para a integração via POST, segue abaixo os dados necessários para envio:

| Dados de Entrada           |  Obrig.         | Formato / Tam. Max   | Descrição                      |
|----------------------------|-----------------|----------------------|--------------------------------|
| access_token               | Sim             | Número               | Token de Acesso                |
| cpf                        | Sim             | Texto                | CPF<sup>1</sup>                |
| email                      | Sim             | Texto                | E-mail<sup>1</sup>             |




<sup>1</sup> Enviando o `cpf` ou o `email` a consulta é simples. Enviando ambos os parâmetros a consulta é completa.
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
            <name>Diana Prince</name>
            <cpf>161.XXX.X36-XX</cpf>
            <email>dianeprince@amazonas.com</email>
            <has_card type="boolean">true</has_card>
            <company nil="true"/>
            <account>
                <token_account>6k63b0a42dd2fe0</token_account>
                <balance type="decimal">10.0</balance>
                <balance_transacted type="decimal">40.0</balance_transacted>
                <account_type_id type="integer">1</account_type_id>
                <status_id type="integer">2</status_id>
                <status_name>Ativo</status_name>
                <verified type="boolean">false</verified>
                <account_verification>
                    <status_id type="integer">94</status_id>
                    <status_name>Novo</status_name>
                </account_verification>
            </account>
            <addresses type="array">
                <address>
                    <person_address_id type="integer">136424</person_address_id>
                    <street>Avenida Esmeralda</street>
                    <number>570</number>
                    <type_address>B</type_address>
                    <neighborhood>Jardim Esmeralda</neighborhood>
                    <postal_code>17516000</postal_code>
                    <completion></completion>
                    <city>Marília</city>
                    <state>SP</state>
                    <primary type="boolean">true</primary>
                </address>
                <address>
                    <person_address_id type="integer">137723</person_address_id>
                    <street>Avenida Esmeralda</street>
                    <number>570</number>
                    <type_address>B</type_address>
                    <neighborhood>Jardim Esmeralda</neighborhood>
                    <postal_code>17516000</postal_code>
                    <completion></completion>
                    <city>Marília</city>
                    <state>SP</state>
                    <primary type="boolean">false</primary>
                </address>
                <address>
                    <person_address_id type="integer">137780</person_address_id>
                    <street>B</street>
                    <number>123</number>
                    <type_address>B</type_address>
                    <neighborhood>Sé</neighborhood>
                    <postal_code>17525181</postal_code>
                    <completion></completion>
                    <city>Marilia</city>
                    <state>SP</state>
                    <primary type="boolean">false</primary>
                </address>
            </addresses>
            <contacts type="array">
                <contact>
                    <person_contact_id type="integer">244567</person_contact_id>
                    <value>1499999999</value>
                    <type_contact>M</type_contact>
                    <primary type="boolean">true</primary>
                </contact>
                <contact>
                    <person_contact_id type="integer">244568</person_contact_id>
                    <value>dianeprince@amazonas.com</value>
                    <type_contact>E</type_contact>
                    <primary type="boolean">false</primary>
                </contact>
                <contact>
                    <person_contact_id type="integer">246836</person_contact_id>
                    <value>1433114455</value>
                    <type_contact>H</type_contact>
                    <primary type="boolean">false</primary>
                </contact>
            </contacts>
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