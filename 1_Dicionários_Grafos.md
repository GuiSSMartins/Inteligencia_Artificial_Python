# Algoritmos sobre grafos em Python

Os grafos em _python_ são represenatdos por _Dicionários_ (explicação no final deste _md_)

2 representações dos grafos:
- Matrizes de adjacência (Listas de adjacências)

## (Resolução da Ficha 1)

![alt text](https://github.com/GuiSSMartins/Inteligencia_Artificial_Python/blob/main/Grafo_Ficha1.png?raw=true)

```python
# Criar os nodes
class Node:
  # Construtor do nodo......
  def __init__(self, name):
    self.m_name = str(name)
    # Colocar objeto que o nodo vai referenciar, pode ser qualquer coisa !!!!!!!!!!!!!!
  
  def __str__(self):
    return "node " + self.m_name
  
  def __repr__(self):
    return "node " + self.m_name
  
  def __getName__(self):
    return self.m_name
    
   def __setName(self, name):
    self.m_name=name
    
  def __eq__(self, other)
    # são iguais se nome igual, senão 
```

```python
# Importar a classe nodo
from nodo import Node

class Graph:
  # Construtor da classe
  def __init__(sefl, directed=False): # Grafo NÃO-Orientado (As arestas não têm sentido)
    self.m_nodes = [] # lista de nodos do grafo
    self.m_directed = directed # se o grafo é direcionado ou não
    self.m_graph = {} # diconário para armazenar os nodos, arestas e pesos
    self.m_h = {} # dicionário para posteriormente armazenar as heurísticas para cada nodo, usado na pesquisa informada
  
  # Escrever grafo como String
  def __str__(self):
    out = ""
    for
  
  # Adicionar aresta no grafo, com peso
  def add_edge(self, node1, node2, weight): # node1 e node2 são os nomes de cada nó
    n1 = Node(node1) # cria um objeto com o nome dado
    n2 = Node(node2) # cria um objeto com o nome dado
    if (n1 not in self.m_nodes):
      self.m_nodes.append(n1)
      self.m_graph[node1] = set()
    else:
      n1 = self.get_node_by_name(node1)
    
    if (n2 not in self.m_nodes):
      self.m_nodes.append(n2)
    else:
      n2 = self.get_node_by_name(node2)
      
    self.m_graph[node1].add((node2, weight))
    
    # se o grafo for Não-direcionado, colocar a aresta inversa
    if not self.m_directed:
      self.m_graph[node2] = set()
      self.m_graph[node2].add((node1, weight))
    
  # Encontrar nodo 
```

### Exemplo de grafo

def main():

g = graph

------------------------------------------------------

## Dicionários

O _Dicionário_ corresponde a uma tabela que mapeia um tipo de objectos (a chave) noutro (o valor). 

A chave tem de ser de um tipo imutável (string, número ou tuplo). O valor pode ser de qualquer tipo.

Um _Dicionário_ é uma tabela _hash_ em que não existe uma ordem das chaves.

```python
# Criar e Aceder a dados de um DIcionário
>>> estudantes = {19777: 'Pedro', 20200: 'Liza', 21999: 'Zanga'}
>>> estudantes[19777] # 'Pedro'

# Modificar valor de uma chave do Dicionário
>>> estudantes[20202]='Chico'
>>> estudantes # {19777: 'Pedro', 21999: 'Zanga', 20202: 'Chico'}

# Devolve uma lista com TODAS as CHAVES do Dicionário
>>> list(estudantes.keys()) # [19777, 21999, 20202]

# Devolve uma lista com TODOS os VALUES do Dicionário
>>> list(estudantes.values()) # ['Pedro', 'Zanga', 'Chico']

# Devolve uma lista dos pares do Dicionário
>>> estudantes.items() # dict_items([(19777, 'Pedro'), (21999, 'Zanga'), (20202, 'Chico')])

# Apagar elemento de um Dicionário
>>> del estudantes[20200]
>>> estudantes # {19777: 'Pedro', 21999: 'Zanga'}

#--------------
#    EXTRA    -
#--------------

# Criar dicionários de dicionários

>>> professores = {'iia': 'LuigiLuis','ec': 'Lou'}�
>>> staff = {'professores': professores, 'estudantes':estudantes}
>>> staff # {'professores': {'iia': 'LuigiLuis', 'ec': 'Lou'}, 'estudantes': {19777: 'Pedro', 21999: 'Zanga', 20202: 'Chico'}}
>>> staff['professores'] # {'iia': 'LuigiLuis', 'ec': 'Lou'}

```
