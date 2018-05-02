---
title: Adquirente Rede
position: 9
menu: gateway
---

**MODALIDADE WEBSERVICE**

Contratação

Contratando a solução da e-Rede será possível oferecer na sua loja:

Cartão de crédito aunteticado (Bandeiras Visa e MasterCard);

* Cartão de crédito aunteticado;
* Cartão de crédito Visa;
* Cartão de crédito MasterCard;
* Cartão de crédito Hiper;
* Cartão de crédito HierpCard;
* Cartão de crédito JCB;
* Cartão de crédito Credz;
* Cartão de débito Visa Electron;
* Cartão de débito Maestro;

Ao final do processo de contratação, deve-se estar de posse das seguintes informações para ativação do e-Rede no Gateway:

* Filiação (PV);
* Token;

O Yapay não participa das negociações entre o estabelecimento e bancos/adquirentes. Desta forma, taxas ou eventuais isenções são tratadas de forma direta entre os envolvidos.

Informações sobre a contratação, <a href="https://www.userede.com.br/nossos-produtos/e-rede" target="_blank" class="linkPadraoVerde">acesse aqui</a>.

**Particulariedades**

* Para esta modalidade é necessário certificado SSL de segurança 2048 bits;
* Esta operadora de cartão permite cadastrar uma informação para aparecer na fatura dos clientes quando realizarem compras sua loja, funcionalidade chamada de SoftDescriptor. Esta deverá possuir até 13 caracteres. Caso queira utilizar, envie ao Suporte SuperPay o nome desejado para configuração em seu estabelecimento.
* Também é possível o envio do SoftDescriptor por pedido, para isto solicite ao Suporte a ativação e envie a informação no campoLivre4 de cada transação;
* Para transações com cartão de débito ou autenticada, o eCommerce deverá enviar o "userAgente" (Identificador do browser utilizado pelo comprador no momento da compra) no campo `<campoLivre1>` e redirecionar o consumidor para o campo `<urlPagamento>` recebida no retorno, onde o mesmo deverá incluir sua senha ou token no ambiente do banco emissor. Apenas após esta etapa, a transação será concluída.
* Para bandeiras de débito (Visa Electron e Maestro) e/ou cartões autenticados (Visa e MasterCard), é preciso a liberação do serviço de 3DS. Portanto, para utilização destas bandeiras solitem a liberação diretamente com a Adquirente Rede.



**Exemplos Cartão de Crédito**

REQUISIÇÃO

Estrutura simplificada de envio para adquirente Rede. Caso seu estabelecimento utilize antifraude, seguir a estrutura completa.

RESPOSTA

Estrtura de retorno adquirente Rede. Os comentários indicam a informação retornada da adquirente em cada campo.


Exemplos Cartão de Crédito
{: .subtitulo }

~~~json
    curl
    --request POST https://sandbox.gateway.yapay.com.br/checkout/api/v3/transacao
    --header "Content-Type: application/json"
    --curl -u usuario:senha 
    --data-binary
    {
    "codigoEstabelecimento" : 1000000000000,
    "codigoFormaPagamento" : 191,
    "transacao" : {
        "numeroTransacao" : 123,
        "valor" : 500000,
        "parcelas" : 1,
        "idioma" : 1
    },
    "dadosCartao" : {
        "nomePortador" : "Teste Teste",
        "numeroCartao" : "5899160000000005",
        "codigoSeguranca" : "123",
        "dataValidade" : "01/2019"
    },
    "itensDoPedido" : [
    {
        "quantidadeProduto" : 1,
        "valorUnitarioProduto" : 500000
    }
    ],
    "dadosCobranca" : {
        "nome" : "Teste Integração",
        "documento" : "12312312312"
    }
    }
~~~
{: title="Estrutura simplificada de envio Rede" }

~~~json
    --header "Content-Type: application/json"
    {
    "numeroTransacao": 123,
    "codigoEstabelecimento": "1000000000000",
    "codigoFormaPagamento": 191,
    "valor": 500000,
    "valorDesconto": 0,
    "parcelas": 1,
    <!--Status que deverá ser tratado pelo eCommerce-->
    "statusTransacao": 1,
    <!--Código de autorização-->
    "autorizacao": "123456",
    <!--Código retorno Cielo-->
    "codigoTransacaoOperadora": "0",
    <!--Data retorno adquirente-->
    "dataAprovacaoOperadora": "24/05/2030",
    <!--TID-->
    "numeroComprovanteVenda": "10117092708342800232",
    "nsu": "428706",
    <!--Mensagem adquirente-->
    "mensagemVenda": "00 - Success",
    "urlPagamento": "14956291484887110cf2a-9aeb-4b34-a869-1a61f0611b66",
    "cartoesUtilizados": ["589916******0005"]
    }

~~~
{: title="Retorno" }


~~~json
    curl
    --request POST https://sandbox.gatway.yapay.com.br/checkout/api/v3/transacao
    --header "Content-Type: application/json"
    --curl -u usuario:senha
    --data-binary
    {
    "codigoEstabelecimento" : 1000000000000,
    "codigoFormaPagamento" : 198,
    "transacao" : {
        "numeroTransacao" : 123,
        "valor" : 511100,
        "parcelas" : 1,
        "idioma" : 1,
        "urlCampainha" : http://seusite.com.br/campainha,
        "urlResultado" : http://seusite.com.br/retorno,
        "campoLivre1" : Mozilla/5.0 (iPad; U; CPU OS 3_2_1 like Mac OS X; en-us) AppleWebKit/531.21.10 (KHTML, like Gecko) Mobile/7B405
    },
    "dadosCartao" : {
        "nomePortador" : "Teste Teste",
        "numeroCartao" : "4002479199570736",
        "codigoSeguranca" : "132",
        "dataValidade" : "01/2019"
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
{: title="Estrutura simplificada de envio Rede" }


~~~json
    --header "Content-Type: application/json"
    {
    "numeroTransacao": 123,
    "codigoEstabelecimento": "1000000000000",
    "codigoFormaPagamento": 198,
    "valor": 511100,
    "valorDesconto": 0,
    "parcelas": 1,
    <!--Status que deverá ser tratado pelo eCommerce-->
    "statusTransacao": 8,
    <!--Código de autorização-->
    "autorizacao": "0",
    <!--Código de erro-->
    "codigoTransacaoOperadora": "0",
    <!--Data retorno adquirente-->
    "dataAprovacaoOperadora": "24/05/2030",
    <!--TID-->
    "numeroComprovanteVenda": "10069930690009F2122A",
    "nsu": "0",
    <!--Mensagem adquirente-->
    "mensagemVenda": "00 - Success",
    <!--URL para redirecionar o consumidor para autenticação-->
    "urlPagamento": "https://sandbox.gateway.yapay.com.br/checkout/erede/pg.do?cod=1506533536609b7edee8b-7549-488a-9ae1-65f9f92a1b4c",
    "cartoesUtilizados": ["400247******0736"]
    }


~~~
{: title="Retorno" }


<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>