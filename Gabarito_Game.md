### RESULUÇÃO LINHA POR LINHA
### Introdução:
Este roteiro ajudará você a criar um jogo estilo Flappy Bird com inteligência artificial para controlar os pássaros. Vamos dividir o script `game` em várias partes para facilitar o entendimento. O código, usa redes neurais e um algoritmo genético para controlar os pássaros no jogo. Cada pássaro é controlado por uma rede neural que toma decisões com base na posição do pássaro e dos tubos. O algoritmo genético otimiza essas redes neurais ao longo de várias gerações, selecionando as melhores redes e criando novas redes através de cruzamento e mutação, permitindo que os pássaros "aprendam" a jogar melhor com o tempo.

### 1. Inicialização do Canvas e Contexto
```javascript
const canvas = document.getElementById('game');
const context = canvas.getContext('2d');
```

- Obtém o elemento `<canvas>` do HTML e o contexto de desenho 2D, onde todos os gráficos do jogo serão desenhados.

### 2. Variáveis e Constantes do Jogo
```javascript
let totalBirds = 250;
let birds = [];
let frames = 0;
const DEGREE = Math.PI / 180;
const sprite = new Image();
sprite.src = 'img/sprite.png';
```

- `totalBirds`: Número total de pássaros no jogo.
- `birds`: Array que armazena todos os pássaros.
- `frames`: Contador de frames para controlar a animação.
- `DEGREE`: Constante para converter graus em radianos.
- `sprite`: Objeto de imagem que contém os sprites do jogo.

### 3. Background e Foreground

```javascript
const background = { ... }
const foreground = { ... }
```

- Definem a aparência e comportamento do fundo e do primeiro plano do jogo, incluindo a função `draw` para desenhá-los no canvas e `update` para atualizar suas posições, criando a ilusão de movimento.

### 4. Tubos (Pipes)
```javascript
const pipes = { ... }
```

- Define a posição, aparência e movimento dos tubos. A função `update` controla a criação de novos tubos e a detecção de colisão com os pássaros, enquanto a função `draw` desenha os tubos no canvas.

### 5. Classe Bird
```javascript
class Bird { ... }
```

- Define a classe `Bird`, que representa um pássaro no jogo. Inclui propriedades como posição, velocidade, estado de vida, animações, etc. Métodos principais:
  - `update()`: Atualiza a posição e animação do pássaro.
  - `draw()`: Desenha o pássaro no canvas.
  - `flap()`: Faz o pássaro subir.

### 6. Informações do Jogo

```javascript
const information = { ... }
```

- Armazena e desenha informações como pontuação, número de pássaros vivos, geração atual e melhor pontuação. Possui métodos para desenhar essas informações e resetar os valores.

### 7. Inteligência Artificial (IA)

```javascript
// IA
let Architect = synaptic.Architect;
let Network = synaptic.Network;
let genomes = [];
let genetic = new Genetic(2, 2, 1);

function updateIA() {
  let alive = totalBirds;
  for(let i = 0; i < birds.length; i++) {
    alive -= birds[i].alive ? 0 : 1;
    genomes[i].score = birds[i].alive ? information.score : genomes[i].score;

    if(birds[i].alive) {
      let input = [
        parseFloat((birds[i].y / 355).toFixed(2)),
        pipes.position.length == 0 ? 1 : parseFloat(((pipes.position[0].y + pipes.height + (pipes.gap / 2)) / 292.5).toFixed(2)),
      ];

      let active = genetic.activateNetwork(genomes[i], input);

      if (active[0] > 0.50) {
        birds[i].flap();
      }
    }
  }

  if(alive == 0) {
    genetic.prepareCrossover();
    information.generation++;
    reset();
  }
}
```

- Usa a biblioteca Synaptic.js para criar redes neurais que controlam os pássaros. A função `updateIA` atualiza o estado dos pássaros usando a IA, decidindo se cada pássaro deve bater as asas com base nas entradas da rede neural.

7.1. Inicialização das Redes Neurais e Algoritmo Genético
```javascript
let Architect = synaptic.Architect;
let Network = synaptic.Network;
let genomes = [];
let genetic = new Genetic(2, 2, 1);
```

- `Architect` e `Network`: Importam classes da biblioteca Synaptic.js para criar e manipular redes neurais.
- `genomes`: Array que armazena os genomas (redes neurais) de cada pássaro.
- `genetic`: Instância de uma classe `Genetic` personalizada, que lida com o algoritmo genético. Este objeto é configurado para trabalhar com redes neurais com 2 entradas, 2 camadas ocultas e 1 saída.

7.2. Função `updateIA`
```javascript
let Architect = synaptic.Architect;
let Network = synaptic.Network;
let genomes = [];
let genetic = new Genetic(2, 2, 1);
```

A função `updateIA` é chamada em cada frame do jogo para atualizar a IA dos pássaros. Vamos analisar cada parte dessa função:

7.3. Contagem de Pássaros Vivos
```javascript
let alive = totalBirds;
for (let i = 0; i < birds.length; i++) {
  alive -= birds[i].alive ? 0 : 1;
  genomes[i].score = birds[i].alive ? information.score : genomes[i].score;
```

- Inicializa a variável `alive` com o número total de pássaros.
- Itera sobre todos os pássaros:
  - Se o pássaro está morto, decrementa `alive`.
  - Atualiza a pontuação do genoma com base na pontuação atual do jogo, se o pássaro estiver vivo.

7.3. Atualização dos Pássaros Vivos
```javascript
  if (birds[i].alive) {
    let input = [
      parseFloat((birds[i].y / 355).toFixed(2)),
      pipes.position.length == 0 ? 1 : parseFloat(((pipes.position[0].y + pipes.height + (pipes.gap / 2)) / 292.5).toFixed(2)),
    ];

    let active = genetic.activateNetwork(genomes[i], input);

    if (active[0] > 0.50) {
      birds[i].flap();
    }
  }
```

- Para cada pássaro vivo:
  - Calcula as entradas para a rede neural do pássaro:
    - A posição vertical do pássaro, normalizada entre 0 e 1.
    - A posição do tubo mais próximo, normalizada entre 0 e 1.
  - Ativa a rede neural do pássaro com essas entradas.
  - Se a saída da rede neural for maior que 0,5, o pássaro bate as asas (`flap`).

7.4. Preparação para a Próxima Geração

```javascript
if (alive == 0) {
  genetic.prepareCrossover();
  information.generation++;
  reset();
}
```

- Se todos os pássaros estiverem mortos (`alive == 0`):
  - Chama a função `prepareCrossover` do objeto `genetic`, que prepara a próxima geração de redes neurais através de cruzamento e mutação.
  - Incrementa a geração atual.
  - Reseta o jogo para a próxima geração.

### 8. Controle do Jogo

```javascript
function createBirds() { ... }
function reset() { ... }
```

- Funções para criar pássaros (`createBirds`) e resetar o jogo (`reset`), que recriam os pássaros e reiniciam os tubos e as informações do jogo.

### 9. Funções de Desenho e Atualização
```javascript
function draw() { ... }
function update() { ... }
```

- `draw()`: Desenha todos os elementos do jogo, incluindo fundo, tubos, primeiro plano, pássaros e informações.
- `update()`: Atualiza o estado do jogo, incluindo a posição dos pássaros, tubos e a IA.

### 10. Loop Principal
```javascript
(function loop() {
  update();
  draw();
  frames++;
  requestAnimationFrame(loop);
})();
```

- O loop principal do jogo, que chama as funções `update` e `draw` continuamente usando `requestAnimationFrame` para criar uma animação suave e responsiva.

