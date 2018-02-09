---
title: Intermediário Financeiro
position: 17
menu: gateway
---


**Contratação**

Abaixo segue lista de intermediário financeiro disponíveis através do Yapay:

* PagSeguro;
* PayPal.

Ao final do processo de contratação, deve-se estar de posse das seguintes informações para ativação no Gateway:

PagSeguro
{:.subtitulo}

* email
* token

Contração <a href="https://pagseguro.uol.com.br/para_seu_negocio/venda_pela_internet.jhtml" target="_blank" class="linkPadraoVerde">acesse aqui</a>.

PayPal
{:.subtitulo}

* assinatura
* email
* usuário
* senha


Contração <a href="https://www.paypal.com/br/home" target="_blank" class="linkPadraoVerde">acesse aqui</a>.

O Yapay não participa das negociações entre o estabelecimento e bancos/administradoras. Desta forma, taxas ou eventuais isenções são tratadas de forma direta entre os envolvidos.

**Particulariedades**

* Modalidade com redirecionamento;
* A URL retornada no campo `<urlPagamento>`;
* Enviar todos campos referente aos dados do comprador.

Configuração ambiente PagSeguro

Configurar em seu painel PagSeguro a URL de notificação do Gateway:


HOMOLOGAÇÃO
{: .subtitulo }

**URL**: `https://gateway.yapay.com.br/checkout/PagamentoPagSeguro/RetornoPagSeguro.do`


PRODUÇÃO
{: .subtitulo }

**URL**: `https://ww7.banrisul.com.br/banricompras/`


**Exemplos**

**REQUISIÇÃO**

Estrutura de envio PayPal.

**RESPOSTA**

Estrtura de retorno PayPal:

~~~text
curl
--request POST https://sanbbox.gateway.yapay.com.br/checkout/api/v3/transacao
--header "Content-Type: application/json"
--curl -u usuario:senha .........
--data-binary
{
   codigoEstabelecimento: 1000000000000,
   codigoFormaPagamento: 39,
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
    nome : Teste Yapay,
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
    nome : Teste Yapay,
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
   "codigoFormaPagamento": 39,
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
   "urlPagamento": "https://sandbox.gateway.yapay.com.br/checkout/PagamentoPagSeguro/PagamentoPagSeguro.do?cod=1413489786995834a2f60-aa50-4615-92bd-45c46a7397a5"
}
~~~
{: title="Retorno" }





<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>