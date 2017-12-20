---
title: Criar Transação
position: 1
menu: gateway
right_code: |
 
---

<span class="post">POST</span><span class="beforePost">/api/v1/transactions/</span>


Para criar uma transação de cartão de crédito, boleto ou transferencia bancária, você deve utilizar o método **Criar Transação**. 

As transações são geradas e identificadas por ID, que são gerados de forma aleatória. Exemplo: `7122dad656cea6364af163f7a5e2f0a8`


Abaixo os parâmetros necessários para criar a transação:

| Parâmetro                                          | Formato  | Descrição                                                 |
|----------------------------------------------------|----------|-----------------------------------------------------------|
| authorization                                      | Texto    |  Token de autenticação                                    |
| transaction[number]                                | Número   |  Número do Pedido                                         |
| transaction[installments]                          | Texto    |  Quantidade de Parcelas     	              	            |
| transaction[soft_descriptor]                       | Texto    |  Descrição da loja na fatura	              	            |
| transaction[fingerprint]                           | Texto    |  Fingerprint                 	              	            |
| transaction[free]                                  | Texto    |  Campo Livre	         	                	            |
| transaction[amount]                                | Decimal  |  Valor         	                               	        |
| transaction[payment][processor]                    | Texto    |  Processador do pagamento (Adquirente) <sup>Tabela 1</sup>|
| transaction[payment][method]                       | Texto    |  Meio de pagamento (Forma) <sup>Tabela 1</sup>            |
| transaction[payment][card][reference]              | Texto    |  Referência do cartão	                                    |
| transaction[payment][card][holder_name]            | Texto    |  Nome impresso no cartão	                                |
| transaction[payment][card][number]                 | Texto    |  Número do cartão	                         	            |
| transaction[payment][card][cvv]                    | Texto    |  Código de segurança do cartão	                        |
| transaction[payment][card][expiration][month]      | Texto    |  Mês de vencimento do cartão (mm)	                        |
| transaction[payment][card][expiration][year]       | Texto    |  Ano de vencimento do cartão (YYYY)	                    |
| transaction[payment][billet][due_date]             | Texto    |  Data de vencimento do boleto	                            |
| transaction[payment][billet][observations][]       | Texto    |  Observações do boleto	                                |
| transaction[urls][notification]                    | Texto    |  URL de notificação	                     	            |
| transaction[urls][cancelation]                     | Texto    |  URL de cancelamento	                     	            |
| transaction[urls][processing]                      | Texto    |  URL de processamento	                     	            |
| transaction[urls][success]                         | Texto    |  URL de sucesso	                 	                    |
| transaction[prices][discount]                      | Decimal  |  Valor do desconto	                     	            |
| transaction[prices][additional]                    | Decimal  |  Valor adicional	                     	                |
| transaction[shipping][method]                      | Texto    |  Tipo de envio	                     	                |
| transaction[shipping][price]                       | Texto    |  Valor do envio	                     	                |
| transaction[products][][code]                      | Texto    |  Código do produto	                     	            |
| transaction[products][][description]               | Texto    |  Descrição do produto	                                    |
| transaction[products][][price]                     | Decimal  |  Valor unitário do produto	                            |
| transaction[products][][quantity]                  | Texto    |  Quantidade de produtos	                                |
| transaction[products][][type]                      | Texto    |  Tipo do produto <sup>Tabela 2</sup>                      |
| transaction[customer][name]                        | Texto    |  Nome do cliente	                 	                    |
| transaction[customer][document]                    | Texto    |  Documento do cliente	                     	            |
| transaction[customer][email]                       | Texto    |  Email do cliente	                     	                |
| transaction[customer][gender]                      | Texto    |  Gênero do cliente <sup>Tabela 3</sup>                    |
| transaction[customer][birth_date]                  | Texto    |  Data de nascimento do cliente	                        |
| transaction[customer][ip]                          | Texto    |  IP do cliente	                 	                    |
| transaction[customer][address][street]             | Texto    |  Endereço do cliente - Logradouro	           	            |
| transaction[customer][address][number]             | Texto    |  Endereço do cliente - Número	                            |
| transaction[customer][address][complement]         | Texto    |  Endereço do cliente - Complemento	                    |
| transaction[customer][address][postal_code]        | Texto    |  Endereço do cliente - CEP	                            |
| transaction[customer][address][neighborhood]       | Texto    |  Endereço do cliente - Bairro	                            |
| transaction[customer][address][city]               | Texto    |  Endereço do cliente - Município	                        |
| transaction[customer][address][state]              | Texto    |  Endereço do cliente - Estado	                            |
| transaction[customer][contacts][][type_contact]    | Texto    |  Contatos do cliente - Tipo <sup>Tabela 4</sup>	        |
| transaction[customer][contacts][][number_contact]  | Texto    |  Contatos do cliente - Número <sup>Tabela 4</sup>	      	|


