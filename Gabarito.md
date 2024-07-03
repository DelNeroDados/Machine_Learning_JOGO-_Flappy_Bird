### RESULUÇÃO LINHA POR LINHA
### Introdução:
Este roteiro ajudará você a criar um jogo estilo Flappy Bird com inteligência artificial para controlar os pássaros. Vamos dividir a classe `Genetic` em várias partes para facilitar o entendimento.

### 1. Função `constructor`

   ```javascript
   class Genetic {
     constructor(input, hidden, output) {
       this.createGenomes(input, hidden, output);
     }
   ```

1.1. **constructor**: 
   - Palavra reservada em JavaScript usada para definir uma função construtora de uma classe. É chamada automaticamente quando um objeto da classe é instanciado.

1.2. **(input, hidden, output)**:
   - Parâmetros da função construtora. São usados para passar valores ao criar uma nova instância da classe.
   - **input**: O número de neurônios na camada de entrada da rede neural.
   - **hidden**: O número de neurônios na camada oculta da rede neural.
   - **output**: O número de neurônios na camada de saída da rede neural.

1.3. **{**:
   - Início do bloco de código da função construtora.

1.4. **this.createGenomes(input, hidden, output);**:
   - `this`: Referência à instância atual da classe.
   - **createGenomes**: Nome do método da classe `Genetic` que será chamado.
   - **(input, hidden, output)**: Argumentos passados ao método `createGenomes`.
   - **this.createGenomes(input, hidden, output);**: Chama o método `createGenomes` com os parâmetros `input`, `hidden` e `output` para criar os genomas iniciais da rede neural.

1.5. **}**:
   - Fim do bloco de código da função construtora.

### 2. Função `createGenomes`

   ```javascript
     createGenomes(input, hidden, output) {
       while(genomes.length < totalBirds) {
         let genome = new Architect.Perceptron(input, hidden, output);
         genome.score = 0;
         genomes.push(genome);
       }
     }
   ```
2.1. **createGenomes**:
   - Nome do método da classe `Genetic`.

2.2. **(input, hidden, output)**:
   - Parâmetros da função. 
   - **input**: Número de neurônios na camada de entrada.
   - **hidden**: Número de neurônios na camada oculta.
   - **output**: Número de neurônios na camada de saída.

2.3. **{**:
   - Início do bloco de código da função.

2.4. **while(genomes.length < totalBirds)**:
   - `while`: Estrutura de repetição que continua executando o bloco de código enquanto a condição é verdadeira.
   - **(genomes.length < totalBirds)**: Condição que verifica se o número de genomas no array `genomes` é menor que `totalBirds`.

2.5. **{**:
   - Início do bloco de código do `while`.

2.6. **let genome**:
   - Declaração de uma variável local chamada `genome`.

2.7. **= new Architect.Perceptron(input, hidden, output);**:
   - Criação de um novo objeto `Perceptron` da biblioteca `Architect` com as camadas especificadas pelos parâmetros `input`, `hidden` e `output`.

2.8. **genome.score = 0;**:
   - Inicialização da propriedade `score` do objeto `genome` com o valor 0.

2.9. **genomes.push(genome);**:
   - Adiciona o objeto `genome` ao array `genomes`.

2.10. **}**:
    - Fim do bloco de código do `while`.

2.11. **}**:
    - Fim do bloco de código da função.

### 3. Função `activateNetwork`

   ```javascript
     activateNetwork(genome, input) {
       return genome.activate(input);
     }
   ```

3.1. **activateNetwork**:
   - Nome do método da classe `Genetic`.

3.2. **(genome, input)**:
   - Parâmetros da função.
   - **genome**: Um objeto de rede neural que será ativado.
   - **input**: Os dados de entrada que serão processados pela rede neural.

3.3. **{**:
   - Início do bloco de código da função.

3.4. **return**:
   - Palavra-chave que indica que a função vai devolver um valor.

3.5. **genome.activate(input);**:
   - Chama o método `activate` do objeto `genome` com o argumento `input`.
   - O método `activate` processa os dados de entrada através da rede neural e retorna a saída.

3.6. **}**:
   - Fim do bloco de código da função.


