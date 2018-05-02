---
title: Criando uma transação
position: 1
menu: gateway
right_code: |
  ~~~ json
  curl
    --request POST https://sandbox.gateway.yapay.com.br/checkout/api/v3/transacao
    --header "Content-Type: application/json"
    --curl -u usuario:senha .........
    --data-binary
    {
      "codigoEstabelecimento" : 1000000000000,
      "codigoFormaPagamento" : 29,
      "transacao" : {
          "numeroTransacao" : 1234,
          "valor" : 2000,
          "valorDesconto" : 0,
          "parcelas" : 1,
          "urlCampainha" : "http://seusite.com.br/campainha",
          "urlResultado" : "http://seusite.com.br/retorno",
          "ip" : "192.168.12.110",
          "idioma" : 1,
          "dataVencimentoBoleto":"13/12/2030"
      },
      "itensDoPedido" : [
      {
          "codigoProduto" : 1,
          "nomeProduto" : "Produto 1",
          "codigoCategoria" : 1,
          "nomeCategoria" : "categoria",
          "quantidadeProduto" : 1,
          "valorUnitarioProduto" : 2000
      }
      ],
      "dadosCobranca" : {
          "codigoCliente" : 1,
          "tipoCliente" : 1,
          "nome" : "Teste 123",
          "email" : "teste@teste.com",
          "dataNascimento" : "10/01/1975",
          "sexo" : "M",
          "documento" : "123.123.123-12",
          "endereco" : {
            "logradouro" : "Rua",
            "numero" : "123",
            "complemento" : "",
            "cep" : "12345-678",
            "bairro" : "Bairro",
            "cidade" : "Cidade",
            "estado" : "SP",
            "pais" : "BR"
            },
          "telefone" : [
            {
            "tipoTelefone" : "1",
            "ddi" : "55",
            "ddd" : "12",
            "telefone" : "1234-5678"
            }
          ]
      },
      "dadosEntrega" : { 
          "nome" : "Teste 123",
          "endereco" : {
            "logradouro" : "Rua",
            "numero" : "123",
            "complemento" : "",
            "cep" : "12345-678",
            "bairro" : "Bairro",
            "cidade" : "Cidade",
            "estado" : "SP",
            "pais" : "BR"
            },
          "telefone" : [
            {
            "tipoTelefone" : "1",
            "ddi" : "55",
            "ddd" : "12",
            "telefone" : "1234-5678"
            }
          ]
      }
    }


  ~~~
  {: title="Exemplo criação transação" }

  ~~~ json
  --header "Content-Type: application/json"
    {  "numeroTransacao": 1234,
      "codigoEstabelecimento": "1000000000000",
      "codigoFormaPagamento": 29,
      "valor": 2000, 
      "valorDesconto": 0, 
      "parcelas": 1, 
      "statusTransacao": 8,
      "autorizacao": "0",
      "codigoTransacaoOperadora": "0",
      "dataAprovacaoOperadora": "", 
      "numeroComprovanteVenda": "", 
      "nsu": "",
      "mensagemVenda": "",
      "urlPagamento": "https://sandbox.gateway.yapay.com.br/checkout/Gerarboleto.do?cod=14956296486904d8312c6-d57a-499e-b53b-504047402e45"
    }

  ~~~
  {: title="Exemplo retorno transação" }
  


---

Estrutura para geração de boletos com carteiras sem ou com registro.

Particulariedades:

* O campo `<estado>` deve ser preenchido apenas com a sigla do Estado;
* O campo `<numeroTransacao>` deve conter até 8 dígitos;
* Caso o campo `<dataVencimentoBoleto>` não for enviado, será utilizado os dias de vencimento configurado internamente no Gateway;
* Para boletos com carteira registrada (contratação a parte), o status retornado pelo Yapay no primeiro momento será 5 (transação em andamento), enquanto para boletos sem registros é retornado 8 (aguardando pagamento);
* Importante a utilização do recurso de Campainha, para atualização dos pedidos no Ecommerce;
* A conciliação de boletos não é realizada automaticamente, funcionalidade deve ser contratada a parte com o comercial@yapay.com.br.


REQUISIÇÃO
{: .subtitulo }

