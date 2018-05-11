---
title: API de Carrinho de Compra
position: 12
menu: intermediador
right_code: |
---


CREATE
{: .subtituloAzul }

<span class="post">POST</span><span class="beforePost">/v1/tmp_transactions/create</span>

O Yapay Intermediador fornece uma ferramenta poderosa para sites que não possuem um carrinho de compras e querem oferecer a possibilidade de visitantes escolherem produtos e finalizarem uma compra.


Esta ferramenta exclusiva também permite que seja possível o seu uso em um ambiente multi-vendedor, onde o site/marketplace pode fornecer um carrinho de compras para todas as lojas simultaneamente, fazendo com que o comprador tenha uma experiência única de compra com o Yapay Intermediador.


| Endereço para Integração                                                                                |
|--------------------------|------------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/v1/tmp_transactions/create   |
| Ambiente de Produção     | http://api.intermediador.yapay.com.br/v1/tmp_transactions/create           |
| Protocolo                | Rest/HTTP                                                                    |

Para a integração via <span class="post">POST</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada                   |  Obrig.  | Descrição                   |
|------------------------------------|----------|-----------------------------|
| token_account                      | Sim      | Token da conta da Loja      |
| reseller_token                     | Não      | Token do Revendedor         |
| transaction_product[][code]        | Sim      | Código do Produto           |
| transaction_product[][description] | Sim      | Descrição do Produto        |
| transaction_product[][quantity]    | Sim      | Quantidade do produto       |
| transaction_product[][price_unit]  | Sim      | Valor do Produto            |
| transaction_product[][extra]       | Não      | Informações extra           |
| transaction_product[][url_img]     | Não      | URL da Imagem do Produto    |
| transaction_product[][sku_code]    | Não      | Número do SKU do Produto    |
| transaction_product[][weight]      | Não      | Peso do Produto             |
| token_transaction                  | Não      | Token da Transação          |
| url_seller                         | Não      | URL do Botão voltar a Loja  |
| url_notification                   | Não      | URL de Notificação          |
| price_discount                     | Não      | Valor do Desconto           |
| postal_code_seller                 | Sim      | CEP de Origem               |
| shipping_type                      | Sim      | Forma de Envio              |
| shipping_price                     | Sim      | Valor do frete              |
| sub_store                          | Não      | Sub-Store                   |
| url_css                            | Não      | URL do CSS Customizado      |
| affiliates[][email]                | Não      | E-mail do afiliado          |
| affiliates[][percentage]           | Não      | Porcentagem do Afiliado     |


Veja abaixo uma chamada de API de exemplo:

  ~~~ php
    <?php
        $params['token_account'] = 'SEU_TOKEN_AQUI';

        $params['transaction_product[1][code]'] = '5';
        $params['transaction_product[1][description]'] = 'Kit com 3 Camisetas Wonder Woman';
        $params['transaction_product[1][quantity]'] = '1';
        $params['transaction_product[1][price_unit]'] = '150.00';        


        $params['postal_code_seller'] = '17516000';

        $params['shipping_type'] = 'Sedex';       
        $params['shipping_price'] = '10';  


        $urlPost = "https://api.intermediador.sandbox.yapay.com.br/v1/tmp_transactions/create";

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

        if($resposta->message_response->message == "success"){
            //Tratamento dos dados de resposta da consulta.
        }else{
            //Tratamento das mensagens de erro
        }
    ?>
  ~~~
  {: title="PHP" }

  ~~~ json
    {
        "token_account": "SEU_TOKEN",
        "postal_code_seller": "17516000",
        "shipping_type": "Sedex",
        "shipping_price": "10",
            
        "transaction_product":[  
            {  
                "description": "Camiseta Wonder Woman",
                "quantity": "1",
                "price_unit": "150.00",
                "code": "1"
            }
        ]	
    }
  ~~~
  {: title="JSON" }

XML de Resposta
{: .subtitulo }

A API de Cadastro de Carrinho retorna a resposta em XML. Exemplo de resposta com sucesso baseando no envio do exemplo acima:


``` xml
    <tmp_transaction>
        <message_response>
            <message>success</message>
        </message_response>
        <data_response>
            <token_transaction>c543a7c7874c71882e6ad8f12f3e46</token_transaction>
            <url_car>https://tc.intermediador.sandbox.yapay.com.br/payment/car/v1/</url_car>
            <transaction_products type="array">
                <transaction_product>
                    <code>1</code>
                    <img nil="true"/>
                    <sku_code nil="true"/>
                    <description>Camiseta Wonder Woman</description>
                    <extra nil="true"/>
                    <price_unit type="decimal">130.0</price_unit>
                    <quantity type="decimal">1.0</quantity>
                    <weight nil="true"/>
                    <id type="integer">8894</id>
                    <type_product nil="true"/>
                </transaction_product>
            </transaction_products>
        </data_response>
    </tmp_transaction>

```

Mensagens de Erro
{: .subtitulo }

No caso de erro, a API retorna uma mensagem de erro. Assim é possível identificar o erro ocorrido e realizar o tratamento através do código e/ou mensagem retornada.