### 4. Função `prepareCrossover`

   ```javascript
     prepareCrossover() {
       genomes = this.selectBestGenomes(2);
       var bestGenomes = _.clone(genomes);
   
       // crossover
       while (genomes.length < (totalBirds - Math.round(totalBirds / 2))) {
           var genA = _.sample(bestGenomes).toJSON();
           var genB = _.sample(bestGenomes).toJSON();
   
           // Cross over and Mutate
           var newGenome = this.mutate(this.crossOver(genA, genB));
   
           genomes.push(Network.fromJSON(newGenome));
       }
   
       while (genomes.length < totalBirds) {
           // Get Genome
           var gen = _.sample(bestGenomes).toJSON();
   
           // Mutate
           var newGenome = this.mutate(gen);
   
           // Add to generation
           genomes.push(Network.fromJSON(newGenome));
       }
     }
   ```

4.1. **prepareCrossover**:
   - Nome do método da classe `Genetic`.

4.2. **()**:
   - Indica que o método não recebe parâmetros.

4.3. **{**:
   - Início do bloco de código da função.

4.4. **genomes = this.selectBestGenomes(2);**:
   - Chama o método `selectBestGenomes` com o argumento `2` e atribui o resultado ao array `genomes`.
   - Seleciona os dois melhores genomas.

4.5. **var bestGenomes = _.clone(genomes);**:
   - Declara a variável `bestGenomes` e a inicializa como uma cópia do array `genomes` usando a função `clone` da biblioteca `_` (Lodash).

4.6. **// crossover**:
   - Comentário que indica o início da seção de crossover.

4.7. **while (genomes.length < (totalBirds - Math.round(totalBirds / 2)))**:
   - Estrutura de repetição `while` que continua executando enquanto o tamanho do array `genomes` for menor que `totalBirds - Math.round(totalBirds / 2)`.
   - Preenche metade da população total.

4.8. **{**:
   - Início do bloco de código do `while`.

4.9. **var genA = _.sample(bestGenomes).toJSON();**:
   - Declara a variável `genA` e a inicializa com um objeto aleatório de `bestGenomes`, convertido para JSON.

4.10. **var genB = _.sample(bestGenomes).toJSON();**:
    - Declara a variável `genB` e a inicializa com outro objeto aleatório de `bestGenomes`, convertido para JSON.

4.11. **// Cross over and Mutate**:
    - Comentário que indica a etapa de crossover e mutação.

4.12. **var newGenome = this.mutate(this.crossOver(genA, genB));**:
    - Declara a variável `newGenome` e a inicializa com o resultado da mutação do crossover entre `genA` e `genB`.

4.13. **genomes.push(Network.fromJSON(newGenome));**:
    - Converte `newGenome` de JSON para um objeto de rede neural e o adiciona ao array `genomes`.

4.14. **}**:
    - Fim do bloco de código do primeiro `while`.

4.15. **while (genomes.length < totalBirds)**:
    - Estrutura de repetição `while` que continua executando enquanto o tamanho do array `genomes` for menor que `totalBirds`.
    - Preenche o restante da população.

4.16. **{**:
    - Início do bloco de código do segundo `while`.

4.17. **var gen = _.sample(bestGenomes).toJSON();**:
    - Declara a variável `gen` e a inicializa com um objeto aleatório de `bestGenomes`, convertido para JSON.

4.18. **var newGenome = this.mutate(gen);**:
    - Declara a variável `newGenome` e a inicializa com o resultado da mutação de `gen`.

4.19. **genomes.push(Network.fromJSON(newGenome));**:
    - Converte `newGenome` de JSON para um objeto de rede neural e o adiciona ao array `genomes`.

4.20. **}**:
    - Fim do bloco de código do segundo `while`.

4.21. **}**:
    - Fim do bloco de código da função.

### 5. Função `selectBestGenomes`

   ```javascript
     selectBestGenomes(selectN) {
       var selected = _.sortBy(genomes, 'score').reverse();
       while (selected.length > selectN) {
         selected.pop();
       }
       return selected;
     }
   ```

5.1. **selectBestGenomes**:
   - Nome do método da classe `Genetic`.

5.2. **(selectN)**:
   - Parâmetro `selectN`, que indica o número de melhores genomas a serem selecionados.

