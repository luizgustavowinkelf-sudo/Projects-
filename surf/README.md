# 🌊 Lo Siento, Wilson

A Wilson surfando a enchente em cima de uma telha, no melhor estilo do meme.
Um arquivo HTML só: as ondas, a cidade submersa, a galinha e os sons são todos
gerados em tempo de execução (Canvas 2D + Web Audio).

## Como jogar

Um botão só — o dedo na tela, o clique ou a barra de espaço:

- **Segure na descida** da onda: a Wilson afunda na água e ganha velocidade.
- **Solte na crista**: ela decola. Quanto mais rápido chegar lá, mais longe voa.
- **Segure no ar**: ela dá giros (cada giro completo vale pontos), mas precisa
  cair alinhada com a onda. Torto demais é tombo: perde quase toda a
  velocidade e a enchente ganha terreno.
- **O entulho boia no fundo dos vales.** Com velocidade você passa voando por
  cima; devagar, bate — e aí é *lo siento, Wilson*.
- **A enchente vem atrás.** A barra no canto mostra a folga; surfar mal deixa
  ela alcançar.

| Ação | Tecla / gesto |
|---|---|
| Afundar / girar | `Espaço`, `↓`, `S`, `Enter`, clique ou toque (segurando) |
| Pausar | `P`, `Esc` ou o botão ⏸ |
| Ligar/desligar som | `M` ou o botão 🔊 |
| Tela cheia | botão ⛶ |

Pontuação: **1 ponto a cada 10 px de distância + 10 por milho + 20 por giro**.
O recorde fica salvo no aparelho (`localStorage`).

## Como a onda funciona

A superfície da água é a soma de três senóides — um marulho longo, uma onda
média e uma ondulação curta:

```js
alturaOnda(x) = BASE + 85·sen(0,0040x) + 30·sen(0,0100x + 1,7) + 8·sen(0,0220x + 4,1)
```

Isso dá um mar infinito, liso e — o que importa para a física — com
**inclinação analítica**: a derivada é exata em qualquer ponto, então a
aceleração na descida, o ângulo da telha e o momento da decolagem saem direto
da fórmula, sem amostragem nem colisão contra polígonos.

A Wilson decola pela **curvatura** da onda: ela deixa a superfície quando a
água encurva mais rápido do que a gravidade consegue segurar, ou seja quando
`κ·v² > g` — a mesma conta que joga um carro para fora no alto de uma lomba.
Segurando o dedo, o peso vira `g·MERGULHO`, e por isso a telha fica colada:
**voa-se soltando na crista**.

No ar a física é outra de propósito: a gravidade cai para `G_AR` e a crista dá
um impulso que cresce com a velocidade (`IMP_BASE + v·IMP_VEL`). Sem esses
dois ajustes o "voo" durava 0,2 s — tempo de pipoco, não de manobra. Com eles,
um voo bom passa de 1 s, que é o necessário para fechar um giro.

O entulho é encaixado no **vale seguinte** ao sorteio (`valeApos`), e não em
qualquer ponto: assim o obstáculo cai sempre onde o jogador ou passa voando
(se manteve velocidade) ou bate (se surfou mal) — em vez de aparecer no meio
de uma subida, onde não haveria o que fazer.

## Ajustes rápidos

```js
const G = 1500, MERGULHO = 2.5, ARRASTO = 0.26;   // gravidade, peso ao segurar, atrito
const G_AR = 950;                                 // gravidade no ar: é ela que dá o arco
const SALTO = 2.2;                                // facilidade de descolar na crista
const IMP_BASE = 150, IMP_VEL = 0.25;             // impulso da crista
const A1 = 85, F1 = 0.0040;                       // tamanho e comprimento do marulho
ondaV = Math.min(430, 170 + dist * 0.006);        // o quanto a enchente aperta
```

Esses números foram calibrados fora do navegador: a física está portada num
script de simulação que roda 30 s de jogo com um piloto ideal e mede
decolagens, tempo no ar e duração do voo para cada combinação. O ajuste
escolhido dá uma decolagem a cada ~2,5 s e voo médio de ~1 s — números que
depois bateram com o jogo rodando de verdade (22% de tempo no ar medido no
navegador contra 26% na simulação).
