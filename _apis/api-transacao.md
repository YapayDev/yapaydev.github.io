---
title: API de Transação
position: 5
menu: intermediador
right_code: |
  ~~~ php
    <?php
        $data['token_account'] = '### Token do Cliente ###';

        $data["customer"]["contacts"][1]["type_contact"] = "H";
        $data["customer"]["contacts"][1]["number_contact"] = "1133221122";
        $data["customer"]["contacts"][2]["type_contact"] = "M";
        $data["customer"]["contacts"][2]["number_contact"] = "11999999999";

        $data["customer"]["addresses"][1]["type_address"] = "B";    
        $data["customer"]["addresses"][1]["postal_code"] = "17000-000";
        $data["customer"]["addresses"][1]["street"] = "Av Themyscira";
        $data["customer"]["addresses"][1]["number"] = "1001";
        $data["customer"]["addresses"][1]["completion"] = "A";
        $data["customer"]["addresses"][1]["neighborhood"] = "Jd das Rochas";
        $data["customer"]["addresses"][1]["city"] = "Themyscira";
        $data["customer"]["addresses"][1]["state"] = "SP";

        $data["customer"]["name"] = "Diana Prince";
        $data["customer"]["birth_date"] = "21/05/1941";
        $data["customer"]["cpf"] = "50235335142";
        $data["customer"]["email"] = "email@cliente.com.br";

        $data["transaction_product"][1]["description"] = "Camiseta Wonder Woman";
        $data["transaction_product"][1]["quantity"] = "1";
        $data["transaction_product"][1]["price_unit"] = "130.00";
        $data["transaction_product"][1]["code"] = "1";
        $data["transaction_product"][1]["sku_code"] = "0001";
        $data["transaction_product"][1]["extra"] = "Informaçã extra";

        $data["transaction"]["available_payment_methods"] = "2,3,4,5,6,7,14,15,16,18,19,21,22,23";   
        $data["transaction"]["order_number"] = "001";   
        $data["transaction"]["customer_ip"] = "127.0.0.1";    
        $data["transaction"]["shipping_type"] = "Sedex";    
        $data["transaction"]["shipping_price"] = "19.80";    
        $data["transaction"]["price_discount"] = "0"; 
        $data["transaction"]["url_notification"] = "http://www.loja.com.br/notificacao/";    
        $data["transaction"]["free"] = "Campo livre";    
        $data["transaction"]["sub_store"] = "LOJA_1";    
      
        $data["payment"]["payment_method_id"] = "6";    


        $url = "https://api.sandbox.traycheckout.com.br/api/v3/transactions/payment";

        ob_start();

        $ch = curl_init();
        curl_setopt($ch, CURLOPT_URL, $url);
        curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
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
    String url = "https://api.sandbox.traycheckout.com.br/api/v3/transactions/payment";
     
    HttpClient client = new HttpClient();
    PostMethod method = new PostMethod(url);
    
    method.getParams().setParameter(HttpMethodParams.RETRY_HANDLER, 
        new DefaultHttpMethodRetryHandler(3, false));
    byte[] responseBody = null;

    try {
        NameValuePair[] data = {
            /* Token da Conta do Lojista */
            new NameValuePair("token_account", "### Token do Cliente ###"),
            
            new NameValuePair("customer[name]", "Diana Prince"),
            new NameValuePair("customer[cpf]", "50235335142"),
            new NameValuePair("customer[email]", "emaildo@cliente.com.br"),
            new NameValuePair("customer[birth_date]", "21/05/1941"),
            new NameValuePair("customer[contacts][][type_contact]", "H"),
            new NameValuePair("customer[contacts][][number_contact]", "1133120001"),
            new NameValuePair("customer[contacts][][type_contact]", "M"),
            new NameValuePair("customer[contacts][][number_contact]", "11999120002"),
            new NameValuePair("customer[addresses][][type_address]", "B"),
            new NameValuePair("customer[addresses][][postal_code]", "17000000"),
            new NameValuePair("customer[addresses][][street]", "Av Themyscira"),
            new NameValuePair("customer[addresses][][number]", "1001"),
            new NameValuePair("customer[addresses][][completion]", "A"),
            new NameValuePair("customer[addresses][][neighborhood]", "Centro"),
            new NameValuePair("customer[addresses][][city]", "São Paulo"),
            new NameValuePair("customer[addresses][][state]", "SP"),
            
            new NameValuePair("transaction[available_payment_methods]", "2,3,4,5,6,7,14,15,16,18,19,21,22,23"),
            new NameValuePair("transaction[order_number]", "0001"),
            new NameValuePair("transaction[customer_ip]", "200.200.200.200"),
            new NameValuePair("transaction[shipping_type]", "Sedex"),
            new NameValuePair("transaction[shipping_price]", "19.80"),
            new NameValuePair("transaction[price_discount]", "7.80"),
            new NameValuePair("transaction[price_additional]", "6.00"),
            new NameValuePair("transaction[url_notification]", "http://www.loja.com.br/notificacao/"),
            new NameValuePair("transaction[free]", "Campo de livre digitação"),
            new NameValuePair("transaction[sub_store]", "LOJA_1"),
            
            new NameValuePair("transaction_product[][description]", "Notebook Preto"),
            new NameValuePair("transaction_product[][quantity]", "1"),
            new NameValuePair("transaction_product[][price_unit]", "321.99"),
            new NameValuePair("transaction_product[][code]", "1"),
            new NameValuePair("transaction_product[][sku_code]", "0001"),
            new NameValuePair("transaction_product[][extra]", "Dados extra do Notebook Preto"),

            /* Dados para Pagamento */
            new NameValuePair("payment[payment_method_id]", "6")
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
    
    string URLAuth = "https://api.sandbox.traycheckout.com.br/api/v3/transactions/payment";
    
    NameValueCollection queryParameters = new NameValueCollection();
    
    queryParameters.Add("token_account", "### Token do Cliente ###");
    
    queryParameters.Add("customer[name]", "Nome do Cliente");
    queryParameters.Add("customer[cpf]", "98489882380");
    queryParameters.Add("customer[email]", "emaildo@cliente.com.br");
    queryParameters.Add("customer[birth_date]", "21/12/1985");
    queryParameters.Add("customer[contacts][][type_contact]", "H");
    queryParameters.Add("customer[contacts][][number_contact]", "1133120001");
    queryParameters.Add("customer[contacts][][type_contact]", "M");
    queryParameters.Add("customer[contacts][][number_contact]", "11999120002");
    queryParameters.Add("customer[addresses][][type_address]", "B");
    queryParameters.Add("customer[addresses][][postal_code]", "04001001");
    queryParameters.Add("customer[addresses][][street]", "Av Paulista");
    queryParameters.Add("customer[addresses][][number]", "112");
    queryParameters.Add("customer[addresses][][completion]", "A");
    queryParameters.Add("customer[addresses][][neighborhood]", "Centro");
    queryParameters.Add("customer[addresses][][city]", "São Paulo");
    queryParameters.Add("customer[addresses][][state]", "SP");

    queryParameters.Add("transaction[available_payment_methods]", "2,3,4,5,6,7,14,15,16,18,19,21,22,23");
    queryParameters.Add("transaction[order_number]", "0001");
    queryParameters.Add("transaction[customer_ip]", "200.200.200.200");
    queryParameters.Add("transaction[shipping_type]", "Sedex");
    queryParameters.Add("transaction[shipping_price]", "19.80");
    queryParameters.Add("transaction[price_discount]", "7.80");
    queryParameters.Add("transaction[price_additional]", "6.00");
    queryParameters.Add("transaction[url_notification]", "http://www.loja.com.br/notificacao/");
    queryParameters.Add("transaction[free]", "Campo de livre digitação");
    queryParameters.Add("transaction[sub_store]", "LOJA_1");

    queryParameters.Add("transaction_product[][description]", "Notebook Preto");
    queryParameters.Add("transaction_product[][quantity]", "1");
    queryParameters.Add("transaction_product[][price_unit]", "321.99");
    queryParameters.Add("transaction_product[][code]", "1");
    queryParameters.Add("transaction_product[][sku_code]", "0001");
    queryParameters.Add("transaction_product[][extra]", "Dados extra do Notebook Preto");

    queryParameters.Add("payment[payment_method_id]", "3");
    queryParameters.Add("payment[split]", "12");
    queryParameters.Add("payment[card_name]", "Nome Impresso no Cartão");
    queryParameters.Add("payment[card_number]", "1234123412341234");
    queryParameters.Add("payment[card_expdate_month]", "01");
    queryParameters.Add("payment[card_expdate_year]", "2016");
    queryParameters.Add("payment[card_cvv]", "123");
    
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

O Yapay disponibiliza uma versão transparente para a integração de transações, permitindo que o usuário efetue o processamento dos pedidos sem necessitar o redirecionamento para outra aplicação e preenchimento de novos formulários.

![Integração Marketplace Yapay](/images/intermediador/conteudo/Integracao_api_LV.png "Integração Marketplace Yapay"){: width="90%" height="auto" }

Através do CPF do cliente é feita a consulta pela existência do seu cadastro e então as transações são atreladas ao mesmo. Caso não exista uma conta, o sistema irá criar uma nova conta com os dados que forem submetidos na integração. Para esta integração, deverá ser feito uso da API a seguir:

Para a integração com a API de Transação, é necessário incluir um script após o processamento da transação, no início da página de finalização da compra. Segue abaixo código do script:

```html
 <script src="https://static.yapay.com.br/js/finger_print.js" type="text/javascript"></script>
```

Além de incluir o script, é necessário realizar a chamada do plugin, no final da mesma página, conforme código javascript abaixo:

```javascript
    jQuery(document).FingerPrint({token_account: 'Token de Integração do Vendedor',
                                  order_number: 'Número do pedido',
                                  production: 'true'});
```

| Endereço para Integração                                                                          |
|--------------------------|------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.sandbox.yapay.com.br/v2/transactions/pay_complete   |
| Ambiente de Produção     | https://api.yapay.com.br/v2/transactions/pay_complete           |
| Protocolo                | Rest/HTTP                                                              |


Para a integração via POST, segue abaixo os dados necessários para envio:

| Dados de Entrada                       |  Obrig.  | Formato / Tam. Max   | Descrição                                                  |
|----------------------------------------|----------|----------------------|------------------------------------------------------------|
| token_account                            |   Sim    |  Texto /20           |  Token de identificação do vendedor                      |
| customer[name]                           |   Sim    |  Texto /100          |  Nome do Comprador                                       |
| customer[cpf]                            |   Sim    |  Texto /14           |  CPF do Comprador                                        |
| customer[email]                          |   Sim    |  Texto /100          |  E-mail do Comprador                                     |
| customer[trade_name]                     |   Não    |  Texto /100          |  Nome Fantasia do Comprador                              |
| customer[company_name]                   |   Não    |  Texto /100          |  Razão Social do Comprador                               |
| customer[cnpj]                           |   Não    |  Texto /18           |  CNPJ do Comprador                                       |
| customer[inscricao_municipal]            |   Não    |  Texto /20           |  Inscrição Municipal do Comprador                        |
| customer[contacts][][type_contact]       |   Sim    |  Texto /1            |  Tipo do Contato <sup>1</sup> (Tabela 1)                 |
| customer[contacts][][number_contact]     |   Sim    |  Texto /10           |  Número do telefone do Comprador                         |
| customer[addresses][][type_address]      |   Sim    |  Texto /1            |  Tipo do Endereço <sup>1</sup> (Tabela 2)                |
| customer[addresses][][postal_code]       |   Sim    |  Texto /8            |  CEP do endereço do Comprador                            |
| customer[addresses][][street]            |   Sim    |  Texto /120          |  Nome da rua do Comprador                                |
| customer[addresses][][number]            |   Sim    |  Texto /10           |  Número do endereço do Comprador                         |
| customer[addresses][][neighborhood]      |   Sim    |  Texto /100          |  Bairro do endereço do Comprador                         |
| customer[addresses][][completion]        |   Não    |  Texto /100          |  Complemento do endereço do Comprador                    |
| customer[addresses][][city]              |   Sim    |  Texto /120          |  Cidade do endereço do Comprador                         |
| customer[addresses][][state]             |   Sim    |  Texto /2            |  Estado do endereço do Comprador                         |
| customer[birth_date]                     |   Não    |  Data / 10           |  Data de aniversário do Comprador                        |
| transaction[available_payment_methods]   |   Não    |  Texto /20           |  Meios de Pagamento disponíveis <sup>2</sup> (Tabela 3)  |
| transaction[order_number]                |   Não    |  Texto /2            |  Número do pedido                                        |
| transaction[customer_ip]                 |   Sim    |  Texto /15           |  IP do Comprador                                         |
| transaction[shipping_type]               |   Não    |  Texto /100          |  Tipo do envio                                           |
| transaction[shipping_price]              |   Não    |  Decimal / 11        |  Preço de Envio. Formato: 0.00                           |
| transaction[price_discount]              |   Não    |  Decimal / 11        |  Valor do desconto. Formato: 0.00                        |
| transaction[price_additional]            |   Não    |  Decimal / 11        |  Valor adicional. Formato: 0.00                          | 
| transaction[url_notification]            |   Não    |  Texto /255          |  URL de Notificação Automática de Status                 |
| transaction[free]                        |   Não    |  Texto /200          |  Campo Livre                                             |
| transaction[sub_store]                   |   Não    |  Texto /20           |  Sub-Loja                                                |
| transaction_product[][description]       |   Sim    |  Texto /100          |  Nome do produto <sup>1</sup>                            |
| transaction_product[][quantity]          |   Sim    |  Número / 3          |  Quantidade do item do produto                           |
| transaction_product[][price_unit]        |   Sim    |  Decimal / 11        |  Valor unitário. Formato: 0.00                           |
| transaction_product[][code]              |   Não    |  Texto /10           |  Código do produto                                       |
| transaction_product[][sku_code]          |   Não    |  Texto /50           |  Código SKU do produto                                   |
| transaction_product[][extra]             |   Não    |  Texto /100          |  Campo Livre do produto                                  |
| payment[payment_method_id]               |   Sim    |  Texto /2            |  Forma de Pagamento                                      |
| payment[split]                           |   Sim    |  Texto /2            |  Número de parcelas (01 a 12)                            |
| payment[person_card_id]                  |   Não    |  Texto /100          |  Código do cartão cadastrado em nosso cofre <sup>3</sup> |
| payment[card_name]                       |   Não    |  Texto /100          |  Nome impresso no cartão                                 |
| payment[card_number]                     |   Não    |  Número /20          |  Número do cartão                                        |
| payment[card_expdate_month]              |   Não    |  Número /2           |  Mês de vencimento do cartão                             |
| payment[card_expdate_year]               |   Não    |  Número / 4          |  Ano de vencimento do cartão                             |
| payment[card_cvv]                        |   Não    |  Número /3           |  Código de segurança do cartão                           |
| payment[billet_date_expiration]          |   Não    |  Data / 10           |  Data de Vendimento do Boleto                            |
| affiliates[][account_email]              |   Não    |  Texto / 100         |  Email do afiliado da transação                          |
| affiliates[][percentage]                 |   Não    |  Número / 3          |  Percentual de repasse ao afiliado <sup>4</sup>          |
| affiliates[][commission_amount]          |   Não    |  Decimal / 11        |  Valor de repasse ao afiliado <sup>4</sup>               | 


<sup>1</sup> Note que nas informações acima que alguns dados possuem uma característica diferente, tendo um elemento [] dentro de sua formatação. Isso ocorre justamente para permitir que sejam enviados diversos itens na mesma requisição. 
{:.info}

<sup>2</sup> O parâmetro `transaction[available_payment_methods]` permite que sejam enviados os códigos de meios de pagamento que poderão ser disponibilizados no processo de recobrança de transações. Os códigos deverão ser enviados separados por vírgula (,). Esse campo é útil quando a loja oferece uma condição especial de pagamento, por exemplo Desconto de 10% no Boleto Bancário. Assim deve-se enviar apenas o código do boleto bancário para que seja disponibilizada somente esta forma de pagamento no processo de recobrança.
{:.info}

<sup>3</sup> O parâmetro `payment[person_card_id]` é informado com o código do cartão de crédito cadastrado em nossos cofres. Esse código é vinculado ao Vendedor e ao Cliente do Cartão de Crétido.
{:.info}

<sup>4</sup> O parâmetro `affiliates[][]` é informado quando é necessário que seja feito Repasse Automático ao Revendedor. Essa opção é utilizada na <a href="/intermediador/integracao-marketplace/#repasse-automatico-ao-revendedor" target="_blank" class="linkPadraoVerde">Integração com Marketplace</a>.
{:.info}



Veja ao lado uma chamada de API de exemplo.

JSON de Resposta
{: .subtitulo }

A API de Processamento de Transações retorna a resposta em JSON.


Exemplo de resposta com sucesso baseando no envio do exemplo acima:

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
                "price_payment": "147.69",
                "price_original": "142.0",
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
                "company_name": "",
                "trade_name": "",
                "cnpj": ""
            }
        }
    }
}
```


Mensagens de Erro
{: .subtitulo }

No caso de erro, a API retorna uma mensagem de erro. Assim é possível identificar o erro ocorrido e realizar o tratamento através do código e/ou mensagem retornada.

Abaixo segue os detalhes de cada nó do JSON de resposta:


```json
{
    "message_response": {
        "message": "error"
    },
    "error_response": {
        "general_errors": [
            {
                "code": "003039",
                "message": "Vendedor inválido ou não encontrado"
            }
        ]
    }
}
```


As mensagens de erros retornados pela API estão listadas na tabela abaixo:

| Código    |  Mensagem                                        |
|-----------|--------------------------------------------------|
|  001001   |     Token inválido ou não encontrado             |
|  003003   |     Forma de Pagamento Inválido                  |
|  003004   |     Número da Parcela Inválido                   |
|  003010   |     Forma de pagamento inválida                  |
|  003011   |     Numero do cartão inválido                    |
|  003012   |     Nome do cartão em branco                     |
|  003014   |     Código de segurança inválido                 |
|  003015   |     Mês de vencimento do cartão inválido         |
|  003016   |     Número de parcelas inválido                  |
|  003020   |     Ano de vencimento do cartão inválido         |
|  003021   |     O vendedor não pode ser igual ao comprador   |
|  003029   |     Código de segurança inválido                 |
|  003039   |     Vendedor inválido ou não encontrado          |
|  003065   |     Valor menor que mínimo permitido             |
|  009006   |     Número da parcela maior que o permitido      |
|  058001   |     Revendedor inválido.                         |


Tabelas Auxiliares
{: .subtitulo }

Na integração existem alguns campos com informações pré-definidas, onde deverão ser enviadas conforme o padrão existente, se for necessário enviar o campo na requisição, ou poderá tratar a informação conforme retorno recebido.

Abaixo segue tabelas com essas informações pré-definidas:

| Tabela 1 – Formas de Contato  |
|--------------|------|
| Residencial  | H    |
| Celular      | M    |
| Comercial    | W    |

| Tabela 2 – Tipos de Endereço |
|--------------|---------------|
| Cobrança     | B             |
| Entrega      | D             |


| Tabela 3 – Formas de Pagamento       |
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
| Transf. Online HSBC             | 21 |
| Transf. Online Bradesco         | 22 |
| Transf. Online Banco do Brasil  | 23 |
| Boleto Bancário                 |    |
| Boleto Bancário                 | 6  |


| Tabela 4 – Status da Transação       |
|---------------------------------|----|
| Aguardando Pagamento            | 4  |
| Em Processamento                | 5  |
| Aprovada                        | 6  |
| Cancelada                       | 7  |
| Em Contestação                  | 24 |
| Em Monitoramento                | 87 |
| Em Recuperação                  | 88 |
| Reprovada                       | 89 |

