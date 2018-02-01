---
title: Pagamento
position: 2
menu: gateway
right_code: |
  ~~~ json
  curl
    --request POST https://sandbox.gateway.yapay.com.br/checkout/api/v3/oneclick/1514483826864c3149224-67db-4557-8950-6a80f708c1c5/autorizar
    --header "Content-Type: application/json"
    --curl -u usuario:senha
    --data-binary
    {
        "codigoEstabelecimento" : 1000000000000,
        "transacao" : {
            "numeroTransacao" : 123,
            "valor" : 100,
            "parcelas" : 1,
            "idioma" : 1
        },
        "dadosCartao" : {
            "codigoSeguranca" : "123"
        },
        "itensDoPedido" : [
        {
            "quantidadeProduto" : 1,
            "valorUnitarioProduto" : 100
        }
        ],
        "dadosCobranca" : {
            "nome" : "Teste Integração",
            "documento" : "12312312312",
            "tipoCliente" : 1
        }
    }

  ~~~
  {: title="Exemplo de transação" }

  ~~~ json
  --header "Content-Type: application/json
    {
      "numeroTransacao": 123,
      "codigoEstabelecimento": "1000000000000",
      "codigoFormaPagamento": 170,
      "valor": 100,
      "valorDesconto": 0,
      "parcelas": 1,
      "oneClick": 1,
      <!--Token utiizado para o pagamento-->
      "token": "1514483826864c3149224-67db-4557-8950-6a80f708c1c5",
      <!--Status que deverá ser tratado pelo eCommerce-->
      "statusTransacao": 1,
      <!--Código de autorização-->
      "autorizacao": "892358",
      <!--Código de retorno operadora-->
      "codigoTransacaoOperadora": "6",
      <!--Data retorno adquirente-->
      "dataAprovacaoOperadora": "2018-01-10 10:18:43",
      <!--TID-->
      "numeroComprovanteVenda": "0110101834052",
      <!--Mensagem adquirente-->
      "mensagemVenda": "Operation Successful"
    }

  ~~~
  {: title="Exemplo retorno" }

---


Com o Token recebido no momento do cadastro, é possível realizar o pagamento de uma venda juntamente com o código de segurança que o usuário irá inserir na página de Checkout.

 <i class="fa fa-exclamation-circle" aria-hidden="true"></i> SANDBOX: `https://sandbox.gateway.yapay.com.br/checkout/api/v3/oneclick/<<`token`>>/autorizar`
{: .informativoVermelho }

<i class="fa fa-exclamation-circle" aria-hidden="true"></i> PRODUÇÃO: `https://gateway.yapay.com.br/checkout/api/v3/oneclick/<<`token`>>/autorizar`
{: .informativoVermelho }


REQUISIÇÃO
{: .subtitulo }

<i class="fa fa-info-circle" aria-hidden="true"></i> Para criar o token, acione o método <span class="post">POST</span>.
{: .informativo }

 Para autenticação, enviar `usuario` e `senha` seguindo os padrões Basic Authentication:


| Campo    | Descrição                |
|----------|--------------------------|
| usuario  | Login do estabelecimento |
| senha    | Senha do estabelecimento |



| Campo                 | Descrição                                                                           | Tipo     | Tamanho       | Obrigatório |
|-----------------------|-------------------------------------------------------------------------------------|----------|---------------|-------------|
| codigoEstabelecimento | Código que identifica o estabelecimento dentro do SuperPay (fornecido pelo gateway) | Numérico | 13 dígitos    | Sim         |
| codigoFormaPagamento  | <a href="/gateway/rest/codigos-da-api-rest/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                                                        | Numérico | Até 3 dígitos | Sim         |
| transacao             | Nó reservado para informações da transação                                          | -        | -             | -           |
| dadosCartao           | Nó reservado para dados de cartão                                                   | -        | -             | -           |
| itensDoPedido         | Nó reservado para informações dos produtos                                          | -        | -             | -           |
| dadosCobranca         | Nó reservado para informações dos dados de cobrança                                 | -        | -             | -           |
| telefone              | Nó reservado para informações de telefone                                           | -        | -             | -           |
| dadosEntrega          | Nó reservado para informações de dados de entrega                                   | -        | -             | -           |

_`transacao`_
{: .subtituloAzul }

