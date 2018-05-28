---
title: API de Código de Rastreio
position: 7
menu: intermediador
right_code: |
  ~~~ php
    <?php

        $params['access_token'] = 'SEU_ACCESS_TOKEN';
        
        $params['order_number'] = '951478';
        $params['url'] = 'http://www.urlsitedeconsulta.com.br';
        $params['code'] = 'AC44112255698998BR';
        $params['tag_search'] = '1';
        $params['date_posting'] = '01/03/2018';
        $params['date_estimed'] = '30/03/2018';

        $urlPost = "https://api.intermediador.sandbox.yapay.com.br/v1/transactions/trace";

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


  ~~~ javascript
    {
        "access_token": "SEU_ACCESS_TOKEN",
        "order_number": "951478",
        "url": "http://www.urlsitedeconsulta.com.br",
        "code": "AC44112255698998BR",
        "tag_search": "1",
        "date_posting": "01/03/2018",
        "date_estimed": "30/03/2018"
    }
  ~~~
  {: title="JSON" }


---

<span class="post">POST</span><span class="beforePost">/v1/transactions/trace</span>


O Yapay disponibiliza uma versão transparente para a integração do código de postagem do produto da transação.

| Endereço para Integração                                                                             |
|--------------------------|---------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/api/v1/transactions/trace  |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/api/v1/transactions/trace          |
| Protocolo                | Rest/HTTP                                                                 |


Para a integração via <span class="post">POST</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada  |  Obrig.  | Descrição                             |
|-------------------|----------|---------------------------------------|
| access_token      | Sim      | Token de acesso                       |
| order_number      | Sim      | Número do pedido                      |
| url               | Não      | URL do site de consulta de postagem   |
| code              | Sim      | Código de postagem                    |
| tag_search        | Não      | Tag de Busca                          |
| date_posting      | Sim      | Data de Postagem                      |
| date_estimed      | Não      | Data estimada de entrega              |


Veja ao lado uma chamada de API de exemplo.

JSON de Resposta
{: .subtitulo }

A API de Código de Rastreio retorna a resposta em XML.


Exemplo de resposta com sucesso baseando no envio do exemplo acima:

```xml
<transaction>
    <message_response>
        <message>success</message>
    </message_response>
    <data_response>
        <transaction_traces type="array">
            <transaction_trace>
                <id type="integer">251</id>
                <transaction_id type="integer">97602</transaction_id>
                <url></url>
                <code>KA1589874554BR</code>
                <date_posting type="date">2018-04-24</date_posting>
                <date_estimed type="date" nil="true"/>
                <date_confirmated type="date" nil="true"/>
                <tag_search></tag_search>
                <created_at type="dateTime">2018-04-25T11:18:01-03:00</created_at>
                <updated_at type="dateTime">2018-04-25T11:18:01-03:00</updated_at>
            </transaction_trace>
        </transaction_traces>
    </data_response>
</transaction>
```


Mensagens de Erro
{: .subtitulo }

No caso de erro, a API retorna uma mensagem de erro. Assim é possível identificar o erro ocorrido e realizar o tratamento através do código e/ou mensagem retornada.

Abaixo segue os detalhes de cada nó do XML de resposta:


```xml
<transaction>
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
</transaction>
```


As mensagens de erros retornados pela API estão listadas na tabela abaixo:

| Código    |  Mensagem                                        |
|-----------|--------------------------------------------------|
| 003006    | Pedido inválido                                  |
| 017001    | Token de sessão inválido                         |
| 060003    | Token de acesso inválido ou expirado.            |



<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>