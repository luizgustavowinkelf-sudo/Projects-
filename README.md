# Projects-

Coleção de projetos pequenos.

**Jogar online:** https://luizgustavowinkelf-sudo.github.io/Projects-/

## 🐔 [Wilson: A Galinha Voadora](wilson/)

Flappy Bird com uma galinha chamada Wilson — arquivo único, sem build.
Abra [`wilson/index.html`](wilson/index.html) no navegador e bata as asas com
`Espaço` ou tocando na tela. Funciona em tela cheia no celular, com botões de
pausa, som e tela cheia desenhados no próprio jogo, e tem placar das dez
melhores pontuações.

## Publicação

O site sai direto da `main` pelo GitHub Pages, sem workflow: em
**Settings → Pages**, com *Source: Deploy from a branch*, branch `main` e
pasta `/ (root)`. A partir daí o GitHub republica sozinho a cada push.

Ligar o Pages na primeira vez é um passo manual: a API de criação do site
exige permissão de administrador do repositório, que o token do Actions não
tem (`Resource not accessible by integration`).

Nesse endereço o placar fica guardado em cada aparelho, porque não há servidor
para gravar as pontuações — a versão com placar compartilhado é a publicada
como Artifact do Claude.
