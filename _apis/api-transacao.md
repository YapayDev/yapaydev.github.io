---
title: API de Transação
position: 5
menu: intermediador
right_code: |
  ~~~ php
    <?php
        $data['token_account'] = 'SEU_TOKEN_AQUI';

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


        $url = "https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/payment";

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

  ~~~ javascript
    var http = require("https");

    var options = {
    "method": "POST",
    "hostname": "api.intermediador.sandbox.yapay.com.br",
    "port": null,
    "path": "/api/v3/transactions/payment",
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
    token_account: 'SEU_TOKEN',
    customer:
    {
        name: 'Diana Price',
        brith_date: '21/05/1941',
        cpf: '31162471298',
        email: 'daniaprice@amazonas.org',
        contacts:
        [ { type_contact: 'H',
        number_contact: '1133221122' 
        } ],
        addresses:
        [ { type_address: 'B',
        postal_code: '17516000',
        street: 'Rua Esmeralda',
        number: '25',
        completion: 'A',
        neighborhood: 'Jd. Esmeralda',
        city: 'Marilia',
        state: 'SP' 
        } ]
        },
    transaction_product: 
    [ {
        description: 'Descrição do Produto',
        quantity: '1',
        price_unit: '300',
        code: '159',
        sku_code: '001',
        extra: 'Campo de Informação Extra'
        } ],
    transaction:
    {
        available_payment_methods: '2,3,4,5,6,7,14,15,16,18,19,21,22,23',
        customer_ip: '127.0.0.1',
        shipping_type: 'Sedex',
        shipping_price: '10',
        price_discount: '0',
        url_notification: '',
        free: 'Campo de Informação livre' },
    payment: {
        payment_method_id: '6'
    }

    } ) );

    req.end();

  ~~~
  {: title="NodeJS" }    

  ~~~ java
    ...
    String url = "https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/payment";
     
    HttpClient client = new HttpClient();
    PostMethod method = new PostMethod(url);
    
    method.getParams().setParameter(HttpMethodParams.RETRY_HANDLER, 
        new DefaultHttpMethodRetryHandler(3, false));
    byte[] responseBody = null;

    try {
        NameValuePair[] data = {
            /* Token da Conta do Lojista */
            new NameValuePair("token_account", "SEU_TOKEN_AQUI"),
            
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
    
    var client = new RestClient("https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/payment");
    var request = new RestRequest(Method.POST);

    request.AddHeader("content-type", "application/json");
    request.AddParameter("application/json", "{\"token_account\":\"SEU_TOKEN\",\"customer\":{\"contacts\":[{\"type_contact\":\"H\",\"number_contact\":\"1133221122\"}],\"addresses\":[{\"type_address\":\"B\",\"postal_code\":\"17516000\",\"street\":\"Av Themyscira\",\"number\":\"1001\",\"completion\":\"Casa A\",\"neighborhood\":\"Jd das Rochas\",\"city\":\"Themyscira\",\"state\":\"SP\"}],\"name\":\"Diana Prince\",\"birth_date\":\"21/05/1941\",\"cpf\":\"50235335142\",\"email\":\"email@docliente.com\"},\"transaction_product\":[{\"description\":\"Camiseta Wonder Woman\",\"quantity\":\"1\",\"price_unit\":\"130\",\"code\":\"1\",\"sku_code\":\"1250\",\"extra\":\"Informação extra\"}],\"transaction\":{\"available_payment_methods\":\"2,3,4,5,6,7,14,15,16,18,19,21,22,23\",\"order_number\":\"1\",\"shipping_type\":\"Sedex\",\"shipping_price\":\"10\",\"price_discount\":\"0\",\"url_notification\":\"http://www.loja.com.br/notificacao\",\"free\":\"Campo Livre\",\"sub_store\":\"LOJA_1\"},\"payment\":{\"payment_method_id\":\"6\"}}", ParameterType.RequestBody);

    IRestResponse response = client.Execute(request);

  ~~~
  {: title="C#" }
  
  ~~~ json    
    {  
        "token_account":"SEU_TOKEN_AQUI",
        "customer":{  
            "contacts":[  
                {  
                    "type_contact":"H",
                    "number_contact":"1133221122"
                },{  
                    "type_contact":"M",
                    "number_contact":"11999999999"
                }         
            ],
            "addresses":[  
                {  
                    "type_address":"B",
                    "postal_code":"17000-000",
                    "street":"Av Themyscira",
                    "number":"1001",
                    "completion":"A",
                    "neighborhood":"Jd das Rochas",
                    "city":"Themyscira",
                    "state":"SP"
                }
            ],
            "name":"Diana Prince",
            "birth_date": "21/05/1941",
            "cpf":"50235335142",
            "email":"email@cliente.com.br"
        },
        "transaction_product":[  
            {  
                "description":"Camiseta Wonder Woman",
                "quantity":"1",
                "price_unit":"130.00",
                "code": "1",
                "sku_code": "0001",
                "extra": "Informação Extra"
            }
        ],
        "transaction":{  
            "available_payment_methods": "2,3,4,5,6,7,14,15,16,18,19,21,22,23",
            "customer_ip":"127.0.0.1",
            "shipping_type":"Sedex",
            "shipping_price":"12",
            "price_discount": "",
            "url_notification":"http://www.loja.com.br/notificacao",
            "free": "Campo Livre"      
            
        },
        "payment":{  
            "payment_method_id":"6"
        }
    }
  ~~~
  {: title="JSON" }  


---

<span class="post">POST</span><span class="beforePost">/api/v3/transactions/payment</span>

O Yapay disponibiliza uma versão transparente para a integração de transações, permitindo que o usuário efetue o processamento dos pedidos sem necessitar o redirecionamento para outra aplicação e preenchimento de novos formulários.

![API Transação Yapay](/images/intermediador/conteudo/Integracao_api_LV.png "API Transação Yapay"){: width="90%" height="auto" }

Através do CPF do cliente é feita a consulta pela existência do seu cadastro e então as transações são atreladas ao mesmo. Caso não exista uma conta, o sistema irá criar uma nova conta com os dados que forem submetidos na integração. Para esta integração, deverá ser feito uso da API a seguir:

Fingerprint
{: .subtitulo }

**1-** No momento que você criou o formulário para envio das informações da transação, você deve adiionar a tag `data-yapay="payment-form"`. Incluindo essa tag será criado um input do tipo `hidden`, com o valor do parâmetro `finger_print` que deve ser enviado junto com os parâmetros de criação na API de Transação. Exemplo de form em HTML:

```html
    <html>
        <body>
            <form action="acao.php" method="post"  data-yapay="payment-form">
                <input type="submit" name="submit" value="Submit" />
            </form>
        </body>
    </html>
```

**2-** No momento do envio para a API de Transação, você deve adicionar o parâmetro `finger_print`. Exempĺo do código em PHP abaixo:

```php
    <?php
        ...
        
        $data["finger_print"] = $_POST['finger_print'];
        
        ...
    ?>
```


**3-** Você deve incluir um script no processamento da transação (na página de checkout), no início da página de finalização da compra. Segue abaixo código do script:

```html
 <script src="https://static.traycheckout.com.br/js/finger_print.js" type="text/javascript"></script>
```

Também deve realizar a chamada do plugin, no final da mesma página. Essa chamada acionará o fingerprint para que seja realizada a coleta e analise de dados. Conforme código javascript abaixo:

```php
    <script type="text/javascript">
        jQuery(document).FingerPrint();
    </script>
```

Após esses procedimentos é enviado juntamente com o JSON de requisição o parâmetro `finger_print`, onde conseguimos realizar a analise antifraude.


O fingerprint funciona nos ambientes `SANDBOX` e `PRODUÇÃO`.
{:.warning }


Após esses procedimentos é enviado juntamente com o JSON de requisição o parâmetro `finger_print`, onde conseguimos realizar a analise antifraude.


| Endereço para Integração                                                                          |
|--------------------------|------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/payment   |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/api/v3/transactions/payment           |
| Protocolo                | Rest/HTTP                                                              |


Para a integração via <span class="post">POST</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada                         |  Obrig.  | Formato / Tam. Max   | Descrição                                                  |
|------------------------------------------|----------|----------------------|------------------------------------------------------------|
| token_account                            |   Sim    |  Texto /20           |  Token de identificação do vendedor                      |
| customer[name]                           |   Sim    |  Texto /100          |  Nome do Comprador                                       |
| customer[cpf]                            |   Sim    |  Texto /14           |  CPF do Comprador                                        |
| customer[email]                          |   Sim    |  Texto /100          |  E-mail do Comprador                                     |
| customer[trade_name]                     |   Não    |  Texto /100          |  Nome Fantasia do Comprador                              |
| customer[company_name]                   |   Não    |  Texto /100          |  Razão Social do Comprador                               |
| customer[cnpj]                           |   Não    |  Texto /18           |  CNPJ do Comprador                                       |
| customer[inscricao_municipal]            |   Não    |  Texto /20           |  Inscrição Municipal do Comprador                        |
| customer[contacts][][type_contact]       |   Sim    |  Texto /1            |  Tipo do Contato <sup>1</sup> (Tabela 1)                 |
| customer[contacts][][number_contact]     |   Sim    |  Texto /11           |  Número do telefone do Comprador                         |
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
| transaction[url_notification]            |   Não    |  Texto /255          |  URL de Notificação Automática de Status<sup>5</sup>     |
| transaction[free]                        |   Não    |  Texto /200          |  Campo Livre                                             |
| transaction[sub_store]                   |   Não    |  Texto /20           |  Sub-Loja                                                |
| transaction_product[][description]       |   Sim    |  Texto /100          |  Nome do produto <sup>1</sup>                            |
| transaction_product[][quantity]          |   Sim    |  Número / 3          |  Quantidade do item do produto                           |
| transaction_product[][price_unit]        |   Sim    |  Decimal / 11        |  Valor unitário. Formato: 0.00                           |
| transaction_product[][code]              |   Não    |  Texto /10           |  Código do produto                                       |
| transaction_product[][sku_code]          |   Não    |  Texto /50           |  Código SKU do produto                                   |
| transaction_product[][extra]             |   Não    |  Texto /100          |  Campo Livre do produto                                  |
| transaction[max_split_transaction]       |   Não    |  Número /10          |  Número máximo de parcelas                                  |
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
| affiliates[][commission_amount]          |   Não    |  Decimal / 11        |  Valor de repasse ao afiliado <sup>5</sup>               |
| reseller_token                           |   Não    |  Texto               |  Valor de repasse ao afiliado <sup>6</sup>               |
| finger_print                             |   Não    |  Texto /100          |  Token gerado pelo FingerPrint <sup>7</sup>              |


<sup>1</sup> Note que nas informações acima que alguns dados possuem uma característica diferente, tendo um elemento [] dentro de sua formatação. Isso ocorre justamente para permitir que sejam enviados diversos itens na mesma requisição. 
{:.info}

<sup>2</sup> O parâmetro `transaction[available_payment_methods]` permite que sejam enviados os códigos de meios de pagamento que poderão ser disponibilizados no processo de recobrança de transações. Os códigos deverão ser enviados separados por vírgula (,). Esse campo é útil quando a loja oferece uma condição especial de pagamento, por exemplo Desconto de 10% no Boleto Bancário. Assim deve-se enviar apenas o código do boleto bancário para que seja disponibilizada somente esta forma de pagamento no processo de recobrança.
{:.info}

<sup>3</sup> O parâmetro `payment[person_card_id]` é informado com o código do cartão de crédito cadastrado em nossos cofres. Esse código é vinculado ao Vendedor e ao Cliente do Cartão de Crétido.
{:.info}

<sup>4</sup> O parâmetro `affiliates[][]` é informado quando é necessário que seja feito Repasse Automático ao Revendedor. Essa opção é utilizada na <a href="/intermediador/integracao-marketplace/#repasse-automatico-ao-revendedor" target="_blank" class="linkPadraoVerde">Integração com Marketplace</a>.
{:.info}

<sup>5</sup> O parâmetro `transaction[url_notification]` é informado para comunicar a sua aplicação a cada alteração de status de uma transação. Saiba mais em <a href="/intermediador/notificacao-automatica-status/" target="_blank" class="linkPadraoVerde">Notificação Automática de Status</a>.
{:.info}

<sup>6</sup> O parâmetro `reseller_token` é informado para comunicar que a transação é vinculada a um revendedor. Dessa forma todas as transações que são enviadas com esse parâmetro ficam vinculadas ao revendedor.
{:.info}

<sup>7</sup> O parâmetro `finger_print` é informado por um script Javascript que faz uma coleta de dados e realiza a analise das informações disponíveis publicamente na máquina. Dessa forma é realizada a Análise de Risco.
{:.warning}


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
| Transf. Online Bradesco         | 22 |
| Transf. Online Banco do Brasil  | 23 |
| Boleto Bancário                 |    |
| Boleto Bancário                 | 6  |
| Saldo em conta                  |    |
| Pagamento com Saldo             | 8  |


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



<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>