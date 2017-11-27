---
title: Pagamento com token
position: 2
menu: gateway
right_code: |
  ~~~ xml
  <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:pag="http://pagamentos.webservices.superpay.ernet.com.br/">
    <soapenv:Header/>
    <soapenv:Body>
        <pag:alteraCadastraPagamentoOneClick>
          <dadosOneClick>
              <codigoEstabelecimento>1318336765212</codigoEstabelecimento>
              <dataValidadeCartao>11/2018</dataValidadeCartao>
              <emailComprador>teste@suporte.com.br</emailComprador>
              <formaPagamento>380</formaPagamento>
              <nomeTitularCartaoCredito>teste SuperPay</nomeTitularCartaoCredito>
              <numeroCartaoCredito>1111222233334444</numeroCartaoCredito>
          </dadosOneClick>
          <token>1476210884949a25ed2d6-17cf-4ac4-af22-5c67d7907ef5</token>
          <usuario>superpay</usuario>
          <senha>superpay</senha>
        </pag:alteraCadastraPagamentoOneClick>
    </soapenv:Body>
  </soapenv:Envelope>
  ~~~
  {: title="Exemplo de alteração de cadastro" }

  ~~~ xml
  <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:Body>
        <ns2:alteraCadastraPagamentoOneClickResponse xmlns:ns2="http://pagamentos.webservices.superpay.ernet.com.br/">
        <return>
              <codigoEstabelecimento>1010101010101010</codigoEstabelecimento>
              <codigoSeguranca/>
              <dataValidadeCartao>11/2018</dataValidadeCartao>
              <emailComprador>teste@suporte.com.br</emailComprador>
              <formaPagamento>380</formaPagamento>
              <nomeTitularCartaoCredito>Teste SuperPay</nomeTitularCartaoCredito>
              <numeroCartaoCredito>111122******4444</numeroCartaoCredito>
        </return>
        </ns2:alteraCadastraPagamentoOneClickResponse>
    </soap:body>
  </soap:envelope>
  ~~~
  {: title="Exemplo retorno alteração de cadastro" }

---

Com o Token recebido no momento do cadastro, é possível realizar o pagamento.

**REQUISIÇÃO**
{: .subtitulo }

<i class="fa fa-info-circle" aria-hidden="true"></i> Para pagamento com token, acione o método `pagamentoOneClickV2`.
{: .informativo }

Para autenticação, enviar usuario e senha:

| Campo   | Descrição                |
|---------|--------------------------|
| usuario | Login do estabelecimento |
| senha   | Senha do estabelecimento |



_`transacaoOneClickWS`_
{: .subtituloAzul }

| Campo                      | Descrição                                                                         | Tipo               | Tamanho	           | Obrigatório |
|----------------------------|-----------------------------------------------------------------------------------|--------------------|--------------------|-------------|
| numeroTransacao            | Código que identifica a transação dentro do Yapay                                 | Numérico           | Até 19 dígitos     | Sim |
| codigoEstabelecimento      | Código que identifica o estabelecimento dentro do Yapay (fornecido pelo gateway)  | Numérico           | 13 dígitos         | Sim |
| token                      | Valor único obtido através do serviço “cadastroPagamentoOneClick2”                | Alfa Numérico      | Até 100 caracteres | Sim |
| cvv                        | Código de segurança do cartão                                                     | Numérico           | Até 4 dígitos      | Sim |
| valor                      | Valor da transação. Deve ser enviado sem pontos ou vírgulas                       | Numérico           | Até 10 dígitos     | Sim |
| valorDesconto              | Valor do desconto da transação. Campo apenas informativo                          | Numérico           | Até 10 dígitos     | Sim |
| taxaEmbarque               | Valor da taxa de embarque. Campo apenas informativo| Numérico                     | Até 10 dígitos     | Sim |
| parcelas                   | Quantidade de parcelas da transação. Verificar se forma de pagamento suporta parcelamento | Numérico | Até 2 dígitos | Sim |
| urlCampainha               | URL será sempre acionada quando o status do pedido mudar. Deve estar preparada para receber dados de campainha | Alfa Numérico | Até 250 caracteres | Não |
| urlRedirecionamentoPago    | Para o modelo de pagamento redirect, O Yapay redirecionará para essa URL em caso de transação aprovada | Alfa Numérico | Até 250 caracteres | Para pagamentos com redirect é obrigatório |
| urlRedirecionamentoNaoPago | Para o modelo de pagamento redirect, O Yapay redirecionará para essa URL em caso de transação reprovada | Alfa Numérico | Até 250 caracteres | Para pagamentos com redirect é obrigatório |
| ip                         | Número do IP do usuário final/cliente. Formato xxx.xxx.xxx.xxx                    | Alfa Numérico  | Até 15 caracteres | Sim |
| origemTransacao            | 1 - eCommerce 2 - Mobile 3 - URA                                                  | Numérico       | -                 | Sim |
| campoLivre1                | Campo Livre 1                                                                     | Alfa Numérico  | Até 16 caracteres | Não |
| campoLivre2                | Campo Livre 2                                                                     | Alfa Numérico  | Até 16 caracteres | Não |
| campoLivre3                | Campo Livre 3                                                                     | Alfa Numérico  | Até 16 caracteres | Não |
| campoLivre4                | Campo Livre 4                                                                     | Alfa Numérico  | Até 16 caracteres | Não |
| campoLivre5                | Campo Livre 5                                                                     | Alfa Numérico  | Até 16 caracteres | Não |
| dadosUsuarioTransacao      | Informações para cobrança e entrega. Informações importantes para análise de fraude | -| -|
| itensDoPedido              | Lista com Itens que estão sendo comprados. Informações importantes para análise de fraude e intermediários financeiros | - | - |


