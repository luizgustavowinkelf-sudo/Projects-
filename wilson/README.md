# 🐔 Wilson: A Galinha Voadora

Um Flappy Bird caseiro onde o herói é a Wilson, uma galinha que decidiu que
gravidade é opinião. Tudo em **um único arquivo HTML** — sem build e sem
imagens: cenário, galinha e sons são desenhados e sintetizados em tempo de
execução (Canvas 2D + Web Audio). A única coisa que vem da rede é a fonte
Baloo 2 do Google Fonts, e o jogo funciona normalmente sem ela (cai para uma
fonte do sistema).

## Como jogar

Abra `wilson/index.html` no navegador (duplo clique já resolve) ou sirva a pasta:

```bash
npx http-server . -p 8080     # depois: http://localhost:8080/wilson/
```

### No celular

O jogo foi feito para funcionar bem no telefone:

- **Tela cheia de verdade**: o campo de jogo assume o formato da tela (entre
  3:4 e 1:2), sem tarjas em cima e embaixo, e respeita o notch via
  `env(safe-area-inset-*)`.
- **Três botões na tela** (pausa, som e tela cheia), porque no celular não
  existe teclado — com alvo de toque maior que o desenho.
- **Sem zoom, sem "puxar para atualizar" e sem seleção de texto** ao tocar.
- **Vibração** curta ao marcar ponto, pegar ovo e bater.
- Pausa sozinho quando você troca de aba ou atende uma ligação.
- Dá para **adicionar à tela de início** (iOS e Android) e abrir como app,
  sem a barra do navegador.

Para jogar no celular a partir do computador, sirva a pasta na rede local e
acesse pelo IP da máquina:

```bash
npx http-server . -p 8080 -a 0.0.0.0    # http://SEU-IP:8080/wilson/
```

### Controles

| Ação | Tecla / gesto |
|---|---|
| Bater as asas | `Espaço`, `↑`, `W`, `Enter`, clique ou toque |
| Pausar | `P`, `Esc` ou o botão ⏸ |
| Ligar/desligar som | `M` ou o botão 🔊 |
| Tela cheia | botão ⛶ (some quando o navegador não permite, como no iOS) |
| Ver o placar | botão 🏆 (canto superior esquerdo) |
| Recomeçar | toque/clique na tela de fim de jogo |

## Placar

Terminou uma partida boa? A tela do placar abre sozinha para você digitar o
nome e entrar no quadro das dez melhores. O botão 🏆 abre o placar a qualquer
momento.

Onde o placar fica guardado depende de onde o jogo está rodando:

- **Publicado como Artifact do Claude** — a página guarda o placar dentro de
  si mesma: ao entrar no quadro, ela se republica com a lista nova (a
  capacidade `artifact` do runtime), e todo mundo que abrir o link vê o mesmo
  placar. Quem tiver o link só para leitura consegue ver o quadro, mas a
  pontuação dessa pessoa fica guardada no aparelho dela — o navegador não
  pode escrever na página em nome dela.
- **Arquivo local, GitHub Pages ou qualquer outro servidor estático** — não
  existe onde escrever, então o placar é o deste aparelho (`localStorage`).
  O jogo avisa isso na hora de salvar.

As linhas que ainda não entraram no placar compartilhado aparecem marcadas
com **só neste aparelho**. Se duas pessoas entrarem no quadro ao mesmo tempo,
uma das publicações perde a corrida; nesse caso o jogo tenta de novo uma
única vez depois que a página recarrega na versão vencedora.

## O que tem no jogo

- **Wilson desenhada no código**: crista, barbela, bico, asa que bate mais
  rápido na subida, pernas que balançam e olhinho que vira `x` na hora do
  tombo.
- **Obstáculos de madeira** de curral em vez dos canos verdes.
- **Ovos dourados** aparecem em ~1/3 das passagens e valem **+2 pontos**.
- **Dificuldade progressiva**: a velocidade sobe de 168 para 268 px/s e a
  passagem encolhe de 200 para 146 px conforme a pontuação.
- **Cenário com parallax**: nuvens, colinas, celeiro, silo e cerca em camadas.
- **Penas voando** a cada batida de asa e uma nuvem de penas na colisão, com
  flash e tremida de tela.
- **Recorde salvo** em `localStorage` e medalhas de ovo: Bronze (5), Prata
  (15), Ouro (30) e Diamante (50).
- **Placar das dez melhores**, compartilhado quando a página pode se
  republicar e local quando não pode (ver acima).
- **Som procedural** (Web Audio): batida de asa, ponto, ovo, colisão e o
  co-co-ri-có final.
- **Responsivo**: 480 px de largura lógica e altura que segue o formato da
  tela, com `devicePixelRatio` para não ficar borrado. A passagem entre os
  obstáculos é proporcional à altura, então a dificuldade é a mesma no
  celular e no monitor.

## Ajustes rápidos

As constantes de gameplay ficam juntas no topo do script, em `index.html`:

```js
const BASE_SPEED = 168, MAX_SPEED = 268;   // velocidade dos obstáculos
const BASE_GAP  = 200, MIN_GAP  = 146;     // tamanho da passagem
const GRAVITY = 1750, FLAP_V = -505;       // peso e força da asada
```
