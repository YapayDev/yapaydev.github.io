---
title: Cancelando transação parcialmente 
position: 5
menu: gateway
right_code: |
  ~~~ xml
  curl
    --request PUT https://sandbox.gateway.yapay.com.br/checkout/api/v3/transacao/10000000000000/1234/cancelar?valor=1000
    --header "Content-Type: application/json"
    --curl -u usuario:senha
    --data-binary
  ~~~
  {: title="Exemplo cancelamento parcial" }

  ~~~ json
  --header "Content-Type: application/json"
    {
      "numeroTransacao": 1234,
      "codigoEstabelecimento": "1000000000000",
      "codigoFormaPagamento": 170,
      "valor": 2000,
      "valorDesconto": 0,
      "parcelas": 1,
      "statusTransacao": 27,
      "autorizacao": "123456",
      "codigoTransacaoOperadora": "0",
      "dataAprovacaoOperadora": "2018-01-03 13:02:53",
      "numeroComprovanteVenda": "10069930690009F2122A",
      "nsu": "428706",
      "mensagemVenda": "Operation Success",
      "urlPagamento": "14956291484887110cf2a-9aeb-4b34-a869-1a61f0611b66",
      "cartoesUtilizados": ["000000*******0001"]
    }
  ~~~
  {: title="Exemplo retorno cancelamento parcial" }

---


Através desta funcionalidade é possível cancelar uma venda parcialmente. Consulte abaixo as adquirentes que fornecem o cancelamento parcial e o prazo de cancelamento:

| Adquirente | Tecnologia | Limite de cancelamento                                         |
|------------|------------|----------------------------------------------------------------|
| Cielo      | API 3.0    | 300 dias após a geração do pedido                              |
| Rede       | E Rede     | Pode variar conforme o ramo de atuação de cada estabelecimento |


**Particulariedades**

* Disponível apenas no plano corporativo;
* Disponível apenas nas adquirentes Cielo ou Rede, nas tecnologias informadas acima.


<i class="fa fa-info-circle" aria-hidden="true"></i> Para enviar a transação, utilize o método <span class="put">PUT</span>.
{: .informativo }

 Para autenticação, enviar `login` e `senha` no HEADER:

| Campo    | Descrição                |
|----------|--------------------------|
| usuario  | Login do estabelecimento |
| senha    | Senha do estabelecimento |


| Campo                 | Descrição                                                                           |
|-----------------------|-------------------------------------------------------------------------------------|
| numeroTransacao       | Código que identifica a transação dentro da Yapay                                |
| codigoEstabelecimento | Código que identifica o estabelecimento dentro da Yapay (fornecido pelo gateway) |
| acao                  | Ação a ser realizada. Enviar "cancelar"                                             |
| valor                 | Valor a ser cancelado                                                               |



**RESPOSTA**

Exemplo retorno de cancelamento de transação ao lado.

| Campo                    | Descrição                                                                                   | Tipo          | Tamanho            |
|--------------------------|---------------------------------------------------------------------------------------------|---------------|--------------------|
| numeroTransacao          | Código que identifica a transação dentro do SuperPay                                        | Numérico      | Até 19 dígitos     |
| codigoEstabelecimento    | Código que identifica o estabelecimento dentro do SuperPay                                  | Numérico      | Até 13 dígitos     |
| codigoFormaPagamento     | <a href="/gateway/rest/codigos-da-api-rest/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                                                                | Numérico      | Até 3 dígitos      |
| valor                    | Valor da transação.                                                                         | Numérico      | Até 10 dígitos     |
| valorDesconto            | Valor desconto                                                                              | Numérico      | Até 10 dígitos     |
| taxaEmbarque             | Valor taxa embarque                                                                         | Numérico      | Até 10 dígitos     |
| parcelas                 | Quantidade de parcelas da transação                                                         | Numérico      | Até 2 dígitos      |
| urlPagamento             | Para o modelo redirect. Essa será a URL de redirecionamento da operação                     | Alfa Numérico | Até 500 caracteres |
| statusTransacao          | Status atual da transação Retornado código 27 se o cancelamento parcial ocorrer com sucesso | Numérico      | Até 2 dígitos      | 
| autorizacao              | Código de autorização da adquirente                                                         | Numérico      | Até 20 dígitos     | 
| codigoTransacaoOperadora | Código da transação na adquirente                                                           | Numérico      | Até 20 dígitos     | 
| dataAprovacaoOperadora   | Data de aprovação na adquirente                                                             | Alfa Numérico | Até 10 dígitos     |
| numeroComprovanteVenda   | Número do comprovante de venda                                                              | Alfa Numérico | Até 20 dígitos     |
| mensagemVenda            | Mensagem de retorno da adquirente                                                           | Alfa Numérico | Até 50 dígitos     |
| cartoesUtilizados        | Número de cartão truncado utilizado na transação                                            | Alfa Numérico | Até 20 dígitos     |




<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>