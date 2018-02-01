---
title: Transação com múltiplos cartões
position: 3
menu: gateway
right_code: |
    ~~~xml
    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:pag="http://pagamentos.webservices.superpay.ernet.com.br/">
    <soapenv:Header/>
    <soapenv:Body>
    <pag:pagamentoTransacaoCompletaMaisCartoesCredito>
        <transacao>
        <codigoEstabelecimento>1000000000000</codigoEstabelecimento>
        <!--enviar o array dadosCartoesCredito de acordo com a quantidade de cartões-->
        <dadosCartoesCredito>
            <codigoFormaPagamento>170</codigoFormaPagamento>
            <codigoSeguranca>123</codigoSeguranca>
            <dataValidadeCartao>12/2016</dataValidadeCartao>
            <nomeTitularCartaoCredito>Teste</nomeTitularCartaoCredito>
            <numeroCartaoCredito>4444333322221111</numeroCartaoCredito>
            <parcelas>1</parcelas>
            <valor>100</valor>
        </dadosCartoesCredito>
        <dadosCartoesCredito>
            <codigoFormaPagamento>171</codigoFormaPagamento>
            <codigoSeguranca>123</codigoSeguranca>
            <dataValidadeCartao>12/2016</dataValidadeCartao>
            <nomeTitularCartaoCredito>Teste</nomeTitularCartaoCredito>
            <numeroCartaoCredito>4444333322221111</numeroCartaoCredito>
            <parcelas>1</parcelas>
            <valor>100</valor>
        </dadosCartoesCredito>
        <dadosUsuarioTransacao>
            <documentoComprador>12312312312</documentoComprador>
            <nomeComprador>Teste SuperPay</nomeComprador>
        </dadosUsuarioTransacao>
        <idioma>1</idioma>
        <numeroTransacao>10</numeroTransacao>
        <urlCampainha></urlCampainha>
        </transacao>
        <usuario>superpay</usuario>
        <senha>superpay</senha>
        </pag:pagamentoTransacaoCompletaMaisCartoesCredito>
    </soapenv:Body>
    </soapenv:Envelope>
    ~~~
    {: title="Exemplo criação transação" }

    ~~~xml
    <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:Body>
        <ns2:pagamentoTransacaoCompletaMaisCartoesCreditoResponse xmlns:ns2="http://pagamentos.webservices.superpay.ernet.com.br/">
            <return>
                <codigoEstabelecimento>1318336765212</codigoEstabelecimento>
                <detalhesFormaPagamentoMultiplosCartoes>
                <autorizacao>123456</autorizacao>
                <codigoFormaPagamento>170</codigoFormaPagamento>
                <codigoTransacaoOperadora>0</codigoTransacaoOperadora>
                <dataAprovacaoOperadora>24/05/2017</dataAprovacaoOperadora>
                <mensagemVenda>Transação autorizada</mensagemVenda>
                <numeroComprovanteVenda>10069930690009F2530A</numeroComprovanteVenda>
                <parcelas>1</parcelas>
                <taxaEmbarque>0</taxaEmbarque>
                <valor>100</valor>
                <valorDesconto>0</valorDesconto>
                </detalhesFormaPagamentoMultiplosCartoes>
                <detalhesFormaPagamentoMultiplosCartoes>
                <autorizacao>0</autorizacao>
                <codigoFormaPagamento>171</codigoFormaPagamento>
                <codigoTransacaoOperadora>0</codigoTransacaoOperadora>
                <dataAprovacaoOperadora>24/05/2017</dataAprovacaoOperadora>
                <mensagemVenda>Transação autorizada</mensagemVenda>
                <numeroComprovanteVenda>10069930690009F2531A</numeroComprovanteVenda>
                <parcelas>1</parcelas>
                <taxaEmbarque>0</taxaEmbarque>
                <valor>200</valor>
                <valorDesconto>0</valorDesconto>
                </detalhesFormaPagamentoMultiplosCartoes>
                <numeroTransacao>10</numeroTransacao>
                <statusTransacao>1</statusTransacao>
            </return>
        </ns2:pagamentoTransacaoCompletaMaisCartoesCreditoResponse>
    </soap:Body>
    </soap:Envelope>
    ~~~
    {: title="Exemplo retorno de transação" }    
---


Esta estrutura permite o envio de dois ou mais cartões em uma mesma requisição, permitindo ao consumidor dividir o valor total da venda entre os seus cartões de crédito. A venda só será finalizada com sucesso, se todos os cartões forem aprovados.

**Particulariedades:**

* Disponível apenas no plano Corporativo;
* Disponível apenas para cartões de crédito modalidade WebService;
* Não disponível no fluxo de Antifraude.

**REQUISIÇÃO**

Abaixo seguem os campos mínimos para finalizar com sucesso uma transação com Múltiplos Cartões.

<i class="fa fa-info-circle" aria-hidden="true"></i> Para enviar a transação, acione o método `pagamentoTransacaoCompletaMaisCartoesCredito`
{: .informativo }

Para autenticação, enviar `usuario` e `senha`:

