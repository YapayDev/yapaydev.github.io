---
title: Transação com Múltiplos Cartões
position: 3
menu: gateway
right_code: |
    ~~~ json
    --request POST https://sandbox.gateway.yapay.com.br/checkout/api/v3/transacao
    --header "Content-Type: application/json"
    --curl -u usuario:senha .........
    --data-binary
    {
    "codigoEstabelecimento" : 1000000000000,
    "codigoFormaPagamento" : 999,
    "dadosMultiplosCartoes": [
        {
            "nomePortador": "CARTAO 1",
            "numeroCartao": "0000000000000001",
            "codigoSeguranca": "321",
            "dataValidade": "12/2024",
            "codigoFormaPagamento": 170,
            "parcelas": 1,
            "valor": 500
        },
        {
            "nomePortador": "CARTAO 2",
            "numeroCartao": "0000000000000001",
            "codigoSeguranca": "123",
            "dataValidade": "12/2022",
            "codigoFormaPagamento": 171,
            "parcelas": 1,
            "valor": 800
        },
    "transacao" : {
        "numeroTransacao" : 1234,
        "valorDesconto" : 0,
        "urlCampainha" : "http://seusite.com.br/campainha",
        "ip" : "192.168.12.110",
        "idioma" : 1,
        "campoLivre1" : "",
        "campoLivre2" : "",
        "campoLivre3" : "",
        "campoLivre4" : "",
        "campoLivre5" : ""
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

    ~~~json
    --header "Content-Type: application/json"
    {
    "numeroTransacao": 1234,
    "codigoEstabelecimento": "1000000000000",
    "multiploCartao": 1,
    "statusTransacao": 1,
    "detalhesMultiploCartao":    [
            {
            "codigoFormaPagamento": 170,
            "valor": 500,
            "valorDesconto": 0,
            "parcelas": 1,
            "autorizacao": "513663",
            "codigoTransacaoOperadora": "6",
            "dataAprovacaoOperadora": "2018-02-21 11:50:21",
            "numeroComprovanteVenda": "0221115021704",
            "mensagemVenda": "Operation Successful"
            },
            {
            "codigoFormaPagamento": 171,
            "valor": 800,
            "valorDesconto": 0,
            "parcelas": 1,
            "autorizacao": "20307",
            "codigoTransacaoOperadora": "6",
            "dataAprovacaoOperadora": "2018-02-21 11:50:22",
            "numeroComprovanteVenda": "0221115022682",
            "mensagemVenda": "Operation Successful"
            }
    ]
    }
    ~~~    
    {: title="Exemplo retorno transação" }
---


Através desta estrutura é possível o envio de mais de um cartão de crédito para aprovação em uma mesma transação, dividindo o valor total do pedido entre os cartões.

**Particulariedades**

* Disponível apenas no plano Corporativo;
* Disponível apenas para cartões de cŕedito na modalidade WS.


**REQUISIÇÃO**


 <i class="fa fa-info-circle" aria-hidden="true"></i> Para enviar a transação, utilize o método <span class="post">POST</span>.
 {: .informativo }

 Para autenticação, enviar `usuario` e `senha` seguindo os patrões **Basic Authentication**:


| Campo    | Descrição                |
|----------|--------------------------|
| usuario  | Login do estabelecimento |
| senha    | Senha do estabelecimento |


| Campo                    | Descrição                                                                        | Tipo     | Tamanho       | Obrigatório |
|--------------------------|----------------------------------------------------------------------------------|----------|---------------|-------------|
| codigoEstabelecimento | Código que identifica o estabelecimento dentro do Yapay (fornecido pelo gateway) | Numérico | 13 dígitos    | Sim         |
| codigoFormaPagamento  | Código da forma de pagamento Enviar 999                                             | Numérico | Até 3 dígitos | Sim         |
| transacao             | Nó reservado para informações da transação                                          | -        | -             | -           |
| dadosMultiplosCartoes | Nó reservado para dados de cartão                                                   | -        | -             | -           |
| itensDoPedido         | Nó reservado para informações dos produtos                                          | -        | -             | -           |
| dadosCobranca         | Nó reservado para informações dos dados de cobrança                                 | -        | -             | -           |
| telefone              | Nó reservado para informações de telefone                                           | -        | -             | -           |
| dadosEntrega          | Nó reservado para informações de dados de entrega                                   | -        | -             | -           |


_`dadosMultiplosCartoes`_
{: .subtituloAzul }

| Campo                | Descrição                                                                | Tipo          | Tamanho           | Obrigatório |
|----------------------|--------------------------------------------------------------------------|---------------|-------------------|-------------|
| nomePortador         | Nome do titular do cartão de crédito (Exatamente como escrito no cartão) | Alfa Numérico | Até 16 dígitos    | Sim         |
| numeroCartao         | Numero do cartão de crédito, sem espaços ou traços                       | Numérico      | Até 22 caracteres | Sim         |
| codigoSeguranca      | Código de segurança do cartão (campo não é armazenado pelo Yapay)        | Numérico      | Até 4 caracteres  | Sim         |
| dataValidade         | Data de validade do cartão. Formato mm/yyyy                              | Alfa Numérico | 7 caracteres      | Sim         |
| codigoFormaPagamento | Código da forma de pagamento                                             | Numérico      | Até 3 dígitos     | Sim         |
| parcelas             | Quantidade de parcelas da transação.                                     | Numérico      | Até 2 dígitos     | Sim         |
| valor                | Valor da transação. Deve ser enviado sem pontos ou vírgulas              | Numérico      | Até 10 dígitos    | Sim         |


| Campo            | Descrição                                                                    | Tipo          | Tamanho           | Obrigatório |
| numeroTransacao  | Código que identifica a transação dentro do Yapay                            | Numérico      | Até 19 dígitos    | Sim         |
| moeda            | Tipo da moeda. OBS: Disponível 'USD" apenas para PayPal Internacional        | Alfa Numérico | Até 10 caracteres | Não         |
| tipoParcelamento | Use "E" para estabelecimento, use "A" para administradora. Caso não for enviado será utilizado as configurações do seu estabelecimento | Alfa Numérico | 1 caracter | Não |
| valorDesconto    | Valor do desconto da transação. Campo apenas informativo                     | Numérico      | Até 10 dígitos    | Sim         |
| urlCampainha     | URL será sempre acionada quando o status do pedido mudar. Deve estar preparada para receber dados de campainha | Alfa Numérico | Até 250 caracteres | Sugerimos o envio para pagamentos com captura manual |
| ip               | Número do IP do usuário final/cliente. Formato xxx.xxx.xxx.xxx               | Alfa Numérico | Até 15 caracteres | Não         |
| idioma           | 1 - Português 2 - Inglês 3 - Espanhol                                        | Numérico      | -                 | Sim         |
| campoLivre1      | Campo Livre 1                                                                | Alfa Numérico | Até 16 caracteres | Não         |
| campoLivre2      | Campo Livre 2                                                                | Alfa Numérico | Até 16 caracteres | Não         |
| campoLivre3      | Campo Livre 3                                                                | Alfa Numérico | Até 16 caracteres | Não         |
| campoLivre4      | Campo Livre 4                                                                | Alfa Numérico | Até 16 caracteres | Não         |
| campoLivre5      | Campo Livre 5                                                                | Alfa Numérico | Até 16 caracteres | Não         |


_`dadosCobranca`_
{: .subtituloAzul }

| Campo          | Descrição                                               | Tipo          | Tamanho            | Obrigatório                                              |
|----------------|---------------------------------------------------------|---------------|--------------------|----------------------------------------------------------|
| nome           | Nome do comprador                                       | Alfa Numérico | Até 100 caracteres | Não, mas sugerimos o envio para identificação do cliente |
| documento      | Documento principal do comprado                         | Alfa Numérico | 30 caracteres      | Não, mas sugerimos o envio para identificação do cliente |
| documento2     | Documento principal do comprado                         | Alfa Numérico | 30 caracteres      | Não                                                      |
| email          | E-mail do comprador                                     | Alfa Numérico | 20 caracteres      | Não                                                      |
| codigoCliente  | Código do Comprador                                     | Alfa Numérico | 20 caracteres      | Não                                                      |
| dataNascimento | Data Nascimento Comprador                               | Alfa Numérico | 10 caracteres      | Não                                                      |
| sexo           | Sexo Comprador                                          | Alfa Numérico | 2 caracteres       | Não                                                      |
| tipoCliente    | Tipo do Cliente - 1 - Pessoa Física 2 - Pessoa Jurídica | Numérico      | Até 8 dígitos      | Não                                                      |
| endereco       | Nó reservado para dados de endereço do comprador        | -             | -                  | -                                                        |
| telefone       | Nó reservado para dados de telefone do comprador        | -             | -                  | -                                                        |

Observação: O envio do nó dadosCobranca é obrigatório.

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
| endereco | Nó reservado para dados de endereço do comprador | -             | -             | -           |
| telefone | Nó reservado para dados de telefone do comprador | -             | -             | -           |


**RESPOSTA**

| Campo                  | Descrição                                               | Tipo     | Tamanho        |
|------------------------|---------------------------------------------------------|----------|----------------|
| numeroTransacao        | Código que identifica a transação dentro do Yapay       | Numérico | Até 19 dígitos |
| codigoEstabelecimento  | Código que identifica o estabelecimento dentro do Yapay | Numérico | 13 dígitos     |
| multiploCartao         | Retornará 1                                             | Numérico | 1 dígito       |
| statusTransacao        | Status atual da transação                               | Numérico | Até 2 dígitos  |
| detalhesMultiploCartao | Nó reservado para retornos de cartão                    | -        | -              |


_`detalhesMultiploCartao`_
{: .subtituloAzul }

| Campo                    | Descrição                           | Tipo          | Tamanho        |
|--------------------------|-------------------------------------|---------------|----------------|
| codigoFormaPagamento     | Código da forma de pagamento        | Numérico      | Até 3 dígitos  |
| valor                    | Valor da transação.                 | Numérico      | Até 10 dígitos |
| valorDesconto            | Valor desconto                      | Numérico      | Até 10 dígitos |
| parcelas                 | Quantidade de parcelas da transação | Numérico      | Até 2 dígitos  |
| autorizacao              | Código de autorização da adquirente | Numérico      | Até 20 dígitos |
| codigoTransacaoOperadora | Código da transação na adquirente   | Numérico      | Até 20 dígitos |
| dataAprovacaoOperadora   | Data de aprovação na adquirente     | Alfa Numérico | Até 10 dígitos |
| numeroComprovanteVenda   | Número do comprovante de venda      | Alfa Numérico | Até 20 dígitos |
| mensagemVenda            | Mensagem de retorno da adquirente   | Alfa Numérico | Até 50 dígitos |


<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>