---
title: Adquirente Rede
position: 2
menu: gateway
---

**MODALIDADE WEBSERVICE**

Contratação

* Contratando a solução da e-Rede será possível oferecer na sua loja:
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

O Superpay não participa das negociações entre o estabelecimento e bancos/adquirentes. Desta forma, taxas ou eventuais isenções são tratadas de forma direta entre os envolvidos.

Informações sobre a contratação, <a href="https://www.userede.com.br/nossos-produtos/e-rede" target="_blank" class="linkPadraoVerde">acesse aqui</a>.

**Particulariedades**

* Para esta modalidade é necessário certificado SSL de segurança 2048 bits;
* Integração na plataforma WebService API 3.0;
* Caso o campo <codigoSeguranca> não for enviado ou for enviado com "000", a transação será encaminhada a Cielo como modelo "Recorrente", onde este campo não é obrigatório. Lembrando que para esta utilização é preciso habilitar junto a Adquirente. Salientamos que a conversão de seu estabelecimento pode diminuir;
* Esta operadora de cartão permite cadastrar uma informação para aparecer na fatura dos clientes quando realizarem compras sua loja, funcionalidade chamada de SoftDescriptor. Esta deverá possuir até 13 caracteres. Caso queira utilizar, envie ao Suporte SuperPay o nome desejado para configuração em seu estabelecimento. Também é possível o envio do SoftDescriptor por pedido, para isto solicite ao Suporte a ativação e envie a informação no campoLivre4 de cada transação;
* Para transações com cartão de débito ou autenticada, o eCommerce deverá redirecionar o consumidor para a <urlPagamento>, onde o mesmo deverá incluir sua senha ou token no ambiente do banco emissor. Apenas após esta etapa, a transação será concluída.

**Processo de Homologação com Adquirente**

Após a integração com o SuperPay, o estabelecimento deverá configurar as credenciais da Cielo no ambiente de produção do SuperPay e apontar sua loja para o ambiente real do Gateway. Após isto, a loja deverá enviar ao Suporte Cielo (cieloecommerce@cielo.com.br) a URL da loja com um produto de teste no valor de R$1,00. O suporte Cielo realizará os testes em ambiente real e caso esteja dentro das conformidades a loja estará apta a realizar vendas em produção.


**Exemplos Cartão de Crédito**

REQUISIÇÃO

Estrutura simplificada de envio para adquirente Cielo. Caso seu estabelecimento utilize antifraude, seguir a estrutura completa.

RESPOSTA

Estrtura de retorno adquirente Cielo. Os comentários indicam a informação retornada da adquirente em cada campo.


~~~json
    curl
    --request POST https://homologacao.superpay.com.br/checkout/api/v2/transacao
    --header "Content-Type: application/json"
    --header "usuario:{"login":"superpay","senha":"superpay"}"
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
        "dataAprovacaoOperadora": "24/05/2017",
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