---
title: API de Cadastro de Cliente
position: 10
menu: intermediador
right_code: |
  ~~~ php
    <?php
        /* Tipo de Conta */ 
        $params['account_type'] = '2';

        /* Dados do Cliente */ 
        $params['email'] = 'emaildo@cliente.com.br'; 
        $params['name'] = 'Nome do Cliente';
        $params['birth_date'] = '21/12/1985'; 
        $params['cpf'] = '98489882380'; 
        $params['relationship'] = 'S'; 
        $params['gender'] = 'M'; 

        /* Dados de Contato */ 
        $params['contacts[][type_contact]'] = 'H'; 
        $params['contacts[][number_contact]'] = '1133120001'; 

        /* Dados de Endereço */
        $params['type_address'] = 'B'; 
        $params['street'] = 'Av Paulista'; 
        $params['number'] = '112'; 
        $params['completion'] = 'A';
        $params['neighborhood'] = 'Centro'; 
        $params['postal_code'] = '04001001'; 
        $params['city'] = 'Sao Paulo'; 
        $params['state'] = 'SP'; 

        /* Dados adicionais de Pessoa Juridica */ 
        $params['trade_name'] = 'Nome Fantasia da Empresa'; 
        $params['company_name'] = 'Razao Social LTDA'; 
        $params['cnpj'] = '38509294000154'; 
        $params['inscricao_municipal'] = '803532446070'; 

        /* Dados de Configuração */ 
        $params['url'] = 'http://www.loja.com.br/'; 
        $params['url_notification'] = 'http://www.loja.com.br/notificacao/'; 
        $params['url_css'] = 'http://www.loja.com.br/style.css'; 
        $params['payment_tax_code'] = '1';
        $params['reseller_token'] = '1';

        $urlPost = "https://api.intermediador.sandbox.yapay.com.br/v1/people/create"; 

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
        String url = "https://api.intermediador.sandbox.yapay.com.br/v1/people/create";
        
        HttpClient client = new HttpClient();
        PostMethod method = new PostMethod(url);
        
        method.getParams().setParameter(HttpMethodParams.RETRY_HANDLER, 
            new DefaultHttpMethodRetryHandler(3, false));
        byte[] responseBody = null;

        try {
            NameValuePair[] data = {
                /* Tipo de Conta */
                new NameValuePair("account_type", "2"),
            
                /* Dados do Cliente */
                new NameValuePair("email", "emaildo@cliente.com.br"),
                new NameValuePair("name", "Nome do Cliente"),
                new NameValuePair("birth_date", "21/12/1985"),
                new NameValuePair("cpf", "98489882380"),
                new NameValuePair("relationship", "S"),
                new NameValuePair("gender", "M"),
            
                /* Dados de Contato */
                new NameValuePair("contacts[][type_contact]", "H"),
                new NameValuePair("contacts[][number_contact]", "1133120001"),
            
                /* Dados de Endereço */
                new NameValuePair("type_address", "B"),
                new NameValuePair("street", "Av Paulista"),
                new NameValuePair("number", "112"),
                new NameValuePair("completion", "A"),
                new NameValuePair("neighborhood", "Centro"),
                new NameValuePair("postal_code", "04001001"),
                new NameValuePair("city", "Sao Paulo"),
                new NameValuePair("state", "SP"),

                /* Dados adicionais de Pessoa Juridica */
                new NameValuePair("trade_name", "Nome Fantasia da Empresa"),
                new NameValuePair("company_name", "Razao Social LTDA"),
                new NameValuePair("cnpj", "38509294000154"),
                new NameValuePair("inscricao_municipal", "803532446070"),

                /* Dados de Configuração */
                new NameValuePair("url", "http://www.loja.com.br/"),
                new NameValuePair("url_notification", "http://www.loja.com.br/notificacao/"),
                new NameValuePair("url_css", "http://www.loja.com.br/style.css"),
                new NameValuePair("payment_tax_code", "1"),
                new NameValuePair("reseller_token", "1")
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
        string URLAuth = "https://api.intermediador.sandbox.yapay.com.br/v1/people/create";
        
        NameValueCollection queryParameters = new NameValueCollection();
        
        /* Tipo de Conta */
        queryParameters.Add("account_type", "2");
        
        /* Dados do Cliente */
        queryParameters.Add("email", "emaildo@cliente.com.br");
        queryParameters.Add("name", "Nome do Cliente");
        queryParameters.Add("birth_date", "21/12/1985");
        queryParameters.Add("cpf", "98489882380");
        queryParameters.Add("relationship", "S");
        queryParameters.Add("gender", "M");
        
        /* Dados de Contato */
        queryParameters.Add("contacts[][type_contact]", "H");
        queryParameters.Add("contacts[][number_contact]", "1133120001");
        
        /* Dados de Endereço */
        queryParameters.Add("type_address", "B");
        queryParameters.Add("street", "Av Paulista");
        queryParameters.Add("number", "112");
        queryParameters.Add("completion", "A");
        queryParameters.Add("neighborhood", "Centro");
        queryParameters.Add("postal_code", "04001001");
        queryParameters.Add("city", "Sao Paulo");
        queryParameters.Add("state", "SP");

        /* Dados adicionais de Pessoa Juridica */
        queryParameters.Add("trade_name", "Nome Fantasia da Empresa");
        queryParameters.Add("company_name", "Razao Social LTDA");
        queryParameters.Add("cnpj", "38509294000154");
        queryParameters.Add("inscricao_municipal", "803532446070");

        /* Dados de Configuração */
        queryParameters.Add("url", "http://www.loja.com.br/");
        queryParameters.Add("url_notification", "http://www.loja.com.br/notificacao/");
        queryParameters.Add("url_css", "http://www.loja.com.br/style.css");
        queryParameters.Add("payment_tax_code", "1");
        queryParameters.Add("reseller_token", "1");
        
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

<span class="post">POST</span><span class="beforePost">/v1/people/create</span>

O Yapay permite a criação de contas para auxiliar no processo de integração.

Através da API de Cadastro de Cliente é possível criar clientes do tipo Pessoa Física ou Pessoa Jurídica, onde são retornados os dados do cliente para integração.

| Endereço para Integração                                                                          |
|--------------------------|------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/v1/people/create  |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/v1/people/create           |
| Protocolo                | Rest/HTTP                                                              |


Para a integração via <span class="post">POST</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada           |  Obrig.         | Formato / Tam. Max   | Descrição                      |
|----------------------------|-----------------|----------------------|--------------------------------|
| account_type               | Sim             | Número               | Tipo de Conta (Tabela 1)       |
| trade_name                 | Sim<sup>2</sup> | Texto                | Nome Fantasia                  |
| company_name               | Sim<sup>2</sup> | Texto                | Razão Social                   |
| cnpj                       | Sim<sup>2</sup> | Texto                | CNPJ                           |
| url                        | Não             | Texto                | Url da Empresa                 |
| url_notification           | Não             | Texto                | Url de Notificação             |
| inscricao_municipal        | Não             | Texto                | Inscrição Municipal            |
| url_css                    | Não             | Texto                | Configuração da URL CSS        |
| email                      | Sim             | Texto                | E-mail                         |
| name                       | Sim             | Texto                | Nome Completo                  |
| birth_date                 | Não             | Data                 | Data de Aniversário            |
| cpf                        | Sim             | Texto                | CPF                            |
| relationship               | Não             | Texto                | Estado Civil (Tabela 2)        |
| gender                     | Não             | Texto                | Sexo (Tabela 3)                |
| contacts[][type_contact]   | Sim             | Texto                | Tipo de Contato<sup>1</sup> (Tabela 4)    |
| contacts[][number_contact] | Sim             | Texto                | Número de telefone<sup>1</sup> |
| type_address               | Sim             | Texto                | Tipo de endereço (Tabela 5)    |
| street                     | Sim             | Texto                | Logradouro                     |
| number                     | Sim             | Texto                | Número                         |
| neighborhood               | Sim             | Texto                | Bairro                         |
| completion                 | Não             | Texto                | Complemento                    |
| postal_code                | Sim             | Texto                | CEP                            |
| city                       | Sim             | Texto                | Cidade                         |
| state                      | Sim             | Texto                | Estado                         |
| payment_tax_code           | Não             | Número               | Código Tabela de Taxas         |
| reseller_token             | Não             | Texto                | Token do Revendedor            |
| password                   | Não             | Texto                | Senha do cliente para acessar o painel |



<sup>1</sup> Note que nas informações acima que alguns dados possuem uma característica diferente, tendo um elemento [] dentro de sua formatação. Isso ocorre justamente para permitir que sejam enviados diversos itens na mesma requisição.
{:.info}

<sup>2</sup> Campos obrigatórios para conta do tipo empresa.
{:.info}


Veja ao lado uma chamada de API de exemplo.

JSON de Resposta
{: .subtitulo }

A API de Cadastro de Cliente retorna a resposta em XML.


Exemplo de resposta com sucesso baseando no envio do exemplo acima:

```xml
    <people>
        <message_response>
            <message>success</message>
        </message_response>
        <data_response>
            <session_id>4c5b02aae656ncab9c80cfe27ec7fc1b</session_id>
            <token_account>0c052fa25j7e312</token_account>
            <customer_name>Nome do Cliente</customer_name>
            <customer_address_id type="integer">138982</customer_address_id>
            <email>emaildo@cliente.com.br</email>
        </data_response>
    </people>
```


Mensagens de Erro
{: .subtitulo }

No caso de erro, a API retorna uma mensagem de erro. Assim é possível identificar o erro ocorrido e realizar o tratamento através do código e/ou mensagem retornada.

Abaixo segue os detalhes de cada nó do XML de resposta:


```xml
    <people>
        <message_response>
            <message>error</message>
        </message_response>
        <error_response>
            <validation_errors type="array">
                <validation_error>
                    <code>3</code>
                    <message>não é válido</message>
                    <field>cpf</field>
                    <message_complete>CPF não é válido</message_complete>
                </validation_error>
            </validation_errors>
        </error_response>
    </people>
```


As mensagens de erros retornados pela API estão listadas na tabela abaixo:

| Código    | Mensagem                |
|-----------|-------------------------|
|  036004   | Cliente não encontrado  |
|  036010   | Tipo de Conta inválido  |
|  058001   | Revendedor inválido.    |




Tabelas Auxiliares
{: .subtitulo }

Na integração existem alguns campos com informações pré-definidas, onde deverão ser enviadas conforme o padrão existente, se for necessário enviar o campo na requisição, ou poderá tratar a informação conforme retorno recebido.

Abaixo segue tabelas com essas informações pré-definidas:

| Tabela 1 – Tipos de Conta  |
|--------------|------|
| Pessoal      | 1    |
| Empresarial  | 2    |


| Tabela 2 – Estado Civil  |
|-------------|------|
| Solteiro    | S    |
| Casado      | M    |
| Separado    | A    |
| Divorciado  | D    |
| Viúvo       | W    |


| Tabela 3 – Gênero  |
|-----------|------|
| Masculino | M    |
| Feminino  | F    |

| Tabela 4 – Contato  |
|-------------|------|
| Residencial | H    |
| Celular     | M    |
| Comercial   | W    |


| Tabela 5 – Tipo de Endereço  |
|-----------|------|
| Cobrança  | B    |
| Entrega   | D    |



<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>