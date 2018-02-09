---
title: Adquirente Cielo
position: 1
---

Contratação e informações meios de pagamento

Na aba lateral direita está disponível exemplos para cada meio de pagamento em XML (para integração REST) e cURL (para integração REST).

Adquirente Cielo
{: .subtitulo }

*MODALIDADE WEBSERVICE*

*Contratação*

Contratando a solução da CIELO para e-commerce será possível oferecer na sua loja:

Vendas de cŕedito autenticadas (Bandeiras Visa e MasterCard);

* Cartão de crédito Amex;
* Cartão de crédito Aura;
* Cartão de crédito Diners;
* Cartão de crédito Discover;
* Cartão de crédito Elo;
* Cartão de crédito JCB;
* Cartão de crédito MasterCard;
* Cartão de crédito Visa;
* Cartão de débito Maestro;
* Cartão de débito Visa Electron;

Ao final do processo de contratação, deve-se estar de posse das seguintes informações para ativação da CIELO no Gateway:

* Merchant ID;
* Merchant Key;

O Yapay não participa das negociações entre o estabelecimento e bancos/adquirentes. Desta forma, taxas ou eventuais isenções são tratadas de forma direta entre os envolvidos.

Para contratar, <a href="https://www.cielo.com.br/sitecielo/afiliacao/credenciamentoafiliacaonaologado.html?idSolucaoCaptura=81" target="_blank" class="linkPadraoVerde">acesse aqui</a>.


*Particulariedades*

* Para esta modalidade é necessário certificado SSL de segurança 2048 bits;
* Integração na plataforma WebService API 3.0;
* Caso o campo `<codigoSeguranca>` não for enviado ou for enviado com "000", a transação será encaminhada a Cielo como modelo "Recorrente", onde este campo não é obrigatório. Lembrando que para esta utilização é preciso habilitar junto a Adquirente. Salientamos que a conversão de seu estabelecimento pode diminuir;
* Esta operadora de cartão permite cadastrar uma informação para aparecer na fatura dos clientes quando realizarem compras sua loja, funcionalidade chamada de SoftDescriptor. Esta deverá possuir até 13 caracteres. Caso queira utilizar, envie ao Suporte Yapay o nome desejado para configuração em seu estabelecimento. Também é possível o envio do SoftDescriptor por pedido, para isto solicite ao Suporte a ativação e envie a informação no campoLivre4 de cada transação;
* Para transações com cartão de débito ou autenticada, o eCommerce deverá redirecionar o consumidor para a `<urlPagamento>`, onde o mesmo deverá incluir sua senha ou token no ambiente do banco emissor. Apenas após esta etapa, a transação será concluída.

**Processo de Homologação com Adquirente**

Após a integração com o Yapay, o estabelecimento deverá configurar as credenciais da Cielo no ambiente de produção do Yapay e apontar sua loja para o ambiente real do Gateway. Após isto, a loja deverá enviar ao Suporte Cielo (cieloecommerce@cielo.com.br) a URL da loja com um produto de teste no valor de R$1,00. O suporte Cielo realizará os testes em ambiente real e caso esteja dentro das conformidades a loja estará apta a realizar vendas em produção.

**Exemplos Cartão de Crédito**

**REQUISIÇÃO**

Estrutura simplificada de envio para adquirente Cielo. Caso seu estabelecimento utilize antifraude, seguir a <a href="/gateway/rest/pagamentos-cartao-credito-rest/#transacao-com-analise-de-fraude" target="_blank" class="linkPadraoVerde">estrutura completa</a>.


**RESPOSTA**

Estrtura de retorno adquirente Cielo. Os comentários indicam a informação retornada da adquirente em cada campo.


**Exemplos Cartão de Débito**

**REQUISIÇÃO**

Estrutura simplificada de envio para adquirente Cielo.

Estrutra simplificada de envio Cielo:

**RESPOSTA**

Estrtura de retorno adquirente Cielo. Os comentários indicam a informação retornada da adquirente em cada campo.



