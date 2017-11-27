---
title: Banco Banrisul
position: 6
menu: gateway
---

**Contratação**

Contratando a solução BanriCompras será possível oferecer na sua loja:

* Boleto sem registro;
* Pagamento pré datado;
* Pagamentos parcelados;
* Pagamentos á vista.

Ao final do processo de contratação, deve-se estar de posse das seguintes informações para ativação do e-Rede no Gateway:

* Código do estabelecimento Banrisul;
* Código da rede;
* Senha de consulta.

O Superpay não participa das negociações entre o estabelecimento e bancos/adquirentes. Desta forma, taxas ou eventuais isenções são tratadas de forma direta entre os envolvidos.

Informações sobre a contratação, entre em contato com banrisul_cartoes_atendimento_adquirencia@banrisul.com.br

Particulariedades

* Modalidades com redirecionamento;
* Para utilização das modalidades Banricompras, todos os campos referente aos dados do cliente devem ser preenchidos;
* Se não for informado uma data de vencimento do boleto, a data de vencimento que aparecerá no boleto será os dias de vencimento configurado internamente no Gateway;
* Processo de homologação junto ao Banrisul obrigatório para liberação em produção.

**Configurações ambiente Banrisul**

Para o Gateway de Pagamento funcionar corretamente, é necessário configurar algumas urls no ambiente do Banricompras.


| Ambiente    | Link Painel Banrisul                      | Url Campainha                                                                | Método para envio |
|-------------|-------------------------------------------|------------------------------------------------------------------------------|-------------------|
| HOMOLOGAÇÃO | https://ww4.banrisul.com.br/banricompras/ | https://homologacao.superpay.com.br/checkout/Banrisul/NotificacaoBanrisul.do | POST              |
| PRODUÇÃO    | https://ww7.banrisul.com.br/banricompras/ | https://superpay2.superpay.com.br/checkout/Banrisul/NotificacaoBanrisul.do   | POST              |



PÁGINAS DE AVISO DE OPERAÇÃO
{:.subtitulo}

| Ambiente    | Link Painel Banrisul                      | Url Sucesso | Url Não Pago |
|-------------|-------------------------------------------|-------------|--------------|
| HOMOLOGAÇÃO | https://ww4.banrisul.com.br/banricompras/ | https://homologacao.superpay.com.br/checkout/Banrisul/RedirecionamentoBanrisulOk.do | https://homologacao.superpay.com.br/superpay/Banrisul/RedirecionamentoBanrisulNoOk.do |
| PRODUÇÃO    | https://ww7.banrisul.com.br/banricompras/ | https://superpay2.superpay.com.br/checkout/Banrisul/RedirecionamentoBanrisulOk.do | https://superpay2.superpay.com.br/checkout/Banrisul/RedirecionamentoBanrisulNoOk.do |



Processo de Homologação

Após realizar a integração com o SuperPay em ambiente de testes e configurações no painel Banrisul, enviar para tecnologia_homologacoes@banrisul.com.br o link de acesso a página de testes, bem como o código de usuário e senha para login. Assim que o processo for finalizado pela equipe Banrisul, os mesmos enviarão os dados de produção para o estabelecimento.

Exemplos

REQUISIÇÃO

Estrutura de envio para banco Banrisul.

Estrutra SOAP de envio Banrisul:


~~~text
    curl
        --request POST https://homologacao.superpay.com.br/checkout/api/v2/transacao
        --header "Content-Type: application/json"
        --header "usuario:{"login":"superpay","senha":"superpay"}"
        --data-binary
        {
        codigoEstabelecimento: 1000000000000,
        codigoFormaPagamento: 26,
        transacao: {
            numeroTransacao: 1,
            valor: 2000,
            valorDesconto: 0,
            parcelas : 1,
            urlCampainha : http://seusite.com.br/campainha,
            urlResultado : http://seusite.com.br/retorno,
            ip : "192.168.12.110",
            idioma : 1,
            dataVencimentoBoleto : "10/10/2018"
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
{: title="Estrutura simplificada de envio Banrisul" }

~~~text
    --header "Content-Type: application/json"
        {
        "numeroTransacao": 1,
        "codigoEstabelecimento": "1000000000000",
        "codigoFormaPagamento": 26,
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
        "urlPagamento": "https://homologacao.superpay.com.br/checkout/Boleto/PagamentoBanrisul.do?cod=141348960683a720e602-5631-4725-8f79-268c06795a3c"
        }
~~~
{: title="Retorno" }