---
title: API de Listagem de Transações
position: 9
menu: intermediador
right_code: |
  ~~~ php
    <?php
        /* Access Token da Conta do Lojista */
        $params['access_token'] = '2aa22p80a8fe8381337fbf348e9fb4743ab239fc67d3714c1bb5a372aa14ee43c';
      
        /* Periodo para listagem */
        $params['initial_date'] = '10/04/2018';        
        $params['finish_date'] = '17/04/2018';        
        $params['per_page'] = '1';  
     
        
        $urlPost = "https://api.intermediador.sandbox.yapay.com.br/v1/transactions/search";

        ob_start();

        $ch = curl_init();
        curl_setopt($ch, CURLOPT_URL, $urlPost);
        curl_setopt($ch, CURLOPT_POST, 1);
        curl_setopt($ch, CURLOPT_SSLVERSION, 1);
        curl_setopt($ch, CURLOPT_POSTFIELDS, $params);
        curl_exec($ch);

        /* XML de retorno */ 
        $resposta = simplexml_load_string(ob_get_contents());

        ob_end_clean();
        curl_close($ch);

        if($resposta->message_response->message == "success"){
            $foi = "ok";
        }else{
            $foi = "não foi";
        }
    ?>
  ~~~
  {: title="PHP" }
---

<span class="post">POST</span><span class="beforePost">/v1/transactions/search</span>

O Yapay disponibiliza um recurso para a listagem de transações. Com este recurso, você poderá realizar a listagem para obter as informações detalhadas das transações, e assim comparar as informações e atualizar o status do pedido com segurança.

Para esta integração, deverá ser feito uso da API a seguir:

| Endereço para Integração                                                                            |
|--------------------------|--------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/v1/transactions/search    |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/v1/transactions/search    |
| Protocolo                | Rest/HTTP                                                                |


Para a integração via <span class="post">POST</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada | Descrição                        |
|------------------|----------------------------------|
| access_token     | Token de Acesso                  |
| transaction_id   | ID da Transação                  |
| order_number     | Número do Pedido                 |
| email_customer   | E-mail do Cliente                |
| extra            | Campo Free                       |
| initial_date     | Data Inicial (dd/mm/aaaa)        |
| finish_date      | Data Final (dd/mm/aaaa)          |
| status_id        | ID do Status <sup>Tabela 1</sup> |
| per_page         | Quantidade por página            |
| type_response    | Tipo de Resposta J para JSON /  OUTROS para XML |

Veja ao lado uma chamada de exemplo da API de Listagem de Transação.

Exemplo de resposta com sucesso baseando no envio do exemplo:

