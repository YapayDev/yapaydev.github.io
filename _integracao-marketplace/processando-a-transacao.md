---
title: Processando a transação
position: 1
menu: intermediador
---

O Yapay disponibiliza a integração transparente com **Marketplace**, onde o usuário consegue finalizar a compra dentro Marketplace, sem necessitar de redirecionamento para outra aplicação e preenchar novos formulários. O usuário finaliza a compra e os dados da transação são enviados via API para o Yapay, após a conclusão é enviado um comprovante de compra para o usuário:

![Integração Marketplace Yapay](/images/intermediador/conteudo/Integracao_api_LV.png "Integração Marketplace Yapay"){: width=80%" height="auto" }

A verificação do cadastro do cliente é feita por uma consulta do CPF do cliente, caso não exista uma conta, o sistema irá criar uma nova conta com os dados que forem submetidos na integração.

Para realizar a integração de forma correta, é necessário incluir um script após o processamento da transação, e também incluir a chamada do plugin no final da página.

Para esta integração, deverá ser feito uso da **API de Transação**, <a href="/intermediador/apis/#api-transacao" target="_blank" class="linkPadraoVerde">clique aqui</a> e veja a documentação.
{:.info}

Para facilitar a exibição do parcelamento no Marketplace, veja a documentação da <a href="/intermediador/apis/#api-simulacao-parcelamento" target="_blank" class="linkPadraoVerde">API de Simulação de Parcelamento</a>.
{:.warning}