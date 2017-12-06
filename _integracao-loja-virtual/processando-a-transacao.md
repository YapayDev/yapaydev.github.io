---
title: Processando a transação
position: 1
menu: intermediador
---

O Yapay disponibiliza a integração de transações transparente, excluindo a necessidade de redirecionamento para outra página e sem preencher outro formulário de cadastro. O cliente fica na sua página e faz a transação com um único cadastro. Na integração transparente o comprador realiza a finalização da compra diretamente na sua loja, atraves da API é enviado os dados para o Yapay e o comprador recebe o comprovante de compra:

![Integração Loja Virtual Yapay](/images/intermediador/conteudo/Integracao_api_LV.png "Integração Loja Virtual Yapay"){: width=80%" height="auto" }

É feita uma consulta atraves do CPF do cliente na base do Yapay, que verifica pela existência do seu cadastro e então as transações são vinculadas ao mesmo. Caso não exista uma conta, o sistema irá criar uma nova conta com os dados que forem submetidos na integração. 

Para realizar a integração é necessário incluir um script após o processamento da transação, e também incluir a chamada do plugin no final da página.

Para esta integração, deverá ser feito uso da **API de Transação**, <a href="/intermediador/apis/#api-transacao" target="_blank" class="linkPadraoVerde">clique aqui</a> e veja a documentação.
{:.info}

Para facilitar a exibição do parcelamento em sua Loja Virtual, veja a documentação da <a href="/intermediador/apis/#api-simulacao-parcelamento" target="_blank" class="linkPadraoVerde">API de Simulação de Parcelamento</a>.
{:.warning}



<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>