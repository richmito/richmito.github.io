---
layout: post
title: "OpenSUSE dia 1"
date: 2016-11-15 21:18:25
image: '/assets/img/'
description:
tags:
categories:
twitter_text:
---  
Pela terceira vez decidi dar uma chance de usar OpenSUSE.  
As duas primeiras tentativas foram frustradas por problemas sérios no gerenciador de boot, que mais tarde descobri serem frutos de uma configuração falha minha. E por problemas nos repositórios, mesmo após sucessivas reinstalações.  
Vamos ignorar esses problemas no momento, depois falo do problema do boot que resolvi.  
Começo da história, sábado (12/11/2016) fiz backup completo dos meus arquivos pessoais do Ubutu 16.04, que usava até então. Tinha instalado este sistema em um disco de 160GB, usado em paralelo ao de 320GB com Windows 10. Pretendia simplesmente aproveitar a partição /home pra evitar o trabalho de recopiar tudo, no meio do processo de instalação, mudei de ideia perante ao gerenciador de discos do OpenSUSE, que me pareceu meio confuso. No fim das contas é saudável fazer uma instalação limpa.  
Com o disco livre do medo de perder arquivos, pude criar nova tabela de partições livremente, ajustando o tamanho adequado pra partição montada como /, raiz do sistema, como 15GB. O resto do espaço ficou pra arquivos da partição /home, tive problemas de armazenamento dos jogos do steam por causa do tamanho da partição raiz antiga, com 50GB. Relembrando que o disco tem apenas 160GB.  
O problema original no uso do OpenSUSE pra mim foi dual boot, o GRUB não reconhecia o Windows instalado (no mesmo disco, em outra partição, diga-se de passagem).  
Busquei tutoriais de dual boot com o OpenSUSE Leap e Windows 10, exatamente como eu queria, descobri que precisava montar a partição EFI do Windows, reprentada pelo famoso Windows Boot Manager, no ponto de montagem /boot/efi, durante o processo de instalação. 
Verificando os discos e seus pontos de montagem com <code>lsblk</code> ainda no Ubuntu, reparei que a partição /dev/sdb2 estava montada em /boot/efi, ué? Mas o Ubuntu já faz isso por padrão. Detalhe que não vem ao caso.  
Caso queira ver o tutorial, cujo processo tem como única diferença a instalação tradicional individual o ponto de montagem de /boot/efi/, [pode clicar aqui](https://tweakhound.com/2015/11/04/dual-boot-opensuse-leap-and-windows-10-uefi/).  


### 1-click Install ###  
Após a instalação, usei o site do OpenSUSE e o 1-Click install para instalar Steam, Opera e alguns outros pacotes, grande maioria sem problemas.  Mas cometi o erro de ativar o repositório Packman.  
Posso falar? 1-click Install é SENSACIONAL, buscar seus programas graficamente usando o navegador (e não um cliente pesado lerdo e ineficiente, alô Ubuntu Software Center), instalá-los com dois cliques, tudo automático e adicionando o repositório pra você, nossa. É algo que não se vê com frequência no Linux.  
Perfeito? não, ele pode instalar pacotes instáveis, repos que possam prover atualizações de pacotes ruins, enfim, todos os riscos de pacotes de fora do repositório (por mais que se um pacote tiver no repositório, poderá ser baixado por lá também, com um botão diferenciado, maior e com destaque), além de que no Opera, tenho que salvar o arquivo ymp e abrir manualmente pro serviço funcionar, então não é literalmente em dois cliques. No Firefox ele funciona 100%, basta clicar que ele abre a tela pra instalar o programa.  

Voltando ao Packman, o que é isso?  Um repositório não oficial, feito pela comunidade, geralmente conta com pacotes em versões mais recentes (e instáveis) compilados pelos usuários, como eu e você. Bem, tudo certo na teoria, instalei o VLC por lá, não abria nem com reza braba. Tive que desativar o repo, remover todos os pacotes do VLC até então instalados (incluso bibliotecas que não apareciam na busca pelo pacote principal) e reinstalar usando o repositório oficial, que por acaso já contava com a mesma versão do repositório Packman. Tudo bonito tudo certo. Deixei pra usar o Packman pra pacotes que realmente precisasse e que não havia no repo oficial. Creio que pacotes oriundos do 1-click Install venham de repos diferentes dos oficiais, ou no mínimo variantes ou subdivisões dos oficiais. Como um repositório multimídia com pacotes de codecs e afins. Mas até então sem problemas que devam ser citados. 

### Plugin Flash ###  
Ah, o velho problema do Linux.  
O método até então comum pra solucionar o fato de a Adobe ter abandonado o suporte ao flash no Linux na versão 11 ([Anúncio oficial](http://blogs.adobe.com/flashplayer/2012/02/adobe-and-google-partnering-for-flash-player-on-linux.html)), era a instalação do PepperFlash, plugin embutido no Google Chrome, que teoricamente era a única opção de ter o flash atualizado e funcionando no Linux.  
[Através de um instalador](https://wiki.debian.org/PepperFlashPlayer), baixava-se o pacote deb do Chrome, extraía o arquivo para uma pasta onde o plugin seria usado pelos navegadores compatíveis, normalmente o Chromium, Opera ou browsers com suporte a plugins PPAPI, a versão mais atual de plugins de navegador. Até certo momento, o Firefox ficava órfão de plugin flash, pois usa o padrão NPAPI, formato do velho Netscape e que havia sendo usado por longos anos antes do PPAPI chegar e ser adotado em larga escala (parte da responsabilidade da adoção desse novo padrão é creditado ao Google Chrome), apesar disso, foi uma mudança bem vinda, já que PPAPI é mais moderno, seguro e estável que NPAPI.  
Porém criaram uma ponte entre o plugin PPAPI e o Firefox, o [Fresh Player](http://www.webupd8.org/2014/05/fresh-player-plugin-pepper-flash.html), assim você poderia instalar o PepperFlash e ter o plugin funcionando no Firefox.   
Eu usava essa solução no Ubuntu. 
Mas o jogo virou não é mesmo??  Ao mesmo tempo que o Google Chrome deixou de permitir o plugin em um arquivo individual, deixando ele embutido no navegador e inacessível a gambiarra feita pra usá-lo em outros browsers.   Não é mais possível baixar o pacote do Chrome, extrair o plugin e apagar o resto ([fonte](http://askubuntu.com/questions/836261/pepperflashplugin-nonfree-package-installation-fails-since-chrome-54-is-out-oct)).  
E AGORA?  
Agora, meu amigo, a Adobe deu pra trás e voltou a fazer o plugin flash pra Linux, inicialmente apenas PPAPI, mas também passou a suportar plugin NPAPI, provendo, de quebra, instaladores RPM e DEB, além de TAR.GZ.  
[Você pode baixar os pacotes aqui](http://labs.adobe.com/downloads/flashplayer.html).   

Fique atento pra baixar o pacote mais adequado pro navegador e sistema operacional que você usa.  
Pacotes DEB funcionam pra Ubuntu, Debian, Elementary, Mint e derivados.  
Pacotes RPM servem pra Fedora, CentOS, Red Hat, OpenSUSE (meu caso) e derivados.  
Pra poder instalar o jekyll e testar a sintaxe deste exato texto no site, precisei instalar o ruby-devel e ruby2.1-rubygem-ffi, apenas gem install jekyll não funcionou.  
