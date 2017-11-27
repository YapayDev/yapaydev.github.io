---
title: Capturando uma transação
position: 4
menu: gateway
right_code: |
    ~~~xml
        <soapenv:envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:pag="http://pagamentos.webservices.superpay.ernet.com.br/">
        <soapenv:header></soapenv:header>
        <soapenv:body>
            <pag:operacaoTransacao>
                <operacao>
                    <codigoEstabelecimento>1000000000000</codigoEstabelecimento>
                    <numeroTransacao>1</numeroTransacao>
                    <operacao>1</operacao>
                </operacao>
                <usuario>superpay</usuario>
                <senha>superpay</senha>
            </pag:operacaoTransacao>
        </soapenv:body>
        </soapenv:envelope>
    ~~~
    {: title="Exemplo captura de transação" }

    ~~~xml
        <soap:envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:body>
            <ns2:pagamentoTransacaoCompletaResponse xmlns:ns2="http://pagamentos.webservices.superpay.ernet.com.br/">
                <return>
                    <autorizacao>123456</autorizacao>
                    <codigoEstabelecimento>1000000000000</codigoEstabelecimento>
                    <codigoFormaPagamento>120</codigoFormaPagamento>
                    <codigoTransacaoOperadora>0</codigoTransacaoOperadora>
                    <dataAprovacaoOperadora>24/05/2017</dataAprovacaOperadora>
                    <mensagemVenda>Transacao capturada com sucesso</mensagemVenda>
                    <numeroComprovanteVenda>1006993069181F841001</numeroComprovanteVenda>
                    <numeroTransacao>1</numeroTransacao>
                    <parcelas>1</parcelas>
                    <statusTransacao>1</statusTransacao>
                    <taxaEmbarque>0</taxaEmbarque>
                    <urlPagamento>14132971582229c00506d-e84d-4526-b902-92190d5aa808<urlpagamento></urlpagamento>
                    <valor>200</valor>
                    <valorDesconto>0</valorDesconto>
                </return>
            </ns2:pagamentoTransacaoCompletaResponse>
        </soap:body>
        </soap:envelope>
    ~~~    
    {: title="Exemplo retorno da captura" }
---

Através desta funcionalidade é possível confirmar uma pré autorização na adquirente, assim o consumidor receberá a cobrança em seu cartão e gerará crédito ao lojista. Os estabelecimentos com captura manual deverão acionar o método de captura em até 5 dias da criação da venda, pois após este período a adquirente cancelará automaticamente a pré autorização.

**REQUISIÇÃO**

<i class="fa fa-info-circle" aria-hidden="true"></i>  Para enviar a transação, acione o método `operacaoTransacao`
{: .informativo }

Para autenticação, enviar `usuario` e `senha`:

| Campo   | Descrição                |
|---------|--------------------------|
| usuario | Login do estabelecimento |
| senha   | Senha do estabelecimento |


| Campo                 | Descrição                                                                                    | Tipo          | Tamanho        |
|-----------------------|----------------------------------------------------------------------------------------------|---------------|----------------|
| numeroTransacao       | Código que identifica a transação dentro do SuperPay                                         | Numérico      | Até 19 dígitos |
| codigoEstabelecimento | Código que identifica o estabelecimento dentro do SuperPay (fornecido pelo gateway)          | Numérico      | 13 dígitos     |
| operacao              | Código que identifica o processo que deseja realizar. Para captura, deve-se enviar o valor 1 | Numérico      | 1 dígito       |


**RESPOSTA**


| Campo                    | Descrição                                                                | Tipo          | Tamanho             |
|--------------------------|--------------------------------------------------------------------------|---------------|---------------------|
| numeroTransacao          | Código que identifica a transação dentro do SuperPay                     | Numérico      | Até 19 dígitos      |
| codigoEstabelecimento    | Código que identifica o estabelecimento dentro do SuperPay               | Numérico      | 13 dígitos          |
| codigoFormaPagamento     | <a href="/gateway/codigos-da-api/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                                             | Numérico      | Até 3 dígitos       |
| valor                    | Valor da transação.                                                      | Numérico      | Até 10 dígitos      |
| taxaEmbarque             | Valor taxa embarque                                                      | Numérico      | Até 10 dígitos      |
| valorDesconto            | Valor desconto                                                           | Numérico      | Até 10 dígitos      |
| parcelas                 | Quantidade de parcelas da transação                                      | Numérico      | Até 2 dígitos       |
| urlPagamento             | Para o modelo redirect. Essa será a URL de redirecionamento da operação  | Alfa Numérico | Até 500 caracteres  |
| statusTransacao          | <a href="/gateway/codigos-da-api/#status-de-transacao" target="_blank" class="linkPadraoVerde">Status atual da transação</a>                                             | Numérico      | Até 2 dígitos       |
| autorizacao              | Código de autorização da adquirente                                      | Numérico      | Até 20 dígitos      |
| codigoTransacaoOperadora | Código da transação na adquirente                                        | Numérico      | Até 20 dígitos      |
| dataAprovacaoOperadora   | Data de aprovação na adquirente                                          | Alfa Numérico | Até 10 dígitos      |
| numeroComprovanteVenda   | Número do comprovante de venda                                           | Alfa Numérico | Até 20 dígitos      |
| mensagemVenda            | Mensagem de retorno da adquirente                                        | Alfa Numérico | Até 50 dígitos      |