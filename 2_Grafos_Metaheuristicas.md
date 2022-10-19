# 2 - Aplicação de Metaheuristicas a Grafos (Não Orientados) e com Peso

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
    g.add_edge("s", "e",2)
    g.add_edge("s", "a",2)
    g.add_edge("e", "f",5)
    g.add_edge("a", "b",2)
    g.add_edge("b", "c", 2)
    g.add_edge("c", "d", 3)
    g.add_edge("d", "t",3)
    g.add_edge("g", "t", 2)
    g.add_edge("f","g",2)
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


## Pesquisa informada Gulosa

## Pesquisa informada A*