Criando uma transação Completa
{: .subtituloAzul }

Veja abaixo um exemplo de código com uma transação completa:

~~~php
    <?php
        $username   = "SEU_EMAIL";
        $password   = "SEU_TOKEN";

        $data["transaction"]["number"] = "2421227";
        $data["transaction"]["installments"] = 1;
        $data["transaction"]["soft_descriptor"] = "Descrição do Software";
        $data["transaction"]["amount"] = "100";

        $data["transaction"]["payment"]["processor"] = "itaushopline";
        $data["transaction"]["payment"]["method"] = "itaushopline_billet";

        $data["transaction"]["shipping"]["method"] = "PAC";
        $data["transaction"]["shipping"]["price"] = "10";

        $data["transaction"]["products"][0]["code"] = "2244";
        $data["transaction"]["products"][0]["description"] = "Camiseta DC Comics";
        $data["transaction"]["products"][0]["price"] = "20";
        $data["transaction"]["products"][0]["quantity"] = "1";
        $data["transaction"]["products"][0]["type"] = "physical";


        $data["transaction"]["customer"]["name"] = "Diana de Themyscira";    
        $data["transaction"]["customer"]["document"] = "85660062326";    
        $data["transaction"]["customer"]["email"] = "diana@amazonas.com";   
        $data["transaction"]["customer"]["gender"] = "female";    
        $data["transaction"]["customer"]["birth_date"] = "15.05.1942";    
        $data["transaction"]["customer"]["ip"] = "127.0.0.1";    

        $data["transaction"]["customer"]["address"]["street"] = "Rua Amazonas Um";    
        $data["transaction"]["customer"]["address"]["number"] = "2";    
        $data["transaction"]["customer"]["address"]["complement"] = "Porta 40";            
        $data["transaction"]["customer"]["address"]["postal_code"] = "17000-000";            
        $data["transaction"]["customer"]["address"]["neighborhood"] = "Pedra Preta";            
        $data["transaction"]["customer"]["address"]["city"] = "Amazonas";  
        $data["transaction"]["customer"]["address"]["state"] = "UF";      

        $data["transaction"]["customer"]["address"]["contacts"][0]["type_contact"] = "H";      
        $data["transaction"]["customer"]["address"]["contacts"][0]["number_contact"] = "14999996655";        


        $url = "https://gtw.sandbox.checkout.tray.com.brapi/v1/transactions.json";

        ob_start();

        $ch = curl_init();
        curl_setopt($ch, CURLOPT_URL, $url);
        curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
        curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
        curl_setopt($ch, CURLOPT_HTTPHEADER, array(
            'Content-Type: application/json',        
            'Authorization: Basic ' . base64_encode("$username:$password"),
            'Content-Length: ' . strlen(json_encode($data)))
        );

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


Criando uma transação simples
{: .subtituloAzul }

Veja abaixo um exemplo de código com uma transação completa:


~~~php
  <?php

      $username   = "diana@amazonas.com";
      $password   = "SEU_TOKEN";

      $data["transaction"]["number"] = "2429977";
      $data["transaction"]["installments"] = 1;      
      $data["transaction"]["amount"] = "1200";

      $data["transaction"]["payment"]["processor"] = "getnet";
      $data["transaction"]["payment"]["method"] = "visa";
      $data["transaction"]["payment"]["card"][reference] = "id99";
      $data["transaction"]["payment"]["card"][holder_name] = "Diana de Themyscira";
      $data["transaction"]["payment"]["card"][number] = "4916328365368562";
      $data["transaction"]["payment"]["card"][cvv] = "273";
      $data["transaction"]["payment"]["card"][expiration][month] = "09";
      $data["transaction"]["payment"]["card"][expiration][year] = "2018";

      $url = "https://gtw.sandbox.checkout.tray.com.brapi/v1/transactions";

      ob_start();

      $ch = curl_init();
      curl_setopt($ch, CURLOPT_URL, $url);
      curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
      curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
      curl_setopt($ch, CURLOPT_HTTPHEADER, array(
          'Content-Type: application/json',        
          'Authorization: Basic ' . base64_encode("$username:$password"),
          'Content-Length: ' . strlen(json_encode($data)))
      );

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


