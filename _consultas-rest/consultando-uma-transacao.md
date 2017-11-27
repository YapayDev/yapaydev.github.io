---
title: Consultando uma Transação
position: 1
menu: gateway
right_code: |
  ~~~ xml
  curl
    --request GET https://sandbox.gateway.yapay.com.br/checkout/api/v3/transacao/10000000000000/1234
    --header "Content-Type: application/json"
    --curl -u usuario:senha .........
    --data-binary

  ~~~
  {: title="Exemplo de consulta" }

  ~~~ xml
  --header "Content-Type: application/json"
    {   "numeroTransacao": 1234,
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
  {: title="Exemplo retorno de consulta" }

---

Para receber novamente os dados de retorno de uma venda, realize uma consulta.

REQUISIÇÃO
{: .subtitulo }

<i class="fa fa-info-circle" aria-hidden="true"></i> Para consultas, acione o método <span class="get">GET</span>.
{: .informativo }

Para autenticação, enviar `usuario` e `senha` no HEADER:

| Campo   | Descrição                |
|---------|--------------------------|
| usuario | Login do estabelecimento |
| senha   | Senha do estabelecimento |


| Campo                 | Descrição                                                                           | Tipo     | Tamanho       | Obrigatório |
|-----------------------|-------------------------------------------------------------------------------------|----------|---------------|-------------|
| numeroTransacao       | Código que identifica a transação dentro do Yapay                                   | Numérico | Até 8 dígitos | Sim         |
| codigoEstabelecimento | Código que identifica o estabelecimento dentro do Yapay (fornecido pelo gateway) | Numérico | 13 dígitos    | Sim         |


**RESPOSTA**

| Campo                    | Descrição                                                  | Tipo          | Tamanho            |
|--------------------------|------------------------------------------------------------|---------------|--------------------|
| numeroTransacao          | Código que identifica a transação dentro do Yapay       | Numérico      | Até 19 dígitos     |
| codigoEstabelecimento    | Código que identifica o estabelecimento dentro do Yapay | Numérico      | 13 dígitos         |
| codigoFormaPagamento     | Código da forma de pagamento                               | Numérico      | Até 3 dígitos      |
| valor                    | Valor da transação.                                        | Numérico      | Até 10 dígitos     |
| valorDesconto            | Valor desconto                                             | Numérico      | Até 10 dígitos     |
| taxaEmbarque             | Valor taxa embarque                                        | Numérico      | Até 10 dígitos     |
| parcelas                 | Quantidade de parcelas da transação                        | Numérico      | Até 2 dígitos      |
| urlPagamento             | Url para autenticação em caso de cartão de débito          | Alfa Numérico | Até 500 caracteres |
| statusTransacao          | Status atual da transação                                  | Numérico      | Até 2 dígitos      |
| autorizacao              | Número de autorização da adquirente                        | Numérico      | Até 20 dígitos     |
| codigoTransacaoOperadora | Código de retorno da adquirente                            | Numérico      | Até 20 dígitos     |
| dataAprovacaoOperadora   | Data aprovação                                             | Alfa Numérico | Até 10 dígitos     |
| numeroComprovanteVenda   | Número Comprovante de venda                                | Alfa Numérico | Até 20 dígitos     |
| mensagemVenda            | Mensagem de venda                                          | Alfa Numérico | Até 50 dígitos     |
| cartoesUtilizados        | Cartões mascarados utilizados na transação                 | Alfa Numérico | Até 20 caracteres  |