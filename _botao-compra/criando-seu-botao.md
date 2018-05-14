---
title: Criando seu próprio botão
position: 1
right_code: |
  ~~~ html
    <form method="post" action="https://tc.intermediador.yapay.com.br/payment/transaction"> 
          <!-- Campos obrigatórios --> 
         <input type="hidden" name="token_account" value="SEU_TOKEN_AQUI"> 
 
        <!-- Dados do produto 1 --> 
         <input type="hidden" name="transaction_product[][description]" value="Notebook Prata"> 
         <input type="hidden" name="transaction_product[][quantity]" value="1"> 
         <input type="hidden" name="transaction_product[][price_unit]" value="2430.00"> 

         <!-- Itens do produto 2 --> 
         <input type="hidden" name="transaction_product[][description]" value="Notebook Branco"> 
         <input type="hidden" name="transaction_product[][quantity]" value="1"> 
         <input type="hidden" name="transaction_product[][price_unit]" value="2599.00"> 
 
         <!-- Código de referência do pagamento no seu sistema (opcional) --> 
         <input type="hidden" name="order_number" value="56789"> 
 
         <!-- submit do form --> 
         <input type="submit" name="submit" value="Pagar com Yapay" > 
    </form>
  ~~~
  {: title="Com 2 produtos" }

  ~~~ html
    <form method="post" action="https://tc.intermediador.yapay.com.br/payment/transaction"> 
 
         <!-- Campos obrigatórios --> 
         <input type="hidden" name="token_account" value="SEU_TOKEN_AQUI"> 
 
         <!-- Dados do produto --> 
         <input type="hidden" name="transaction_product[][description]" value="Notebook Prata"> 
         <input type="hidden" name="transaction_product[][quantity]" value="1"> 
         <input type="hidden" name="transaction_product[][price_unit]" value="2430.00"> 
         <input type="hidden" name="transaction_product[][extra]" value="Informações Adicionais do Produto"> 
         <input type="hidden" name="transaction_product[][code]" value="0001"> 
         <input type="hidden" name="transaction_product[][url_img]" value="http://www.loja.com.br/img_prod.png"> 
         <input type="hidden" name="transaction_product[][sku_code]" value="0001"> 

         <!-- Código de referência do pagamento no seu sistema (opcional) --> 
         <input type="hidden" name="order_number" value="56789"> 
 
        <!--Campos adicionais da transação --> 
        <input name="customer[name]" type="hidden" value="Nome do Cliente"> 
        <input name="customer[cpf]" type="hidden" value="57488378113"> 
        <input name="customer[email]" type="hidden" value="chuck@norris.org"> 
        <input name="customer[contacts][][type_contact]" type="hidden" value="H"> 
        <input name="customer[contacts][][number_contact]" type="hidden" value="1433330000"> 
        <input name="customer[addresses][][type_address]" type="hidden" value="E"> 
        <input name="customer[addresses][][postal_code]" type="hidden" value="17516000"> 
        <input name="customer[addresses][][street] " type="hidden" value="Av de Teste"> 
        <input name="customer[addresses][][number] " type="hidden" value="123"> 
        <input name="customer[addresses][][neighborhood]" type="hidden" value="Centro"> 
        <input name="customer[addresses][][completion]" type="hidden" value="ABC"> 
        <input name="customer[addresses][][city]" type="hidden" value="Marilia"> 
        <input name="customer[addresses][][state]" type="hidden" value="SP"> 
        <input name="customer[birth_date]" type="hidden" value="01/01/1985"> 
        <input name="url_notification" type="hidden" value=" http://www.sualoja.com.br/url_notification.php"> 

         <!-- submit do form --> 
         <input type="submit" name="submit" value="Pagar com Yapay" > 
 
    </form>
  ~~~
  {: title="Com campos adicionais" }

---

Na criação do seu botão você utiliza a integração via **POST**.

Para a utilização da modalidade POST será necessário somente ter conhecimento em HTML, bastando apenas a inclusão de um código HTML em seu site. Esta modalidade fará com que o seu cliente seja redirecionado para o Yapay, onde finalizará sua compra.

<!-- ![Integração Yapay via POST](/images/intermediador/conteudo/Integracao_post.png "Integração Yapay via POST") -->


Integração Completa via POST
{: .subtitulo }

Para uma integração com mais dados e produtos, poderá ser utilizada uma integração mais avançada com o Yapay. Esta transação irá receber além dos dados da conta e pedido, uma maior quantidade de produtos.

Após receber o post de dados, o Yapay irá automaticamente redirecionar o usuário para a página de finalização de compra, onde o mesmo poderá escolher a forma de pagamento e informar os dados do cartão de crédito.

Para a integração basta ser realizado um POST:

| Endereço para Integração  |                                                                   |
|---------------------------|-------------------------------------------------------------------|
| Ambiente de Testes        | https://tc.intermediador.sandbox.yapay.com.br/payment/transaction |
| Ambiente de Produção      | https://tc.intermediador.yapay.com.br/payment/transaction         |
| Protocolo                 | POST                                                              |


Para a integração via POST, segue abaixo os dados necessários para envio:

