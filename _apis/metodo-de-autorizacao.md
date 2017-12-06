---
title: Método de Autorização
position: 3
menu: intermediador
---

A autenticação será possível somente se a aplicação estiver devidamente cadastrada, homologada e sem restrições no Yapay. Para iniciar a autenticação, é necessário redirecionar o usuário para a URL de autenticação do Yapay via Browser, juntamente com os parâmetros que identifiquem a aplicação.

O Yapay apresentará uma interface para o usuário confirmar a permissão de acesso a suas informações e recursos. Após a autorização, o Yapay retornará um código de autorização para o aplicativo.

Ao receber o código de autorização (**code**), o aplicativo deverá requisitar o código de acesso (**access_token**) ao servidor do Yapay informando o código de autorização (**code**), **consumer_key** e **consumer_secret**.

Com o código de acesso (**access_token**) o aplicativo poderá acessar os recursos e informações do cliente.

Além do código de acesso, o aplicativo receberá o código de atualização (**refresh_token**), esse código será utilizado para manter o código de acesso ativo no sistema do Yapay através de uma API de atualização de código.
	
Abaixo a sequência de autenticação:

![Fluxo da Autenticação](/images/intermediador/conteudo/uml.png "Fluxo da Autenticação"){: width="70%" height="auto" }


<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>