---
layout: post
title: "Plugin Flash Player no Linux, parece que o jogo virou"
date: 2016-11-16 01:46:09
image: '/assets/img/'
description:
tags: Linux Resolvido
categories:
twitter_text:
---  
Ah, o velho problema do Linux.
O método até então comum pra solucionar o fato de a Adobe ter abandonado o suporte ao flash no Linux na versão 11 ([Anúncio oficial](http://blogs.adobe.com/flashplayer/2012/02/adobe-and-google-partnering-for-flash-player-on-linux.html)), era a instalação do PepperFlash, plugin embutido no Google Chrome, que teoricamente era a única opção de ter o flash atualizado e funcionando no Linux.
[Através de um instalador](https://wiki.debian.org/PepperFlashPlayer), baixava-se o pacote deb do Chrome, extraía o arquivo para uma pasta onde o plugin seria usado pelos navegadores compatíveis, normalmente o Chromium, Opera ou browsers com suporte a plugins PPAPI, a versão mais atual da API de plugins de navegador (quer saber mais sobre elas? [leia aqui](http://superuser.com/questions/654595/adobe-flash-player-ppapi-vs-npapi-in-google-chrome). Até certo momento, o Firefox ficava órfão de plugin flash, pois usa o padrão NPAPI, formato do velho Netscape e que havia sendo usado por longos anos antes do PPAPI chegar e ser adotado em larga escala (parte da responsabilidade da adoção desse novo padrão é creditado ao Google Chrome), apesar disso, foi uma mudança bem vinda, já que PPAPI é mais moderno, seguro e estável que NPAPI.  
O plugin flash oriundo do Google Chrome com o padrão PPAPI foi batizado de PepperFlash.  
Porém criaram uma ponte entre o plugin PPAPI e o Firefox, o [Fresh Player](http://www.webupd8.org/2014/05/fresh-player-plugin-pepper-flash.html), assim você poderia instalar o PepperFlash e ter o plugin funcionando no Firefox.
Eu usava essa solução no Ubuntu.
Mas o jogo virou não é mesmo??  Ao mesmo tempo que o Google Chrome deixou de permitir o plugin em um arquivo individual, deixando ele embutido no navegador e inacessível a gambiarra feita pra
usá-lo em outros browsers.   Não é mais possível baixar o pacote do Chrome, extrair o plugin e apagar o resto ([fonte](http://askubuntu.com/questions/836261/pepperflashplugin-nonfree-package-installation-fails-since-chrome-54-is-out-oct)).
E AGORA?       
Agora, meu amigo, a Adobe deu pra trás e voltou a fazer o plugin flash pra Linux, inicialmente apenas PPAPI, mas também passou a suportar plugin NPAPI, provendo, de quebra, instaladores RPM e DEB, além de TAR.GZ.      
[Você pode baixar os pacotes aqui](http://labs.adobe.com/downloads/flashplayer.html).

Antes de ficar perdido no meio de tantas opções, vou ajudar a escolher o pacote certo.  
Você precisará de algumas informações do seu sistema.   
* Arquitetura  
* Navegador a usar o plugin  
* Pacote usado pela sua distro  

Digite <code>uname -m</code> no terminal pra saber a arquitetura, se a resposta ao comando for x86_64, o sistema é 64bits, se for i386 ou i686, é 32bits.  
  

Navegador não tem mistério, se precisa instalar o plugin pro Firefox e derivados, como Iceweasel, Waterfox, etc. Baixe o plugin NPAPI.  
Se usa Chrome, Opera, Chromium, Vivaldi, Epiphany, escolha plugin PPAPI. Costumeiramente navegadores que usam como base o WebKit, costumam usar plugins desse padrão.  
Apesar do Google Chrome (e seus derivados diretos, como Chromium) terem desabilitado o suporte a plugins NPAPI, outros browsers que usam WebKit podem suportar o NPAPI normalmente. Verifique antes.    
Distro é fácil também. Como distribuições Linux mais comuns e usadas são baseadas no Debian, como Ubuntu, Mint, Elementary. Usam os pacotes em formato DEB, baixe esse.  
Se usa Fedora, OpenSUSE, Red Hat, Mandriva/OpenMandriva, e derivados, pegue o pacote RPM.  
Ou pode baixar o pacote TAR.GZ com os arquivos necessários sem distinção de distribuição, funciona bem pra Slackware, Arch, e demais distros que não usam nem RPM nem DEB, contando com instalação manual do plugin ou scripts próprios pra extração e instalação do pacote, trabalho feito pelos contribuidores da distro e não pela Adobe.  

Eu no momento to usando OpenSUSE, arquitetura 64bits. Quer dizer que preciso baixar o pacote RPM, 64bits.  

Esses passos são necessários até o momento que alguma boa alma crie repositórios que façam todo esse trabalho (incluso a parte do Download) e instale o plugin na sua distro sem muito esforço.  Como esse plugin ainda é novidade, por enquanto não há nada disso. Tal qual o velho flashplugin-installer fazia (e ainda faz né) normalmente.  


Relembrando que este plugin trata-se de um beta, por causa disso ele tem versão superior ao plugin tradicional usado tanto no Chrome pra Linux como o plugin pra Windows e OS X.  
"Yay que ótimo!", calma lá, beta significa que ainda está sendo testado, pode ter reação inesperada ou bugs, leia-se "pode" como vai, eventualmente, mesmo que seus bugs não influenciem no comportamento evidente. Tenha cuidado ao usá-lo em serviços e sites que demandem gastos ou algo muito importante, você foi avisado!.  
Como no momento a única coisa que preciso usar flash é o player de gifs do facebook, e como só tive problemas nele com o Opera (aparentemente já foi resolvido) então tudo certo.  

Falando em Opera...   
### Novo Plugin Flash no Opera ###   

Ué mais problemas? É só mais umzinho. O plugin instalado por pacote manda o arquivo pra uma pasta específica, que no caso do PPAPI, pacote RPM em sistema 64bits, vai pra <code>/usr/lib64/flash-plugin/libpepflashplayer.so</code>, mas o Opera procura plugin no próprio diretório (<code>/usr/lib64/opera/plugins/</code>.  
E agora? Agora você pode criar um link simbólico [aqui o Guia Foca falando sobre ele](http://www.guiafoca.org/cgs/guia/iniciante/ch-cmdv.html) usando o comando seguinte:  
<code>sudo ln -s /usr/lib64/flash-plugin/libpepflashplayer.so /usr/lib64/opera/plugins/libpepflashplayer.so</code> Esse comando funciona pra sistemas 64bits, caso use 32bits simplesmente mude o diretório de /usr/lib64/ pra /usr/lib/, assim:  
<code>sudo ln -s /usr/lib/flash-plugin/libpepflashplayer.so /usr/lib/opera/plugins/libpepflashplayer.so</code>   

Caso utilize o Chromium e tem o pacote PepperFlash instalado (seja anteriormente ao problema do Chrome não incluir mais o arquivo de plugin ou hoje em dia mesmo), basta criar o link pro diretório do PepperFlash e mandar o plugin pra lá que ele será reconhecido pelo Opera, dois coelhos com uma cajadada só (sempre quis usar essa expressão).  
<code>/usr/lib64/chromium/PepperFlash/</code>

Pode testar se o plugin tá funcionando, abra e feche o browser, e veja se foi reconhecido digitando <code>about:plugins </code> na barra de endereços.  

![Imagem](http://i.imgur.com/GYc1VGL.jpg)  
Verá algo similar a isso na lista de plugins.  

Não tá satisfeito ainda? Abra o [teste padrão da Adobe ](https://www.adobe.com/br/software/flash/about/).  
![teste da adobe](http://i.imgur.com/c1isZVo.png) 


## Onde meu browser procura os plugins no Linux? ##  
Poxa, o que você indicou não deu certo, o que eu faço?  
Vamos ver o jeito difícil.  


Creio que seja um consenso, que a pasta "plugins" dentro da pasta padrão do browser, possa carregar os plugins pra ele.  
Exemplo: /usr/lib/netscape/plugins  
ou C:\Program Files(x86)\Mozilla Firefox\plugins 
por aí vai.     
### Navegadores que tem como base o Gecko: ###   
[Segundo este documento](https://developer.mozilla.org/en-US/docs/Plugins/Guide/Plug-in_Basics#How_Gecko_Finds_Plug-ins), navegadores que usam Gecko, do qual o Firefox está incluso, encontram seus plugins nas pastas:  
<code>~/.mozilla/plugins</code><br>
<code>/usr/lib/mozilla/plugins</code><br>
<code>/usr/lib64/mozilla/plugins</code><br>  
Acrescendo a pasta <code>/usr/lib64/browser-plugins</code> por experiência própria.  
Quais são os navegadores que usam Gecko? 
Aqui tem uma [boa lista](https://en.wikipedia.org/wiki/List_of_web_browsers#Gecko-based).  

### Navegadores que tem como base o WebKit:###  
A quantidade de browsers que usam WebKit como engine é abundante. Não cabe a mim abordar cada um individualmente, e levando em conta que muitos deles suportam tanto o NPAPI e PPAPI, a lista de pastas onde buscam plugins seria imensa. Então leve em conta as pastas de plugins padrão do Gecko, somando as pastas do qual o PepperFlash é instalado, após extração do Chrome (que no momento é malsucedida).  
Quer uma listinha dos browsers que usam WebKit? [TOMA](https://en.wikipedia.org/wiki/List_of_web_browsers#WebKit-based).  

O PepperFlash foi inicialmente um plugin pra ser usado pelo Chromium, criando uma alternativa substitutiva ao Google Chrome, então vamos ter como base o diretório dele, dependendo de como sua distro nomeia o pacote do programa:  
<code>/usr/lib64/chromium-browser/PepperFlash</code>
<code>/usr/lib64/chromium/PepperFlash</code>  
Agora uma lista oficial do engine WebKit [fonte](http://stackoverflow.com/questions/10208392/how-does-webkit-find-libflashplayer-so): 
Pra mim é evidente que a lista inclui o suporte a plugin NPAPI.   
*  <code>$MOZ_PLUGIN_PATH</code><br>
*  <code>$MOZILLA_HOME/plugins</code><br>
*  <code>$HOME/.mozilla/plugins</code><br>
*  <code>$HOME/.netscape/plugins</code><br>
*  <code>/usr/lib/browser/plugins</code><br>
*  <code>/usr/local/lib/mozilla/plugins</code><br>
*  <code>/usr/lib/firefox/plugins</code><br>
*  <code>/usr/lib64/browser-plugins</code><br>
*  <code>/usr/lib/browser-plugins</code><br>
*  <code>/usr/lib/mozilla/plugins</code><br>
*  <code>/usr/local/netscape/plugins</code><br>
*  <code>/opt/mozilla/plugins</code><br>
*  <code>/opt/mozilla/lib/plugins</code><br>
*  <code>/opt/netscape/plugins</code><br>
*  <code>/opt/netscape/communicator/plugins</code><br>
*  <code>/usr/lib/netscape/plugins</code><br>
*  <code>/usr/lib/netscape/plugins-libc5</code><br>
*  <code>/usr/lib/netscape/plugins-libc6</code><br>
*  <code>/usr/lib64/netscape/plugins</code><br>
*  <code>/usr/lib64/mozilla/plugins</code><br>
*  <code>/usr/lib/nsbrowser/plugins</code><br>
*  <code>/usr/lib64/nsbrowser/plugins</code><br>


O [site do Opera](http://www.opera.com/docs/linux/plugins/install/#flash) diz que o local onde ele busca o plugin é apenas no:  
<code>/usr/lib64/opera/plugins</code>  
A partir de testes, vi que o Opera busca plugins também no diretório:  
<code>/usr/lib64/chromium/PepperFlash</code>   
Caso você use Ubuntu, a pasta padrão do Chromium será <code>/usr/lib64/chromium-browser/PepperFlash</code> ou <code>/usr/lib64/chromium-browser/plugins/</code>  
Acredito que ele também busque em:  
<code>/usr/lib64/flashplugin-installer</code>   
Mas evitei instalar esse pacote pra não desconfigurar os plugins já instalados. 
Ou seja, você pode instalar o PepperFlash, e posteriormente criar um link simbólico pro plugin da Adobe no lugar do PepperFlash do instalador.  

Significa que em qualquer dessas pastas que você puser o arquivo de plugin ou um link simbólico dele, seu navegador enxergará e poderá usar o bendito Flash Player.  

Ah, só pra constar, concentrei tudo no flash, mas isso funciona pra absolutamente qualquer plugin de browser viu? Desde que obedeça as versões do plugin pra NPAPI ou pra PPAPI.    
 
