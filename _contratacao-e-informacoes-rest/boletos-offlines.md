---
title: Boletos Offlines
position: 10
menu: gateway
---


**BOLETOS REGISTRADOS**

Com esta modalidade, os bancos possuem conehcimento do boleto desde sua geração, permitindo o lojista realizar protestos ao cliente caso o pagamento não for realizado.

_Para utilização de qualquer boleto com carteira registrada é preciso realizar a abertura de relacionamento entre o banco e VAN homologada com o Yapay._


Santander
{:.subtitulo}

* agência;
* conta;
* código do cedente;
* número da carteira;
* espécie de documento; (Exemplos: DM, RM, ME, NP)
* código de transmissão.

Caixa Econômica Federal
{:.subtitulo}

* agência;
* conta;
* código do convênio;
* número da carteira;
* código de operação;
* espécie de documento. (Exemplos: DM, RM, ME, NP)


Itaú
{:.subtitulo}

* agência;
* conta;
* número da carteira;
* espécie de documento. (Exemplos: DM, RM, ME, NP)


Bradesco
{:.subtitulo}

* agência;
* conta;
* número da carteira;
* espécie de documento. (Exemplos: DM, RM, ME, NP)


Banco do Brasil
{:.subtitulo}

* agência;
* conta;
* código do convênio;
* número da carteira;
* variação da carteira;
* espécie de documento. (Exemplos: DM, RM, ME, NP);
* client ID;
* secret;


**Particulariedades**

* Para a geração de Boleto offlines, todos os campos referente aos dados do cliente devem ser preenchidos;
* Arquivo de registro e conciliação com layout de 400 posições para todos os bancos;
* Campo `<estadoComprador>` deve ser preenchido pela sigla;
* O tamanho do número do pedido, deverá possuir no máximo 8 dígitos;
* Se não for informado uma data de vencimento do boleto na requisição, a data de vencimento que aparecerá no boleto será os dias de vencimento configurados internamente no Gateway;
* A URL retornada no campo `<urlPagamento>` em SOAP e `<url_acesso>` em REST deverá ser repassada ao comprador para visualização/pagamento do boleto;
* A requisição e retorno do SuperPay para boletos registrados possuem a mesma estrutura dos sem registro, porém o status a ser retornado será 5 (transação em andamento) ao invés de 8 (aguardando pagamento);
* Para ativação do boleto registrado e Módulo de Conciliação entrar em contato com comercial@superpay.com.br;
* O Superpay não participa das negociações entre o estabelecimento e bancos/administradoras. Desta forma, taxas ou eventuais isenções são tratadas de forma direta entre os envolvidos.


**BOLETOS SEM REGISTROS**

O Gateway de Pagamento aceita boletos sem registro emitidos pelos seguintes bancos:

* Itaú;
* Bradesco;
* Banco do Brasil;
* Caixa;
* Santander.

Ao final do processo de contratação, deve-se estar de posse das seguintes informações para ativação dos boletos no Gateway:

* Convênio;
* Agência;
* Conta;
* Número da Carteira;
* Espécie de Documento. (Exemplos: DM, RM, ME, NP)


**Particulariedades**

* Para a geração de Boleto offlines, todos os campos referente aos dados do cliente devem ser preenchidos.
* Campo `<estadoComprador>` deve ser preenchido pela sigla;
* O tamanho do número do pedido, deverá possuir no máximo 8 dígitos;
* Se não for informado uma data de vencimento do boleto na requisição, a data de vencimento que aparecerá no boleto será os dias de vencimento configurados internamente no Gateway;
* A URL retornada no campo `<urlPagamento>` em SOAP e `<url_acesso>` em REST deverá ser repassada ao comprador para visualização/pagamento do boleto;
* Conciliação de boletos não é realizada automaticamente, para tal deve ser contratado o Módulo de Conciliação do Gateway. Para informações entrar em contato com comercial@yapay.com.br;
* O Superpay não participa das negociações entre o estabelecimento e bancos/administradoras. Desta forma, taxas ou eventuais isenções são tratadas de forma direta entre os envolvidos.




**Contratação**

Contratando a solução BBOnline será possível oferecer na sua loja:

* Boleto sem ou com registro, dependendo de seu contrato com o banco;
* Transferência Eletrônica.

Ao final do processo de contratação, deve-se estar de posse das seguintes informações para ativação do e-Rede no Gateway:

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

Estrutura de envio para geração de boletos sem/com registro.

RESPOSTA

Estrtura de retorno Boleto registrado:


~~~text
curl
--request POST https://homologacao.superpay.com.br/checkout/api/v2/transacao
--header "Content-Type: application/json"
--header "usuario:{"login":"superpay","senha":"superpay"}"
--data-binary
{
   codigoEstabelecimento: 1000000000000,
   codigoFormaPagamento: 30,
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
   "codigoFormaPagamento": 30,
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
   "urlPagamento": "https://homologacao.superpay.com.br/superpay/GeradorBoleto.do?cod=1413487983447baddcb56-0126-4353-9253-538f64d"
}
~~~
{: title="Retorno" }