Veja abaixo um exemplo de código com uma transação simples:


Criando uma transação com Análise de Risco
{: .subtituloAzul }

Para criar uma transação com **Análise de Risco**, você precisa ter configurado no seu cadastro de vendedor qual é a empresa de risco contratada.

| Análise de Risco                                                                      | Integração |
|:-------------------------------------------------------------------------------------:|:-----------------------------------------------------------:|
| ![ClearSale](/images/gateway/servicos/ClearSale.png){: .imgLogoTable }                | ![Yapay Intermediadork](/images/checked-verde.svg){: .imgBtnTable } |
| ![FControl](/images/gateway/servicos/FControl.png){: .imgLogoTable }                  | ![Yapay Intermediadork](/images/checked-verde.svg){: .imgBtnTable } |


JSON Response
{: .subtituloAzul }

Abaixo você visualiza a resposta em JSON do método **Criar Transação**, a resposta do servidor será a mesma para ambas as integrações:

~~~json
{
    "transaction": {
        "id": "7122dad656cea6364af163f7a5e2f0a8",
        "number": "1202877",
        "status": "unpaid",
        "created_at": "2017-09-22T13:55:02.000-03:00",
        "tid": null,
        "nsu": null,
        "fingerprint": null,
        "free": null,
        "ip": "127.0.0.1",
        "payment": {
            "method": "itaushopline_billet",
            "processor": "itaushopline",
            "installments": 1,
            "processing_type": "authorized",
            "prices": {
                "total": 1132,
                "additional": "0.0",
                "discount": "0.0"
            },
            "seller_settings": [],
            "card": {
                "number": null,
                "expiration": {
                    "month": null,
                    "year": null
                }
            },
            "billet": {
                "code": "",
                "due_date": null
            },
            "flag_url": "https://gtw.sandbox.checkout.tray.com.br/assets/payment_methods/823.png"
        },
        "customer": {
            "id": 10033,
            "name": "Diana de Themyscira",
            "customer_document": "2244222211",
            "created_at": "2017-09-20T21:36:19.000-03:00",
            "updated_at": "2017-09-22T13:55:02.000-03:00",
            "email": "diana@amazonas.com",
            "birth_date": "15.05.1942",
            "gender": "F",
            "seller_document": null,
            "company_name": null
        },
        "urls": {
            "notification": null,
            "cancelation": null,
            "processing": null,
            "success": null
        },
        "shipping": {
            "type": "PAC",
            "price": "10.0"
        },
        "products": [
            {
                "id": 41260,
                "transaction_id": 45023,
                "code": "2244",
                "description": "Camiseta DC Comics",
                "quantity": "1.0",
                "price_unit": "20.0",
                "weight": "1.0",
                "shipping_cost": "0.0",
                "created_at": "2017-09-22T13:55:02.000-03:00",
                "updated_at": "2017-09-22T13:55:02.000-03:00",
                "url_img": null
            }
        ],
        "response": {
            "tid": null,
            "pan": null,
            "billet_bar_code": "",
            "url_payment": "http://gtw.sandbox.checkout.tray.com.br/api/print/7122dad656cea6364af163f7a5e2f0a8",
            "status": {
                "id": 3,
                "name": "Não Paga"
            },
            "authentication": {
                "code": null,
                "message": null,
                "eci": null,
                "price": null,
                "datetime": 0
            },
            "authorization": {
                "lr": null,
                "message": null,
                "authorization_code": null,
                "authorization_price": null,
                "datetime": 0
            },
            "cancellation": {
                "code": null,
                "message": null,
                "price": null,
                "datetime": 0
            }
        },
        "processor": {
            "payment": {
                "success": true,
                "chave": "X[183]M[175]",
                "url_comunication": "https://shopline.itau.com.br/shopline/Impressao.aspx",
                "billet": {
                    "success": true,
                    "pdf_url": "http://images.teste.tray.net.br/23/billet/2/pdf/450231202877.pdf",
                    "billet_bar_code": ""
                }
            }
        }
    }
}
~~~


