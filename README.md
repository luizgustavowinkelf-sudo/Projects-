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

O site é publicado pelo GitHub Pages a cada push na `main`, pelo workflow
[`.github/workflows/pages.yml`](.github/workflows/pages.yml). Ele liga o Pages
sozinho na primeira execução (`actions/configure-pages` com `enablement: true`),
então não é preciso configurar nada em Settings.

Nesse link o placar fica guardado em cada aparelho, porque não há servidor
para gravar as pontuações — a versão com placar compartilhado é a publicada
como Artifact do Claude.
