---
title: Transação simplificada
position: 1
menu: gateway
right_code: |
  ~~~ xml
        <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:pag="http://pagamentos.webservices.superpay.ernet.com.br/">
        <soapenv:Header/>
        <soapenv:Body>
        <pag:pagamentoTransacaoCompleta>
            <transacao>
            <codigoEstabelecimento>1000000000000</codigoEstabelecimento>
            <codigoFormaPagamento>170</codigoFormaPagamento>
            <numeroTransacao>1</numeroTransacao>
            <dadosUsuarioTransacao>
            <documentoComprador>12312312312</documentoComprador>
            <nomeComprador>Teste SuperPay</nomeComprador>
            </dadosUsuarioTransacao>
            <dataValidadeCartao>12/2026</dataValidadeCartao>
            <nomeTitularCartaoCredito>teste superpay</nomeTitularCartaoCredito>
            <numeroCartaoCredito>4444333322221111</numeroCartaoCredito>
            <codigoSeguranca>123</codigoSeguranca>
            <parcelas>1</parcelas>
            <valor>200</valor>
            </transacao>
            <usuario>superpay</usuario>
            <senha>superpay</senha>
            </pag:pagamentoTransacaoCompleta>
        </soapenv:Body>
        </soapenv:Envelope>
  ~~~
  {: title="Exemplo criação transação" }

  ~~~ xml
  <soap:envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:body>
        <ns2:pagamentoTransacaoCompletaResponse xmlns:ns2="http://pagamentos.webservices.superpay.ernet.com.br/">
          <return>
              <autorizacao>0</autorizacao>
              <codigoEstabelecimento>1000000000000</codigoEstabelecimento>
              <codigoFormaPagamento>179</codigoFormaPagamento>
              <codigoTransacaoOperadora>0</codigoTransacaoOperadora>
              <dataAprovacaoOperadora>24/05/2017</dataAprovacaOperadora>
              <mensagemVenda></mensagemVenda>
              <numeroComprovanteVenda>1006993069181F841001</numeroComprovanteVenda>
              <numeroTransacao>1</numeroTransacao>
              <parcelas>1</parcelas>
              <statusTransacao>5</statusTransacao>
              <taxaEmbarque>0</taxaEmbarque>
              <urlPagamento>https://homologacao.superpay.com.br/checkout/PagamentoCielo/PagamentoVisaElectron.do?          cod=1503069157836b501aa77-6988-427c-9c8e-bead7409c669</urlpagamento>
              <valor>200</valor>
              <valorDesconto>0</valorDesconto>
          </return>
        </ns2:pagamentoTransacaoCompletaResponse>
    </soap:body>
  </soap:envelope>
  ~~~
  {: title="Exemplo retorno transação" }
  


---

Estrutura e exemplo de uma transação simples para cartão de crédito. As funcionalidades, como Análise de Fraude, Recorrência, OneClick e demais formas de pagamento precisam de uma estrutura mais completa para um perfeito funcionamento. Consulte as demais estruturas e exemplos desta documentação.

REQUISIÇÃO
{: .subtitulo }

<i class="fa fa-info-circle" aria-hidden="true"></i> Para enviar a transação, acione o método `pagamentoTransacaoCompleta`.
{: .informativo }

Para autenticação, enviar usuario e senha:

| Campo   | Descrição                |
|---------|--------------------------|
| usuario | Login do estabelecimento |
| senha   | Senha do estabelecimento |


_`transacaoCompletaWS`_
{: .subtituloAzul }