Tabelas Auxiliares
{: .subtituloAzul }

Separamos as tabelas para auxiliarem a integração, abaixo você consegue visualiza-las:


| Tabela 1 – Tipo de Processador de Pagamento |
| Method                 | Processor          | Descrição                               |
|------------------------|--------------------|-----------------------------------------|
| visa                   | cielo              | Adquirente                              |
| mastercard             | cielo              | Adquirente                              |
| elo                    | cielo              | Adquirente                              |
| discover               | cielo              | Adquirente                              |
| diners                 | cielo              | Adquirente                              |
| visa_redirect          | cielo              | Adquirente                              |
| mastercard_redirect    | cielo              | Adquirente                              |
| elo_redirect           | cielo              | Adquirente                              |
| discover_redirect      | cielo              | Adquirente                              |
| diners_redirect        | cielo              | Adquirente                              |
| american_express       | cielo              | Adquirente                              |
| aura                   | cielo              | Adquirente                              |
| jcb                    | cielo              | Adquirente                              |
| aura_redirect          | cielo              | Adquirente                              |
| jcb_redirect           | cielo              | Adquirente                              |
| maestro                | cielo              | Adquirente                              |
| visa                   | erede              | Adquirente                              |
| mastercard             | erede              | Adquirente                              |
| diners                 | erede              | Adquirente                              |
| hipercard              | erede              | Adquirente                              |
| hiper                  | erede              | Adquirente                              |
| visa                   | getnet             | Adquirente                              |
| mastercard             | getnet             | Adquirente                              |
| clearsale              | clearsale          | Análise de Risco                        |
| clearsale_start        | clearsale          | Análise de Risco                        |
| fcontrol_frame         | fcontrol           | Análise de Risco                        |
| fcontrol               | fcontrol           | Análise de Risco                        |
| itaushopline_card      | itaushopline       | Banco                                   |
| itaushopline_billet    | itaushopline       | Banco                                   | 
| billet                 | bradesco           | Banco                                   | 
| visa                   | mercado_pago       | Intermediador                           |
| american_express       | mercado_pago       | Intermediador                           |
| mastercard             | mercado_pago       | Intermediador                           |
| aura                   | mercado_pago       | Intermediador                           |
| diners                 | mercado_pago       | Intermediador                           |
| hipercard              | mercado_pago       | Intermediador                           |
| elo                    | mercado_pago       | Intermediador                           |
| mercadolivre_card      | mercado_pago       | Intermediador                           |
| billet                 | mercado_pago       | Intermediador                           |
| bb_transference        | mercado_pago       | Intermediador                           |
| bradesco_transference  | mercado_pago       | Intermediador                           |
| account_money          | mercado_pago       | Intermediador                           |
| mercado_pago_ws        | mercado_pago       | Intermediador                           |
| moip_redirect          | moip               | Intermediador                           |  
| hipercard              | moip               | Intermediador                           |  
| aura                   | moip               | Intermediador                           |  
| visa                   | moip               | Intermediador                           |  
| mastercard             | moip               | Intermediador                           |  
| american_express       | moip               | Intermediador                           |  
| diners                 | moip               | Intermediador                           |  
| oi_paggo               | moip               | Intermediador                           |  
| billet                 | moip               | Intermediador                           |  
| banrisul               | moip               | Intermediador                           |  
| unibanco               | moip               | Intermediador                           |  
| banco_real             | moip               | Intermediador                           |  
| itau                   | moip               | Intermediador                           |  
| bradesco               | moip               | Intermediador                           |  
| bb                     | moip               | Intermediador                           |    
| pagseguro              | pagseguro          | Intermediador                           |
| palpay_redirect        | paypal             | Intermediador                           | 



| Tabela 2 – Tipo do Produto  |
|-----------------------------|
| physical                    |
| digital                     |
| service                     |


| Tabela 3 – Tipo de Gênero  |
|----------------------------|
| male                       |
| female                     |


| Tabela 4 – Tipos de Endereço |
|--------------|---------------|
| Cobrança     | B             |
| Entrega      | D             |