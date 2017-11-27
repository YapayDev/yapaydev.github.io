---
title: Adquirente Stone
position: 5
menu: gateway
---


Contratação

Contratando a solução da Stone eCommerce será possível oferecer na sua loja:

* Cartão de crédito Visa;
* Cartão de crédito MasterCard;

Ao final do processo de contratação, deve-se estar de posse das seguintes informações para ativação do e-Rede no Gateway:

* Sale affiliation key;
* Stone Code;

O Superpay não participa das negociações entre o estabelecimento e bancos/adquirentes. Desta forma, taxas ou eventuais isenções são tratadas de forma direta entre os envolvidos.

Informações sobre a contratação, <a href="https://stone-pagamentos.typeform.com/to/A4caIq" target="_blank" class="linkPadraoVerde">acesse aqui</a>.

**Particulariedades**

* Para esta modalidade é necessário certificado SSL de segurança 2048 bits;
* Integração apenas na modalidade WebService.


**Exemplos**

REQUISIÇÃO

Estrutura simplificada de envio para adquirente GetNet. Caso seu estabelecimento utilize antifraude, seguir a estrutura completa.


Estrutra simplificada REST de envio GetNet:


RESPOSTA

Estrtura de retorno adquirente GetNet. Os comentários indicam a informação retornada da adquirente em cada campo.

~~~json
    curl
        --request POST https://homologacao.superpay.com.br/checkout/api/v2/transacao
        --header "Content-Type: application/json"
        --header "usuario:{"login":"superpay","senha":"superpay"}"
        --data-binary
        {
        "codigoEstabelecimento" : 1000000000000,
        "codigoFormaPagamento" : 351,
        "transacao" : {
            "numeroTransacao" : 123,
            "valor" : 500000,
            "parcelas" : 1,
            "idioma" : 1
        },
        "dadosCartao" : {
            "nomePortador" : "Teste Teste",
            "numeroCartao" : "5431111111111111",
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
{: title="Estrutura simplificada de envio Stone" }

~~~json
    --header "Content-Type: application/json"
        {
        "numeroTransacao": 123,
        "codigoEstabelecimento": "1000000000000",
        "codigoFormaPagamento": 351,
        "valor": 100,
        "valorDesconto": 0,
        "parcelas": 1,
        <!--Status que deverá ser tratado pelo eCommerce-->
        "statusTransacao": 1,
        <!--Código de autorização-->
        "autorizacao": "1234",
        <!--Código retorno Stone-->
        "codigoTransacaoOperadora": "0",
        <!--Data retorno adquirente-->
        "dataAprovacaoOperadora": "20/10/2017 16:36:43",
        <!--TID-->
        "numeroComprovanteVenda": "1662429594",
        "nsu": "",
        <!--Mensagem adquirente-->
        "mensagemVenda": "Transação Aprovada",
        "urlPagamento": "14956291484887110cf2a-9aeb-4b34-a869-1a61f0611b66",
        "cartoesUtilizados": ["543111******1111"]
        }
~~~
{: title="Retorno" }