5.3. **{**:
   - Início do bloco de código da função.

5.4. **var selected = _.sortBy(genomes, 'score').reverse();**:
   - Declara a variável `selected` e a inicializa com o array `genomes` ordenado pelo atributo `score` em ordem decrescente, utilizando a função `sortBy` da biblioteca `_` (Lodash).

5.5. **while (selected.length > selectN)**:
   - Estrutura de repetição `while` que continua executando enquanto o tamanho do array `selected` for maior que `selectN`.

5.6. **{**:
   - Início do bloco de código do `while`.

5.7. **selected.pop();**:
   - Remove o último elemento do array `selected`, reduzindo o seu tamanho.

5.8. **}**:
   - Fim do bloco de código do `while`.

5.9. **return selected;**:
   - Retorna o array `selected`, que agora contém os melhores genomas, de acordo com o valor de `selectN`.

5.10. **}**:
    - Fim do bloco de código da função.

### 6. Função `crossOver`

   ```javascript
     crossOver(netA, netB) {
       // Swap (50% prob.)
       if (Math.random() > 0.5) {
           var tmp = netA;
           netA = netB;
           netB = tmp;
       }
   
       // Clone network
       netA = _.cloneDeep(netA);
       netB = _.cloneDeep(netB);
   
       // Cross over data keys
       this.crossOverDataKey(netA.neurons, netB.neurons, 'bias');

       return netA;
     }
   ```

6.1. **crossOver(netA, netB)**:
   - Nome do método da classe `Genetic`, que recebe dois parâmetros `netA` e `netB`.

6.2. **{**:
   - Início do bloco de código da função.

6.3. **// Swap (50% prob.)**:
   - Comentário explicando que há uma troca dos valores dos parâmetros `netA` e `netB` com 50% de probabilidade.

6.4. **if (Math.random() > 0.5)**:
   - Estrutura condicional `if` que verifica se um número aleatório entre 0 e 1 é maior que 0.5.

6.5. **{**:
   - Início do bloco de código do `if`.

6.6. **var tmp = netA;**:
   - Declara a variável `tmp` e a inicializa com o valor de `netA`.

6.7. **netA = netB;**:
   - Atribui o valor de `netB` a `netA`.

6.8. **netB = tmp;**:
   - Atribui o valor de `tmp` a `netB`, completando a troca.

6.9. **}**:
   - Fim do bloco de código do `if`.

6.10. **// Clone network**:
    - Comentário indicando que as redes serão clonadas.

6.11. **netA = _.cloneDeep(netA);**:
    - Clona profundamente `netA` usando a função `cloneDeep` da biblioteca `_` (Lodash).

6.12. **netB = _.cloneDeep(netB);**:
    - Clona profundamente `netB` usando a função `cloneDeep` da biblioteca `_` (Lodash).

6.13. **// Cross over data keys**:
    - Comentário indicando que a função `crossOverDataKey` será chamada para realizar o crossover das chaves de dados.

6.14. **this.crossOverDataKey(netA.neurons, netB.neurons, 'bias');**:
    - Chama o método `crossOverDataKey` da classe `Genetic`, passando os neurônios de `netA`, os neurônios de `netB` e a string `'bias'` como argumentos.

6.15. **return netA;**:
    - Retorna `netA`, que agora contém os resultados do crossover.

6.16. **}**:
    - Fim do bloco de código da função.

### 7. Função `crossOverDataKey`
   ```javascript
  crossOverDataKey(a, b, key) {
    var cutLocation = Math.round(a.length * Math.random());

    var tmp;
    for (var k = cutLocation; k < a.length; k++) {
        // Swap
        tmp = a[k][key];
        a[k][key] = b[k][key];
        b[k][key] = tmp;
    }
  }
   ```

7.1. **crossOverDataKey(a, b, key)**:
   - Nome do método da classe `Genetic`, que recebe três parâmetros: `a`, `b`, e `key`.

