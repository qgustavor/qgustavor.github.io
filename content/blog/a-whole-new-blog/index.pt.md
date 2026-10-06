---
title: Um admirável blog novo!
date: 2026-10-05T20:32:00
description: ''
tags: []
---

Decidi resetar meu blog do zero! Tudo começou porque [eu fui comentar que é fácil abrir um blog no GitHub Pages](https://ursal.zone/@gustavo/117372789749280829) enquanto o meu estava abandonado. Então decidi arrumar o meu: joguei tudo que tinha fora e agora é um blog completamente novo.

Esse blog começou lá no Tumblr. Era uma época simples: dava para postar imagem, agendar postagem, era simples, mas funcionava. Só que era terrível também, aquele editor de postagens do Tumblr era terrível, e eu não tinha muito controle também.

Aí migrei para o GitHub Pages usando Jekyll. No início eu postava escrevendo Markdown, mas não durou umas cinco ou sete postagens, fiz um script que me permitia escrever no Google Docs e ele postava usando uma tarefa agendada. Nessa época eu tinha um plano de postar todo dia, e eu escrevia sobre os animes que eu assistia. Na verdade, eu só queria ganhar um _achievement_ de dar _commit_ no GitHub todo dia.

Só que eu não gostava de uma coisa: tinha vez que eu escrevia uma coisa no Google Docs e quando aparecia no site, tinha algum bug causado pela conversão Google Docs→Markdown. Aí eu resolvi migrar o site para Wordpress, mantendo a hospedagem no GitHub Pages. Tem plugin para isso (WP2Static, Simply Static) mas não presta, aí eu acabei usando o HTTrack e um script para arrumar os problemas que apareciam (tirar o wp_json, wp_admin e outras coisas do código).

Durou um tempinho dessa forma, mas achei um tanto enjoado: não conseguia editar postagens no celular de jeito nenhum (o aplicativo do Wordpress não conectava à minha instância local de jeito nenhum) e era muito lento. Daí eu pensei em partir para uma solução mais robusta:

Pensei: se o blog fosse gerado em JavaScript, eu poderia ter o mesmo código que roda na geração do blog no editor, assim eu posso ter um editor que é fiel à forma que as postagens irão aparecer no blog. Além disso, posso já implementar um blog multi-língue e postar em inglês também. Só que foi mais complicado do que pareceu: tentei usar Nuxt, fiz um site beeem simples, e abandonei. Não tive tempo para fazer um editor específico para o meu caso e nem terminar de arrumar o layout.

Agora estou usando Hugo e Sveltia CMS. O Hugo é rápido e, diferente dos outros, já tem suporte nativo a blogs com mais de uma língua. Encontrei um tema bom e que foi fácil de deixar de um jeito que eu me agrade e dá para eu melhorar no futuro. Estou usando o Sveltia CMS para escrever essa postagem e é bem prático: não precisa de conta no Netlify, aliás, melhor que isso, ele permite editar o blog sem mexer em conta nenhuma, é muito bom.

A única coisa que acabo sentindo falta é que não tenho como ver a postagem no blog em tempo real que nem era no Wordpress, nem tenho os blocos para deixar imagens alinhadas à esquerda ou direita ou até na tela inteira. Mas, antes ter algo mais simples do que abandonar de novo.

E é isso, um admirável blog novo! Quem pegou a referência, saiba, na postagem em inglês a referência é de outra música. E isso é o legal de blogs multi-língue: não é uma tradução de máquina de uma língua para outra, eu dou meus toques aqui e ali.
