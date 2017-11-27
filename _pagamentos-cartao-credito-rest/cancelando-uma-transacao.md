---
title: Cancelando uma transação
position: 5
menu: gateway
right_code: |
  ~~~ xml
    curl
        --request PUT https://sandbox.gateway.yapay.com.br/checkout/api/v2/transacao/10000000000000/1234/cancelar
        --header "Content-Type: application/json"
        --curl -u usuario:senha .........
        --data-binary
  ~~~
  {: title="Exemplo cancelamento de transação" }

  ~~~ xml
    --header "Content-Type: application/json"
        {
        "numeroTransacao": 1234,
        "codigoEstabelecimento": "1000000000000",
        "codigoFormaPagamento": 170,
        "valor": 2000,
        "valorDesconto": 0,
        "parcelas": 1,
        "statusTransacao": 13,
        "autorizacao": "123456",
        "codigoTransacaoOperadora": "0",
        "dataAprovacaoOperadora": "24/05/2017",
        "numeroComprovanteVenda": "10069930690009F2122A",
        "nsu": "428706",
        "mensagemVenda": "Operation Success",
        "urlPagamento": "https://sandbox.gateway.yapay.com.br/checkout/PagamentoCielo/PagamentoCielo.do?cod=14956291484887110cf2a-9aeb-4b34-a869-1a61f0611b66",
        "cartoesUtilizados": ["000000*******0001"]
        }
  ~~~
  {: title="Exemplo retorno cancelamento" }

---


Através desta funcionalidade é possível cancelar uma venda pré autorizada ou capturada. Consulte abaixo o prazo de cancelamento para cada adquirente:

| Adquirente | Limite de cancelamento            |
|------------|-----------------------------------|
| Cielo      | 300 dias após a geração do pedido |
| Rede       | 24 horas após geração do pedido   |
| Elavon     | 24 horas após geração do pedido   |
| GETNET     | 24 horas após geração do pedido   |
| Stone      | 180 dias após a geração do pedido |
| Bin        | 90 dias após captura do pedido    |

**REQUISIÇÃO**

<i class="fa fa-info-circle" aria-hidden="true"></i> Para enviar a transação, utilize o método <span class="put">PUT</span>.
{: .informativo }

 Para autenticação, enviar `login` e `senha` no HEADER:

| Campo    | Descrição                |
|----------|--------------------------|
| usuario  | Login do estabelecimento |
| senha    | Senha do estabelecimento |


| Campo                 | Descrição                                                                            |
|-----------------------|--------------------------------------------------------------------------------------|
| numeroTransacao       | Código que identifica a transação dentro do Yapay                                 |
| codigoEstabelecimento | Código que identifica o estabelecimento dentro do Yapay (fornecido pelo gateway)  |
| acao                  | Ação a ser realizada. Enviar "cancelar"                                              |

**RESPOSTA**


| Campo                    | Descrição                                                                | Tipo          | Tamanho             |
|--------------------------|--------------------------------------------------------------------------|---------------|---------------------|
| numeroTransacao          | Código que identifica a transação dentro do Yapay                     | Numérico      | Até 19 dígitos      |
| codigoEstabelecimento    | Código que identifica o estabelecimento dentro do Yapay               | Numérico      | 13 dígitos          |
| codigoFormaPagamento     | <a href="/gateway/rest/codigos-da-api-rest/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                                           | Numérico      | Até 3 dígitos       |
| valor                    | Valor da transação.                                                      | Numérico      | Até 10 dígitos      |
| valorDesconto            | Valor desconto                                                           | Numérico      | Até 10 dígitos      |
| taxaEmbarque             | Valor taxa embarque                                                      | Numérico      | Até 10 dígitos      |
| parcelas                 | Quantidade de parcelas da transação                                      | Numérico      | Até 2 dígitos       |
| urlPagamento             | Para o modelo redirect. Essa será a URL de redirecionamento da operação  | Alfa Numérico | Até 500 caracteres  |
| statusTransacao          | <a href="/gateway/rest/codigos-da-api-rest/#status-de-transacao" target="_blank" class="linkPadraoVerde">Status atual da transação</a>                                             | Numérico      | Até 2 dígitos       |
| autorizacao              | Código de autorização da adquirente                                      | Numérico      | Até 20 dígitos      |
| codigoTransacaoOperadora | Código da transação na adquirente                                        | Numérico      | Até 20 dígitos      |
| dataAprovacaoOperadora   | Data de aprovação na adquirente                                          | Alfa Numérico | Até 10 dígitos      |
| numeroComprovanteVenda   | Número do comprovante de venda                                           | Alfa Numérico | Até 20 dígitos      |
| mensagemVenda            | Mensagem de retorno da adquirente                                        | Alfa Numérico | Até 50 dígitos      |