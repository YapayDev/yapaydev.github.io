---
title: Capturando uma transação
position: 4
menu: gateway
right_code: |
    ~~~json
    curl
        --request PUT https://sandbox.gateway.yapay.com.br/checkout/api/v3/transacao/1000000000000/1234/capturar
        --curl -u usuario:senha .........
        --header "Content-Type: application/json"
        --data-binary

    ~~~
    {: title="Exemplo captura de transação" }

    ~~~json
    --header "Content-Type: application/json"
        {
        "numeroTransacao": 1234,
        "codigoEstabelecimento": "1000000000000",
        "codigoFormaPagamento": 170,
        "valor": 2000,
        "valorDesconto": 0,
        "parcelas": 1,
        "statusTransacao": 1,
        "autorizacao": "123456",
        "codigoTransacaoOperadora": "0",
        "dataAprovacaoOperadora": "24/05/2030",
        "numeroComprovanteVenda": "10069930690009F2122A",
        "nsu": "428706",
        "mensagemVenda": "Operation Success",
        "urlPagamento": "https://sandbox.gateway.yapay.com.br/checkout/PagamentoCielo/PagamentoCielo.do?cod=14956291484887110cf2a-9aeb-4b34-a869-1a61f0611b66",
        "cartoesUtilizados": ["000000*******0001"]
        }


    ~~~    
    {: title="Exemplo retorno da captura" }
---

Através desta funcionalidade é possível confirmar uma pré autorização na adquirente, assim o consumidor receberá a cobrança em seu cartão e gerará crédito ao lojista. Os estabelecimentos com captura manual deverão acionar o método de captura em até 5 dias da criação da venda, pois após este período a adquirente cancelará automaticamente a pré autorização.


**REQUISIÇÃO**

<i class="fa fa-info-circle" aria-hidden="true"></i> Para enviar a transação, utilize o método <span class="put">PUT</span>.
{: .informativo }

 Para autenticação, enviar `login` e `senha` no HEADER:

| Campo    | Descrição                |
|----------|--------------------------|
| usuario  | Login do estabelecimento |
| senha    | Senha do estabelecimento |


| Campo                 | Descrição                                                                           |
|-----------------------|-------------------------------------------------------------------------------------|
| numeroTransacao       | Código que identifica a transação dentro do Yapay                                |
| codigoEstabelecimento | Código que identifica o estabelecimento dentro do Yapay (fornecido pelo gateway) |
| acao                  | Ação a ser realizada. Enviar "capturar"                                             |



**RESPOSTA**

| Campo                    | Descrição                                                               | Tipo          | Tamanho            |
|--------------------------|-------------------------------------------------------------------------|---------------|--------------------|
| numeroTransacao          | Código que identifica a transação dentro do Yapay                    | Numérico      | Até 19 dígitos     |
| codigoEstabelecimento    | Código que identifica o estabelecimento dentro do Yapay              | Numérico      | 13 dígitos         |
| codigoFormaPagamento     | <a href="/gateway/rest/codigos-da-api-rest/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                                            | Numérico      | Até 3 dígitos      |
| valor                    | Valor da transação.                                                     | Numérico      | Até 10 dígitos     |
| valorDesconto            | Valor desconto                                                          | Numérico      | Até 10 dígitos     |
| taxaEmbarque             | Valor taxa embarque                                                     | Numérico      | Até 10 dígitos     |
| parcelas                 | Quantidade de parcelas da transação                                     | Numérico      | Até 2 dígitos      |
| urlPagamento             | Para o modelo redirect. Essa será a URL de redirecionamento da operação | Alfa Numérico | Até 500 caracteres |
| statusTransacao          | <a href="/gateway/rest/codigos-da-api-rest/#status-de-transacao" target="_blank" class="linkPadraoVerde">Status atual da transação</a>                                               | Numérico      | Até 2 dígitos      |
| autorizacao              | Código de autorização da adquirente                                     | Numérico      | Até 20 dígitos     |
| codigoTransacaoOperadora | Código da transação na adquirente                                       | Numérico      | Até 20 dígitos     |
| dataAprovacaoOperadora   | Data de aprovação na adquirente                                         | Alfa Numérico | Até 10 dígitos     |
| numeroComprovanteVenda   | Número do comprovante de venda                                          | Alfa Numérico | Até 20 dígitos     |
| mensagemVenda            | Mensagem de retorno da adquirente                                       | Alfa Numérico | Até 50 dígitos     |
| cartoesUtilizados        | Número de cartão truncado utilizado na transação                        | Alfa Numérico | Até 20 dígitos     |

Ao lado você pode visualizar um exemplo de retorno da transação.



<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>