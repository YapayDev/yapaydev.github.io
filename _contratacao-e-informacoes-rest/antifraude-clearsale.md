---
title: Antifraude ClearSale
position: 1
menu: gateway
---

O gateway fornece a possibilidade de incluir um analisador de fraude para garantir a segurança das transações.

Quando um analisador de fraude/risco é ativado, ele se encaixa depois que a transação é autorizada e antes que a mesma seja capturada. O processo como um todo segue o seguinte fluxo:

* Transação é enviada para a operadora /instituição financeira para ser autorizada.
* Uma vez autorizada, o gateway envia a transação para análise de fraude.
* Caso seja aprovada na análise, a transação entrará em modo de espera para ser enviada para a captura (de forma automática ou manual, de acordo com as configurações do estabelecimento). Caso seja negada na análise, a transação será automaticamente cancelada na operadora.

<!-- O Gateway de Pagamento Yapay possui integração com o sistema de prevenção de risco e fraude ClearSale, nas seguintes modalidades **Total, Total Garantido, Application, ID e Start**. Caso for utilizado a funcionalidade de Finger Print da Clear Sale, o campo SessionID deverá ser enviado no `campoLivre2` do Gateway Yapay. Para maiores informações acesse: <a href="http://br.clear.sale" target="_blank" class="linkPadraoVerde">http://br.clear.sale</a> -->

Sistemas Integrados com a Yapay
{: .subtitulo }

O Gateway de Pagamenta Yapay possui integração com o sistema de prevenção de risco e fraude ClearSale, nas seguintes modalidades Total, Total Garantido, Application, RealTime e Start. Caso for utilizado a funcionalidade de Fingerprint da ClearSale, o campo SessionID deverá ser enviado no campoLivre2 da Yapay. Para ter mais informações e receber um contato, sem compromisso de nosso time, acesse: <a href="https://lp.br.clear.sale/yapay" target="_blank" class="linkPadraoVerde">https://lp.br.clear.sale/yapay</a>
 
Para consultar valores dos planos da ClearSale com condições especiais da parceria, entre em contato através do email: **parcerias@clear.sale**


Informações para configuração
{: .subtitulo }

**TOTAL/TOTAL GARANTIDO e APPLICATION**

* Entity Code

**START**

* Entity Code

**ID**
* Entity Code




<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>