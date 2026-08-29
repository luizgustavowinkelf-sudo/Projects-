# Projects-

Coleção de projetos pequenos.

**Jogar online:** https://luizgustavowinkelf-sudo.github.io/Projects-/

Dois jogos com a galinha Wilson, cada um em **um arquivo HTML só** — sem
build, sem imagens, sem bibliotecas: cenário, personagem e som são gerados em
tempo de execução com Canvas 2D e Web Audio.

## 🪶 [Wilson: A Galinha Voadora](wilson/)

Flappy Bird de curral: bata as asas com `Espaço` ou tocando na tela, desvie
das cercas e pegue os ovos dourados. Tem placar das dez melhores pontuações.

## 🌊 [Lo Siento, Wilson](surf/)

A Wilson surfando a enchente em cima de uma telha, como no meme. Um botão só:
segure na descida da onda para ganhar velocidade, solte na crista para
decolar, gire no ar e fuja da água que vem atrás.

Os dois funcionam em tela cheia no celular, com botões de pausa, som e tela
cheia desenhados dentro do próprio jogo.

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