| Campo                 | Descrição                                                                           | Tipo     | Tamanho              | Obrigatório |
|-----------------------|-------------------------------------------------------------------------------------|----------|----------------------|-------------|
| numeroTransacao       | Código que identifica a transação dentro do SuperPay                                | Numérico | Até 19 dígitos       | Sim         |
| codigoEstabelecimento | Código que identifica o estabelecimento dentro do SuperPay (fornecido pelo gateway) | Numérico | 13 dígitos           | Sim         |
| codigoFormaPagamento  | <a href="/gateway/rest/codigos-da-api-rest/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                                                        | Numérico | Até 3 dígitos        | Sim         |
| valor                 | Valor da transação. Deve ser enviado sem pontos ou vírgulas                         | Numérico | Até 10 dígitos       | Sim         |
| moeda                 | Tipo da moeda. OBS: Disponível 'USD" apenas para PayPal Internacional               | Alfa Numérico	Até 10 caracteres | Não         |
| tipoParcelamento      | Use "E" para estabelecimento, use "A" para administradora. Caso não for enviado será utilizado as configurações do seu estabelecimento | Alfa Numérico | 1 caracter | Não |
| valorDesconto         | Valor do desconto da transação. Campo apenas informativo                                                       | Numérico      | Até 10 dígitos     | Não |
| parcelas              | Quantidade de parcelas da transação. Verificar se forma de pagamento suporta parcelamento                      | Numérico      | Até 2 dígitos      | Sim |
| urlCampainha          | URL será sempre acionada quando o status do pedido mudar. Deve estar preparada para receber dados de campainha | Alfa Numérico | Até 250 caracteres | Não |
| urlResultado          | Para o modelo de pagamento redirect, O SuperPay redirecionará para essa URL                                    | Alfa Numérico | Até 250 caracteres | Não |
| ip                    | Número do IP do usuário final/cliente. Formato xxx.xxx.xxx.xxx                                                 | Alfa Numérico | Até 15 caracteres  | Não |
| idioma                | 1 - Português 2 - Inglês 3 - Espanhol                                                                          | Numérico	    | -                  | Sim |
| campoLivre1           | Campo Livre 1                                                                                                  | Alfa Numérico | Até 16 caracteres  | Não |
| campoLivre2           | Campo Livre 2                                                                                                  | Alfa Numérico | Até 16 caracteres  | Não |
| campoLivre3           | Campo Livre 3                                                                                                  | Alfa Numérico | Até 16 caracteres  | Não |
| campoLivre4           | Campo Livre 4                                                                                                  | Alfa Numérico | Até 16 caracteres  | Não |
| campoLivre5           | Campo Livre 5                                                                                                  | Alfa Numérico | Até 16 caracteres  | Não |



_`dadosCartao`_
{: .subtituloAzul }

| Campo           | Descrição                                                            | Tipo     | Tamanho          | Obrigatório |
|-----------------|----------------------------------------------------------------------|----------|------------------|-------------|
| codigoSeguranca | Código de segurança do cartão (campo não é armazenado pelo SuperPay) | Numérico | Até 4 caracteres | Sim         |


_`dadosCobranca`_
{: .subtituloAzul }

| Campo          | Descrição                                                | Tipo          | Tamanho            | Obrigatório |
|----------------|----------------------------------------------------------|---------------|--------------------|-------------|
| nome           | Nome do comprador                                        | Alfa Numérico | Até 100 caracteres | Sim         |
| documento      | Documento principal do comprado                          | Alfa Numérico | 30 caracteres      | Sim         |
| documento2     | Documento principal do comprado                          | Alfa Numérico | 30 caracteres      | Não         |
| codigoCliente  | Código do Comprador                                      | Alfa Numérico | 20 caracteres      | Não         |
| dataNascimento | Data Nascimento Comprador                                | Alfa Numérico | 10 caracteres      | Não         |
| sexo           | Sexo Comprador                                           | Alfa Numérico | 2 caracteres       | Não         |
| tipoCliente    | Tipo do Cliente - 1 - Pessoa Física 2 - Pessoa Jurídica  | Numérico      | Até 8 dígitos      | Sim         |
| endereco       | Nó reservado para dados de endereço do comprador         | - | - | - |
| telefone       | Nó reservado para dados de telefone do comprador         | - | - | - |


_`itensDoPedido`_
{: .subtituloAzul }

