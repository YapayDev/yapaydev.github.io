---
title: Transação com Análise de Fraude
position: 2
menu: gateway
right_code: |
    ~~~xml
        <soapenv:envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:pag="http://pagamentos.webservices.superpay.ernet.com.br/">
        <soapenv:header></soapenv:header>
        <soapenv:body>
            <pag:pagamentoTransacaoCompleta>
                <transacao>
                    <campoLivre1></campoLivre1>
                    <campoLivre2></campoLivre2>
                    <campoLivre3></campoLivre3>
                    <campoLivre4></campoLivre4>
                    <campoLivre5></campoLivre5>
                    <codigoEstabelecimento>1000000000000</codigoEstabelecimento>
                    <codigoFormaPagamento>170</codigoFormaPagamento>
                    <codigoSeguranca>123</codigoSeguranca>
                    <dadosUsuarioTransacao>
                    <bairroEnderecoComprador>Vila</bairroEnderecoComprador>
                    <bairroEnderecoEntrega>centro</bairroEnderecoEntrega>
                    <cepEnderecoComprador>05707001</cepEnderecoComprador>
                    <cepEnderecoEntrega>05707001</cepEnderecoEntrega>
                    <cidadeEnderecoComprador>Sao Paulo</cidadeEnderecoComprador>
                    <cidadeEnderecoEntrega>Sao Paulo</cidadeEnderecoEntrega>
                    <codigoCliente>1</codigoCliente>
                    <codigoTipoTelefoneComprador>1</codigoTipoTelefoneComprador>
                    <codigoTipoTelefoneEntrega>1</codigoTipoTelefoneEntrega>
                    <complementoEnderecoComprador></complementoEnderecoComprador>
                    <complementoEnderecoEntrega></complementoEnderecoEntrega>
                    <dataNascimentoComprador>10/01/1980</dataNascimentoComprador>
                    <dddComprador>11</dddComprador>
                    <dddEntrega>11</dddEntrega>
                    <ddiComprador>55</ddiComprador>
                    <ddiEntrega>55</ddiEntrega>
                    <documento2Comprador></documento2Comprador>
                    <documentoComprador>12345678919</documentoComprador>
                    <emailComprador>superpay@superpay.com.br</emailComprador>
                    <enderecoComprador>Rua do Comprador</enderecoComprador>
                    <enderecoEntrega>Rua do Comprador</enderecoEntrega>
                    <estadoEnderecoComprador>SP</estadoEnderecoComprador>
                    <estadoEnderecoEntrega>SP</estadoEnderecoEntrega>
                    <nomeComprador>Testes de integracao Cartão</nomeComprador>
                    <numeroEnderecoComprador>123</numeroEnderecoComprador>
                    <numeroEnderecoEntrega>123</numeroEnderecoEntrega>
                    <paisComprador>BR</paisComprador>
                    <paisEntrega>BR</paisEntrega>
                    <sexoComprador>M</sexoComprador>
                    <telefoneComprador>1234123123</telefoneComprador>
                    <telefoneEntrega>1234123123</telefoneEntrega>
                    <tipoCliente>1</tipoCliente>
                    </dadosUsuarioTransacao>
                <dataDalidadeCartao>10/2017</dataValidadeCartao>
                    <IP>10.100.1.12</IP>
                    <idioma>1</idioma>
                    <itensDoPedido>
                    <codigoCategoria>1</codigoCategoria>
                    <codigoProduto>1</codigoProduto>
                    <nomeCategoria>Roupa</nomeCategoria>
                    <nomeProduto>Camiseta</nomeProduto>
                    <quantidadeProduto>1</quantidadeProduto>
                    <valorUnitarioProduto>200</valorUnitarioProduto>
                    </itensDoPedido>
                    <nomeTitularCartaoCredito>Teste Integracao</nomeTitularCartaoCredito>
                    <numeroCartaoCredito>4444333322221111</numeroCartaoCredito>
                    <numeroTransacao>1</numeroTransacao>
                    <origemTransacao>1</origemTransacao>
                    <parcelas>1</parcelas>
                    <taxaEmbarque>0</taxaEmbarque>
                    <urlCampainha>http://www.sualoja.campainha.com.br</urlCampainha>
                    <urlRedirecionamentoNaoPago>http://www.google.com.br</urlRedirecionamentoNaoPago>
                    <urlRedirecionamentoPago>http://www.google.com.br</urlRedirecionamentoPago>
                    <valor>200</valor>
                    <valorDesconto>0</valorDesconto>
                </transacao>
                <usuario>superpay</usuario>
                <senha>superpay</senha>
            </pag:pagamentoTransacaoCompleta>
        </soapenv:body>
        </soapenv:envelope>
    ~~~
    {: title="Exemplo criação transação" }

    ~~~xml
        <soap:envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:body>
            <ns2:pagamentoTransacaoCompletaResponse xmlns:ns2="http://pagamentos.webservices.superpay.ernet.com.br/">
                <return>
                    <autorizacao>123456</autorizacao>
                    <codigoEstabelecimento>1000000000000</codigoEstabelecimento>
                    <codigoFormaPagamento>170</codigoFormaPagamento>
                    <codigoTransacaoOperadora>0</codigoTransacaoOperadora>
                    <dataAprovacaoOperadora>24/05/2017</dataAprovacaOperadora>
                    <mensagemVenda>Transacao autorizada</mensagemVenda>
                    <numeroComprovanteVenda>1006993069181F841001</numeroComprovanteVenda>
                    <numeroTransacao>1</numeroTransacao>
                    <parcelas>1</parcelas>
                    <statusTransacao>15</statusTransacao>
                    <taxaEmbarque>0</taxaEmbarque>
                    <urlPagamento>14132971582229c00506d-e84d-4526-b902-92190d5aa808<urlpagamento></urlpagamento>
                    <valor>200</valor>
                    <valorDesconto>0</valorDesconto>
                </return>
            </ns2:pagamentoTransacaoCompletaResponse>
        </soap:body>
        </soap:envelope>
    ~~~    
    {: title="Exemplo retorno transação" }
