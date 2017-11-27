---
title: API de Simulação de Parcelamento
position: 8
menu: intermediador
right_code: |
  ~~~ php
    <?php
        /* Token da conta da Loja */
        $params['token_account'] = '4f14b0a42dd2fe0';        

        /* Valor da Transação */
        $params['price'] = '1134.30';


        $urlPost = "https://api.sandbox.traycheckout.com.br/v1/transactions/simulate_splitting";

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
---

O TrayCheckout disponibiliza a API de Simulação de Cálculo de Parcelamento para facilitar o calculo de parcelamento, onde através do token do lojista e o valor da transação, é retornada a simulação do parcelamento de todas as formas de pagamento.

A API de Simulação de Cálculo de Parcelamento é utilizada somente para facilitar a exibição deste parcelamento na loja virtual, onde é enviada somente a quantidade de parcelas para a <a href="/intermediador/apis/#api-transacao" target="_blank" class="linkPadraoVerde">API de Transação</a>.

| Endereço para Integração                                                                                |
|--------------------------|------------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.sandbox.traycheckout.com.br/v1/transactions/simulate_splitting   |
| Ambiente de Produção     | https://api.traycheckout.com.br/v1/transactions/simulate_splitting           |
| Protocolo                | Rest/HTTP                                                                    |

Para a integração via POST, segue abaixo os dados necessários para envio:

| Dados de Entrada                       |  Obrig.  | Formato / Tam. Max   | Descrição                     |
|----------------------------------------|----------|----------------------|-------------------------------|
| token_account                          |   Sim    |  Texto / 20          |  Token da conta da Loja       |   
| price                                  |   Sim    |  Decimal / 11        |  Valor da Transação           |   

Veja ao lado uma chamada de API de exemplo:

XML de Resposta
{: .subtitulo }

A API de Processamento de Transações retorna a resposta em XML.

Abaixo um detalhamento de cada nó do XML de resposta:

```xml         
<transaction>                                                      Nó principal da resposta
                  
<transaction>                  
    <data_response>                                                Nó que contém o resultado da resposta
                  
<transaction>                  
    <data_response>                  
        <payment_methods type="array">                             Nó que contém os métodos de pagamento
                  
<transaction>                  
    <data_response>                  
        <payment_methods type="array">                  
            <payment_method>                                       Nó que contém o método de pagamento
         
<transaction>         
    <data_response>         
        <payment_methods type="array">         
            <payment_method>         
                <splittings type="array">                          Nó que contém os detalhamentos dos pagamentos
                   
<transaction>                   
    <data_response>                   
        <payment_methods type="array">                   
            <payment_method>                   
                <splittings type="array">                   
                    <splitting>                                    Nó que contém o detalhamento do pagamento
                   
<transaction>                   
    <data_response>                   
        <payment_methods type="array">                   
            <payment_method>                   
                <splittings type="array">                   
                    <splitting>                                       
                        <split type="integer">                     Número da parcela
         
<transaction>         
    <data_response>         
        <payment_methods type="array">         
            <payment_method>         
                <splittings type="array">         
                    <splitting>                                                     
                        <value_split>1134.30</value_split>         Valor da parcela

<transaction>
    <data_response>
        <payment_methods type="array">
            <payment_method>
                <splittings type="array">
                    <splitting>                    
                        <value_transaction>                        Valor da transação

<transaction>
    <data_response>
        <payment_methods type="array">
            <payment_method>
                <splittings type="array">
                    <splitting>                    
                        <addition_retention>                       Valor adicionar

<transaction>
    <data_response>
        <payment_methods type="array">
            <payment_method>
                <splittings type="array">
                    <splitting>                    
                        <split_rate type="integer">                Taxa do parcelamento
```


Exemplo de resposta com sucesso baseando no envio do exemplo acima:


