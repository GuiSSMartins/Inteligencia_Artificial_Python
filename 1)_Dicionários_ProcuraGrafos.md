# 1) Algoritmos Procura (Não-informada/Sem heuristicas) em grafos - _Python_

Os grafos em _python_ são represenatdos por _Dicionários_ (explicação no final deste _md_)

2 representações dos grafos:
- Matrizes de adjacência (Listas de adjacências)

## (Resolução da Ficha 1)

![alt text](https://github.com/GuiSSMartins/Inteligencia_Artificial_Python/blob/main/Grafo_Ficha1.png?raw=true)

Problema:
Estado Inicial:

```python
# Criar os nodes
class Node:
  # Construtor do nodo......
  def __init__(self, name):
    self.m_name = str(name)
    # Colocar objeto que o nodo vai referenciar, pode ser qualquer coisa !!!!!!!!!!!!!!
  
  # Devolve a representação na forma de string do nodo por forma a ser de leitura 'amigável'
  def __str__(self):
    return "node " + self.m_name
  
  # Devolve representação 'oficial' do objeto
  # neste caso particular pode ser igual a __str__
  def __repr__(self):
    return "node " + self.m_name
  
  # Obter o nome de um nodo
  def __getName__(self):
    return self.m_name
  
  # Atualizar o nome de um nodo
  def __setName(self, name):
    self.m_name=name
  
  # Método utilizado para comparar dois nodos
  # neste caso, dois nodos são iguais se os nomes forem iguais
  def __eq__(self, other):
    # são iguais se nome igual, não usa o id
    return self.m_name == other.m_name
  
  # Devolve o hash de um nodo.
  # Ao implementar o método __eq__ torna-se também necessário definir __hash__.
  # Caso contrário o objeto torna-se unhashable
  def __hash__(self):
      return hash(self.m_name)
```

## Construção de Grafos + Funções de manipulação

```python
# Importar a classe nodo
from nodo import Node

import networkx as nx
import matplotlib.pyplot as plt

class Graph:
  # Construtor da classe
  def __init__(sefl, directed=False): # Grafo NÃO-Orientado (As arestas não têm sentido)
    self.m_nodes = [] # Lista de nodos do grafo
    self.m_directed = directed # se o grafo é direcionado ou não
    self.m_graph = {} # Diconário para armazenar os nodos, arestas e pesos
    self.m_h = {} # Dicionário para posteriormente armazenar as heurísticas para cada nodo, usado na pesquisa informada
  
  # Escrever grafo como String
  def __str__(self):
      out = ""
      for key in self.m_graph.keys():
          out = out + "node " + str(key) + ": " + str(self.m_graph[key]) + "\n"
      return out
  
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
  def get_node_by_name(self, name):
    search_node = Node(name)
    for node in self.m_nodes:
      if node == search_node:
        return node
      else:
        return None
        
  #####################################
  # Imprimir arestas (!!! plural !!!)
  #####################################
  def imprime_aresta(self)_
    listaA = ""
    for nodo in self.m_graph.keys():
      for (nodo2, custo) in self.m_graph[nodo]:
        listaA = listaA + nodo + " ->" + nodo2 + " custo:" + str(custo) + "\n"
    return listaA
  
  ##############################
  # Devolver o custo da aresta
  ##############################
  def get_arc_cost(self, node1, node2):
    custoT = math.inf # rever algortimo de Dijsktra
    a = self.m_graph[node1] # lista de arestas para aquele nodo
    for (nodo, custo) in a:
      if nodo==node2:
        custoT=custo
    return custoT
  
  ########################################
  # Dado um caminho, calcula o seu custo
  ########################################
  def calcula_custo(self, caminho): # caminho funciona como um array
    # caminho é uma lista de nodos
    teste=caminho
    custo=0
    i=0
    while i+1 < len(teste):
      custo = custo + self.get_arc_cost(teste[i], teste[i+1])
      i=i+1
    return custo
    
  ###############################
  # desenha grafo  modo grafico
  ###############################
  def desenha(self):
      # criar lista de vertices
      lista_v = self.m_nodes
      lista_a = []
      g=nx.Graph()

      #Converter para o formato usado pela biblioteca networkx
      for nodo in lista_v:
          n = nodo.getName()
          g.add_node(n)
          for (adjacente, peso) in self.m_graph[n]:
              lista = (n, adjacente)
              #lista_a.append(lista)
              g.add_edge(n,adjacente,weight=peso)

      #desenhar o grafo
      pos = nx.spring_layout(g)
      nx.draw_networkx(g, pos, with_labels=True, font_weight='bold')
      labels = nx.get_edge_attributes(g, 'weight')
      nx.draw_networkx_edge_labels(g, pos, edge_labels=labels)

      plt.draw()
      plt.show()
```
--------------------------------------------------
### Exemplo de grafo
```python
#Importar classes nodo e grafo
from grafo import Graph
from nodo import Node

def main():
    #Criar instância de grafo
    g = Graph()

    #################################
    # Adicionar vertices ao grafo g
    #################################
    g.add_edge("s", "e",2)
    g.add_edge("s", "a",2)
    g.add_edge("e", "f",5)
    g.add_edge("a", "b",2)
    g.add_edge("b", "c", 2)
    g.add_edge("c", "d", 3)
    g.add_edge("d", "t",3)
    g.add_edge("g", "t", 2)
    g.add_edge("f","g",2)

    ######################
    # Cosntrução de menu
    ######################
    saida = -1
    while saida != 0:
        print("1-Imprimir Grafo")
        print("2-Desenhar Grafo")
        print("3-Imprimir  nodos de Grafo")
        print("4-Imprimir arestas de Grafo")
        print("5-DFS")
        print("0-Saír")

        saida = int(input("introduza a sua opcao-> "))
        if saida == 0:
            print("saindo.......")
        elif saida == 1:
            #Escrever o grafo como string
            print(g)
            l=input("prima enter para continuar")
        elif saida == 2:
            #Desenhar o grafo de forma gráfica
            g.desenha()
        elif saida == 3:
            #Imprimir as chaves do dicionario que representa o grafo
            print(g.m_graph.keys())
            l = input("prima enter para continuar")
        elif saida == 4:
            #imprimir todas as arestas do grafo
            print(g.imprime_aresta())
            l = input("prima enter para continuar")
        elif saida == 5:
            #Efetuar  pesquisa de caminho entre nodo inicial e final com DFS
            inicio=input("Nodo inicial->")
            fim = input("Nodo final->")
            print(g.procura_DFS( inicio, fim, path=[], visited=set()))
            l = input("prima enter para continuar")
        else:
            print("Opção inválida...")
            l = input("prima enter para continuar")

if __name__ == "__main__":
    main()
```

-------------------------------------

### Algoritmos de procura/pesquisa em grafos (param quando chegam ao nodo "end")
#### (Trabalho Prático - comparação entre diferentes tipos de algoritmos de pesquisa em grafos)
Devolvem-nos os caminhos para atingir os vários nodos, até que se atinja o nodo final/_"end"_

(Estes algoritmos não nos devolvem garantidamente o melhor caminho; __apenas__ devolve o __1º caminho__)

## -> Procura DFS - Depth First Search (Pesquisa em Profundidade)

```python
# Continuação da classe Graph

###############################################################
# Procura DFS - Depth First Search (Pesquisa em Profundidade)
###############################################################
def procura_DFS(self, start, end, path=[], visited=set()): # path é uma lista (Pode ter Repetidos)
  path.append(start)
  visited.add(start)   # podemos admitir que o start é o vértice atual
  
  # m_graph -> lista de adjacências
  
  if start == end:
    # calcular o custo do caminho; função calcula custo
    custoT = self.calcula_custo(path)
    return (path, custoT)
  for (adjacente, peso) in self.m_graph[start]:
    if adjacente not in visited:
      resultado = self.procura_DFS(adjacente, end, path, visited) # recursivo
      if resultado is not None:
        return resultado
  path.pop() # se não encontra, remover o que está no caminho...
  return None

# Variação com Limitação do nº de ramificações (solução para evitarmos os grafos infinitos)
# (ver slides de IA)

```


![alt text](https://github.com/GuiSSMartins/Inteligencia_Artificial_Python/blob/main/dfs.jpg)



-------------------------------------------------
## -> Procura BFS - Breadth-first search (Pesquisa em largura)

```python
############################################################
# Procura BFS - Breadth-first search (Pesquisa em largura)
############################################################
def procura_BFS(self, start, end):
  # definir nodos visitados para evitar ciclos
  visited = set()
  fila = Queue()
  
  ###################################################
  # adicionar o nodo inicial à fila e aos visitados
  ###################################################
  fila.put(start)
  visited.add(start)
  
  # garantir que o 'start node' não tem pais
  parent = dict()
  parent[start] = None
  
  path_found = False # ainda não encontramos 
  while not fila.empty() and path_found == False:
    nodo_atual = fila.get()
    if nodo_atual == end:
      path_found = True
    else:
      for (adjacente, peso) in self.m_graph[nodo_atual]:
        if adjacente not in visited.
          fila.put(adjacente)
          parent[adjacente] = nodo_atual
          visited.add(adjacente)
    
  # reconstruir o caminho (nestes casos, como queremos que atinja o Nodo FINAL,...
  # 
  path = []
  if path_found:
    path.append(end)
    while parent[end] is not None:
      path.append(parent[end])
```

![alt text](https://github.com/GuiSSMartins/Inteligencia_Artificial_Python/blob/main/Breadth-First-Search-Algorithm.gif)

------------------------------------------------------

## Dicionários

O _Dicionário_ corresponde a uma tabela que mapeia um tipo de objectos (a chave) noutro (o valor). 

A chave tem de ser de um tipo imutável (string, número ou tuplo). O valor pode ser de qualquer tipo.

Um _Dicionário_ é uma tabela _hash_ em que não existe uma ordem das chaves.

```python
#############################################################################
# Criar e Aceder a dados de um Dicionário (Esquerda: KEYS; Direita: VALUES)
#############################################################################
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

####################################################
#    EXTRA -  Criar dicionários de dicionários     -
####################################################

>>> professores = {'iia': 'LuigiLuis','ec': 'Lou'}�
>>> staff = {'professores': professores, 'estudantes':estudantes}
>>> staff # {'professores': {'iia': 'LuigiLuis', 'ec': 'Lou'}, 'estudantes': {19777: 'Pedro', 21999: 'Zanga', 20202: 'Chico'}}
>>> staff['professores'] # {'iia': 'LuigiLuis', 'ec': 'Lou'}

```