---


A utilização desta estrutura é indicada para envio de pedidos com a forma de pagamento cartão de crédito, onde o estabelecimento possui contratação de umas das empresas de análise de risco integradas pelo Yapay, sendo elas ClearSale (modalidades: Total/Total Garantido, Application, ID e Start) e FControl (modalidade Fila).

<i class="fa fa-exclamation-circle" aria-hidden="true"></i> Contratação a parte com as empresas **ClearSale** e **FControl**.
{: .informativoVermelho }

**REQUISIÇÃO**


 <i class="fa fa-info-circle" aria-hidden="true"></i> Para enviar a transação, acione o método `pagamentoTransacaoCompleta`
 {: .informativo }

 Para autenticação, enviar usuario e senha:

| Campo    | Descrição                |
|----------|--------------------------|
| usuario  | Login do estabelecimento |
| senha    | Senha do estabelecimento |

`transacaoCompletaWS`
{: .subtituloAzul }

| Campo                    | Descrição                                                                                  | Tipo          | Tamanho            | Obrigatório |
|--------------------------|--------------------------------------------------------------------------------------------|---------------|--------------------|-------------|
| numeroTransacao          | Código que identifica a transação dentro do Yapay                                       | Numérico      | Até 19 dígitos     | Sim         |
| codigoEstabelecimento    | Código que identifica o estabelecimento dentro do Yapay (fornecido pelo gateway)        | Numérico      | 13 dígitos         | Sim         |
| codigoFormaPagamento     | <a href="/gateway/codigos-da-api/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                                                               | Numérico      | Até 3 dígitos      | Sim         |
| valor                    | Valor da transação. Deve ser enviado sem pontos ou vírgulas                                | Numérico      | Até 10 dígitos     | Sim         |
| parcelas                 | Quantidade de parcelas da transação. Verificar se forma de pagamento suporta parcelamento  | Numérico      | Até 2 dígitos      | Sim         |
| nomeTitularCartaoCredito | Nome do titular do cartão de crédito (Exatamente como escrito no cartão)                   | Alfa Numérico | Até 16 dígitos     | Sim         |
| numeroCartaoCredito      | Numero do cartão de crédito, sem espaços ou traços                                         | Numérico      | Até 22 caracteres  | Sim         |
| codigoSeguranca          | Código de segurança do cartão (campo não é armazenado pelo Yapay)                       | Numérico      | Até 4 caracteres   | Sim         |
| dataValidadeCartao       | Data de validade do cartão. Formato mm/yyyy                                                | Alfa Numérico | 7 caracteres       | Sim         |
| urlCampainha             | URL será sempre acionada quando o status do pedido mudar. Deve estar preparada para receber dados de campainha | Alfa Numérico | Até 250 caracteres | Não |
| urlRedirecionamentoPago  | Para o modelo de pagamento redirect, O Yapay redirecionará para essa URL em caso de transação aprovada      | Alfa Numérico | Até 250 caracteres | Para pagamentos redirecionáveis é obrigatório |
| ip                       | Número do IP de origem. Formato xxx.xxx.xxx.xxx                                            | Alfa Numérico | Até 15 caracteres  | Não         |
| idioma                   | 1 - Português 2 - Inglês 3 - Espanhol                                                      | Numérico      | 1 dígito           | Sim         |
| origemTransacao          | 1 - eCommerce 2 - Mobile 3 - URA                                                           | Numérico      | 1 dígito           | Sim         |
| campoLivre1              | Campo Livre 1                                                                              | Alfa Numérico | Até 16 caracteres  | Não         |
| campoLivre2              | Campo Livre 2 (Envio do FingerPrint ClearSale)                                             | Alfa Numérico | Até 16 caracteres  | Não         |
| campoLivre3              | Campo Livre 3 (Envio do canal de venda ClearSale Total/Total Garantido e Application - solicitar ativação para Suporte Yapay) | Alfa Numérico | Até 16 caracteres | Não |
| campoLivre4              | Campo Livre 4                                                                              | Alfa Numérico | Até 16 caracteres  | Não         |
| campoLivre5              | Campo Livre 5                                                                              | Alfa Numérico | Até 16 caracteres  | Não         |


