# Ficha 3 - Algoritmos Maximin

__Maiores dificuldades__: transformar o probelma num GRAFO.

(Resolução Ficha Prática nº3)

- Capacidade do B1 (Balde 1): 4 litros 
- Capacidade do B2 (Balde 2): 3 litros

Estado objetivo: uma das jarras tem de ficar com 2 litros.

(ver na folha à parte, a construção do grafo característico deste problema)




### Código

```python
# Problema dos baldes: dois baldes  a-> 4 litros e b -> 3 litros
# Começar do estado (0,0)  e chegar a (2,0)
# estados possiveis-> tuplos com qualquer combinaçao (x,y) pertencendo  x e y {0,1,2,3,4}

# Ações
# - encher totalmente um balde
# - esvaziar totalmente um balde
# - despejar um balde no outro ate que o ultimo fique cheio
# - despejar um balde no outro ate que o primeiro fique vazio

# Necessário modelar o problema como um grafo


from nodo import Node
from Graph import Grafo
from queue import Queue

class Balde():

    # start deve ser a capacidade dos dois baldes no inicio ex (0,0) "estado inicial"
    # goal deve ser o objectivo ex (2,0).  " estado final"
    # os estados são representados por "(x,y)" como string, em que x e y representam as quantidades de agua nos jarros

    def __init__(self, start="(0,0)", goal="(2,0)", cap1=4, cap2=3):
        self.g=Grafo(directed=True)
        self.start=start
        self.goal=goal
        self.balde1=cap1   # capacidade do balde 1
        self.balde2=cap2   # capacidade do balde 2

    # Partindo do estado inicial, utilizando as ações possíveis como transições construir o grafo
    def cria_grafo(self):
        # Criar um grafo partindo do estado inicial
        # com todasas transições posiveis

    # Dado um estado, expande para outros mediante as açoes possiveis
    def expande(self,estado):
        # To do...

    # Devolve o estado resultante de esvaziar o primeiro balde
    def esvazia1(self, nodo):
        # To do...

    # Devolve o estado resultante de esvaziar o segundo balde
    def esvazia2(self, nodo):
        # To do...

    # Devolve o estado resultante de encher totalmente o primeiro balde da torneira
    def enche1(self, nodo):
        # To do...

    # Devolve o estado resultante de encher totalmente o segundo balde da torneira
    def enche2(self, nodo):
        # To do...


    # Devolve o estado resultante de despejar o balde 1 no balde 2
    def despeja12(self, nodo):
        # To do...


    # Devolve o estado resultante de despejar o balde 2 no balde 1
    def despeja21(self, nodo):
        # To do...

    # Encontra a solução utilizando DFS (recorre à classe grafo e node implementada antes
    def solucaoDFS(self,start,goal):
        # To do...

    # Encontra a solução utilizando BFS (recorre à classe grafo e node implementada antes
    def solucaoBFS(self,start,goal):
        return self.g.procura_BFS(start,goal)

    # Greedy - necessita de heuristica
    def solucaoGreedy(self,start, goal):
        return self.g.greedy(start,goal)

    # A* - necessita de heuristica
    def solucaoAStar(self, start, goal):
        # To do...

    # Outra solução - procura caminho à medida que constrói o grafo
    def encontraDFS(self,start,end, visitados=[], caminho=[]):
        # To do...

    ##################################################################################
    # Dados dois estados e1 e e2, devolve a ação que origina a transição de e1 para e2
    ##################################################################################
    def mostraA(self,e1,e2):
        # To do...

    ########################################################
    # Imprimir sequência de ações para um caminho encontrado
    ########################################################
    def imprimeA(self,caminho):
  
  
  
class main():

  problema = Balde()
  problema.cria_grafo()
  
  # Tratamos os estados como Strings
