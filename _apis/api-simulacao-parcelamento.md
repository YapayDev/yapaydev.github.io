---
title: API de Simulação de Parcelamento
position: 13
menu: intermediador
right_code: |
  ~~~ php
    <?php
        
            

        /* Valor da Transação */
        $params['price'] = '1134.30';


        $urlPost = "https://api.intermediador.sandbox.yapay.com.br/v1/transactions/simulate_splitting";

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

<span class="post">POST</span><span class="beforePost">/api/v1/transactions/simulate_splitting</span>

O Yapay disponibiliza a API de Simulação de Cálculo de Parcelamento para facilitar o calculo de parcelamento, onde através do token do lojista e o valor da transação, é retornada a simulação do parcelamento de todas as formas de pagamento.

A API de Simulação de Cálculo de Parcelamento é utilizada somente para facilitar a exibição deste parcelamento na loja virtual, onde é enviada somente a quantidade de parcelas para a <a href="/intermediador/apis/#api-transacao" target="_blank" class="linkPadraoVerde">API de Transação</a>.

| Endereço para Integração                                                                                |
|--------------------------|------------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/v1/transactions/simulate_splitting   |
| Ambiente de Produção     | http://api.intermediador.yapay.com.br/v1/transactions/simulate_splitting           |
| Protocolo                | Rest/HTTP                                                                    |

Para a integração via <span class="post">POST</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada |  Obrig.  | Formato / Tam. Max   | Descrição                     |
|------------------|----------|----------------------|-------------------------------|
| token_account    |   Sim    |  Texto / 20          |  Token da conta da Loja       |
| price            |   Sim    |  Decimal / 11        |  Valor da Transação           |
| type_response    |   Não    |  Decimal / 11        |  Tipo de Resposta  `J => JSON, OUTROS => XML`         |

Veja ao lado uma chamada de API de exemplo:

Resposta da API
{: .subtitulo }

A API de Simulação de Parcelamento retorna a resposta em XML ou JSON. Na resposta é mostrado todos os meios de pagamentos disponíveis.

Abaixo um detalhamento de cada nó do JSON de resposta:


```javascript
{
    "message_response": {
        "message": "success"
    },
    "data_response": {
        "payment_methods": [
            {
                "splittings": [
                    {
                        "split": 1,
                        "value_split": "1000.00",
                        "value_transaction": "1000.00",
                        "addition_retention": "0.00",
                        "split_rate": 0
                    },
                    {
                        "split": 2,
                        "value_split": "514.97",
                        "value_transaction": "1029.94",
                        "addition_retention": "0.00",
                        "split_rate": "1.99"
                    },
                    {
                        "split": 3,
                        "value_split": "346.69",
                        "value_transaction": "1040.07",
                        "addition_retention": "0.00",
                        "split_rate": "1.99"
                    },
                    {
                        "split": 4,
                        "value_split": "268.96",
                        "value_transaction": "1075.84",
                        "addition_retention": "0.00",
                        "split_rate": "2.99"
                    },
                    {
                        "split": 5,
                        "value_split": "218.29",
                        "value_transaction": "1091.45",
                        "addition_retention": "0.00",
                        "split_rate": "2.99"
                    },
                    {
                        "split": 6,
                        "value_split": "184.54",
                        "value_transaction": "1107.24",
                        "addition_retention": "0.00",
                        "split_rate": "2.99"
                    },
                    {
                        "split": 7,
                        "value_split": "160.45",
                        "value_transaction": "1123.15",
                        "addition_retention": "0.00",
                        "split_rate": "2.99"
                    },
                    {
                        "split": 8,
                        "value_split": "148.47",
                        "value_transaction": "1187.76",
                        "addition_retention": "0.00",
                        "split_rate": "3.99"
                    },
                    {
                        "split": 9,
                        "value_split": "134.43",
                        "value_transaction": "1209.87",
                        "addition_retention": "0.00",
                        "split_rate": "3.99"
                    },
                    {
                        "split": 10,
                        "value_split": "123.23",
                        "value_transaction": "1232.30",
                        "addition_retention": "0.00",
                        "split_rate": "3.99"
                    },
                    {
                        "split": 11,
                        "value_split": "114.09",
                        "value_transaction": "1254.99",
                        "addition_retention": "0.00",
                        "split_rate": "3.99"
                    },
                    {
                        "split": 12,
                        "value_split": "106.49",
                        "value_transaction": "1277.88",
                        "addition_retention": "0.00",
                        "split_rate": "3.99"
                    }
                ],
                "price_customer": "1000.00",
                "price_seller": "935.70",
                "price_original": "1000.00",
                "split": 12,
                "payment_method_name": "Visa",
                "payment_method_id": 3
            }
        ]
    }
}
```



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

<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>