| Campo                   | Descrição                                                                                 | Tipo          | Tamanho           | Obrigatório |
|-------------------------|-------------------------------------------------------------------------------------------|---------------|-------------------|-------------|
| numeroTransacao         | Código que identifica a transação dentro do SuperPay                                      | Numérico      | Até 19 dígitos    | Sim         |
| codigoEstabelecimento   | Código que identifica o estabelecimento dentro do SuperPay (fornecido pelo gateway)       | Numérico      | 13 dígitos        | Sim         |
| codigoFormaPagamento    | <a href="/gateway/codigos-da-api/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                                                              | Numérico      | Até 3 dígitos     | Sim         |
| valor                   | Valor da transação. Deve ser enviado sem pontos ou vírgulas                               | Numérico      | Até 10 dígitos    | Sim         |
| parcelas                | Quantidade de parcelas da transação. Verificar se forma de pagamento suporta parcelamento | Numérico      | Até 2 dígitos     | Sim         |
nomeTitularCartaoCredito  | Nome do titular do cartão de crédito (Exatamente como escrito no cartão)                  | Alfa Numérico | Até 16 dígitos    | Sim         |
numeroCartaoCredito       | Numero do cartão de crédito, sem espaços ou traços                                        | Numérico      | Até 22 caracteres | Sim         |
codigoSeguranca           | Código de segurança do cartão (campo não é armazenado pelo SuperPay)                      | Numérico      | Até 4 caracteres  | Sim         |
dataValidadeCartao        | Data de validade do cartão. Formato mm/yyyy                                               | Alfa Numérico | 7 caracteres      | Sim         |
urlCampainha              | URL será sempre acionada quando o status do pedido mudar. Deve estar preparada para receber dados de campainha | Alfa Numérico | Até 250 caracteres | Não |
urlRedirecionamentoPago   | Para o modelo de pagamento redirect, O SuperPay redirecionará para essa URL em caso de transação aprovada | Alfa Numérico | Até 250 caracteres | Para pagamentos redirecionáveis é obrigatório |
urlRedirecionamentoPago   | Para o modelo de pagamento redirect, O SuperPay redirecionará para essa URL em caso de transação negada | Alfa Numérico | Até 250 caracteres | Para pagamentos redirecionáveis é obrigatório |
dadosUsuarioTransacao     | Array dados do comprador  | - | - | - |


_`dadosUsuarioTransacao`_
{: .subtituloAzul }

| Campo               | Descrição                        | Tipo           | Tamanho             | Obrigatório |
|---------------------|----------------------------------|----------------|---------------------|-------------|
| nomeComprador       | Nome do comprador                | Alfa Numérico  | Até 100 caracteres  | Não         |
| documentoComprador  | Documento principal do comprado  | Alfa Numérico  | 30 caracteres       | Não         |

**RESPOSTA**

| Campo                    | Descrição                                                                | Tipo           | Tamanho            |
|--------------------------|--------------------------------------------------------------------------|----------------|--------------------|
| numeroTransacao          | Código que identifica a transação dentro do SuperPay                     | Numérico       | Até 19 dígitos     |
| codigoEstabelecimento    | Código que identifica o estabelecimento dentro do SuperPay               | Numérico       | 13 dígitos         |
| codigoFormaPagamento     | <a href="/gateway/rest/codigos-da-api-rest/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                                             | Numérico       | Até 3 dígitos      |
| valor                    | Valor da transação.                                                      | Numérico       | Até 10 dígitos     |
| valorDesconto            | Valor desconto                                                           | Numérico       | Até 10 dígitos     |
| taxaEmbarque             | Valor taxa embarque                                                      | Numérico       | Até 10 dígitos     |
| parcelas                 | Quantidade de parcelas da transação                                      | Numérico       | Até 2 dígitos      |
| urlPagamento             | Para o modelo redirect. Essa será a URL de redirecionamento da operação  | Alfa Numérico  | Até 500 caracteres |
| statusTransacao          | <a href="/gateway/codigos-da-api/#status-de-transacao" target="_blank" class="linkPadraoVerde">Status atual da transação</a> | Numérico       | Até 2 dígitos      |
| autorizacao              | Código de autorização da adquirente                                      | Numérico       | Até 20 dígitos     |
| codigoTransacaoOperadora | Código da transação na adquirente                                        | Numérico       | Até 20 dígitos     |
| dataAprovacaoOperadora   | Data de aprovação na adquirente                                          | Alfa Numérico  | Até 10 dígitos     |
| numeroComprovanteVenda   | Número do comprovante de venda                                           | Alfa Numérico  | Até 20 dígitos     |
| mensagemVenda            | Mensagem de retorno da adquirente                                        | Alfa Numérico  | Até 50 dígitos     |



Ao lado você pode visualizar um exemplo de retorno da transação.




<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>