Exemplo de um retorno com erro:

```xml
    <tmp_transaction>
        <message_response>
            <message>error</message>
        </message_response>
        <error_response>
            <general_errors type="array">
                <general_error>
                    <code>001001</code>
                    <message>Token inválido ou não encontrado</message>
                </general_error>
            </general_errors>
        </error_response>
    </tmp_transaction>
```

As mensagens de erros retornados pela API estão listadas na tabela abaixo:

| Código   |  Mensagem                                        |
|----------|--------------------------------------------|
| 001001   | Token inválido ou não encontrado           |
| 003003   | Forma de Pagamento Inválido                |
| 003004   | Número da Parcela Inválido                 |
| 003010   | Forma de pagamento inválida                |
| 003011   | Numero do cartão inválido                  |
| 003012   | Nome do cartão em branco                   |
| 003014   | Código de segurança inválido               |
| 003015   | Mês de vencimento do cartão inválido       |
| 003016   | Número de parcelas inválido                |
| 003020   | Ano de vencimento do cartão inválido       |
| 003021   | O vendedor não pode ser igual ao comprador |
| 003029   | Código de segurança inválido               |
| 003039   | Vendedor inválido ou não encontrado        |
| 003065   | Valor menor que mínimo permitido           |
| 009006   | Número da parcela maior que o permitido    |
| 058001   | Revendedor inválido.                       |
       


GET
{: .subtituloAzul }


<span class="post">POST</span><span class="beforePost">/v1/tmp_transactions/get</span>


Quando utilizada a API de Carrinho de Compras, é possível consultar essas informações para a exibição, possibilidade de visitantes visualizar os produtos e finalizarem uma compra. Através da API de Consulta Transação Temporária, é possível resgatar as informações armazenadas através da API de Carrinho de Compras, sem redirecionar o cliente para o ambiente do Yapay Intermediador.


| Endereço para Integração                                                                                |
|--------------------------|------------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/v1/tmp_transactions/get   |
| Ambiente de Produção     | http://api.intermediador.yapay.com.br/v1/tmp_transactions/get           |
| Protocolo                | Rest/HTTP                                                                    |


Para a integração via POST, segue abaixo os dados necessários para envio:

| Dados de Entrada                   |  Obrig.  | Descrição                   |
|------------------------------------|----------|-----------------------------|
| token_account                      | Sim      | Token da conta da Loja      |
| token_transaction                  | Sim      | Token da Transação          |
| order_number                       | Não      | Número do Pedido            |



Veja abaixo uma chamada de API de exemplo:

  ~~~ php
    <?php        
        
        $params['token_transaction'] = 'feb6765f08df66859a4da644db150c';
        



        $urlPost = "https://api.intermediador.sandbox.yapay.com.br/v1/tmp_transactions/get";

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

        if($resposta->message_response->message == "success"){
            //Tratamento dos dados de resposta da consulta.
        }else{
            //Tratamento das mensagens de erro
        }
    ?>
  ~~~
  {: title="PHP" }

  ~~~ json
    {        
        "token_transaction": "c2b2adfc55b52b88c7249fe0a689c9"
    }
  ~~~
  {: title="JSON" }

XML de Resposta
{: .subtitulo }

A API de Consulta de Carrinho retorna a resposta em XML. Exemplo de resposta com sucesso baseando no envio do exemplo acima:


``` xml
    <?xml version="1.0" encoding="UTF-8"?>
    <tmp_transaction>
        <data_response>
            <tmp_transactions type="array">
                <tmp_transaction>
                    <token_transaction>c2b2a95dfc55b52b88c7249fa689c9</token_transaction>
                    <url_car>https://tc.intermediador.sandbox.yapay.com.br/payment/car/v1/</url_car>
                    <transaction_products type="array">
                        <transaction_product>
                            <code>1</code>
                            <img nil="true"/>
                            <sku_code nil="true"/>
                            <description>Camiseta Wonder Woman</description>
                            <extra nil="true"/>
                            <price_unit type="decimal">130.0</price_unit>
                            <quantity type="decimal">1.0</quantity>
                            <weight nil="true"/>
                            <id type="integer">8896</id>
                            <type_product nil="true"/>
                        </transaction_product>
                    </transaction_products>
                </tmp_transaction>
            </tmp_transactions>
        </data_response>
        <message_response>
            <message>success</message>
        </message_response>
    </tmp_transaction>

```

Mensagens de Erro
{: .subtitulo }

No caso de erro, a API retorna uma mensagem de erro. Assim é possível identificar o erro ocorrido e realizar o tratamento através do código e/ou mensagem retornada.


Exemplo de um retorno com erro:

```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <tmp_transaction>
        <error_response>
            <errors type="array">
                <error>
                    <message>Transação temporária não encontrada</message>
                    <code>038002</code>
                </error>
            </errors>
        </error_response>
        <message_response>
            <message>error</message>
        </message_response>
    </tmp_transaction>

```

As mensagens de erros retornados pela API estão listadas na tabela abaixo:

| Código   |  Mensagem                                        |
|----------|--------------------------------------------|
| 038002   | Transação temporária não encontrada        |
       

<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>