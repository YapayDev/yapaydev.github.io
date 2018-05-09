---
title: Cancelando uma recorrência
position: 3
menu: gateway
right_code: |
  ~~~ xml
  curl
    --request PUT https://sandbox.gateway.yapay.com.br/checkout/api/v3/recorrencia/10000000000000/2/cancelar
    --header "Content-Type: application/json"
    --curl -u usuario:senha .........
    --data-binary
  ~~~
  {: title="Exemplo cancelamento de transação" }

  ~~~ xml
  --header "Content-Type: application/json"
    "recorrencia": {
      "estabelecimento": "1000000000000",
      "numeroRecorrencia": 2,
      "codigoFormaPagamento": 170,
      "valor": 13000,
      "numeroCobrancaTotal": 3,
      "numeroCobrancaRestantes": 3,
      "status": 0,
      "mensagem": "Recorrência cancelada com sucesso.",
      "numeroPedido": null,
      "statusTransacao": null,
      "autorizacao": null,
      "codigoTransacaoOperadora": null,
      "dataAprovacaoOperadora": null,
      "numeroComprovanteVenda": null,
      "mensagemVenda": null
      }


  ~~~
  {: title="Exemplo retorno cancelamento" }

---


**REQUISIÇÃO**

<i class="fa fa-info-circle" aria-hidden="true"></i> Para cancelar uma recorrência, utilize o método <span class="put">PUT</span>.
{: .informativo }

 Para autenticação, enviar `login` e `senha` no HEADER:

| Campo    | Descrição                |
|----------|--------------------------|
| usuario  | Login do estabelecimento |
| senha    | Senha do estabelecimento |



| Campo             | Descrição                                                                           | Tipo       |
|-------------------|-------------------------------------------------------------------------------------|------------|
| numeroRecorrencia | Número da Recorrência a ser cancelada                                               | Numérico   |
| estabelecimento   | Código que identifica o estabelecimento dentro do Yapay (fornecido pelo gateway) | Numérico   |
| acao              | Ação para realizar o processamento                                                  | "cancelar" |


**RESPOSTA**

| Campo                    | Descrição                                          |
|--------------------------|----------------------------------------------------|
| numeroRecorrencia        | Número da Recorrência                              |
| estabelecimento          | Código do estabelecimento, fornecido pelo Yapay |
| valor                    | Valor                                              |
| codigoFormaPagamento     | <a href="/gateway/rest/codigos-da-api-rest/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a> |
| numeroCobrancaTotal      | Quantidade máxima de cobranças                     |
| numeroCobrancaRestantes  | Quantidade de cobranças restantes                  |
| status                   | Status atual da recorrência                        |
| mensagem                 | Mensagem da recorrência                            |
| numeroPedido             | Número da Cobrança Recorrente                      |
| statusTransacao          | Status atual da transação recorrente               |
| autorizacao              | Código de autorização da Adquirente                |
| codigoTransacaoOperadora | <a href="/gateway/codigos-da-api/#status-de-transacao" target="_blank" class="linkPadraoVerde">Status atual da transação</a> |
| dataAprovacaoOperadora   | Data aprovação Adquirente                          |
| numeroComprovanteVenda   | Número Comprovante Adquirente                      |
| mensagemVenda            | Mensagem Venda Adquirente                          |

Ao lado você pode visualizar um exemplo de retorno da transação.


<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>