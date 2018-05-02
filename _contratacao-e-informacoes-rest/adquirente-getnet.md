---
title: Adquirente GetNet
position: 5
menu: gateway
---


**Contratação**

Contratando a solução da GetNet eCommerce será possível oferecer na sua loja:

* Cartão de crédito Visa;
* Cartão de crédito MasterCard;

Ao final do processo de contratação, deve-se estar de posse das seguintes informações para ativação da GetNet no Gateway:

* Merchant Id;
* Terminal Id;
* Usuário;
* Senha.

O Yapay não participa das negociações entre o estabelecimento e bancos/adquirentes. Desta forma, taxas ou eventuais isenções são tratadas de forma direta entre os envolvidos.

Informações sobre a contratação, <a href="https://www.getnet.com.br/#/solucoes/e-commerce" target="_blank" class="linkPadraoVerde">acesse aqui</a>.

**Particulariedades**

* Para esta modalidade é necessário certificado SSL de segurança 2048 bits;
* Integração apenas na modalidade WebService.

Exemplos

REQUISIÇÃO

Estrutura simplificada de envio para adquirente GetNet. Caso seu estabelecimento utilize antifraude, seguir a estrutura completa.


Estrutra simplificada REST de envio GetNet:


RESPOSTA

Estrtura de retorno adquirente GetNet. Os comentários indicam a informação retornada da adquirente em cada campo.

~~~json
    curl
        --request POST https://sanbbox.gateway.yapay.com.br/checkout/api/v3/transacao
        --header "Content-Type: application/json"
        --curl -u usuario:senha .........
        --data-binary
        {
        "codigoEstabelecimento" : 1000000000000,
        "codigoFormaPagamento" : 271,
        "transacao" : {
            "numeroTransacao" : 123,
            "valor" : 500000,
            "parcelas" : 1,
            "idioma" : 1
        },
        "dadosCartao" : {
            "nomePortador" : "Teste Teste",
            "numeroCartao" : "5453010000083303",
            "codigoSeguranca" : "123",
            "dataValidade" : "12/2030"
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
{: title="Estrutura simplificada de envio GetNet" }

~~~json
    --header "Content-Type: application/json"
        {
        "numeroTransacao": 123,
        "codigoEstabelecimento": "1000000000000",
        "codigoFormaPagamento": 271,
        "valor": 100,
        "valorDesconto": 0,
        "parcelas": 1,
        <!--Status que deverá ser tratado pelo eCommerce-->
        "statusTransacao": 1,
        <!--Código de autorização-->
        "autorizacao": "1234",
        <!--Código retorno GetNet-->
        "codigoTransacaoOperadora": "0",
        <!--Data retorno adquirente-->
        "dataAprovacaoOperadora": "1017",
        <!--TID-->
        "numeroComprovanteVenda": "1662429594",
        "nsu": "",
        <!--Mensagem adquirente-->
        "mensagemVenda": "CAPTURED",
        "urlPagamento": "14956291484887110cf2a-9aeb-4b34-a869-1a61f0611b66",
        "cartoesUtilizados": ["545301******3303"]
        }
~~~
{: title="Retorno" }


<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>