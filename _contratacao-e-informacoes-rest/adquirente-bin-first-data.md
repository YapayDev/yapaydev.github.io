---
title: Adquirente Bin - First Data
position: 3
menu: gateway
---

**Contratação**

Contratando a solução da Bin eCommerce será possível oferecer na sua loja:

* Cartão de crédito Visa;
* Cartão de crédito MasterCard;
* Cartão de crédito Cabal;

Ao final do processo de contratação, deve-se estar de posse das seguintes informações para ativação do e-Rede no Gateway:

* Store Id;
* User Id;
* Password;
* Arquivo do certificado BIN;
* Senha do certificado;
* Terminal ID.

O Superpay não participa das negociações entre o estabelecimento e bancos/adquirentes. Desta forma, taxas ou eventuais isenções são tratadas de forma direta entre os envolvidos.

Informações sobre a contratação, acesse aqui

Particulariedades

* Para esta modalidade é necessário certificado SSL de segurança 2048 bits;
* Integração apenas na modalidade WebService.

Informações sobre a contratação, <a href="https://www.bin.com.br/content/bin/pt_br/home/peca-ja/solicite-seu-credenciamento.html" target="_blank" class="linkPadraoVerde">acesse aqui</a>.

**Particulariedades**

* Para esta modalidade é necessário certificado SSL de segurança 2048 bits;
* Integração apenas na modalidade WebService.


Exemplos

REQUISIÇÃO

Estrutura simplificada de envio para adquirente Bin. Caso seu estabelecimento utilize antifraude, seguir a estrutura completa.

Estrutra simplificada REST de envio Bin:

RESPOSTA

Estrtura de retorno adquirente Bin. Os comentários indicam a informação retornada da adquirente em cada campo

~~~json
    curl
        --request POST https://homologacao.superpay.com.br/checkout/api/v2/transacao
        --header "Content-Type: application/json"
        --header "usuario:{"login":"superpay","senha":"superpay"}"
        --data-binary
        {
        "codigoEstabelecimento" : 1000000000000,
        "codigoFormaPagamento" : 381,
        "transacao" : {
            "numeroTransacao" : 123,
            "valor" : 500000,
            "parcelas" : 1,
            "idioma" : 1
        },
        "dadosCartao" : {
            "nomePortador" : "Teste Teste",
            "numeroCartao" : "5547220000000102",
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
{: title="Estrutura simplificada de envio Cielo" }

~~~json
    --header "Content-Type: application/json"
    {
    "numeroTransacao": 123,
    "codigoEstabelecimento": "1000000000000",
    "codigoFormaPagamento": 381,
    "valor": 100,
    "valorDesconto": 0,
    "parcelas": 1,
    <!--Status que deverá ser tratado pelo eCommerce-->
    "statusTransacao": 1,
    <!--Código de autorização-->
    "autorizacao": "657409",
    <!--Código retorno Bin-->
    "codigoTransacaoOperadora": "0",
    <!--Data retorno adquirente-->
    "dataAprovacaoOperadora": "20/10/2017 16:36:43",
    <!--TID-->
    "numeroComprovanteVenda": "Y:657409:4514266711:PPX :632615",
    "nsu": "",
    <!--Mensagem adquirente-->
    "mensagemVenda": "APPROVAL 000009113",
    "urlPagamento": "14956291484887110cf2a-9aeb-4b34-a869-1a61f0611b66",
    "cartoesUtilizados": ["554722******0102"]
    }
~~~
{: title="Retorno" }