`dadosUsuarioTransacao`
{: .subtituloAzul }


| Campo                                | Descrição                                              | Tipo          | Tamanho            | Obrigatório  |
|--------------------------------------|--------------------------------------------------------|---------------|--------------------|--------------|
| codigoCliente                        | Código que identifica o cliente no estabelecimento     | Alfa Numérico | 20 caracteres      | Não          |
| tipoCliente                          | 1 - Pessoa Física 2 - Pessoa Jurídica                  | Numérico      | 1 dígito           | Sim          |
| nomeComprador                        | Nome do comprador                                      | Alfa Numérico | Até 100 caracteres | Sim          |
| documentoComprador                   | Documento principal do comprador                       | Alfa Numérico | 30 caracteres      | Sim          |
| documento2Comprador                  | Documento complementar do comprador                    | Alfa Numérico | 30 caracteres      | Não          |
| sexoComprador                        | M – Masculino / F – Feminino                           | Alfa Numérico | 1 caracter         | Não          |
| dataNascimentoComprador              | Data de nascimento do comprador. Formato dd/mm/yyyy    | Alfa Numérico | 10 caracteres      | Sim          |
| telefoneComprador                    | Telefone do comprador sem espaços ou traços            | Alfa Numérico | Até 10 caracteres  | Sim          |
| dddComprador                         | DDD do telefone do comprador                           | Alfa Numérico | Até 3 caracteres   | Sim          |
| ddiComprador                         | DDI do telefone do comprador                           | Alfa Numérico | Até 3 caracteres   | Sim          |
| codigoTipoTelefoneComprador          | 1 - Outros 2 - Residencial 3 - Comercial               | Numérico      | 1 dígito           | Sim          |
| telefoneAdicionalComprador           | Telefone adicional do comprador. Sem espaços ou traços | Alfa Numérico | Até 10 caracteres  | Não          |
| dddAdicionalComprador                | DDD do telefone adicional do comprador                 | Alfa Numérico | Até 3 caracteres   | Não          |
| ddiAdicionalComprador                | DDI do telefone adicional do comprador                 | Alfa Numérico | Até 3 caracteres   | Não          |
| codigoTipoTelefoneAdicionalComprador | 1 - Outros 2 - Residencial 3 - Comercial               | Numérico      | 1 dígito           | Sim          |
| emailComprador                       | E-mail do comprador                                    | Alfa Numérico | Até 100 caracteres | Sim          |
| enderecoComprador                    | Logradouro do comprador                                | Alfa Numérico | Até 100 caracteres | Sim          |
| numeroEnderecoComprador              | Número do logradouro do comprador                      | Alfa Numérico | Até 10 caracteres  | Sim          |
| bairroEnderecoComprador              | Bairro comprador                                       | Alfa Numérico | Até 50 caracteres  | Sim          |
| complementoEnderecoComprador         | Complemento do endereço comprador                      | Alfa Numérico | Até 50 caracteres  | Não          |
| cidadeEnderecoComprador              | Cidade do comprador                                    | Alfa Numérico | Até 50 caracteres  | Sim          |
| estadoEnderecoComprador              | Estado do comprador                                    | Alfa Numérico | Até 2 caracteres   | Sim          |
| paisComprador                        | Pais do Comprador                                      | Alfa Numérico | Até 10 caracteres  | Sim          |
| cepEnderecoComprador                 | CEP do comprador. Enviar sem traços ou espaços         | Alfa Numérico | Até 10 caracteres  | Sim          |
| enderecoEntrega                      | Logradouro de entrega                                  | Alfa Numérico | Até 100 caracteres | Não          |
| numeroEnderecoEntrega                | Número do logradouro de entrega                        | Alfa Numérico | Até 10 caracteres  | Não          |
| bairroEnderecoEntrega                | Bairro do logradouro de entrega                        | Alfa Numérico | Até 50 caracteres  | Não          |
| complementoEnderecoEntrega           | Complemento do endereço de entrega                     | Alfa Numérico | Até 50 caracteres  | Não          |
| cidadeEnderecoEntrega                | Cidade de entrega                                      | Alfa Numérico | Até 50 caracteres  | Não          |
| estadoEnderecoEntrega                | Estado de entrega                                      | Alfa Numérico | 2 caracteres       | Não          |
| paisEntrega                          | Pais de entrega                                        | Alfa Numérico | Até 10 caracteres  | Sim          |
| cepEnderecoEntrega                   | CEP de entrega. Enviar sem traços ou espaços           | Alfa Numérico | Até 10 caracteres  | Não          |
| telefoneEntrega                      | Telefone de entrega. Sem espaços ou traços             | Alfa Numérico | Até 10 caracteres  | Não          |
| dddEntrega                           | DDD do telefone de entrega                             | Alfa Numérico | Até 3 caracteres   | Não          |
| ddiEntrega                           | DDI do telefone de entrega                             | Alfa Numérico | Até 3 caracteres   | Não          |
| codigoTipoTelefoneEntrega            | 1 - Outros 2 - Residencial 3 - Comercial               | Numérico      | 1 dígito           | Sim          |
| telefoneAdicionalEntrega             | Telefone adicional de entrega. Sem espaços ou traços   | Alfa Numérico | Até 3 caracteres   | Não          |
| dddAdicionalEntrega                  | DDD do telefone adicional de entrega                   | Alfa Numérico | Até 3 caracteres   | Não          |
| ddiAdicionalEntrega                  | DDI do telefone adicional de entrega                   | Alfa Numérico | Até 3 caracteres   | Não          |
| codigoTipoTelefoneAdicionalEntrega   | 1 - Outros 2 - Residencial 3 - Comercial               | Numérico      | 1 dígito           | Sim          |



