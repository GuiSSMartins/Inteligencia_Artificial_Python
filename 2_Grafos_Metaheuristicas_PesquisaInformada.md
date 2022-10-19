# 2 - Aplicação de Metaheuristicas - Pesquisa Informada - a Grafos (Não Orientados) e com Peso

![alt text](https://github.com/GuiSSMartins/Inteligencia_Artificial_Python/blob/main/Grafo_Peso_Ficha2.png?raw=true)

- __Representaçaõ do Estado__:
- __Estado inicial__:
- __Estado/teste objetivo__: Lisboa
- __Custo da Solução__:


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
    g.add_edge("elvas", "borba",15) # custos
    g.add_edge("borba", "estremoz",2)

    # INCOMPLETO

    g.add_edge("redondo","monsaraz",30)
    g.add_edge("monsaraz","barreiro",120)
    g.add_edge("barreiro","baixadabanheira", 5)
    g.add_edge("baixadabanheira","moita", 7)
    g.add_edge("moita","alcochete", 20)
    g.add_edge("alcochete", "lisboa", 20)
    
    g.add_heuristica("elvas", 276) # pesos
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
    self.m_h = {} # dicionário para posteriormente armazenar as heurísticas para cada nodo, usado na pesquisa informada
    # --------------------------------------------------------------------------------------------------------------
```
## 0) Heurística
- É uma estimação adequada do custo ou longitude do passo (no espaço de procura) desde um estado até um objetivo.
- Procura Heurística ou Informada.

Custos ótimos: têm sempre uma estrela __*__

Dado um nó _n_:
- __g(n)__ = custo desde o nó inicial até n.
- __h(n)__ = função heurística aplicada ao nó n. É o custo estimado desde n até uma solução.
- __h*(n)__ = custo real de um caminho óptimo desde n até uma solução.
- __f(n) = g(n) + h(n)__ : custo estimado de uma solução que passa pelo nó n.


## 1) Pesquisa informada Gulosa (_Greedy Search_)


## 2) Pesquisa informada A*

