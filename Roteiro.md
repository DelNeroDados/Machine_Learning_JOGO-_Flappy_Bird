## Roteiro para Implementar o Código

### Introdução
Vamos aprender a criar uma inteligência artificial (IA) que ensina um passarinho a jogar Flappy Bird usando Redes Neurais e Algoritmos Genéticos. Vamos seguir passos detalhados para escrever o código necessário.


### Recursos Necessários
- Editor de código (VS Code).
- Biblioteca Synaptic.js para redes neurais.
- Biblioteca Lodash para manipulação de dados.
- Sprites e elementos visuais para o jogo Flappy Bird.


### Passo a passo

1. **Verificar o Ambiente de Desenvolvimento**
   - Se necessário, instalar um editor de código como VS Code.
   - Criar uma nova pasta para o projeto.
   - Baixar e incluir as bibliotecas Synaptic.js e Lodash no projeto.

2. **Configurar a Estrutura Inicial do Jogo**
   - Criar um arquivo HTML para o jogo.
   - Criar um arquivo JavaScript para a lógica do jogo.
   - Adicionar um canvas no HTML para desenhar o jogo.

3. **Criar a Classe `Genetic`**
   - Definir a classe `Genetic` com um construtor que inicializa os genomas.
   - Implementar o método `createGenomes` para criar genomas usando a arquitetura Perceptron da biblioteca Synaptic.

4. **Método `createGenomes`**
   - Escrever um loop que cria genomas até atingir o número total de pássaros (`totalBirds`).
   - Inicializar cada genoma com um score de 0 e adicioná-los ao array `genomes`.

5. **Método `activateNetwork`**
   - Definir um método que recebe um genoma e um input.
   - Ativar a rede neural do genoma com o input e retornar o resultado.

6. **Método `prepareCrossover`**
   - Selecionar os melhores genomas com base no score.
   - Clonar os melhores genomas.
   - Realizar o cruzamento e a mutação para criar novos genomas até preencher o número total de pássaros.
   - Adicionar os novos genomas ao array `genomes`.

7. **Método `selectBestGenomes`**
   - Ordenar os genomas pelo score em ordem decrescente.
   - Manter apenas os melhores genomas (número especificado por `selectN`).
   - Retornar os genomas selecionados.

8. **Método `crossOver`**
   - Definir um método que realiza o cruzamento entre dois genomas.
   - Clonar os genomas e trocar alguns dados (bias) entre eles.
   - Retornar o novo genoma resultante do cruzamento.

9. **Método `crossOverDataKey`**
   - Trocar os valores de um determinado atributo (como 'bias') entre dois arrays de neurônios.
   - Definir um ponto de corte aleatório e trocar os valores a partir desse ponto.

10. **Método `mutate`**
    - Definir um método que aplica mutações em um genoma.
    - Alterar os valores de atributos (como 'bias' e 'weight') de forma aleatória com uma certa taxa de mutação.

11. **Método `mutateDataKeys`**
    - Alterar os valores de um determinado atributo em um array com base em uma taxa de mutação.
    - Adicionar uma pequena variação aleatória aos valores.

12. **Integrar a IA ao Jogo**
    - Usar os métodos da classe `Genetic` para treinar e evoluir a IA enquanto o jogo roda.
    - Implementar a lógica para atualizar o jogo, desenhar os elementos e processar as entradas e saídas da IA.

13. **Testar e Ajustar**
    - Testar o jogo para verificar se a IA está aprendendo a jogar.
    - Ajustar os parâmetros da rede neural e do algoritmo genético para melhorar o desempenho.