~~~text
    curl
        --request POST https://sandbox.gateway.yapay.com.br/checkout/api/v3/transacao
        --header "Content-Type: application/json"
        --curl -u usuario:senha .........
        --data-binary
        {
        "codigoEstabelecimento" : 1000000000000,
        "codigoFormaPagamento" : 171,
        "transacao" : {
            "numeroTransacao" : 123,
            "valor" : 100,
            "parcelas" : 1,
            "idioma" : 1
        },
        "dadosCartao" : {
            "nomePortador" : "Teste Teste",
            "numeroCartao" : "0000000000000001",
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

~~~text
    --header "Content-Type: application/json"
        {
        "numeroTransacao": 123,
        "codigoEstabelecimento": "1000000000000",
        "codigoFormaPagamento": 171,
        "valor": 2000,
        "valorDesconto": 0,
        "parcelas": 1,
        <!--Status que deverá ser tratado pelo eCommerce-->
        "statusTransacao": 1,
        <!--Código de autorização-->
        "autorizacao": "123456",
        <!--Código erro em caso de negação-->
        "codigoTransacaoOperadora": "0",
        <!--Data retorno adquirente-->
        "dataAprovacaoOperadora": "24/05/2017",
        <!--TID-->
        "numeroComprovanteVenda": "10069930690009F2122A",
        "nsu": "428706",
        <!--Mensagem adquirente-->
        "mensagemVenda": "Operation Success",
        "urlPagamento": "https://gateway.yapay.com.br/checkout/PagamentoCielo/PagamentoCielo.do?cod=14956291484887110cf2a-9aeb-4b34-a869-1a61f0611b66",
        "cartoesUtilizados": ["000000*******0001"]
        }
~~~
{: title="Retorno" }



**CHECKOUT CIELO (REDIRECIONADO)**

**Contratação**

Contratando a solução da CIELO para e-commerce será possível oferecer os seguintes meios de pagamento na sua loja:

* Cartão de crédito Amex;
* Cartão de crédito Aura;
* Cartão de crédito Diners;
* Cartão de crédito Discover;
* Cartão de crédito Elo;
* Cartão de crédito JCB;
* Cartão de crédito MasterCard;
* Cartão de crédito Visa;
* Cartão de débito Maestro;
* Cartão de débito Visa Electron;

Ao final do processo de contratação, deve-se estar de posse das seguintes informações para ativação da CIELO no Gateway:

* Código de filiação;
* Merchant ID;

O Yapay não participa das negociações entre o estabelecimento e bancos/adquirentes. Desta forma, taxas ou eventuais isenções são tratadas de forma direta entre os envolvidos.

Para contratar, <a href="https://www.cielo.com.br/aceite-cartao/checkout/" target="_blank" class="linkPadraoVerde">acesse aqui</a>.


**Particulariedades**

* Para utilização correta desta forma de pagamento, deve se enviado ao Suporte Yapay uma URL para redirecionamento do usuário após finalização do pagamento. Esta URL deve ser informada de forma completa, iniciando em HTTP ou HTTPS;
* O eCommerce deverá redirecionar o consumidor para a URL retornada no campo `<urlPagamento>`;
* Importante a utilização da campainha para atualização de status no eCommerce após finalização do pagamento;
* O eCommerce enviará um único código ao Gateway relacionado ao meio de pagamento Checkout (52) e após a abertura da URL o consumidor escolherá a bandeira de cartão;
* Necessário algumas configurações no painel Cielo. Passo a passo no próximo tópico deste documento.

**Configuração painel Cielo**

Etapas para configuração:

* 1- Acesse o gerenciador Cielo
* 2- Clique na aba "Configurações" --> "Configurações da loja"
* 3- Primeiramente habilite em "Modo de Teste"
* 4- Inclua as URLs abaixo:

**EM TESTES Subtituir o valor 10000000000 pelo código de estabelecimento Yapay**

| Nome do campo            | URL                                                                                                                 |
|--------------------------|---------------------------------------------------------------------------------------------------------------------|
| URL Retorno              | https://sandbox.gateway.yapay.com.br/checkout/PagamentoCielo/RetornoCheckout?codE=10000000000&acao=retorno           |
| URL Notificação          | https://sandbox.gateway.yapay.com.br/checkout/PagamentoCielo/NotificacaoCheckout?codE=10000000000&acao=notificacao   |
| URL de Mudança de Status | https://sandbox.gateway.yapay.com.br/checkout/PagamentoCielo/NotificacaoCheckout?codE=10000000000&acao=mudancaStatus |


**EM PRODUÇÃO Subtituir o valor 10000000000 pelo código de estabelecimento SuperPay**

| Nome do Campo            | URL                                                                                                                 |
|--------------------------|---------------------------------------------------------------------------------------------------------------------|
| URL Retorno              | https://gateway.yapay.com.br/checkout/PagamentoCielo/RetornoCheckout?codE=10000000000&acao=retorno             |
| URL Notificação          | https://gateway.yapay.com.br/checkout/PagamentoCielo/NotificacaoCheckout?codE=10000000000&acao=notificacao     |
| URL de Mudança de Status | https://gateway.yapay.com.br/checkout/PagamentoCielo/NotificacaoCheckout?codE=10000000000&acao=mudancaStatus   |



**Processo de Homologação com Adquirente**

Após a integração com o Yapay, o estabelecimento deverá configurar as credenciais da Cielo no ambiente de produção do Yapay e apontar sua loja para o ambiente real do Gateway. Após isto, a loja deverá enviar ao Suporte Cielo (cieloecommerce@cielo.com.br) a URL da loja com um produto de teste no valor de R$1,00. O suporte Cielo realizará os testes em ambiente real e caso esteja dentro das conformidades a loja estará apta a realizar vendas em produção.


Exemplos

**REQUISIÇÃO**

Estrutura simplificada de envio para adquirente Cielo. Caso seu estabelecimento utilize antifraude, seguir a estrutura completa.

Estrutra simplificada REST de envio Cielo.

**RESPOSTA**

Estrtura de retorno adquirente Cielo. Os comentários indicam a informação retornada da adquirente em cada campo.

~~~json
  curl
        --request POST https://sanbbox.gateway.yapay.com.br/checkout/api/v3/transacao
        --header "Content-Type: application/json"
        --curl -u usuario:senha .........
        --data-binary
        {
        "codigoEstabelecimento" : 1000000000000,
        "codigoFormaPagamento" : 52,
        "transacao" : {
            "numeroTransacao" : 123,
            "valor" : 100,
            "parcelas" : 1,
            "idioma" : 1
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
{: title="Envio" }


~~~json
  --header "Content-Type: application/json"
    {
    "numeroTransacao": 123,
    "codigoEstabelecimento": "1000000000000",
    "codigoFormaPagamento": 52,
    "valor": 2000,
    "valorDesconto": 0,
    "parcelas": 1,
    <!--Status que deverá ser tratado pelo eCommerce-->
    "statusTransacao": 5,
    <!--Código de autorização-->
    "autorizacao": "0",
    <!--Código erro em caso de negação-->
    "codigoTransacaoOperadora": "0",
    <!--URL para redirecionar o consumidor-->
    "urlPagamento": "https://sandbox.gateway.yapay.com.br/checkout/PagamentoCielo/checkout?cod=14956291484887110cf2a-9aeb-4b34-a869-1a61f0611b66"
    }
~~~
{: title="Retorno" }


Estrutura de retorno após a finalização do pagamento. (Consulta do Ecommerce após acionamento de campainha):

~~~json
    --header "Content-Type: application/json"
    {
    "numeroTransacao":123,"
    codigoEstabelecimento":"1000000000000",
    "codigoFormaPagamento":52,
    "valor":2000,"
    valorDesconto":0,"
    parcelas":2, 
    <!--Status da Transacao-->
    "statusTransacao":1,"
    <!--Data de retorno da operadora-->
    dataAprovacaoOperadora":"04/01/2018 10:39:42",
    <!--Comprovante de venda-->
    "numeroComprovanteVenda":"040120181039401403",
    <!--NSU-->
    "nsu":"d8aa2b2933ca4a63b425a2cf1012c0f0",
    <!-Bandeira escolhida no ambiente Cielo-->
    "bandeira":"Cartão de Crédito - Elo",
    "urlPagamento":"15150694525329e353c97-2477-4df5-943c-6e3600ef3f38"
    }
~~~
{: title="Retorno" }


<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>