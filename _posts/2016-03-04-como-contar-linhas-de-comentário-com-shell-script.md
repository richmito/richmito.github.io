---
layout: post
title: "Como contar linhas de comentário com shell script"
date: 2016-03-04 00:09:33
image: '/assets/img/'
description:
tags:
categories: programação linux tutorial
twitter_text:
---
# Como contar linhas de comentário com shell script
Pra facilitar o aprendizado de python, sempre comento em qualquer código o que algumas partes fazem, de forma detalhada. O que o comando faz, por exemplo. No fim acabo com um código de verdade relativamente pequeno e muitas linhas de comentários.  
Isso é um problema? Não, mas em um determinado exercício, precisava comparar a quantidade de linhas de uma versão anterior do código e a atual, pra saber qual dos dois usava menos linhas com o mesmo resultado.  
Usar o próprio python pra isso seria trabalhoso, devido a eu estar no começo do aprendizado, decidi usar uma ferramenta que sempre tive a mão no sistema, e que muitas vezes se mostrou bastante poderosa: Shell Script.  

Primeiro, precisamos de um comando que exiba o conteúdo do arquivo contendo a fonte do programa, nisso há vários jeitos, aqui eu preferi usar o <code>cat</code>, o cat tem a função de concatenar arquivos e exibir seu conteúdo na saída padrão, que é a tela do terminal, mas esta saída pode ser direcionada pra outro comando ou para um arquivo também.  
a sintaxe do cat é a seguinte:  
<code>cat arquivo.txt</code>  

Agora podemos exibir no console o conteúdo do arquivo, precisamos filtrar pra mostrar apenas o que queremos.  

Com <code>grep</code>, que recebe informação de algo e filtra seguindo o conjunto de caracteres inseridos em seguida.  
Exemplo:  

<code>lspci | grep VGA</code>  
  
Eu uso este comando pra saber qual o nome das placa de vídeo instaladas :)  

Esta barra vertical <code>|</code> serve pra enviar a saída padrão do primeiro comando pra entrada padrão do comando seguinte, ao invés de exibí-lo na tela.  
o comando acima executa o programa <code>lspci</code>, que lista dispositivos conectados nos barramentos PCI do computador (Placa de vídeo, por exemplo), em seguida envia o resultado do comando, várias linhas de texto, pro <code>grep</code>, que filtra e exibe *apenas as linhas contendo os caracteres "VGA"*, respeitando maísculas e minúsculas.  

  
Com o grep em mãos, sei exibir na tela apenas as linhas com o caractere que representa os comentários na linguagem, no caso do python e do próprio shell script, este caractere é o <code>#</code>.  
  
Falta a última parte, um programa que conte as linhas exibidas na tela, que no nosso caso, são os comentários. Esse programa é o <code>wc</code>, sigla do inglês para Word Count, contar palavras. Serve pra contar número de linhas de um arquivo, entre outras funções.  
sua sintaxe é <code>wc -l arquivo.txt</code>  

<h2>TL;DR:</h2>  
Supondo que o nome do seu arquivo seja helloworld.py:  
<code>cat helloworld.py | grep # | wc -l</code>  
O resultado do comando é o número de linhas de comentários no arquivo helloworld.py.  
Pra saber o número total de linhas no arquivo, use o <code>wc -l helloworld.py</code>, depois só subtrair um de outro :)  


EDIT: o bróder [Davidson Mizael](https://github.com/davidsonmizael) pôs no mesmo comando de uma forma mais eficiente  
<code>cat helloworld.py | grep -v # | wc -l</code>  
ou  
<code>grep -v # helloworld.py | wc -l</code>  
Assim, com o parâmetro -v do grep, não é preciso subtrair depois  