```xml
{
<?xml version="1.0" encoding="UTF-8"?>
<transaction>
    <data_response>
        <session_id nil="true"/>
        <transactions type="array">
            <transaction>
                <order_number>TESTE-5853642</order_number>
                <free nil="true"/>
                <transaction_id type="integer">TESTE-5853642</transaction_id>
                <status_name>Cancelada</status_name>
                <status_id type="integer">7</status_id>
                <date_transaction>2018-04-05T15:35:14</date_transaction>
                <split type="integer">1</split>
                <price_payment type="decimal">1.0</price_payment>
                <date_payment>2018-04-05T15:35:15</date_payment>
                <transaction_token>f3166af4c88k836e0047fb929a644d7b</transaction_token>
                <sub_store>Loja Teste</sub_store>
                <available_payment_methods nil="true"/>
                <url_notification></url_notification>
                <url_css nil="true"/>
                <url_shipping nil="true"/>
                <url_stock nil="true"/>
                <url_success nil="true"/>
                <url_process nil="true"/>
                <url_cancel nil="true"/>
                <message_cancellation nil="true"/>
                <schedule_credit type="date">2018-05-05</schedule_credit>
                <price_seller type="decimal">0.54</price_seller>
                <price_original type="decimal">1.0</price_original>
                <price_additional type="decimal">0.0</price_additional>
                <price_discount type="decimal">0.0</price_discount>
                <shipping_price type="decimal">0.0</shipping_price>
                <shipping_type>Frete Grátis</shipping_type>
                <payment>
                    <price_payment type="decimal">1.0</price_payment>
                    <payment_response>Mensagem de venda</payment_response>
                    <url_payment></url_payment>
                    <date_approval>2018-04-05T15:35:15</date_approval>
                    <tid>0111276032815324372004</tid>
                    <split type="integer">1</split>
                    <date_payment>2018-04-05T15:35:15</date_payment>
                    <date_cancel>2018-04-05T15:39:00</date_cancel>
                    <payment_method_id type="integer">4</payment_method_id>
                    <payment_method_name>Mastercard</payment_method_name>
                    <card_id type="integer">1234</card_id>
                    <number_proccess type="integer">115438</number_proccess>
                    <linha_digitavel nil="true"/>
                </payment>
                <products type="array">
                    <product>
                        <code>806</code>
                        <description>Teste Homologação YaPay</description>
                        <extra nil="true"/>
                        <price_unit type="decimal">1.0</price_unit>
                        <quantity type="decimal">1.0</quantity>
                        <sku_code nil="true"/>
                        <url_img nil="true"/>
                    </product>
                </products>
                <transaction_affiliates type="array"/>
                <customer>
                    <name>Diana Price</name>
                    <cpf>50235335142</cpf>
                    <email>email@cliente.com.br</email>
                    <cnpj></cnpj>
                    <company_name>Diana Price</company_name>
                    <trade_name>Diana Price</trade_name>
                    <addresses type="array">
                        <address>
                            <street>Avenida Governador Santos Neves</street>
                            <number>451</number>
                            <neighborhood>Centro</neighborhood>
                            <postal_code>29900031</postal_code>
                            <completion></completion>
                            <city>Marilia</city>
                            <state>SP</state>
                        </address>
                    </addresses>
                    <contacts type="array">
                        <contact>
                            <contact_id type="integer">255703</contact_id>
                            <value>2733710802</value>
                            <type_contact>W</type_contact>
                            <primary type="boolean">true</primary>
                        </contact>
                    </contacts>
                </customer>
                <seller>
                    <name>Vendedor</name>
                    <cpf>37026673505</cpf>
                    <email>email@dovendedor.com.br</email>
                    <cnpj></cnpj>
                    <company_name></company_name>
                    <trade_name></trade_name>
                    <addresses type="array">
                        <address>
                            <street>Avenida Esmeralda</street>
                            <number>852</number>
                            <neighborhood>Jardim Esmeralda</neighborhood>
                            <postal_code>17516000</postal_code>
                            <completion>Casa 8112</completion>
                            <city>Marília</city>
                            <state>SP</state>
                        </address>
                    </addresses>
                    <contacts type="array">
                        <contact>
                            <contact_id type="integer">244367</contact_id>
                            <value>149974400000</value>
                            <type_contact>M</type_contact>
                            <primary type="boolean">true</primary>
                        </contact>
                    </contacts>
                </seller>
            </transaction>
        </transactions>
        <paginate>
            <current_page type="integer">0</current_page>
            <per_page type="integer">1</per_page>
            <amount_page type="integer">27</amount_page>
            <count type="integer">27</count>
        </paginate>
    </data_response>
    <message_response>
        <message>success</message>
    </message_response>
</transaction>

```



Exemplo de um retorno com erro:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<transaction>
    <error_response>
        <errors type="array">
            <error>
                <message>Token inválido ou não encontrado</message>
                <code>001001</code>
            </error>
        </errors>
    </error_response>
    <message_response>
        <message>error</message>
    </message_response>
</transaction>
```

As mensagens de erros retornados pela API estão listadas na tabela abaixo:

| Código    |  Mensagem                             |
|-----------|---------------------------------------|
| 001001    | Token inválido ou não encontrado      |
| 003022    | Data final inválida                   |
| 003023    | Data inicial inválida                 |
| 017001    | Token de sessão inválido              |
| 058001    | Revendedor inválido.                  |
| 060003    | Token de acesso inválido ou expirado. |



Tabelas Auxiliares
{: .subtitulo }

Na integração existem alguns campos com informações pré-definidas, onde deverão ser enviadas conforme o padrão existente, se for necessário enviar o campo na requisição, ou poderá tratar a informação conforme retorno recebido.

Abaixo segue tabelas com essas informações pré-definidas:

| Tabela 1 – Status da Transação       |
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