| Dados de Entrada                      | Formato / Tam. Max              | Descrição                                |
|---------------------------------------|---------------------------------|------------------------------------------|
|   token_account                       |   Texto / 15	                  |   Token de identificação da loja         |
|   transaction_product[][description]	|   Texto / 150                   |   Descrição do produto <sup>1</sup>      |
|   transaction_product[][quantity]	    |   Número / 5	                  |   Quantidade do produto                  |
|   transaction_product[][price_unit]	  |   Decimal / Ex: 0.00	          |   Valor do produto                       |

<sup>1</sup> Note que nas informações acima que alguns dados possuem uma característica diferente, tendo um elemento [] dentro de sua formatação. Isso ocorre justamente para permitir que sejam enviados diversos itens na mesma requisição.
{: .info }


Veja ao lado um POST de exemplo com 2 produtos.

Para melhorar o processo de integração, é possível enviar dados adicionais que completarão automaticamente os dados no Yapay, evitando que o consumidor digite novamente as informações.

Os dados adicionais que podem ser enviados neste POST são:

| Dados de Entrada                      | Formato / Tam. Max              | Descrição                                |
|---------------------------------------|---------------------------------|------------------------------------------|
| transaction_product[][code]           |  Número / 20                    |  Código do produto                       |
| transaction_product[][extra]          |  Texto / 45                     |  Informações extras do produto           |
| transaction_product[][url_img]        |  Url / 255                      |  URL da imagem do produto                |
| transaction_product[][sku_code]       |  Texto / 20                     |  Código SKU do produto                   |
| order_number                          |  Número / 20                    |  Número do pedido                        |
| free                                  |  Texto / 100                    |  Informações extras da transação         |
| price_additional                      |  Decimal / Ex: 0.00             |  Valor adicional da transação            |
| price_discount                        |  Decimal / Ex: 0.00             |  Valor do desconto da transação          |
| url_notification                      |  Url / 255                      |  Endereço do site de notificação         |
| url_success                           |  Url / 255                      |  URL para redirecionamento caso concluída a transação com sucesso <sup>2</sup>   |
| url_process                           |  Url / 255                      |  URL para redirecionamento caso pedido esteja aguardando a confirmação de pagamento <sup>2</sup> |
| url_cancel                            |  Url / 255                      |  URL para redirecionamento caso concluída a transação mas ocorreu falha no pagamento <sup>2</sup> |
| shipping_type                         |  Texto / 15                     |  Tipo de envio                           |
| shipping_price                        |  Decimal / Ex: 0.00             |  Valor do envio                          |
| sub_store                             |  Texto / 20                     |  Sub-Loja                                |
| url_css                               |  Url / 255                      |  URL do CSS customizado                  |
| available_payment_methods             |  Texto /20                      |  Meios de Pagamento disponíveis          |
| max_split_transaction                 |  Número /10                     |  Número máximo de parcelas               |
| customer[name]                        |  Texto /100                     |  Nome do Comprador                       |
| customer[cpf]                         |  Texto /14                      |  CPF do Comprador                        |
| customer[email]                       |  Texto /100                     |  E-mail do Comprador                     |
| customer[birth_date]                  |  Data / 10                      |  Data de Nascimento do Comprador         |
| customer[contacts][][type_contact]    |  Texto /1                       |  Tipo do Contato.<sup>1</sup> (Tabela 1) |
| customer[contacts][][number_contact]  |  Texto /10                      |  Número do telefone do Comprador         |
| customer[addresses][][type_address]   |  Texto /1                       |  Tipo do Endereço <sup>1</sup> (Tabela 2)           |
| customer[addresses][][postal_code]    |  Texto /8                       |  CEP do endereço do Comprador            |
| customer[addresses][][street]         |  Texto /120                     |  Nome da rua do Comprador                |
| customer[addresses][][number]         |  Texto /10                      |  Número do endereço do Comprador         |
| customer[addresses][][neighborhood]   |  Texto /100                     |  Bairro do endereço do Comprador         |
| customer[addresses][][completion]     |  Texto /100                     |  Complemento do endereço do Comprador    |
| customer[addresses][][city]           |  Texto /120                     |  Cidade do endereço do Comprador         |
| customer[addresses][][state]          |  Texto /2                       |  Estado do endereço do Comprador         |           


<sup>1</sup> Note que nas informações acima que alguns dados possuem uma característica diferente, tendo um elemento [] dentro de sua formatação. Isso ocorre justamente para permitir que sejam enviados diversos itens na mesma requisição. 
{: .info }
<sup>2</sup> Para o redirecionamento basta utilizar somente o campo url_process, pois caso seja omitido os campos url_success e url_cancel, é utilizado o campo url_process para o redirecionamento.
{: .info }


Veja ao lado um POST de exemplo com os campos adicionais:

Tabelas Auxiliares
{: .subtitulo }

Na integração existem alguns campos com informações pré-definidas, onde deverão ser enviadas conforme o padrão existente.

Abaixo segue tabelas com essas informações pré-definidas:


| Tabela 1 - Contato |
|--------------------|---|
| Residencial        | H |
| Celular            | M |
| Comercial          | W |


| Tabela 2 - Tipos de Endereço |
|-------------|---|
| Cobrança    | D |
| Entrega     | B |


<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>