_`dadosUsuarioTransacao`_
{: .subtituloAzul }


| Campo                        | Descrição                                           | Tipo          | Tamanho            | Obrigatório                 |
|------------------------------|-----------------------------------------------------|---------------|--------------------|-----------------------------|
| codigoCliente                | Código que identifica o cliente no estabelecimento  | Alfa Numérico | 20 caracteres      | Não                         |
| tipoCliente                  | 1 - Pessoa Física 2 - Pessoa Jurídica               | Numérico      | 1 dígito           | Sim                         |
| nomeComprador                | Nome do comprador                                   | Alfa Numérico | Até 100 caracteres | Caso utilize antifraude sim |
| documentoComprador           | Documento principal do comprador                    | Alfa Numérico | 30 caracteres      | Caso utilize antifraude sim |
| sexoComprador                | M – Masculino / F – Feminino                        | Alfa Numérico | 1 caracter         | Não                         |
| dataNascimentoComprador      | Data de nascimento do comprador. Formato dd/mm/yyyy | Alfa Numérico | 10 caracteres      | Caso utilize antifraude sim |
| telefoneComprador            | Telefone do comprador sem espaços ou traços         | Alfa Numérico | Até 10 caracteres  | Caso utilize antifraude sim |
| dddComprador                 | DDD do telefone do comprador                        | Alfa Numérico | Até 3 caracteres   | Caso utilize antifraude sim |
| ddiComprador                 | DDI do telefone do comprador                        | Alfa Numérico | Até 3 caracteres   | Caso utilize antifraude sim |
| codigoTipoTelefoneComprador  | 1 - Outros 2 - Residencial 3 - Comercial            | Numérico      | 1 dígito           | Sim                         |
| emailComprador               | E-mail do comprador                                 | Alfa Numérico | Até 100 caracteres | Caso utilize antifraude sim |
| enderecoComprador            | Logradouro do comprador                             | Alfa Numérico | Até 100 caracteres | Caso utilize antifraude sim |
| numeroEnderecoComprador      | Número do logradouro do comprador                   | Alfa Numérico | Até 10 caracteres  | Caso utilize antifraude sim |
| bairroEnderecoComprador      | Bairro comprador                                    | Alfa Numérico | Até 50 caracteres  | Caso utilize antifraude sim |
| complementoEnderecoComprador | Complemento do endereço comprador                   | Alfa Numérico | Até 50 caracteres  | Não                         |
| cidadeEnderecoComprador      | Cidade do comprador                                 | Alfa Numérico | Até 50 caracteres  | Caso utilize antifraude sim |
| estadoEnderecoComprador      | Estado do comprador                                 | Alfa Numérico | Até 2 caracteres   | Caso utilize antifraude sim |
| cepEnderecoComprador         | CEP do comprador. Enviar sem traços ou espaços      | Alfa Numérico | Até 10 caracteres  | Caso utilize antifraude sim |
| enderecoEntrega              | Logradouro de entrega                               | Alfa Numérico | Até 100 caracteres | Caso utilize antifraude sim |
| numeroEnderecoEntrega        | Número do logradouro de entrega                     | Alfa Numérico | Até 10 caracteres  | Caso utilize antifraude sim |
| bairroEnderecoEntrega        | Bairro do logradouro de entrega                     | Alfa Numérico | Até 50 caracteres  | Caso utilize antifraude sim |
| complementoEnderecoEntrega   | Complemento do endereço de entrega                  | Alfa Numérico | Até 50 caracteres  | Não                         |
| cidadeEnderecoEntrega        | Cidade de entrega                                   | Alfa Numérico | Até 50 caracteres  | Caso utilize antifraude sim |
| estadoEnderecoEntrega        | Estado de entrega                                   | Alfa Numérico | 2 caracteres       | Caso utilize antifraude sim |
| cepEnderecoEntrega           | CEP de entrega. Enviar sem traços ou espaços        | Alfa Numérico | Até 10 caracteres  | Caso utilize antifraude sim |
| telefoneEntrega              | Telefone de entrega. Sem espaços ou traços          | Alfa Numérico | Até 10 caracteres  | Caso utilize antifraude sim |
| dddEntrega                   | DDD do telefone de entrega                          | Alfa Numérico | Até 3 caracteres   | Caso utilize antifraude sim |
| ddiEntrega                   | DDI do telefone de entrega                          | Alfa Numérico | Até 3 caracteres   | Caso utilize antifraude sim |
| codigoTipoTelefoneEntrega    | 1 - Outros 2 - Residencial 3 - Comercial            | Numérico      | 1 dígito           | Sim                         |


