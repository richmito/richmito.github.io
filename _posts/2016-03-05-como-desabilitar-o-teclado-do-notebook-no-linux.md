---
layout: post
title: "Como desabilitar o teclado do notebook no Linux"
date: 2016-03-05 20:33:53
image: '/assets/img/'
description:
tags:
categories:
twitter_text:
---

# Como desabilitar o teclado do notebook no Linux
Pra quem usa notebook como computador principal, em algum momento enfrentou problema com as partes embutidas nele.  
Touchpad, tela, teclado, superaquecimento, etc., no meu caso, foi o teclado que ganhou uns respingos de líquido e tinha pressionamento de teclas fantasmas. Problema bem grande na hora de usar pois o botão "home" traz ao topo de qualquer página, navegar na internet virou um inferno, fora problemas ao digitar senhas, por exemplo.  
Encontrei em um fórum os comandos pra desabilitar o teclado embutido no notebook através do <code>xinput</code>, o programa que recebe os periféricos de entrada do X, o servidor gráfico do Linux.  
Entre os periféricos de entrada estão controles, teclado, mouse, touchpad e demais sensores que o computador conta, como acelerômetro (para notebooks embutidos de sensor pro caso de queda acidental), entre outros.  

Comande o xinput pra listar os dispositivos conectados <code>xinput list</code>  
Aqui resultou nisso  
  
$ xinput list  
⎡ Virtual core pointer                    	id=2	[master pointer  (3)]   
⎜   ↳ Virtual core XTEST pointer              	id=4	[slave  pointer  (2)]  
⎜   ↳ USB Optical Mouse                       	id=12	[slave  pointer  (2)]  
⎜   ↳ PS/2 Logitech Wheel Mouse               	id=14	[slave  pointer  (2)]  
⎜   ↳ SIGMACHIP USB Keyboard                  	id=10	[slave  pointer  (2)]  
⎣ Virtual core keyboard                   	id=3	[master keyboard (2)]  
    ↳ Virtual core XTEST keyboard             	id=5	[slave  keyboard (3)]  
    ↳ Power Button                            	id=6	[slave  keyboard (3)]  
    ↳ Video Bus                               	id=7	[slave  keyboard (3)]  
    ↳ Power Button                            	id=8	[slave  keyboard (3)]  
    ↳ Sleep Button                            	id=9	[slave  keyboard (3)]  
    ↳ *AT Translated Set 2 keyboard            	**id=13**	[slave  keyboard (3)]*  
    ↳ SIGMACHIP USB Keyboard                  	id=11	[slave  keyboard (3)]  
    
A primeira lista indica dispositivos apontadores, como mouse, mesa digitalizadora e touchscreen, a segunda, os de teclado, como o teclado comum, de notebook e controles.
Essa parte provavelmente será diferente com cada pessoa, mas não demora muito a encontrar qual o teclado do notebook e qual seu USB, pelo nome, aqui é bem óbvio claro, pelo nome "USB" no segundo teclado, mas pode variar bastante.  
Identifique qual o teclado do seu notebook e guarde o número ID dele, nesse caso foi 13.  

Agora vamos desabilitar o dispositivo pelo número ID:  
<code>xinput float 13</code>  
Não é preciso permissão root pra isso.  
<h2>Desabilitei o teclado errado, e agora?</h2>  
<code>xinput reattach *id do dispositivo* *dispositivo mestre*</code>  
Como assim dispositivo mestre? Repare bem na saída do comando xinput list, os dispositivos de teclado são subordinados a um "teclado mestre". Nesse caso, o ID do teclado mestre é 3.  
<code>xinput reattach 13 3</code>  
Reatachei o dispositivo 13 (teclado do notebook) no dispositivo mestre 3, Virtual core Keyboard.  

<h2>Mas o teclado não funciona, como vou digitar os comandos?</h2>  
Reinicie o sistema que ele religa os dispositivos.  

Terá de fazer o processo toda vez que reiniciar o sistema, mas basta um pequeno script sendo iniciado junto do sistema que o processo fica automático.  
O procedimento funciona pra qualquer dispositivo reconhecido pelo xinput, também serve pra desabilitar um mouse deituoso ou o teclado, temporariamente.  


Fontes:  
[Manual do Xinput (em inglês)](http://www.x.org/archive/current/doc/man/man1/xinput.1.xhtml)  
[Ask Ubuntu - Is there a way to disable a laptop's internal keyboard?
](http://askubuntu.com/questions/160945/is-there-a-way-to-disable-a-laptops-internal-keyboard)  
