---
layout: post
title: "Programa para gravar imagens de disco em pendrive"
date: 2016-08-02 03:13:35
image: '/assets/img/'
description:
tags:
categories:
twitter_text:
---
  
# Tenho uma Imagem de disco para ser instalada em pendrive, o que faço?
Atente para o fato que estou recomendando programas específicos pra sistemas que necessitem da gravação direta de imagem para funcionar. Não é o caso do Ubuntu, que instala um gerenciador de boot no pendrive e simplesmente copia os arquivos necessários ao funcionamento para o pendrive.  

Alguns sistemas como OpenSUSE, Raspbian e Chromium OS, necessariamente precisam de gravação direta pra funcionar em mídias removíveis, como DVDs, pendrives e cartões de memória. 
## LiveUSB Install ##  
Cá está um programa tradicional pra instalação de sistemas em pendrives, serve pra gravação direta (como os demais daqui) e gravação via gerenciador de boot, como Ubuntu, Mint, Fedora, etc. Fiz questão de incluí-lo aqui por motivos de: é um ótimo programa! Um dos poucos com interface gráfica e listinha das distros compatíveis. O outro similar a esse, apesar de, na minha opinião, conter menos recursos, é o [Unetbootin](https://unetbootin.github.io/).  
Pra usar o LiveUSB Install, baixe os pacotes no [site oficial](http://live.learnfree.eu/en/). Usando Linux ou Windows, sim ele é multiplataforma.   


## SUSE Studio Image Writer ##  
Segundo a [wiki do OpenSUSE](https://pt.opensuse.org/SDB:Live_USB "Wiki do OpenSUSE"), caso use Windows, use o SUSE Studio Image Writer, o mesmo caso use OpenSUSE (o que não faz sentido caso seu objetivo seja instalar o sistema.)  

## USBWriter ##
Desta vez apenas pra Windows, tem o mesmo propósito e funcionalidade
[Aqui a descrição e como baixar](https://sourceforge.net/p/usbwriter/wiki/Documentation/)  

## dd ##  
Ferramenta que no fim das contas tem propósito similar, porém, possui uma gama de funções bem mais ampla. Permite copiar, gravar, criar arquivos de acordo com diferentes configurações. Vem incluso na grande maioria das distros Linux, mas pode ser usada no Windows e OS X também.   
Sua usabilidade é mais...detalhada, pra não usar a palavra "difícil". Grandes poderes vem com grandes responsabilidades, isso se aplica ao dd. 
A [Arch Wiki](https://wiki.archlinux.org/index.php/USB_flash_installation_media#In_GNU.2FLinux) contém instruções de como usá-lo.  

### Beleza, mas qual deles resolveu seu problema na hora de instalar o Chromium OS e o OpenSUSE? ##

Nenhum, amiguinho. Poderia ter resolvido? Claro, mas eu preferi usar um outro chamado Etcher.  

![Interface do Etcher](https://www.etcher.io/static/images/product.gif)


Por quê?  
Etcher é multiplataforma, simples de usar, valida a gravação pra evitar o uso de mídias corrompidas, e o grande diferencial: é portátil de verdade.  
Baixa o pacote (que, diga-se de passagem, é maior que o de costume pra programas Linux), marca como executável (passo que o sistema impõe pra evitar a execução acidental de programas maliciosos, meio inimaginável no Windows) e dá duplo clique. 
O melhor de tudo, já existem vários outros programas que possam funcionar da mesma forma, usando a ferramenta [AppImage](http://appimage.org).  
