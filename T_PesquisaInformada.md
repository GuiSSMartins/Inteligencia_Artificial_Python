# Trabalho Prático 1 - Algoritmos de Procura (_Pesquisa Informada e Não-Informada_)
----------------------------------

O que usei para escrever esta explicação:
- Explicação simles de IA em jogos 2D do _GeeksForGeeks_: https://www.geeksforgeeks.org/a-search-algorithm/
- Explicação dos métodos em mapas-2D: https://towardsdatascience.com/a-star-a-search-algorithm-eb495fb156bb (... verificar se tem artigo grátis para o ler ...)
- Implementações A* em python: https://github.com/BaijayantaRoy/Medium-Article/blob/master/A_Star.ipynb, https://gist.github.com/ryancollingwood/32446307e976a11a1185a5394d6657bc, (pseudocódigo) https://medium.com/@nicholas.w.swift/easy-a-star-pathfinding-7e6689c7f7b2

Neste ponto do trabalho __(1ª parte)__, apenas é necessário:
- implementar _apenas_ __um__ dos algoritmos de pesquisa informada OU não-informada sobre o mapa (independentemente de este ser o mais eficiente ou não; em princípio, a implementação de vários algoritmos só será feita na 2ª fase);
- por agora, terá _apenas_ __1 veículo__; por isso, não nos temos de preocupar com possíveis colisões;
- existe a possibilidade de o sair da pista, sendo que quando essa situação ocorrer o carro terá de voltar para a posição anterior, assumindo um valor de velocidade zero.

__ATENÇÃO:__ Estes _links_ mostram análises para caos muitos simples, onde os carros andam à mesma velocidade. MAS, neste projeto para IA, os carros têm uma aceleração, variável entre -1, 0 e 1. Sem dúvida, isto tornará o programa bem mais difícil.

-----------------------------

## -> Como podemos criar um grafo a partir de um _mapa-2D_ (conhecido como problema do _Path Finding_)

__Jogo__: _VectorRace_ / _RaceTrack_

Seguindo a sugestão de mapa feita no enunciado (do ficheiro _circuito.txt_):

__X X X X X X X X X X__

__X X - - - X X - - X__

__X - - - - - - - - F__

__X P - - X X X - - F__

__X - - - - - - - - F__

__X X X X - - - - X X__

__X X X X X X X X X X__

Podemos converter o mapap numa matriz de caracteres, onde:
- __P__ -> posição inicial do veículo
- __-__ -> indica local que um veículo pode percorrer
- __X__ -> obstáculo do caminho (evitar) 
- __F__ -> meta (como há vários valores de meta final, sem dúvida vai complicar um bocado o algoritmo)

Escrever tuplos ('caracter', num travessia). ATENÇÃO: num travessia não é igual a Custo.

Neste mapa, o custo de cada arco deverá ser apenas 1.

Na posição inicial, deve ter valor igual a 1 de 'num travessia'; depois vai-se adicionando uma unidade por cada nova iteração realizad nos novos pontos do mapa.

Aplicar um algirtmo semelhante ao de travessia

## -> Comparação de Algoritmos _(Qual deles é o mais eficaz para a resolução deste problema?)_

- Algortimo por Profundidade:
- A* (_A star_):

Apesar do A* ser o melhor algoritmo para este tipo de casos, não podemos esquecer que este não dá garantidamente a melhor solução para o probelma do caminho amis curto em circuitos.

## -> Proposta de Cálculo de uma Aproximação da distância de 

Como o carro pode mover em 8 direções, a melhor _heurística_ h(n) será a da __Distância DIAGONAL__. (para entender melhor, ver o seguinte link (principalmente com as fórmulas mais complicadas para o diagonal Distance): https://www.growingwiththeweb.com/2012/06/a-pathfinding-algorithm.html)

APenas se o carro andasse de forma Up, Down, Right, Left, usariamos apenas o de Manhattan.
