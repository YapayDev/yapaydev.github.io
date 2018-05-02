---
title: Transação simplificada
position: 1
menu: gateway
right_code: |
  ~~~ json
  curl
    --request POST https://sandbox.gateway.yapay.com.br/checkout/api/v3/transacao
    --header "Content-Type: application/json"
    --curl -u usuario:senha .........
    --data-binary
    {
      "codigoEstabelecimento" : 1000000000000,
      "codigoFormaPagamento" : 179,
      "transacao" : {
          "numeroTransacao" : 123,
          "valor" : 100,
          "parcelas" : 1,
          "idioma" : 1,
          "urlCampainha" : "http://seusite.com.br/campainha",
          "urlResultado" : "http://seusite.com.br/retorno"
      },
      "dadosCartao" : {
          "nomePortador" : "Teste Teste",
          "numeroCartao" : "0000000000000001",
          "codigoSeguranca" : "123",
          "dataValidade" : "12/2030"
      },
      "itensDoPedido" : [
      {
          "codigoProduto" : 1,
          "nomeProduto" : "Produto 1",
          "codigoCategoria" : 1,
          "nomeCategoria" : "categoria",
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
      "dataAprovacaoOperadora": "24/05/2030",
      "numeroComprovanteVenda": "10069930690009F2122A",
      "nsu": "428706",
      "mensagemVenda": "Operation Success",
      "urlPagamento": "https://sandbox.gateway.yapay.com.br/checkout/PagamentoCielo/PagamentoVisaElectron.do?cod=14132971582229c00506d-e84d-4526-b902-92190d5aa808",
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
| urlCampainha    | URL será sempre acionada quando o status do pedido mudar. Deve estar preparada para receber dados de campainha | Alfa Numérico | Até 250 caracteres | Sim
| urlResultado    | Para o modelo de pagamento redirect, O Yapay redirecionará para essa URL                                    | Alfa Numérico | Até 250 caracteres | Para pagamentos redirecionáveis é obrigatório |


_`dadosCobranca`_
{: .subtituloAzul }

| Campo     | Descrição                       | Tipo          | Tamanho            | Obrigatório |
|-----------|---------------------------------|---------------|--------------------|-------------|
| nome      | Nome do comprador               | Alfa Numérico | Até 100 caracteres | Não         |
| documento | Documento principal do comprado | Alfa Numérico | 30 caracteres      | Não         |


_`telefone`_
{: .subtituloAzul }

| Campo        | Descrição                                                                                  | Tipo          | Obrigatório |
|--------------|--------------------------------------------------------------------------------------------|---------------|-------------|
| tipoTelefone | 1 = Outros / 2 = Residencial / 3 = Comercial / 4 = Recados / 5 = Cobrança / 6 = Temporário | Numérico      | Sim         |
| ddi          | Código DDI do telefone                                                                     | Alfa Numérico | Sim         |
| ddd          | Código DDD do telefone                                                                     | Alfa Numérico | Sim         |
| telefone     | Número do telefone                                                                         | Alfa Numérico | Sim         |

_`dadosEntrega`_
{: .subtituloAzul }

| Campo    | Descrição                                        | Tipo          | Tamanho       | Obrigatório |
|----------|--------------------------------------------------|---------------|---------------|-------------|
| nome     | Nome do comprador                                | Alfa Numérico | 20 caracteres | Não         |
| email    | E-mail do comprador                              | Alfa Numérico | 20 caracteres | Não         |
| endereco | Nó reservado para dados de endereço do comprador | -             | -             | -           |
| telefone | Nó reservado para dados de telefone do comprador | -             | -             | -           |


**RESPOSTA**

Para geração do boleto o eCommerce deverá redirecionar o consumidor para a URl retornada no campo

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
| statusTransacao          | <a href="/gateway/codigos-da-api/#status-de-transacao" target="_blank" class="linkPadraoVerde">Status atual da transação</a> | Numérico       | Até 2 dígitos      |
| autorizacao              | Código de autorização da adquirente                                      | Numérico       | Até 20 dígitos     |
| codigoTransacaoOperadora | Código da transação na adquirente                                        | Numérico       | Até 20 dígitos     |
| dataAprovacaoOperadora   | Data de aprovação na adquirente                                          | Alfa Numérico  | Até 10 dígitos     |
| numeroComprovanteVenda   | Número do comprovante de venda                                           | Alfa Numérico  | Até 20 dígitos     |
| mensagemVenda            | Mensagem de retorno da adquirente                                        | Alfa Numérico  | Até 50 dígitos     |


Ao lado você pode visualizar um exemplo de retorno da transação.



<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>