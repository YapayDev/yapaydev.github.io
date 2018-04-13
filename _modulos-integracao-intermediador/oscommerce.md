---
title: OsCommerce
position: 6
menu: intermediador
---

Para disponibilizar o Yapay como facilitador de pagamento na plataforma OsCommerce, basta baixar o pacote disponível no site institucional do Yapay, extrair a pasta com o módulo e enviar para sua loja. 

Fique atento que sua versão de instalação OsCommerce deve ser compatível com o módulo Yapay.

1- Instalação do Módulo OsCommerce
{: .subtitulo }

Para instalar o módulo é necessário baixar o pacote através do link abaixo:

<a href="http://integracao.traycheckout.com.br/documentacao/download/yapay/oscommerce/yapayintermediador_oscommerce.zip" class="btn  btn-default btn-wide btn-call-to-action btnMagento"><i class="fa fa-arrow-circle-down" aria-hidden="true"></i>OsCommerce</a>


Descompacte o arquivo baixado e copie as pastas e arquivos para o diretório raiz de sua instalação do OsCommerce, caso o sistema exiba a mensagem de mesclagem ou substituição de arquivos, clique em sim para todos.

Passos para instalação via FTP, utilizando o WinSCP:

1. Enviar o conteúdo da pasta extraída para o servidor da loja virtual, utilizando um software FTP (neste exemplo utilizamos o WinSCP)

2. Ao efetuar a conexão no FTP, no lado direito serão mostradas as pastas que estão dentro do servidor, acesse a pasta que está sua loja OsCommerce

3. Enviar as pastas e arquivos extraídos (pastas **ext** e **includes** e arquivo **checkout_Yapay.php**) do módulo Yapay para a pasta raiz da instalação de sua loja OsCommerce

Cuidado para não arrastar em cima de uma pasta, se isso acontecer você terá uma pasta dentro da outra e então este módulo não funcionará.

![OsCommerce, instalação](/images/intermediador/conteudo/install_oscommerce_1.png "OsCommerce, instalação"){:width="100%" height="auto"}

Segue a visualização dos diretórios da instalação do OsCommerce:

![OsCommerce, instalação](/images/intermediador/conteudo/install_oscommerce_2.png "OsCommerce, instalação"){:width="100%" height="auto"}


Após a conclusão do envio do módulo Yapay, acesse a administração do OsCommerce e entre na seção de **Pagamentos** do menu **Módulos**, onde será localizado o módulo Yapay.

![OsCommerce, instalação](/images/intermediador/conteudo/install_oscommerce_3.png "OsCommerce, instalação"){:width="100%" height="auto"}

Clique na opção do módulo Yapay onde será mostrado o módulo conforme a imagem abaixo. Ative o módulo clicando em **Instalar** no lado direito da listagem:

![OsCommerce, instalação](/images/intermediador/conteudo/install_oscommerce_4.png "OsCommerce, instalação"){:width="100%" height="auto"}

O próximo passo é configurar o módulo (veja o item 2), inserindo os dados de cadastro de sua conta para liberar os pagamentos em sua conta Yapay.

2- Configuração do Módulo OsCommerce
{: .subtitulo }

Para a configuração do módulo, acesse o menu **Módulos > Pagamento**, e selecione a opção **Yapay**, onde será exibido o botão **Editar**.

Ao clicar no botão **Editar**, serão listadas todas as informações para a configuração do módulo, onde poderá localizar o Token na área administrativa do Yapay, no menu **Perfil da Conta > Minha Conta > Dados da Conta**.

Segue abaixo imagem com as opções para a configuração do módulo:

![OsCommerce, instalação](/images/intermediador/conteudo/install_oscommerce_5.png "OsCommerce, instalação"){:width="100%" height="auto"}


Opções de configuração do módulo Yapay:
{: .subtitulo }

**Yapay:** opção para habilitar o Yapay na finalização de compra

**Token:** chave gerada no seu painel de administração do Yapay

**Tipo de Integração** três opções de exibição do Yapay, onde:

- **REDIRECT:** O consumidor é redirecionado para o ambiente do Yapay para finalização da transação

- **FRAME:** O Yapay é aberto dentro da loja virtual, possibilitando o comprador finalizar a compra sem sair da loja

- **MODAL:** Ao finalizar a compra, o Yapay será exibido sobre a loja virtual, sem o consumidor sair do ambiente da loja



<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>