7.2. **{**:
   - Início do bloco de código da função.

7.3. **var cutLocation = Math.round(a.length * Math.random());**:
   - Declara a variável `cutLocation` e a inicializa com um número arredondado que é a multiplicação do comprimento de `a` por um número aleatório entre 0 e 1.

7.4. **var tmp;**:
   - Declara a variável `tmp` sem inicializá-la.

7.5. **for (var k = cutLocation; k < a.length; k++)**:
   - Inicia um loop `for` que começa em `cutLocation` e vai até o comprimento de `a`.

7.6. **{**:
   - Início do bloco de código do `for`.

7.7. **// Swap**:
   - Comentário indicando que a operação de troca será realizada.

7.8. **tmp = a[k][key];**:
   - Atribui o valor da propriedade `key` do elemento `a[k]` à variável `tmp`.

7.9. **a[k][key] = b[k][key];**:
   - Atribui o valor da propriedade `key` do elemento `b[k]` à propriedade `key` do elemento `a[k]`.

7.10. **b[k][key] = tmp;**:
    - Atribui o valor de `tmp` à propriedade `key` do elemento `b[k]`.

7.11. **}**:
    - Fim do bloco de código do `for`.

7.12. **}**:
    - Fim do bloco de código da função.

### 8. Função `mutate`

   ```javascript
     mutate(net) {
       this.mutateDataKeys(net.neurons, 'bias', 0.3);
       this.mutateDataKeys(net.connections, 'weight', 0.3);
       return net;
     }
   ```

8.1. **mutate(net)**:
   - Nome do método da classe `Genetic`, que recebe um parâmetro chamado `net`.

8.2. **{**:
   - Início do bloco de código da função.

8.3. **this.mutateDataKeys(net.neurons, 'bias', 0.3);**:
   - Chama o método `mutateDataKeys` da mesma classe (`this`), passando três argumentos: 
     - `net.neurons`: a propriedade `neurons` do objeto `net`.
     - `'bias'`: a string `'bias'`, indicando que a mutação será aplicada aos valores de `bias`.
     - `0.3`: o valor da taxa de mutação (30%).

8.4. **this.mutateDataKeys(net.connections, 'weight', 0.3);**:
   - Chama o método `mutateDataKeys` novamente, desta vez passando:
     - `net.connections`: a propriedade `connections` do objeto `net`.
     - `'weight'`: a string `'weight'`, indicando que a mutação será aplicada aos valores de `weight`.
     - `0.3`: o valor da taxa de mutação (30%).

8.5. **return net;**:
   - Retorna o objeto `net`, que foi modificado pelas mutações aplicadas.

8.6. **}**:
   - Fim do bloco de código da função.

### 9. Função `mutateDataKeys`

   ```javascript
     mutateDataKeys(a, key, mutationRate) {
       for (var k = 0; k < a.length; k++) {
   
         if (Math.random() > mutationRate) {
             continue;
         }
   
         a[k][key] += a[k][key] * (Math.random() - 0.5) * 3 + (Math.random() - 0.5);
       }
     }
   }
   ```

9.1. **mutateDataKeys(a, key, mutationRate)**:
   - Nome do método da classe `Genetic`, que recebe três parâmetros:
     - `a`: uma lista de objetos.
     - `key`: uma chave que será usada para acessar valores nos objetos da lista `a`.
     - `mutationRate`: a taxa de mutação (um número entre 0 e 1).

9.2. **{**:
   - Início do bloco de código da função.

9.3. **for (var k = 0; k < a.length; k++)**:
   - Início de um loop `for` que itera sobre cada elemento na lista `a`. A variável `k` é o índice do loop.

9.4. **{**:
   - Início do bloco de código do loop.

9.5. **if (Math.random() > mutationRate)**:
   - Gera um número aleatório entre 0 e 1 e compara com `mutationRate`.
   - Se o número aleatório for maior que `mutationRate`, então:

9.6. **continue;**:
   - Continua para a próxima iteração do loop, pulando as linhas seguintes dentro do loop para este `k`.

9.7. **a[k][key] += a[k][key] * (Math.random() - 0.5) * 3 + (Math.random() - 0.5);**:
   - Modifica o valor de `a[k][key]` adicionando a ele um valor aleatório.
   - Este valor é calculado como: `a[k][key] * (Math.random() - 0.5) * 3 + (Math.random() - 0.5)`.
     - `Math.random() - 0.5` gera um número entre -0.5 e 0.5.
     - Multiplica esse número por 3, aumentando a variação.
     - Adiciona outro número entre -0.5 e 0.5.
     - O resultado é uma pequena variação aleatória aplicada ao valor original `a[k][key]`.

9.8. **}**:
   - Fim do bloco de código do loop.



