---
title: Glossário
position: 2
menu: gateway
navbar: rest
---

Tudo que você precisa para se integrar ao nosso Gateway.

Gateway de pagamento é uma solução tecnológica, que permite, facilmente, que quaisquer sistemas que possam se comunicar via WebService, realizem cobranças via boleto, cartão e transferências bancárias. Uma vez integrado ao Yapay, seu sistema estará pronto para disponibilizar diversas Formas de Pagamento.

| Termo                       | Descrição                                                                                                              |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------|
| Autorização          | A etapa inicial do processo, onde a operadora financeira é acionada pelo Yapay. Essa etapa verifica a condição de crédito do cliente, ou seja, verifica se o mesmo possui crédito suficiente para realizar a compra. Em caso positivo, aquele valor é sensibilizado no limite do cartão.                            |
| Autenticação         | Processo onde o portador é encaminhado para a página do banco emissor, afim de assegurar que é o portador legítimo do cartão. |
| Captura              | A confirmação da transação. Nesta etapa o Yapay aciona a operadora financeira para confirmar uma transação previamente autorizada. Somente nessa etapa em que o cliente será realmente cobrado.                                                                                                                      |
| Cancelamento         | Cancelamento de uma compra realizada com cartão.                                                                              |
| One Click            | Através desta funcionalidade é possível o cadastro dos cartões dos consumidores para serem utilizados em compras futuras.     |
| Recorrência          | Agendamento de cobranças. O Gateway é responsável por realizar as cobranças de acordo com a data agendada pelo eCommerce.     |
| Modelo WebService    | Consumidor digitará os dados de cartão na página de Checkout do eCommerce.                                                    |
| Modelo Redirecionado | Consumidor digitará os dados de cartão na página da adquirente.                                                               |