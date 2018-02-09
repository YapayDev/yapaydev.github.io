---
title: Banco do Brasil Online
position: 13
menu: gateway
---

**Contratação**

Contratando a solução BBOnline será possível oferecer na sua loja:

* Boleto sem ou com registro, dependendo de seu contrato com o banco;
* Transferência Eletrônica.

Ao final do processo de contratação, deve-se estar de posse das seguintes informações para ativação do Banco do Brasil Online no Gateway:

* Códido do convênio;
* Código cobrança.

O Yapay não participa das negociações entre o estabelecimento e bancos/adquirentes. Desta forma, taxas ou eventuais isenções são tratadas de forma direta entre os envolvidos.

Informações sobre a contratação, <a href="http://www.bb.com.br/portalbb/page100,116,2532,1,1,1,1.bb?codigoNoticia=5575&codigoMenu=164&codigoRet=5435&bread=6_2" target="_blank" class="linkPadraoVerde">acesse aqui</a>




**Particulariedades**

* Modalidades com redirecionamento;
* Para utilização das modalidades BBOnline, todos os campos referente aos dados do cliente devem ser preenchidos;
* Se não for informado uma data de vencimento do boleto, a data de vencimento que aparecerá no boleto será os dias de vencimento configurado internamente no Gateway;



Exemplos

REQUISIÇÃO

Estrutura de envio para banco do Brasil.

RESPOSTA

Estrtura de retorno BBOnline:




~~~text
curl
--request POST https://sanbbox.gateway.yapay.com.br/checkout/api/v3/transacao
--header "Content-Type: application/json"
--curl -u usuario:senha .........
--data-binary
{
   codigoEstabelecimento: 1000000000000,
   codigoFormaPagamento: 21,
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
   "codigoFormaPagamento": 21,
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
   "urlPagamento": "https://gateway.yapay.com.br/checkout/PagamentoBBOnline/PagamentoBBOnline.do?cod=147499950329455715d65-621f-4b80-896c-5d1a645fb9e0"
}

~~~
{: title="Retorno" }






<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>