_`itemPedidoTransacaoWS`_
{: .subtituloAzul }


| Campo                | Descrição                                                          | Tipo          | Tamanho        | Obrigatório                 |
|----------------------|--------------------------------------------------------------------|---------------|----------------|-----------------------------|
| codigoProduto        | Código único que identifica cada produto                           | Alfa Numérico | 20 caracteres  | Caso utilize antifraude sim |
| codigoCategoria      | Código que identifica categoria do produto                         | Alfa Numérico | 20 caracteres  | Caso utilize antifraude sim |
| nomeProduto          | Nome do Produto                                                    | Alfa Numérico | 100 caracteres | Caso utilize antifraude sim |
| quantidadeProduto    | Quantidade comprada do produto                                     | Numérico      | Até 8 dígitos  | Caso utilize antifraude sim |
| valorUnitarioProduto | Valor unitário do produto. Deve ser enviado sem pontos ou vírgulas | Numérico      | Até 10 dígitos | Caso utilize antifraude sim |
| nomeCategoria        | Nome da categoria do produto                                       | Alfa Numérico | 100 caracteres | Caso utilize antifraude sim |




**RESPOSTA**


| Campo                    | Descrição                                                  | Tipo          | Tamanho            |
|--------------------------|------------------------------------------------------------|---------------|--------------------|
| numeroTransacao          | Código que identifica a transação dentro do SuperPay       | Numérico      | Até 19 dígitos     |
| codigoEstabelecimento    | Código que identifica o estabelecimento dentro do SuperPay | Numérico      | 13 dígitos         |
| codigoFormaPagamento     | <a href="/gateway/codigos-da-api/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                              | Numérico      | Até 3 dígitos      |
| valor                    | Valor da transação.                                        | Numérico      | Até 10 dígitos     |
| valorDesconto            | Valor desconto                                             | Numérico      | Até 10 dígitos     |
| taxaEmbarque             | Valor taxa embarque                                        | Numérico      | Até 10 dígitos     |
| parcelas                 | Quantidade de parcelas da transação                        | Numérico      | Até 2 dígitos      |
| urlPagamento             | Url para autenticação em caso de cartão de débito          | Alfa Numérico | Até 500 caracteres |
| statusTransacao          | <a href="/gateway/codigos-da-api/#status-de-transacao" target="_blank" class="linkPadraoVerde">Status atual da transação</a>                                  | Numérico      | Até 2 dígitos      |
| autorizacao              | Número de autorização da adquirente                        | Numérico      | Até 20 dígitos     |
| codigoTransacaoOperadora | Código de retorno da adquirente                            | Numérico      | Até 20 dígitos     |
| dataAprovacaoOperadora   | Data aprovação                                             | Alfa Numérico | Até 10 dígitos     |
| numeroComprovanteVenda   | Número Comprovante de venda                                | Alfa Numérico | Até 20 dígitos     |
| mensagemVenda            | Mensagem de venda                                          | Alfa Numérico | Até 50 dígitos     |