``` xml
<?xml version="1.0" encoding="UTF-8"?>
<transaction>
    <data_response>
        <payment_methods type="array">
            <payment_method>
                <splittings type="array">
                    <splitting>
                        <split type="integer">1</split>
                        <value_split>1134.30</value_split>
                        <value_transaction>1134.30</value_transaction>
                        <addition_retention>0.00</addition_retention>
                        <split_rate type="integer">0</split_rate>
                    </splitting>
                    <splitting>
                        <split type="integer">2</split>
                        <value_split>584.14</value_split>
                        <value_transaction>1168.28</value_transaction>
                        <addition_retention>0.00</addition_retention>
                        <split_rate type="decimal">1.99</split_rate>
                    </splitting>                    
                </splittings>
                <price_customer>1134.30</price_customer>
                <price_seller>1061.42</price_seller>
                <price_original>1134.30</price_original>
                <split type="integer">12</split>
                <payment_method_name>Visa</payment_method_name>
                <payment_method_id type="integer">3</payment_method_id>
            </payment_method>
            <payment_method>
                <splittings type="array">
                    <splitting>
                        <split type="integer">1</split>
                        <value_split>1134.30</value_split>
                        <value_transaction>1134.30</value_transaction>
                        <addition_retention>0.00</addition_retention>
                        <split_rate type="integer">0</split_rate>
                    </splitting>
                    <splitting>
                        <split type="integer">2</split>
                        <value_split>584.14</value_split>
                        <value_transaction>1168.28</value_transaction>
                        <addition_retention>0.00</addition_retention>
                        <split_rate type="decimal">1.99</split_rate>
                    </splitting>                    
                </splittings>
                <price_customer>1134.30</price_customer>
                <price_seller>1061.42</price_seller>
                <price_original>1134.30</price_original>
                <split type="integer">12</split>
                <payment_method_name>Mastercard</payment_method_name>
                <payment_method_id type="integer">4</payment_method_id>
            </payment_method>
            <payment_method>
                <splittings type="array">
                    <splitting>
                        <split type="integer">1</split>
                        <value_split>1134.30</value_split>
                        <value_transaction>1134.30</value_transaction>
                        <addition_retention>0.00</addition_retention>
                        <split_rate type="integer">0</split_rate>
                    </splitting>
                </splittings>
                <price_customer>1134.30</price_customer>
                <price_seller>1061.42</price_seller>
                <price_original>1134.30</price_original>
                <split type="integer">1</split>
                <payment_method_name>Boleto Bancario</payment_method_name>
                <payment_method_id type="integer">6</payment_method_id>
            </payment_method>
    </data_response>
    <message_response>
        <message>success</message>
    </message_response>
</transaction>

```

Mensagens de Erro
{: .subtitulo }

No caso de erro, a API retorna uma mensagem de erro. Assim é possível identificar o erro ocorrido e realizar o tratamento através do código e/ou mensagem retornada.

Abaixo segue os detalhes de cada nó do XML de resposta:    

```xml
<transaction>                                 Nó principal da resposta

<transaction>
    <error_response>                          Nó que contém o resultado da resposta  

<transaction>    
    <error_response>
        <errors type="array">                 Nó que contém os erros encontrados

<transaction>    
    <error_response>
        <errors type="array">
            <error>                           Nó que contém o detalhamento de um erro

<transaction>    
    <error_response>
        <errors type="array">
            <error> 
                <code>                        Código do erro retornado

<transaction>    
    <error_response>
        <errors type="array">
            <error> 
                <message>                     Mensagem de erro retornada

<transaction>    
    <message_response>                        Nó que contém o resultado da resposta
        
<transaction>    
    <message_response>        
        <message>                             Resposta sobre a solicitação 
                                              Em caso de sucesso: success 
                                              Em caso de erro: error

```

Exemplo de um retorno com erro:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<transaction>
    <error_response>
        <errors type="array">
            <error>
                <code>001001</code>
                <message>Token inválido ou não encontrado</message>
            </error>
        </errors>
    </error_response>
    <message_response>
        <message>error</message>
    </message_response>
</transaction>
```

As mensagens de erros retornados pela API estão listadas na tabela abaixo:

| Código   |  Mensagem                                        | 
|----------|--------------------------------------------------|
|  001001  | Token inválido ou não encontrado             |
|  003002  | Valor da Transação Inválido                  |
|  003010  | Forma de pagamento inválida                  |
|  003004  | Número da Parcela Inválido                   |
|  009006  | Número da parcela maior que o permitido      |
|  009003  | Tabela taxa inativa ou não encontrada        |
       
Tabelas Auxiliares
{: .subtitulo }

Na integração existem alguns campos com informações pré-definidas, onde deverão ser enviadas conforme o padrão existente, se for necessário enviar o campo na requisição, ou poderá tratar a informação conforme retorno recebido.

Abaixo segue tabelas com essas informações pré-definidas:

| Tabela 1 – Status da Transação  |                       
|---------------------------|-----|
| Aguardando Pagamento      | 4   |
| Em Processamento          | 5   |
| Aprovada                  | 6   |
| Cancelada                 | 7   |
| Em Contestação            | 24  |
| Em Monitoramento          | 87  |
| Em Recuperação            | 88  |
| Reprovada                 | 89  |