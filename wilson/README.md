# 🐔 Wilson: A Galinha Voadora

Um Flappy Bird caseiro onde o herói é a Wilson, uma galinha que decidiu que
gravidade é opinião. Tudo em **um único arquivo HTML** — sem build, sem
dependências, sem imagens externas: cenário, galinha e sons são desenhados e
sintetizados em tempo de execução (Canvas 2D + Web Audio).

## Como jogar

Abra `wilson/index.html` no navegador (duplo clique já resolve) ou sirva a pasta:

```bash
npx http-server . -p 8080     # depois: http://localhost:8080/wilson/
```

### Controles

| Ação | Tecla / gesto |
|---|---|
| Bater as asas | `Espaço`, `↑`, `W`, `Enter`, clique ou toque |
| Pausar | `P` ou `Esc` |
| Ligar/desligar som | `M` ou o botão no canto superior direito |
| Recomeçar | toque/clique na tela de fim de jogo |

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
- **Som procedural** (Web Audio): batida de asa, ponto, ovo, colisão e o
  co-co-ri-có final.
- **Responsivo**: o canvas é 480×720 lógico e escala para caber na tela, com
  suporte a devicePixelRatio para não ficar borrado.

## Ajustes rápidos

As constantes de gameplay ficam juntas no topo do script, em `index.html`:

```js
const BASE_SPEED = 168, MAX_SPEED = 268;   // velocidade dos obstáculos
const BASE_GAP  = 200, MIN_GAP  = 146;     // tamanho da passagem
const GRAVITY = 1750, FLAP_V = -505;       // peso e força da asada
```
