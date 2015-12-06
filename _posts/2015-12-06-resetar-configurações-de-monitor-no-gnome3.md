---
layout: post
title: "Resetar configurações de monitor no GNOME3"
date: 2015-12-06 02:21:01
image: '/assets/img/'
description:
tags: Linux GNOME Resolvido xrandr
categories:
twitter_text:
---

# Resetar configurações de monitor no GNOME3

### Como estava antes?
Uso dois monitores, configurados pra espelhar a imagem. Devido a uma falha  no monitor principal do notebook que não tem contraste e tem a tela muito clara, uso ele basicamente como um desktop. 

### O que fiz pra dar problema?
A alguns dias, pra economizar energia, decidi desligar o monitor principal, mas notei que havia outro disponível.  
Executei o comando <code>xrandr</code> e vi que aquela terceira saída de vídeo é equivalente a saída de TV, pelo conector S-Video (o notebook é tão velho que tem uma entrada FireWire, de quebra, defasada). Por algum motivo o sistema reconhecia a saída S-Video como se estivesse ligada, porém desativada. Tentei ativá-la pra ver o que daria, besteira tava feita.  

### Qual o problema?
Ambos os monitores alternavam entre resoluções repetidamente, ambos pretos, sem o mouse passar entre eles.

### O problema é isolado ou localizado a algum programa?
O problema acontecia apenas no GNOME, tenho OpenBox instalado e experimentei abrí-lo, tudo funcionando na mais perfeita harmonia, monitores espelhados, pois aparentemente o OpenBox usa as configurações automáticas do XRandr.  
Percebi que a configuração errada era localizada apenas no meu usuário padrão, e apenas no GNOME. 
Descobri isso quando loguei no GNOME com usuário root e logando no meu usuário normal no OpenBox, ambos funcionando bem.

### Como poderia resolver o problema?

Precisava encontrar onde estava o bendido arquivo de configuração que guardava as alterações feitas no programa Telas, do GNOME

## Agora vou descrever o processo que me levou a descobrir a solução, se não quiser ler tudo, vá direto pra solução, lá embaixo, tá?

Mexendo no GNOME com usuário root, notei que no DConf, gerenciador de configurações avançadas do GNOME, similar ao Regedit do Windows, seguindo o caminho: <code> Org>Gnome>Settings-daemon>Plugins>xrandr</code>,
que o arquivo de configuração de monitor da interface gráfica estava localizado no XML:  
<code>/etc/gnome-settings-daemon/xrandr/monitors.xml</code>  
Também descobri que cada opção de configuração do GNOME, como Rede ou Privacidade, é um plugin, e que o plugin de configurar o Display no GNOME é relacionado ao XRandr.  
Ótimo, já tenho onde procurar, mas a pasta <code>/etc/gnome-settings-daemon</code> nem existia :/  
Com um LOCATE, procurei por "settings-daemon", filtrando o resultado pra exibir apenas o que estivesse dentro da pasta "/etc/", que me interessava  
<code>locate settings-daemon | grep /etc/</code>  
o programa locate serve pra consultar uma base de dados contendo o nome e caminho de todos os arquivos em seu disco. Pra atualizar a base de dados antes de fazer a busca, digite "updatedb" com usuário root, ou sudo, assim:  
<code>sudo updatedb</code>  
Infelizmente a busca retornou apenas o caminho da pasta de configurações do MATE, que tinha instalado no computador a algum tempo.  
<code>/etc/mate-settings-daemon  
/etc/mate-settings-daemon/xrandr  
/etc/mate-settings-daemon/xrandr/monitors.xml</code>  
Tentei criar a pasta /etc/gnome-settings-daemon/xrandr/ e copiar o arquivo monitors.xml pra ela, depois de reiniciar o sistema não houve efeito. :(  
Mas o Linux tem dois locais pra procurar arquivos de configuração por padrão, a pasta /etc/ e a pasta .config, na minha pasta de usuário, sempre dando prioridade pra minha pasta de usuário.  
Por esse motivo, permite ter vários usuários no sistema e cada um manter a maioria das configurações de seus programas de forma independente, no caso de não haver um arquivo de configuração na pasta de usuário, costumeiramente o programa verifica na pasta /etc/, em alguns casos, copia a configuração de /etc/ pra pasta de usuário, como um modelo, e permitindo que aquele usuário use o programa e salve as alterações na sua cópia do arquivo recém criada, sem precisar mexer no arquivo-mestre em /etc/, que apenas o usuário root pode alterar

## Solução do problema
Entrei na minha pasta de usuário, depois na pasta .config, lá estava o bendido arquivo monitors.xml, que continha as configurações problemáticas dos meus monitores, simplesmente o apaguei e reiniciei o sistema.  
Quer um meio mais fácil? Execute o comando abaixo:  
<code>mv ~/.config/monitors.xml ~/.config/monitors.xml.old</code>  
Caso você seja alguém cauteloso ou não sabe se a configuração antiga pode ser refeita manualmente, é sensato criar uma cópia deste arquivo em outra pasta ou renomeá-lo para "monitors.xml.old" na mesma pasta, usando qualquer outro nome que o lembre pra que aquele arquivo serve, claro.  
O comando acima faz exatamente isso, não apaga, apenas renomeia o arquivo, permitindo que outro seja criado pelo sistema, mas sem perder o anterior.  
Depois de reiniciar o sistema, o GNOME retornou as configurações padrão de monitor, ou seja, ambos espelhados e ambos ligados, como antes.  


Uso Debian 8 x86_64  
GNOME 3.14.0