<i class="fa fa-info-circle" aria-hidden="true"></i> Para enviar a transação, utilize o método <span class="post">POST</span>.
{: .informativo }

Para autenticação, enviar `login` e `senha` no HEADER:

| Campo   | Descrição                |
|---------|--------------------------|
| usuario | Login do estabelecimento |
| senha   | Senha do estabelecimento |



| Campo                   | Descrição                                                                                 | Tipo          | Tamanho           | Obrigatório |
|-------------------------|-------------------------------------------------------------------------------------------|---------------|-------------------|-------------|
| codigoEstabelecimento   | Código que identifica o estabelecimento dentro do Yapay (fornecido pelo gateway)       | Numérico      | 13 dígitos        | Sim         |
| codigoFormaPagamento    | <a href="/gateway/rest/codigos-da-api-rest/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>  | Numérico      | Até 3 dígitos     | Sim         |
| transacao               | Nó reservado para informações da transação                                                | - | - | - |
| dadosCartao             | Nó reservado para dados de cartão                                                         | - | - | - |
| dadosCobranca           | Nó reservado para informações dos dados de cobrança                                       | - | - | - |
| telefone                | Nó reservado para informações de telefone                                                 | - | - | - |
| dadosEntrega            | Nó reservado para informações de dados de entrega                                         | - | - | - |

_`transacao`_
{: .subtituloAzul }

| Campo                 | Descrição                                                                                               | Tipo          | Tamanho        | Obrigatório |
|-----------------------|----------------------------------------------------------------------------------------------------------------|---------------|----------------|-----|
| numeroTransacao       | Código que identifica a transação dentro do Yapay                                                              | Numérico      | Até 19 dígitos | Sim |
| codigoEstabelecimento | Código que identifica o estabelecimento dentro do Yapay (fornecido pelo gateway)                            | Numérico       | 13 dígitos     | Sim |
| codigoFormaPagamento  | <a href="/gateway/rest/codigos-da-api-rest/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>  | Numérico      | Até 3 dígitos     | Sim         |
| valor                 | Valor da transação. Deve ser enviado sem pontos ou vírgulas                                                    | Numérico       | Até 10 dígitos | Sim |
| valorDesconto         | Valor do desconto da transação. Campo apenas informativo                                                       | Numérico       | Até 10 dígitos | Sim |
| urlCampainha          | URL será sempre acionada quando o status do pedido mudar. Deve estar preparada para receber dados de campainha | Alfa Numérico  | Até 250 caracteres | Sim |
| dataVencimentoBoleto  | Data de vencimento do boleto, se não enviado será utilizado os dias da configuração                            | Alfa Numérico  | Até 10 caracteres  | Não |
| urlResultado          | Para o modelo de pagamento redirect, O Yapay redirecionará para essa URL                                    | Alfa Numérico  | Até 250 caracteres | Para pagamentos redirecionáveis é obrigatório |
| ip                    | Número do IP do usuário final/cliente. Formato xxx.xxx.xxx.xxx                                                 | Alfa Numérico | Até 15 caracteres  | Não |
| idioma                | 1 - Português 2 - Inglês 3 - Espanhol                                                                          | Numérico      | -                  | Sim |
| campoLivre1           | Campo Livre 1 | Alfa Numérico                                                                                  | Até 16 caracteres                  | Não |
| campoLivre2           | Campo Livre 2 | Alfa Numérico                                                                                  | Até 16 caracteres                  | Não |
| campoLivre3           | Campo Livre 3 | Alfa Numérico                                                                                  | Até 16 caracteres                  | Não |
| campoLivre4           | Campo Livre 4 | Alfa Numérico                                                                                  | Até 16 caracteres                  | Não |
| campoLivre5           | Campo Livre 5 | Alfa Numérico                                                                                  | Até 16 caracteres                  | Não |



_`dadosCobranca`_
{: .subtituloAzul }