`itemPedidoTransacaoWS`
{: .subtituloAzul }

| Campo                | Descrição                                                          | Tipo          | Tamanho        | Obrigatório |
|----------------------|--------------------------------------------------------------------|---------------|----------------|-------------|
| codigoProduto        | Código único que identifica cada produto                           | Alfa Numérico | 20 caracteres  | Sim         |
| codigoCategoria      | Código que identifica categoria do produto                         | Alfa Numérico | 20 caracteres  | Sim         |
| nomeProduto          | Nome do Produto                                                    | Alfa Numérico | 100 caracteres | Sim         |
| quantidadeProduto    | Quantidade comprada do produto                                     | Numérico      | Até 8 dígitos  | Sim         |
| valorUnitarioProduto | Valor unitário do produto. Deve ser enviado sem pontos ou vírgulas | Numérico      | Até 10 dígitos | Sim         |
| nomeCategoria        | Nome da categoria do produto                                       | Alfa Numérico | 100 caracteres | Sim         |

**RESPOSTA**

| Campo                     | Descrição                                                               | Tipo           | Tamanho            |
|---------------------------|-------------------------------------------------------------------------|----------------|--------------------|
| numeroTransacao           | Código que identifica a transação dentro do Yapay                    | Numérico       | Até 19 dígitos     |
| codigoEstabelecimento     | Código que identifica o estabelecimento dentro do Yapay              | Numérico       | 13 dígitos         |
| codigoFormaPagamento      | <a href="/gateway/codigos-da-api/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                                            | Numérico       | Até 3 dígitos      |
| valor                     | Valor da transação.                                                     | Numérico       | Até 10 dígitos     |
| valorDesconto             | Valor desconto                                                          | Numérico       | Até 10 dígitos     |
| taxaEmbarque              | Valor taxa embarque                                                     | Numérico       | Até 10 dígitos     |
| parcelas                  | Quantidade de parcelas da transação                                     | Numérico       | Até 2 dígitos      |
| urlPagamento              | Para o modelo redirect. Essa será a URL de redirecionamento da operação | Alfa Numérico  | Até 500 caracteres |
| statusTransacao           | Status atual da transação                                               | Numérico       | Até 2 dígitos      |
| autorizacao               | Código de autorização da adquirente                                     | Numérico       | Até 20 dígitos     |
| codigoTransacaoOperadora  | Código da transação na adquirente                                       | Numérico       | Até 20 dígitos     |
| dataAprovacaoOperadora    | Data de aprovação na adquirente                                         | Alfa Numérico  | Até 10 dígitos     |
| numeroComprovanteVenda    | Número do comprovante de venda                                          | Alfa Numérico  | Até 20 dígitos     |
| mensagemVenda             | Mensagem de retorno da adquirente                                       | Alfa Numérico  | Até 50 dígitos     |





