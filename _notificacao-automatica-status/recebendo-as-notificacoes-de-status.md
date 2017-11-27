---
title: Recebendo as notificações de status
position: 1
menu: intermediador
---

O Yapay pode comunicar com sua aplicação a cada alteração de status de uma transação, fazendo com que seu sistema acompanhe todo o fluxo de status e esteja sempre atualizado quanto a situação da transação.

![Fluxo de notificação automática](/images/intermediador/conteudo/Notificacao_automatica.png "Fluxo de notificação automática"){: width="70%" height="auto"}

Integração com Notificação Automática de Status
{: .subtitulo }

Para a integração com a notificação automática de status, é necessário configurar uma URL que receberá a chamada, processará os dados recebidos, e em seguida irá obter mais detalhes da transação através de uma API específica. Esse parâmetro está disponível em ambas as integrações (POST ou API) e chama-se **transaction[url_notification]**.

O Yapay irá realizar o POST com a seguinte informação:

| Parâmetro enviado via Post                      |
|--------------------------|----------------------|
| token_transaction        | Token da transação   |


A notificação será realizada através de um POST, que espera receber o retorno **“HTTP 200”** de sua aplicação. Caso a página esteja fora do ar ou com algum outro erro e não retorne “HTTP 200”, **serão feitas novas tentativas a cada 12 horas durante 3 dias**.

Após receber esta informação, deverá ser feita a consulta pelas informações completas da transação, através da <a href="/intermediador/apis/#api-consulta-transacao" target="_blank" class="linkPadraoVerde">API de Consulta de Transação</a>.
{:.info}