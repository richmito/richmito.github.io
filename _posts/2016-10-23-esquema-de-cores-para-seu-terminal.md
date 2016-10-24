---
layout: post
title: "Esquema de cores para seu terminal"
date: 2016-10-23 21:52:13
image: '/assets/img/'
description:
tags:
categories:
twitter_text:
---  

# Torne seu terminal mais bonito com estes esquemas de cores  #
Já deve fazer um bom tempo que o terminal no monitor verde de fósforo deixou de ser realidade no dia-dia de quem costuma trabalhar usando console.  
Programadores, administradores de sistemas, analistas, ou quem quer que precise do terminal, deveria saber que syntax highlight (pode ser traduzido como realce de sintaxe) além de tornar mais produtivo, menos cansativo, torna o serviço esteticamente mais agradável.  
Realce de sintaxe se tornou algo fundamental com a quantidade de informações que temos que lidar. Sem ele nos perderíamos na selva de colchetes e parênteses no código. Tanto que a maioria, senão todos, os editores de código modernos contém de alguma forma realce. Cada um no seu estilo, e variando de acordo com a linguagem utilizada.  
Sempre impondo um padrão de cores, caso o usuário decida criar o seu próprio, pode fazer besteira e deixar o realce confuso ou até inutilizável. Aí entram as paletas de cores. Alguns se tornaram famosos, como o [Solarized](ethanschoonover.com/solarized
). Tão famosos que possui versões pros mais distintos editores, IDEs e terminais.  
Mas, até então, as paletas de cores serviam especificamente pros programas, como IDEs e editores. Muito lógico já que a larga maioria deles possui janela e interface próprias. Mas como ficam os programas que rodam diretamente no terminal?  
O editor Vim, no meu caso, foi o maior problema. Instalava bonitinho o tema pro Vim, funcionava perfeito na versão GTK (Vim-gnome), mas ao rodar a versão pura do console....as cores voltavam ao normal do padrão ou simplesmente ficavam confusas, trocadas.  

## Solução: [Base-16](https://github.com/chriskempson/base16) ##  
Projeto fundado pelo Chris Kempson, agora mantido também por 24 contribuidores, provê um repositório de esquemas de cores pra 23 editores ou emuladores de terminal. Incluindo o gnome-terminal e xfce4-terminal. Além de scripts pra instalação dos temas facilmente.  
No meu caso, que no momento to usando o gnome-terminal (apesar do xfce4-terminal ser o meu preferido), selecionei o meu terminal na lista "template repository", entrei no repo específico do meu terminal, baixei usando as instruções de instalação logo abaixo da lista de arquivos.   
Rode o script correspondente ao tema que prefere. 
Apesar de no site dizer que basta a instalação do script principal pros outros aparecerem na lista, não consegui, tive que instalar manualmente os que queria testar :c  
*Antes*![Antes](http://i.imgur.com/kaTR0ix.png)  
*Depois*![Depois](http://i.imgur.com/Vj6yNok.png)