| Campo   | Descrição                |
|---------|--------------------------|
| usuario | Login do estabelecimento |
| senha   | Senha do estabelecimento |

`transacaoCompletaWS`
{: .subtituloAzul }

| Campo                 | Descrição                                                                                                      | Tipo          | Tamanho    | Obrigatório |
|-----------------------|----------------------------------------------------------------------------------------------------------------|---------------|------------|-------------|
| numeroTransacao       | Código que identifica a transação dentro do Yapay                                                           | Numérico      | Até 19 dígitos     | Sim |
| codigoEstabelecimento | Código que identifica o estabelecimento dentro do Yapay (fornecido pelo gateway)                            | Numérico      | 13 dígitos         | Sim |
| urlCampainha          | URL será sempre acionada quando o status do pedido mudar. Deve estar preparada para receber dados de campainha | Alfa Numérico | Até 250 caracteres | Não |
| idioma                | 1 - Português 2 - Inglês 3 - Espanhol                                                                          | Numérico      | 1 dígito           | Sim |
| dadosUsuarioTransacao | Array dados do comprador                                                                                       | - | - | - |
| dadosCartoesCredito   | Lista com informações dos cartões de créditos                                                                  | - | - | - |


`dadosUsuarioTransacao`
{: .subtituloAzul }

| Campo              | Descrição                       | Tipo          | Tamanho            | Obrigatório |
|--------------------|---------------------------------|---------------|--------------------|-------------|
| nomeComprador      | Nome do comprador               | Alfa Numérico | Até 100 caracteres | Não         |
| documentoComprador | Documento principal do comprado | Alfa Numérico | 30 caracteres      | Não         |


`dadosCartaoCredito`
{: .subtituloAzul }

O array com os dados abaixo devem ser repetidos de acordo com a qauntidade de cartão a ser enviada.

| Campo                    | Descrição                                                                                 | Tipo          | Tamanho           | Obrigatório |
|--------------------------|-------------------------------------------------------------------------------------------|---------------|-------------------|-------------|
| codigoFormaPagamento     | <a href="/gateway/rest/codigos-da-api-rest/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a> | Numérico | 2 dígitos | Sim |
| valor                    | Valor da transação. Deve ser enviado sem pontos ou vírgulas                               | Numérico      | Até 10 dígitos    | Sim |
| parcelas                 | Quantidade de parcelas da transação. Verificar se forma de pagamento suporta parcelamento | Numérico      | Até 2 dígitos     | Sim |
| nomeTitularCartaoCredito | Nome do titular do cartão de crédito (Exatamente como escrito no cartão)                  | Alfa Numérico | Até 16 caracteres | Sim |
| numeroCartaoCredito      | Numero do cartão de crédito, sem espaços ou traços                                        | Numérico      | Até 22 caracteres | Sim |
| codigoSeguranca          | Código de segurança do cartão (campo não é armazenado pelo Yapay)                      | Numérico      | Até 4 caracteres  | Sim |
| dataValidadeCartao       | Data de validade do cartão. Formato mm/yyyy                                               | Alfa Numérico | 7 caracteres      | Sim |


**RESPOSTA** 

| Campo                                    | Descrição                                                   | Tipo     | Tamanho        |
|------------------------------------------|-------------------------------------------------------------|----------|----------------|
| numeroTransacao                          | Código que identifica a transação dentro do Yapay        | Numérico | Até 19 dígitos |
| codigoEstabelecimento                    | Código que identifica o estabelecimento dentro do Yapay  | Numérico | 13 dígitos     |
| statusTransacao                          | <a href="/gateway/codigos-da-api/#status-de-transacao" target="_blank" class="linkPadraoVerde">Status atual da transação</a>                                   | Numérico | Até 2 dígitos  |
| detalhesFormaPagamentoMultiplosCartoesWS | Lista com informações dos cartões de créditos               |     -    |       -        |


`detalhesFormaPagamentoMultiplosCartoesWS`
{: .subtituloAzul }

| Campo                    | Descrição                           | Tipo          | Tamanho           |
|--------------------------|-------------------------------------|---------------|-------------------|
| valor                    | Valor da transação                  | Numérico      | Até 10 dígitos    |
| valorDesconto            | Valor do desconto da transação      | Numérico      | Até 10 dígitos    |
| taxaEmbarque             | Valor da taxa de embarque           | Numérico      | Até 10 dígitos    |
| parcelas                 | Quantidade de parcelas da transação | Numérico      | Até 2 dígitos     |
| autorizacao              | Código de autorização da adquirente | Numérico      | Até 20 dígitos    |
| codigoTransacaoOperadora | Código da transação na adquirente   | Numérico      | Até 20 dígitos    |
| dataAprovacaoOperadora   | Data de aprovação na adquirente     | Alfa Numérico | Até 10 caracteres |
| numeroComprovanteVenda   | Número do comprovante de venda      | Alfa Numérico | Até 20 caracteres |
| mensagemVenda            | Mensagem de retorno da adquirente   | Alfa Numérico | Até 50 caracteres |


<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>