---
title: SafetyPay
position: 11
menu: gateway
---


Com este meio de pagamento é possível trabalhar com transferências entre vários bancos sem possuir contrato com cada um deles.

**Contratação**

Contratando a solução da SafetyPay para e-commerce será possível oferecer na sua loja:

Transferência entre bancos;
Ao final do processo de contratação, deve-se estar de posse das seguintes informações para ativação dos boletos no Gateway:

* API Key;
* Signature Key;
* Usuário;
* Senha.

O Yapay não participa das negociações entre o estabelecimento e bancos/adquirentes. Desta forma, taxas ou eventuais isenções são tratadas de forma direta entre os envolvidos.

Para contratar, <a href="http://www.safetypay.com/pt/produtos-e-solucoes/pagamento-online/" target="_blank" class="linkPadraoVerde">acesse aqui</a>.



**Particulariedades**

* Modalidade com redirecionamento;
* A URL retornada no campo `<urlPagamento>` em SOAP e `<url_acesso>` em REST deverá ser repassada ao comprador para visualização/pagamento do boleto;
* Enviar todos campos referente aos dados do comprador.


**Configuração ambiente SafetyPay**

Configurar em seu painel safetyPay a URL de notificação do Gateway + seu código de estabelecimento Yapay:


| Ambiente    | URL                                                                                                    |
|-------------|--------------------------------------------------------------------------------------------------------|
| HOMOLOGAÇÃO | https://homologacao.superpay.com.br/checkout/SafetyPay/Notificacao?codigoEstabelecimento={CODIGOYAPAY} |
| PRODUÇÃO    | https://superpay2.superpay.com.br/checkout/SafetyPay/Notificacao?codigoEstabelecimento={CODIGOYAPAY}   |


**Exemplo URL notificação:** https://gateway.yapay.com.br/checkout/SafetyPay/Notificacao?codigoEstabelecimento=1000000000000


Exemplos

REQUISIÇÃO

Estrutura de envio SafetyPay.

RESPOSTA

Estrtura de retorno SafetyPay:

~~~text
curl
--request POST https://homologacao.superpay.com.br/checkout/api/v2/transacao
--header "Content-Type: application/json"
--header "usuario:{"login":"superpay","senha":"superpay"}"
--data-binary
{
   codigoEstabelecimento: 1000000000000,
   codigoFormaPagamento: 155,
   transacao: {
    numeroTransacao: 1,
    valor: 2000,
    valorDesconto: 0,
    parcelas : 1,
    urlCampainha : http://seusite.com.br/campainha,
    urlResultado : http://seusite.com.br/retorno,
    ip : "192.168.12.110",
    idioma : 1
   },
   itensDoPedido: [
  {
    codigoProduto: 1,
    nomeProduto: Blusa,
    codigoCategoria: 1,
    nomeCategoria : Roupa,
    quantidadeProduto : 1,
    valorUnitarioProduto : 2000
  }
   ],
   dadosCobranca : {
    codigoCliente : 1,
    tipoCliente : 1,
    nome : Teste SuperPay,
    email : teste@teste.com,
    dataNascimento : "",
    sexo : "M",
    documento : "12312321312",
    endereco : {
    logradouro : Rua Teste,
    numero : 123,
    complemento : "",
    cep : 12345-678,
    bairro : Bairro Teste,
    cidade : Cidade Teste,
    estado : SP,
    pais : BR
  },
  telefone : [
  {
    tipoTelefone : 1,
    ddi : 55,
    ddd : 12,
    telefone : 1234-5678
  }
  ]
   },
   dadosEntrega : {
    nome : Teste SuperPay,
    email : teste@teste.com,
    endereco : {
    logradouro : Rua teste,
    numero : 123,
    complemento : "",
    cep : 12345-678,
    bairro : Bairro Teste,
    cidade : Cidade Teste,
    estado : SP,
    pais : BR
  },
  telefone : [
  {
    tipoTelefone : 1,
    ddi : 55,
    ddd : 12,
    telefone : 1234-5678
  }
  ]
   }
}


~~~
{: title="Estrutura simplificada de envio Bradesco ShopFacil" }

~~~text
--header "Content-Type: application/json"
{
   "numeroTransacao": 1,
   "codigoEstabelecimento": "1000000000000",
   "codigoFormaPagamento": 155,
   "valor": 2000,
   "valorDesconto": 0,
   "parcelas": 1,
   "statusTransacao": 8,
   "autorizacao": ,
   "codigoTransacaoOperadora": "0",
   "dataAprovacaoOperadora": ,
   "numeroComprovanteVenda": ,
   "nsu": ,
   "mensagemVenda": ,
   "urlPagamento": "https://homologacao.superpay.com.br/checkout/PagamentoSafetyPay/PagamentoSafetyPay.do?cod=141348960683a720e602-5631-4725-8f79-268c06795a3c"
}
~~~
{: title="Retorno" }



