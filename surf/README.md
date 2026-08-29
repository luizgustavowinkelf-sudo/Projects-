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

A Wilson decola quando a onda "foge" debaixo dos pés: se a posição dela em
queda livre no próximo quadro ficar acima da água, ela deixa de estar na
superfície. É a mesma conta que faz uma rampa lançar um skatista.

O entulho é encaixado no **vale seguinte** ao sorteio (`valeApos`), e não em
qualquer ponto: assim o obstáculo cai sempre onde o jogador ou passa voando
(se manteve velocidade) ou bate (se surfou mal) — em vez de aparecer no meio
de uma subida, onde não haveria o que fazer.

## Ajustes rápidos

```js
const G = 1500, MERGULHO = 2.5, ARRASTO = 0.26;   // gravidade, peso ao segurar, atrito
const VX_MIN = 120, VX_MAX = 1020;                // limites de velocidade
const A1 = 85, F1 = 0.0040;                       // tamanho e comprimento do marulho
ondaV = Math.min(430, 170 + dist * 0.006);        // o quanto a enchente aperta
```