| Campo                | Descrição                                                          | Tipo          | Tamanho        | Obrigatório |
|----------------------|--------------------------------------------------------------------|---------------|----------------|-------------|
| codigoProduto        | Código único que identifica cada produto                           | Alfa Numérico | 20 caracteres  | Não         |
| codigoCategoria      | Código que identifica categoria do produto                         | Alfa Numérico | 20 caracteres  | Não         |
| nomeProduto          | Nome do Produto                                                    | Alfa Numérico | 100 caracteres | Não         |
| quantidadeProduto    | Quantidade comprada do produto                                     | Numérico      | Até 8 dígitos  | Sim         |
| valorUnitarioProduto | Valor unitário do produto. Deve ser enviado sem pontos ou vírgulas | Numérico      | Até 10 dígitos | Sim         |
| nomeCategoria        | Nome da categoria do produto                                       | Alfa Numérico | 100 caracteres | Não         |


_`endereco`_
{: .subtituloAzul }

| Campo       | Descrição               | Tipo          | Obrigatório |
|-------------|-------------------------|---------------|-------------|
| logradouro  | Endereço do comprador   | Alfa Numérico | Não         |
| numero      | Número do comprador     | Alfa Numérico | Não         |
| bairro      | Bairro do comprador     | Alfa Numérico | Não         |
| complemento | Complemento do endereço | Alfa Numérico | Não         |
| cidade      | Cidade do comprador     | Alfa Numérico | Não         |
| estado      | Estado do comprador     | Alfa Numérico | Não         |
| cep         | CEP do comprador        | Alfa Numérico | Não         |
| pais        | País do comprador       | Alfa Numérico | Não         |


_`telefone`_
{: .subtituloAzul }

| Campo        | Descrição                                                                                  | Tipo          | Obrigatório |
|--------------|--------------------------------------------------------------------------------------------|---------------|-------------|
| tipoTelefone | 1 = Outros / 2 = Residencial / 3 = Comercial / 4 = Recados / 5 = Cobrança / 6 = Temporário | Numérico      | Não         |
| ddi          | Código DDI do telefone                                                                     | Alfa Numérico | Não         |
| ddd          | Código DDD do telefone                                                                     | Alfa Numérico | Não         |
| telefone     | Número do telefone                                                                         | Alfa Numérico | Não         |


_`dadosEntrega`_
{: .subtituloAzul }


| Campo    | Descrição                                        | Tipo          | Tamanho       | Obrigatório |
|----------|--------------------------------------------------|---------------|---------------|-------------|
| nome     | Nome do comprador                                | Alfa Numérico | 20 caracteres | Não         |
| email    | E-mail do comprador                              | Alfa Numérico | 20 caracteres | Não         |
| endereco | Nó reservado para dados de endereço do comprador | - | - | - |
| telefone | Nó reservado para dados de telefone do comprador | - | - | - |


**RESPOSTA**

| Campo                    | Descrição                                                  | Tipo          | Tamanho           |
|--------------------------|------------------------------------------------------------|---------------|-------------------|
| numeroTransacao          | Código que identifica a transação dentro do SuperPay       | Numérico      | Até 19 dígitos    |
| codigoEstabelecimento    | Código que identifica o estabelecimento dentro do SuperPay | Numérico      | 13 dígitos        |
| codigoFormaPagamento     | <a href="/gateway/rest/codigos-da-api-rest/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                               | Numérico      | Até 3 dígitos     |
| valor                    | Valor da transação.                                        | Numérico      | Até 10 dígitos    |
| valorDesconto            | Valor desconto                                             | Numérico      | Até 10 dígitos    |
| parcelas                 | Quantidade de parcelas da transação                        | Numérico      | Até 2 dígitos     |
| oneClick                 | 1 para OneClick                                            | Numérico      | 1 dígito          |
| token                    | Token utilizado para o pagamento                           | Alfa Numérico | Até 60 caracteres |
| statusTransacao          | Status atual da transação                                  | Numérico      | Até 2 dígitos     |
| autorizacao              | Código de autorização da adquirente                        | Numérico      | Até 20 dígitos    |
| codigoTransacaoOperadora | Código da transação na adquirente                          | Numérico      | Até 20 dígitos    |
| dataAprovacaoOperadora   | Data de retorno na adquirente                              | Alfa Numérico | Até 10 caracteres |
| numeroComprovanteVenda   | Número do comprovante de venda                             | Alfa Numérico | Até 20 caracteres |
| mensagemVenda            | Mensagem de retorno da adquirente                          | Alfa Numérico | Até 50 caracteres |


<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>