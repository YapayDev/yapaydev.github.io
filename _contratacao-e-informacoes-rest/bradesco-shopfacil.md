---
title: Bradesco ShopFácil
position: 8
menu: gateway
---


**BOLETO**

Contratação

Contratando a solução Bradesco ShopFácil será possível oferecer na sua loja:

* Boleto sem ou com registro, dependendo de seu contrato com o banco;

Ao final do processo de contratação, deve-se estar de posse das seguintes informações para ativação do e-Rede no Gateway:

* Merchantid;
* Email de acesso ao gerenciador;
* Chave de Acesso; (Gerada dentro do gerenciador do Bradesco, passo a passo abaixo);
* Número da Carteira.


O Superpay não participa das negociações entre o estabelecimento e bancos/adquirentes. Desta forma, taxas ou eventuais isenções são tratadas de forma direta entre os envolvidos.

Informações sobre a contratação, <a href="http://www.bradesco.com.br/html/corporate/produtos-servicos/parcerias-e-oportunidades/shopfacil-empresa.shtm" target="_blank" class="linkPadraoVerde">acesse aqui</a>

**Particulariedades**

* Modalidades com redirecionamento;
* Para utilização das modalidades ShopFácil, todos os campos referente aos dados do cliente devem ser preenchidos;
* Se não for informado uma data de vencimento do boleto, a data de vencimento que aparecerá no boleto será os dias de vencimento configurado internamente no Gateway;

Configurações ambiente ShopFácil

_Gerando chave de acesso_

Procedimento idêntico em ambos ambientes:

| Ambiente    | URL                                                            |
|-------------|----------------------------------------------------------------|
| HOMOLOGAÇÃO | https://homolog.meiosdepagamentobradesco.com.br/gerenciadorapi |
| PRODUÇÃO    | https://meiosdepagamentobradesco.com.br/gerenciadorapi         |



Após logar, acesse Configurações > Meios de Pagamento > Boleto Bancário, inclua uma palavra secreta para geração da chave.

_Configurando URL de notificação_

Após logar, acesse Configuração > Meios de Pagamento > Boleto Bancário, incluir no campo "URL de notificação":

| Ambiente    | URL                                                            |
|-------------|----------------------------------------------------------------|
| HOMOLOGAÇÃO | https://homologacao.yapay.com.br/checkout/bradesco/confirmaBoletoRegistro |
| PRODUÇÃO    | https://yapay.com.br/checkout/bradesco/confirmaBoletoRegistro   |


Processo de Homologação
{:.subtitulo}

Procedimento deve ser realizado em duas etapas, ambiente de homologação e ambiente de Produção:

_Homologação_

Realizar as configurações no painel Bradesco conforme informado acima e solicitar ao Suporte SuperPay realizar a configuração do meio de pagamento em nosso ambiente de homologação, informando a ele os dados abaixo:

* Merchantid;
* Email de acesso ao gerenciador de homologação;
* Chave de acesso de homologação;
* Número da carteira;

A loja virtual deverá estar apontando para o ambiente de homologação e depois disto basta enviar email kit@scopus.com.br com a URL da loja com um produto de R$1,00 disponível para testes e o CNPJ do estabelecimento. Depois que a equipe do Bradesco validar este ambiente, o estabelecimento receberá novos dados, desta vez os dados reais da loja. E o procedimento deverá ser repedito porém desta vez em ambiente de produção.


_Produção_

Realizar as configurações no painel Bradesco conforme informado acima e solicitar ao Suporte SuperPay realizar a configuração do meio de pagamento em nosso ambiente de produção, informando a ele os dados abaixo:

* Merchantid;
* Email de acesso ao gerenciador de homologação;
* Chave de acesso de homologação;
* Número da carteira;

A loja virtual deverá estar apontando para o ambiente de produção e depois disto basta enviar email kit@scopus.com.br com a URL da loja com um produto de R$1,00 disponível para testes e o CNPJ do estabelecimento. Depois que a equipe do Bradesco validar este ambiente, o estabelecimento estará apto a realizar vendas em produção.




**Exemplos**

REQUISIÇÃO

Estrutura de envio para banco Bradesco.

Estrutra REST de envio Bradesco Transferência:

Estrtura de retorno Bradesco.



~~~text
curl
--request POST https://homologacao.yapay.com.br/checkout/api/v2/transacao
--header "Content-Type: application/json"
--header "usuario:{"login":"superpay","senha":"superpay"}"
--data-binary
{
   codigoEstabelecimento: 1000000000000,
   codigoFormaPagamento: 18,
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
   "codigoFormaPagamento": 18,
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
   "urlPagamento": "https://homologacao.superpay.com.br/checkout/Transferencia/PagamentoBradescoShopFacil.do?cod=141348960683a720e602-5631-4725-8f79-268c06795a3c"
}
~~~
{: title="Retorno" }

