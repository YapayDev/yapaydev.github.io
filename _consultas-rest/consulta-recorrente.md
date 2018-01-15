---
title: Consulta recorrente
position: 2
menu: gateway
right_code: |
  ~~~ xml
  curl
    --request GET https://sandbox.gateway.yapay.com.br/checkout/api/v3/recorrencia/10000000000000/2
    --header "Content-Type: application/json"
    --curl -u usuario:senha .........
    --data-binary
  ~~~
  {: title="Exemplo criação transação" }

  ~~~ xml
  --header "Content-Type: application/json"
    "recorrencia": {
      "estabelecimento": "1000000000000",
      "numeroRecorrencia": 2,
      "codigoFormaPagamento": 170,
      "valor": 13000,
      "numeroCobrancaTotal": 0,
      "numeroCobrancaRestantes": -1,
      "status": 0,
      "mensagem": "Processamento realizado com sucesso.",
      "numeroPedido": 20001,
      "statusTransacao": 1,
      "autorizacao": "123456",
      "codigoTransacaoOperadora": "00",
      "dataAprovacaoOperadora": "30/05/2017",
      "numeroComprovanteVenda": "1006993069000891071A",
      "mensagemVenda": "Operation Success"
      }

  ~~~
  {: title="Exemplo retorno transação" }

---

Consulta para receber informações da recorrência e da última cobrança realizada.


REQUISIÇÃO
{: .subtitulo }

<i class="fa fa-info-circle" aria-hidden="true"></i> Para consultas, acione o método <span class="get">GET</span>.
{: .informativo }

Para autenticação, enviar `usuario` e `senha` no HEADER:

| Campo   | Descrição                |
|---------|--------------------------|
| usuario | Login do estabelecimento |
| senha   | Senha do estabelecimento |


| Campo             | Descrição                                                                           | Tipo     | Tamanho       | Obrigatório |
|-------------------|-------------------------------------------------------------------------------------|----------|---------------|-------------|
| numeroRecorrencia | Número da Recorrência a ser consultado                                              | Numérico | Até 8 dígitos | Sim         |
| estabelecimento   | Código que identifica o estabelecimento dentro do Yapay (fornecido pelo gateway) | Numérico | 3 dígitos     | Sim         |

**RESPOSTA**

| Campo                    | Descrição                                                                                                                                    |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| numeroRecorrencia        | Número da Recorrência                                                                                                                        |
| estabelecimento          | Código do estabelecimento, fornecido pelo Yapay                                                                                           |
| valor                    | Valor                                                                                                                                        |
| statusTransacao          | Status atual da transação recorrente                                                                                                         |
| numeroPedido             | Número do Pedido                                                                                                                             |
| numeroCobrancaTotal      | Quantidade total de cobranças pedidas no cadastro. Caso não tenha sido pedido um valor limite, este campo retornará a mensagem: “Sem Limite" |
| numeroCobrancaRestantes  | Quantidade restante de cobranças a serem efetuadas.                                                                                          |
| autorizacao              | Código de autorização retornado pela operadora. Retornado apenas se alguma cobrança já ocorreu                                               |
| codigoTransacaoOperadora | Código de transação retornado pela operadora. Retornado apenas se alguma cobrança já ocorreu                                                 |
| dataAprovacaoOperadora   | Data de aprovação retornado pela operadora. Retornado apenas se alguma cobrança já ocorreu                                                   |
| numeroComprovanteVenda   | Número do comprovante de venda retornado pela operadora. Retornado apenas se alguma cobrança já ocorreu                                      |
| mensagemVenda            | Mensagem de venda retornado pela operadora. Retornado apenas se alguma cobrança já ocorreu                                                   |

Ao lado você pode visualizar um exemplo de retorno da transação.



<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>