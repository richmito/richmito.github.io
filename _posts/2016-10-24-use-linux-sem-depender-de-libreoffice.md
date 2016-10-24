---
layout: post
title: "use Linux sem depender de LibreOffice"
date: 2016-10-24 13:17:12
image: '/assets/img/'
description:
tags:
categories:
twitter_text:
---  
# Instale o Office 2007 no Linux funcionando perfeitamente #  
Aos macacos velhos do Linux, sim, usarei Wine, mas no fim ainda deixarei uma segunda opção de bônus.  

Provavelmente veio aqui pois não quer ser obrigado a utilizá-lo, usando de sua liberdade de usar algo não livre.  
"Ah mas usa linux pra quê se vai enxer de programa do Windows?" Essa é outra discussão. Acima de tudo, sistema operacional é uma ferramenta, se ela não atende as necessidades do usuário, ele é ruim.  Assim como o Windows peca pelos programas fechados, que dificulta eu saber como funciona o sistema e, caso dê problema, dificulta encontrar a solução (aqueles processos consumindo processador e RAM e tendo nome de apenas *System* me deixam bastante puto). To usando de toda minha força de vontade pra não seguir falando disso o resto do texto. Vamos prosseguir.  

## LibreOffice é ruim? Não seria o suficiente pro usuário médio? ##  
Mas é claro que não, LibreOffice é uma suite completa para a grande maioria, senão todos, os recursos que um usuário comum necessita. PORÉM, sua interface e compatibilidade com os formatos proprietários da concorrência tornam-no a pedra no sapato seja de quem está começando agora ou quem usa Linux faz tempo.  

Você pode usar ambos simultâneamente, naturalmente, escolhendo o que lhe convém de acordo com a ocasião.  

## O que seu tutorial tem de diferente de tantos outros por aí? ##  
Na verdade, não muito, simplesmente é o meu jeitinho de instalar, que sei que funciona e que usei N vezes no trabalho ou em casa.  

## Qual sistema usará como base pro tutorial? e versões de software? ##  
Requisitos Mínimos:  
Ubuntu 14.04 ou superior (32 ou 64bits)  
Wine 1.6:i386 ou superior

Pode funcionar em outras versões? Sim, mas desde o Ubuntu 14.04 o Wine vem com versão adequada direto do repositório oficial, sem necessidade de PPAs ou outros repositórios externos. O objetivo é o mínimo de trabalho e downloads possíveis.  

É fundamental a instalação do wine na arquitetura de i386, wine 64bits não funciona com o Office 2007, que só tem versão 32bits.  
### Passos necessário caso você use sistema 64bits ###  
<br><br>Diz ao seu gerenciador de pacotes que você trabalhará com pacotes da arquitetura i386, também conhecido como 32bits <br>
<code>sudo dpkg --add-architecture i386</code>  <br>
<br>Atualista sua lista de pacotes, recebendo instruções pra tornar disponíveis também os pacotes 32bits  
<code>sudo apt update</code>  <br>
<br>Instala o pacote Wine, e suas dependências, na arquitetura 32bits e não na nativa, 64bits. Esse download pode ser relativamente grande, acima dos 100mb, se for o primeiro pacote 32bits que instala no seu sistema.

<code>sudo apt install wine:i386</code>  <br>

 
### Passos necessário caso você use sistema 32bits ###  
<br><code>sudo apt update</code><br>
<code>sudo apt install wine</code>


Pronto, se não houve erros, o wine está instalado certinho. Vamos preparar o disco/pasta do Office 2007.  
Você precisará saber navegar pelas pastas no terminal usando o comando <code>cd</code>. Caso não saiba, [aqui tem um ótimo tutorial](http://www.dltec.com.br/blog/linux/dicas-de-uso-para-o-comando-cd-do-linux/), dê uma olhada e depois volte aqui, ok?  

Deixe a pasta de instalação do Office em um local facilmente acessível, como sua pasta de Downloads ou próximo da sua pasta de usuário. Vamos supor que a pasta esteja em <code>~/Downloads/office2007/</code>. Lembrando que esse til significa o caminho da sua pasta de usuário, no caso, <code>/home/NOMEDEUSUARIO/Downloads/office2007</code>. Pra evitar ter que digitar seu nome de usuário, simplesmente usamos esse atalhoszinho do til.  

Crie um prefixo do Wine na pasta ~/.office2007/ usando o comando a seguir:  
<br><code> WINEARCH=win32 WINEPREFIX=~/.office2007 winecfg </code><br>
O que esse comando faz? Ele cria a pasta oculta .office2007 na sua pasta de usuário, e instala nela a base da virtualização do Wine. Se abrí-la verá que tem o "disco C", contendo a pasta Windows, a de Program Files, etc. Além disso, diz ao Wine "aqui use os arquivos pra rodar programas do Windows 32bits apenas", isso é necessário pro Office 2007, caso use Linux 64bits, mesmo usando 32bits não faz mal algum inserir esse comando.   
O prefixo serve pra isolar os programas do Wine em diferentes locais, evitando que as configurações de um programa influenciem em outro. Instalar o Office desta forma não vai mexer nos outros programas instalados com Wine no seu computador. Assim tudo funciona como esperado.  
A partir de agora os comandos do Wine que quisermos que funcionem pro Office 2007 terão de ter o prefixo dele.  
Ah, depois de rodar o comando, a janela do Winecfg será aberta, pode fechá-la.  

Hora de rodar o instalador do Office 2007.  
<br><code>  WINEPREFIX=~/.office2007 wine ~/Downloads/office2007/setup.exe </code><br> 
Na hora de inserir o serial ele pode dar uma pequena travada, mas fique tranquilo. Rode a instalação normalmente.  







[Fonte principal usada como base](https://wiki.archlinux.org/index.php/Microsoft_Office_2007)
[Fonte da solução do problema do PowerPoint](https://ubuntuforums.org/showthread.php?t=1632527)
 