| Campo           | Descrição                                               | Tipo          | Tamanho            | Obrigatório |
|-----------------|--------------------------------------------------- -----|---------------|--------------------|-------------|
| nome            | Nome do comprador                                       | Alfa Numérico | Até 100 caracteres | Sim         |
| documento       | Documento principal do comprado                         | Alfa Numérico | 30 caracteres      | Sim         |
| documento2      | Documento principal do comprado                         | Alfa Numérico | 30 caracteres      | Não         |
| email           | E-mail do comprador                                     | Alfa Numérico | 20 caracteres      | Sim         |
| codigoCliente   | Código do Comprador                                     | Alfa Numérico | 20 caracteres      | Não         |
| dataNascimento  | Data Nascimento Comprador                               | Alfa Numérico | 10 caracteres      | Não         |
| sexo            | Sexo Comprador                                          | Alfa Numérico | 2 caracteres       | Não         |
| tipoCliente     | Tipo do Cliente - 1 - Pessoa Física 2 - Pessoa Jurídica | Numérico      | Até 8 dígitos      | Sim         |
| endereco        | Nó reservado para dados de endereço do comprador        | - | - | - |
| telefone        | Nó reservado para dados de telefone do comprador        | - | - | - |


_`endereco`_
{: .subtituloAzul }

| Campo       | Descrição               | Tipo          | Obrigatório |
|-------------|-------------------------|---------------|-------------|
| logradouro  | Endereço do comprador   | Alfa Numérico | Sim         |
| numero      | Número do comprador     | Alfa Numérico | Sim         |
| bairro      | Bairro do comprador     | Alfa Numérico | Sim         |
| complemento | Complemento do endereço | Alfa Numérico | Não         |
| cidade      | Cidade do comprador     | Alfa Numérico | Sim         |
| estado      | Estado do comprador     | Alfa Numérico | Sim         |
| cep         | CEP do comprador        | Alfa Numérico | Sim         |
| pais        | País do comprador       | Alfa Numérico | Não         |


_`telefone`_
{: .subtituloAzul }

| Campo        | Descrição                                                                                  | Tipo          | Obrigatório |
|--------------|--------------------------------------------------------------------------------------------|---------------|-------------|
| tipoTelefone | 1 = Outros / 2 = Residencial / 3 = Comercial / 4 = Recados / 5 = Cobrança / 6 = Temporário | Numérico      | Sim         |
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


_`itensDoPedido`_
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

| Campo                    | Descrição                                                                | Tipo           | Tamanho            |
|--------------------------|--------------------------------------------------------------------------|----------------|--------------------|
| numeroTransacao          | Código que identifica a transação dentro do Yapay                     | Numérico       | Até 19 dígitos     |
| codigoEstabelecimento    | Código que identifica o estabelecimento dentro do Yapay               | Numérico       | 13 dígitos         |
| codigoFormaPagamento     | <a href="/gateway/rest/codigos-da-api-rest/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                                             | Numérico       | Até 3 dígitos      |
| valor                    | Valor da transação.                                                      | Numérico       | Até 10 dígitos     |
| valorDesconto            | Valor desconto                                                           | Numérico       | Até 10 dígitos     |
| taxaEmbarque             | Valor taxa embarque                                                      | Numérico       | Até 10 dígitos     |
| parcelas                 | Quantidade de parcelas da transação                                      | Numérico       | Até 2 dígitos      |
| urlPagamento             | PUrl para geração do boleto                                              | Alfa Numérico  | Até 500 caracteres |
| statusTransacao          | <a href="/gateway/rest/codigos-da-api-rest/#status-de-transacao" target="_blank" class="linkPadraoVerde">Status atual da transação</a> | Numérico       | Até 2 dígitos      |
| autorizacao              | Retornado "0" para boletos                                               | Numérico       | Até 20 dígitos     |
| codigoTransacaoOperadora | Retornado "0" para boletos                                               | Numérico       | Até 20 dígitos     |
| dataAprovacaoOperadora   | Retornado em branco para boletos                                         | Alfa Numérico  | Até 10 dígitos     |
| numeroComprovanteVenda   | Retornado em branco para boletos                                         | Alfa Numérico  | Até 20 dígitos     |
| mensagemVenda            | Retornado em branco para boletos                                         | Alfa Numérico  | Até 50 dígitos     |





Ao lado você pode visualizar um exemplo de retorno da transação.


<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>