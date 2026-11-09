---
title: Algumas reflexões sobre o estado atual das runtimes de JavaScript
date: 2026-11-09T13:48:00
description: Gustavo desabafa sobre o estado das runtimes de JavaScript
---

Desde o início de 2026 tenho tentado trabalhar no [adorai](https://adorai.neocities.org). Dito isso, é uma bagunça: a lógica principal vive em um arquivo .js gigante, então preciso modularizá-lo para poder continuar desenvolvendo de maneira sã. Portanto, criei uma nova pasta para este projeto chamada "vite-project" e fui em [vite.dev](https://vite.dev/) verificar qual é a forma atual de iniciar um projeto Vite. Então, me peguei com um dilema: *qual runtime usar?*

Bem, quais runtimes eu costumo usar para meus projetos? Node.js, Deno e Bun. Então, o que devo usar? O Node.js é antigo, então talvez deva considerar outra coisa? O Bun funciona, mas é feito de qualquer jeito (o mantenedor deles enviou recentemente uma enorme PR mudando muitos e muitos arquivos, reescrevendo quase tudo). O Deno vai parar de ser mantido após outubro de 2027, mas talvez existam forks...

Então verifiquei o GitHub do Deno e encontrei [esta discussão](https://github.com/denoland/deno/issues/37030) e encontrei uma reclamação estranha (mas interessante) sobre o Deno: *foi um erro torná-lo compatível com o Node.js?* Um dos comentários até comentou sobre [o fork deles do Deno](https://ende.sh/) sem compatibilidade com Node.js (sobre o qual comentarei mais tarde).

Essa questão me irrita. Claro, talvez o grande problema com o Deno tenha sido tentar torná-lo compatível com o Node.js. Assim, por um lado, se o Deno é compatível com o Node.js, as pessoas podem substituir o Node.js pelo Deno e obter os recursos que o Node.js não tem, é uma coisa boa, não? Bem, ajuda a atrair usuários, mas por que as pessoas desenvolveriam ferramentas e bibliotecas para o Deno? *Basta desenvolver para o Node.js e o Deno será compatível.*

Então o maior problema disso é que prejudica a cultura de desenvolvimento FOSS em torno do JavaScript: se o Node.js fornece algo mais fácil de implementar do que um padrão web, então os desenvolvedores de bibliotecas só se importariam em apoiar padrões se quisessem por causa de suas próprias crenças. Exemplo: o MEGAJS tem uma versão especificamente para Node.js porque sua implementação de criptografia suporta streaming e o Web Crypto não (até o momento da escrita), então as versões não-Node precisam implementar criptografia no espaço do usuário, em puro JS, o que, para ser justo, eu não gosto (é arriscado demais).

Além disso, quando o Deno 2 foi lançado, a versão que introduziu a maioria das alterações de compatibilidade com o Node.js, ele acabou quebrando projetos do Deno 1 que assumiam que um package.json próximo aos scripts seria ignorado. Tive que adicionar `--no-config` a muitos e muitos scripts meus por causa disso. No Deno 1, você podia importar bibliotecas npm usando o especificador `npm:`, mas ao migrar para o Deno 2, ele tenta usar um package.json próximo para resolver pacotes npm. Uma *breaking change* repentina!

Então, claro, o Ende remove isso, sem especificador `npm:`, sem os built-ins de `node:`, mas por quê? Como mencionei antes, os desenvolvedores de bibliotecas não têm muitos incentivos para migrar seu código para usar padrões web em vez de built-ins do Node.js, não é como se as pessoas fossem escrever bibliotecas JSR de repente só porque um único runtime decidiu retornar aos ideais originais do Deno de apoiar os padrões abertos da web. Sem mencionar que o desenvolvimento desse runtime foi tão rápido que só se pode assumir que foi acelerado por IA (o que parece ser verdade, a partir do arquivo `agents.md` no repositório de documentação) sem a devida supervisão humana, o que é perigoso para caramba.

---

Bem, antes deste evento "Cloudflare comprou o Deno", eu classificaria esses três runtimes da seguinte forma:

- Node.js: use quando quiser se sentir seguro, quiser algo testado "em batalha" ao longo dos anos.
- Deno: use se quiser compartilhar scripts independentes. Não, o sistema de permissões não merece sua atenção.
- Bun: se você quiser distribuir seu código como arquivos executáveis independentes, ou apenas quiser um runtime mais rápido, e não tiver medo de código cagado por IA.

Mas agora eu não recomendaria o Deno — nem os forks do Deno — para isso. E é uma pena! É uma pena porque me lembra de outro grande problema das plataformas atuais: o travamento em torno da Microsoft.

Veja, a Microsoft comprou o GitHub e o NPM, e recentemente eles têm enviado atualizações disfarçadas de "atualizações de segurança" que tornaram o NPM mais difícil de usar sem o GitHub e/ou outras ferramentas aprovadas. Eles anunciaram que tornarão mais difícil a importação de módulos de CDNs HTTPS (que é como o SheetJS CE recomenda a instalação) alegando que são menos seguros. Tudo isso leva apenas a um aprisionamento de plataforma. Isso machuca a comunidade.

Se você não pode usar HTTPS como alternativa ao NPM e hospedar seus pacotes você mesmo, qual é a alternativa? JSR? Talvez, mas as regras do JSR são muito mais restritivas do que as do NPM. Não consigo publicar o megajs no JSR devido aos seus requisitos, principalmente o que você não pode publicar módulos CommonJS. O JSR não é um registro de pacotes para JavaScript, é um registro de pacotes para runtimes JavaScript para servidores que suportam ESM. Exigir ESM significa para mim que eu não poderia mais dar suporte a duas versões legadas do megajs (ou eu teria que hospedá-las em outro lugar). Claro, a próxima versão do megajs será apenas ESM, mas não é uma escolha fácil para os desenvolvedores de bibliotecas pararem de dar suporte às coisas só porque o registro deles não permite. Veja, as pessoas preferem rehospedar o SheetJS CE no NPM em vez de cumprir a regra de "use nossa CDN, por favor", isso quebra o fluxo de trabalho das pessoas, por mais irritante que seja.

---

Então, em conclusão, estou irritado e boto não tenho grandes esperanças no JavaScript. Provavelmente usarei o Bun em vez do Node.js para o adorai, porque se as coisas piorarem para o Bun, posso simplesmente mudar para o Node.js e ele é mais rápido. Com certeza no futuro terei que aprender uma linguagem melhor para os servidores de meus projetos, talvez Rust ou Go, não sei.
