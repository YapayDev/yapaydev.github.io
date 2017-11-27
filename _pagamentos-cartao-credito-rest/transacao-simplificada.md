---
title: Transação simplificada
position: 1
menu: gateway
right_code: |
  ~~~ json
  curl
    --request POST https://sandbox.gateway.yapay.com.br/checkout/api/v3/transacao
    --curl -u usuario:senha .........
    --header "Content-Type: application/json"
    --data-binary
    {
      "codigoEstabelecimento" : 1000000000000,
      "codigoFormaPagamento" : 170,
      "transacao" : {
          "numeroTransacao" : 123,
          "valor" : 100,
          "parcelas" : 1,
          "idioma" : 1
      },
      "dadosCartao" : {
          "nomePortador" : "Teste Teste",
          "numeroCartao" : "0000000000000001",
          "codigoSeguranca" : "123",
          "dataValidade" : "12/2017"
      },
      "itensDoPedido" : [
      {
          "quantidadeProduto" : 1,
          "valorUnitarioProduto" : 100
      }
      ],
      "dadosCobranca" : {
          "nome" : "Teste Integração",
          "documento" : "12312312312"
      }
    }
  ~~~
  {: title="Exemplo criação transação" }

  ~~~ json
  --header "Content-Type: application/json"
    {
      "numeroTransacao": 123,
      "codigoEstabelecimento": "1000000000000",
      "codigoFormaPagamento": 170,
      "valor": 2000,
      "valorDesconto": 0,
      "parcelas": 1,
      "statusTransacao": 1,
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
  {: title="Exemplo retorno transação" }
  


---

Estrutura e exemplo de uma transação simples para cartão de crédito. As funcionalidades, como Análise de Fraude, Recorrência, OneClick e demais formas de pagamento precisam de uma estrutura mais completa para um perfeito funcionamento. Consulte as demais estruturas e exemplos desta documentação.

REQUISIÇÃO
{: .subtitulo }

<i class="fa fa-info-circle" aria-hidden="true"></i> Para enviar a transação, utilize o método <span class="post">POST</span>.
{: .informativo }

Para autenticação, enviar `login` e `senha` no HEADER:

| Campo   | Descrição                |
|---------|--------------------------|
| usuario | Login do estabelecimento |
| senha   | Senha do estabelecimento |



| Campo                   | Descrição                                                                                 | Tipo          | Tamanho           | Obrigatório |
|-------------------------|-------------------------------------------------------------------------------------------|---------------|-------------------|-------------|
| codigoEstabelecimento   | Código que identifica o estabelecimento dentro do Yapay (fornecido pelo gateway)       | Numérico      | 13 dígitos        | Sim         |
| codigoFormaPagamento    | <a href="/gateway/rest/codigos-da-api-rest/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                             
                                 | Numérico      | Até 3 dígitos     | Sim         |
| transacao               | Nó reservado para informações da transação                                                | - | - | - |
| dadosCartao             | Nó reservado para dados de cartão                                                         | - | - | - |
| dadosCobranca           | Nó reservado para informações dos dados de cobrança                                       | - | - | - |

_`transacao`_
{: .subtituloAzul }

| Campo           | Descrição                                                                                                      | Tipo          | Tamanho        | Obrigatório |
|-----------------|----------------------------------------------------------------------------------------------------------------|---------------|----------------|-----|
| numeroTransacao | Código que identifica a transação dentro do Yapay                                                              | Numérico      | Até 19 dígitos | Sim |
| valor           | Valor da transação. Deve ser enviado sem pontos ou vírgulas                                                    | Numérico      | Até 10 dígitos | Sim |
| parcelas        | Quantidade de parcelas da transação. Verificar se forma de pagamento suporta parcelamento                      | Numérico      | Até 2 dígitos  | Sim |
| urlCampainha    | URL será sempre acionada quando o status do pedido mudar. Deve estar preparada para receber dados de campainha | Alfa Numérico | Até 250 caracteres | Não
| urlResultado    | Para o modelo de pagamento redirect, O Yapay redirecionará para essa URL                                    | Alfa Numérico | Até 250 caracteres | Para pagamentos redirecionáveis é obrigatório |


_`dadosCartao`_
{: .subtituloAzul }

| Campo           | Descrição                                                                | Tipo          | Tamanho           | Obrigatório |
|-----------------|--------------------------------------------------------------------------|---------------|-------------------|-----|
| nomePortador    | Nome do titular do cartão de crédito (Exatamente como escrito no cartão) | Alfa Numérico | Até 16 dígitos    | Sim |
| numeroCartao    | Numero do cartão de crédito, sem espaços ou traços                       | Numérico      | Até 22 caracteres | Sim |
| codigoSeguranca | Código de segurança do cartão (campo não é armazenado pelo Yapay)     | Numérico      | Até 4 caracteres  | Sim |
| dataValidade    | Data de validade do cartão. Formato mm/yyyy                              | Alfa Numérico | 7 caracteres      | Sim |


_`itensDoPedido`_
{: .subtituloAzul }

| Campo                | Descrição                                                          | Tipo     | Tamanho        | Obrigatório |
|----------------------|--------------------------------------------------------------------|----------|----------------|-------------|
| quantidadeProduto    | Quantidade comprada do produto                                     | Numérico | Até 8 dígitos  | Sim         |
| valorUnitarioProduto | Valor unitário do produto. Deve ser enviado sem pontos ou vírgulas | Numérico | Até 10 dígitos | Sim         |

_`dadosCobranca`_
{: .subtituloAzul }

| Campo     | Descrição                       | Tipo          | Tamanho            | Obrigatório |
|-----------|---------------------------------|---------------|--------------------|-------------|
| nome      | Nome do comprador               | Alfa Numérico | Até 100 caracteres | Não         |
| documento | Documento principal do comprado | Alfa Numérico | 30 caracteres      | Não         |



**RESPOSTA**

| Campo                    | Descrição                                                                | Tipo           | Tamanho            |
|--------------------------|--------------------------------------------------------------------------|----------------|--------------------|
| numeroTransacao          | Código que identifica a transação dentro do Yapay                     | Numérico       | Até 19 dígitos     |
| codigoEstabelecimento    | Código que identifica o estabelecimento dentro do Yapay               | Numérico       | 13 dígitos         |
| codigoFormaPagamento     | <a href="/gateway/rest/codigos-da-api-rest/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                                             | Numérico       | Até 3 dígitos      |
| valor                    | Valor da transação.                                                      | Numérico       | Até 10 dígitos     |
| valorDesconto            | Valor desconto                                                           | Numérico       | Até 10 dígitos     |
| taxaEmbarque             | Valor taxa embarque                                                      | Numérico       | Até 10 dígitos     |
| parcelas                 | Quantidade de parcelas da transação                                      | Numérico       | Até 2 dígitos      |
| urlPagamento             | Para o modelo redirect. Essa será a URL de redirecionamento da operação  | Alfa Numérico  | Até 500 caracteres |
| statusTransacao          | <a href="/gateway/rest/codigos-da-api-rest/#status-de-transacao" target="_blank" class="linkPadraoVerde">Status atual da transação</a> | Numérico       | Até 2 dígitos      |
| autorizacao              | Código de autorização da adquirente                                      | Numérico       | Até 20 dígitos     |
| codigoTransacaoOperadora | Código da transação na adquirente                                        | Numérico       | Até 20 dígitos     |
| dataAprovacaoOperadora   | Data de aprovação na adquirente                                          | Alfa Numérico  | Até 10 dígitos     |
| numeroComprovanteVenda   | Número do comprovante de venda                                           | Alfa Numérico  | Até 20 dígitos     |
| nsu                      | Número do NSU da adquirente                                              | Alfa Numérico  | Até 20 caracteres  |
| mensagemVenda            | Mensagem de retorno da adquirente                                        | Alfa Numérico  | Até 50 dígitos     |
| cartoesUtilizados        | Cartões mascarados utilizados na transação                               | Alfa Numérico  | Até 20 caracteres  |


Ao lado você pode visualizar um exemplo de retorno da transação.
