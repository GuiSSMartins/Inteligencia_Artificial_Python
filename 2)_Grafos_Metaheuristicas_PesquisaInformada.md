# 2) Aplicação de Metaheuristicas - Pesquisa Informada - a Grafos (Não Orientados) e com Peso

![alt text](https://github.com/GuiSSMartins/Inteligencia_Artificial_Python/blob/main/Grafo_Peso_Ficha2.png?raw=true)

- __Representaçaõ do Estado__:
- __Estado inicial__:
- __Estado/teste objetivo__: Lisboa
- __Solução__: Redondo -> Monsaraz -> Barreiro -> Palmela -> Almada -> Lisboa
- __Custo da Solução__: 215


(ver os desenhos feitos no tablet para a aplicação dos algoritmos)

## Implementação do grafo em Python

```python
#Importar classes nodo e grafo
from grafo import Graph
from nodo import Node

def main():
    #Criar instância de grafo
    g = Graph()

    #Adicionar vertices ao grafo g
    g.add_edge("elvas", "borba",15) # custo da aresta
    g.add_edge("borba", "estremoz",2)

    # INCOMPLETO

    g.add_edge("redondo","monsaraz",30)
    g.add_edge("monsaraz","barreiro",120)
    g.add_edge("barreiro","baixadabanheira", 5)
    g.add_edge("baixadabanheira","moita", 7)
    g.add_edge("moita","alcochete", 20)
    g.add_edge("alcochete", "lisboa", 20)
    
    g.add_heuristica("elvas", 276) # valor da heuristica h(n) do nõ n
    g.add_heuristica("borba", 250)
    g.add_heuristica("estremoz", 145)
    g.add_heuristica("evora", 95)
    g.add_heuristica("montemor", 70)
    g.add_heuristica("vendasnovas", 45)
    g.add_heuristica("arraiolos", 220)
    g.add_heuristica("alcacer", 140)
    g.add_heuristica("palmela", 85)
```

Correções feitas para nos adaptarmos melhor aos grafos COM PESO

```python

class Graph:
  # Construtor da classe
  def __init__(sefl, directed=False): # Grafo NÃO-Orientado (As arestas não têm sentido)
    self.m_nodes = [] # lista de nodos do grafo
    self.m_directed = directed # se o grafo é direcionado ou não
    self.m_graph = {} # diconário para armazenar os nodos, arestas e pesos
    # -------------------------------------------------------------------------------------------------------------
    self.m_h = {} # dicionário para armazenar as heurísticas para cada nodo, usado na pesquisa informada
    # --------------------------------------------------------------------------------------------------------------
```
## 0) Heurística
- É uma estimação adequada do custo ou longitude do passo (no espaço de procura) desde um estado até um objetivo.
- Procura Heurística ou Informada.

```python
# (acrescentar à classe Grafo)

##########################################
# Adiciona heuristica a nodo
#############################################

def add_heuristica(self, n, estima):
        n1 = Node(n)
        if n1 in self.m_nodes:
            self.m_h[n] = estima

###################################################
# Devolve vizinhos de um nó
###################################################

def getNeighbours(self, nodo):
    lista = []
    for (adjacente, peso) in self.m_graph[nodo]:
        lista.append((adjacente, peso))
    return lista
```

_Custos ótimos_: têm sempre uma estrela __*__

Dado um nó _n_:
- __g(n)__ = custo desde o nó inicial até n.
- __h(n)__ = função heurística aplicada ao nó n. É o custo estimado desde n até uma solução.
- __h*(n)__ = custo real de um caminho óptimo desde n até uma solução.
- __f(n) = g(n) + h(n)__ : custo estimado de uma solução que passa pelo nó n.

------------------------------------------------------

# 1) Pesquisa GULOSA Informada (_Greedy Search_)

(Versão pouco rigorosa): É uma adaptação do algoritmo BFS (de pesquisa em largura). Dentro da lista de nós adjacentes a partir daqueles já visitados, escolher aquele que tiver __menor valor__ de heuristica __h(n)__ .

# ATENÇÃO:
Neste tipo de algoritmos, há casos em que temos de procurar pelo __menor__ valor de heuristica (caminho mais curto) OU pelo __MAIOR__ valor de h(n) (caminho amis comprido).

Chagamos à solução ótima da Pesquisa Informada Gulosa quando todos os nós tiverem sido visitados __OU__ quando tivermos alcançado o vértico objetivo/final.

-> _Exemplo do grafo de cima_

__ATENÇÃO__: com os NÓS _ADJACENTES_ aos __já visitados__

-> _RESULTADO_ (com estado inicial em Redondo): __Redondo -> Monsaraz -> Barreiro -> Palmela -> Almada -> Lisboa__ (_Custo da Solução_: 215)

```python
# (acrescentar à classe Grafo)

#biblioteca necessária para se poder utilizar o valor math.inf  (infinito)
import math

#############################################
# Pesquisa gulosa
#############################################

def greedy(self, start, end):
    # open_list é uma lista de nodos visitados, mas com vizinhos que ainda não foram todos visitados, começa com o start 
    # closed_list é uma lista de nodos visitados e todos os seus vizinhos também já o foram
    open_list = set([start])
    closed_list = set([])

    # parents é um dicionário que mantém o antecessor de um nodo começa com start
    parents = {}
    parents[start] = start

    while len(open_list) > 0:
        n = None

        # encontrar nodo com a menor heuristica
        for v in open_list:
            if n == None or self.m_h[v] < self.m_h[n]:
                n = v

        if n == None:
            print('Path does not exist!')
            return None

        # se o nodo corrente é o destino, reconstruir o caminho a partir desse nodo 
        # até ao start, seguindo o antecessor
        if n == end:
            reconst_path = []

            while parents[n] != n:
                reconst_path.append(n)
                n = parents[n]

            reconst_path.append(start)

            reconst_path.reverse()

            return (reconst_path, self.calcula_custo(reconst_path))

        # para todos os vizinhos  do nodo corrente
        for (m, weight) in self.getNeighbours(n):
            # Se o nodo corrente nao esta na open nem na closed list
            # adiciona-lo à open_list e marcar o antecessor
            if m not in open_list and m not in closed_list:
                open_list.add(m)
                parents[m] = n


        # remover n da open_list e adiciona-lo à closed_list
        # porque todos os seus vizinhos foram inspecionados
        open_list.remove(n)
        closed_list.add(n)

    print('Path does not exist!')
    return None
```

![alt text](https://github.com/GuiSSMartins/Inteligencia_Artificial_Python/blob/main/greedy-search-path-example.gif)

------------------------------------------------------

# 2) Pesquisa informada A* (_A star_)

(Versão pouco rigorosa): Dentro da lista de nós __adjacentes__ aos já visitados, aplicar a fórmula __f(n) = g(n) + h(n)__ e escolher o nó que tiver menor valor de __f(n)__; escolher esse como nó seguinte da pesquisa no grafo.

Chagamos à solução ótima da Pesquisa Informada A* quando todos os nós tiverem sido visitados __OU__ quando tivermos alcançado o vértico objetivo/final.

-> _Exemplo do grafo de cima_

__ATENÇÃO__: com os NÓS _ADJACENTES_ aos __já visitados__

-> _RESULTADO_ (com estado inicial em Redondo): __Redondo ->          -> Lisboa__ (_Custo da Solução_: ...)


```python
# (acrescentar à classe Grafo)

#biblioteca necessária para se poder utilizar o valor math.inf  (infinito)
import math

#############################################
# Pesquisa A* (A star)    ATENÇÃO: esta é a minha versão, pode estar errado
#############################################

def astar(self, start, end):
    # open_list é uma lista de nodos visitados, mas com vizinhos que ainda não foram todos visitados, começa com o start 
    # closed_list é uma lista de nodos visitados e todos os seus vizinhos também já o foram
    open_list = set([start])
    closed_list = set([])

    # parents é um dicionário que mantém o antecessor de um nodo
    # e o peso total desde esse nodo até ao start (começa com start)
    parents = {}
    parents[start] = (start,0)

    while len(open_list) > 0:
        n = None

        # encontrar nodo com o menor valor (menor peso + menor heuristica)
        custoTotal = math.inf
        for v in open_list:
            (parent, weightParent) = parents[v]
            custoNodoAtual = weightParent + self.get_arc_cost(self, parent, v) + self.m_h[n] 
            # custo segundo as heuristicas: f(n) = g(n) + h(n)
            if n == None or custoNodoAtual < custoTotal:
                n = v
                custoTotal = custoNodoAtual

        if n == None:
            print('Path does not exist!')
            return None

        # se o nodo corrente é o destino, reconstruir o caminho a partir desse nodo 
        # até ao start, seguindo o antecessor
        if n == end:
            reconst_path = []

            while parents[n] != n:
                reconst_path.append(n)
                (n, weightN) = parents[n]

            reconst_path.append(start)

            reconst_path.reverse()

            return (reconst_path, self.calcula_custo(reconst_path))

        # para todos os vizinhos  do nodo corrente
        for (m, weight) in self.getNeighbours(n):
            # Se o nodo corrente nao esta na open nem na closed list
            # adiciona-lo à open_list e marcar o antecessor
            if m not in open_list and m not in closed_list:
                open_list.add(m)
                parents[m] = (n, parents[n][1] + self.get_arc_cost(self, n, m))


        # remover n da open_list e adiciona-lo à closed_list
        # porque todos os seus vizinhos foram inspecionados
        open_list.remove(n)
        closed_list.add(n)

    print('Path does not exist!')
    return None
```

![alt text](https://github.com/GuiSSMartins/Inteligencia_Artificial_Python/blob/main/AatrExample.gif)
