# Ficha 3 - Transformação dos Problemas em GRAFOS

__Maiores dificuldades__: transformar o problema num GRAFO.

(Resolução Ficha Prática nº3)

- Capacidade do B1 (Balde 1): 4 litros 
- Capacidade do B2 (Balde 2): 3 litros

Estado objetivo: uma das jarras tem de ficar com 2 litros.

(ver na folha à parte, a construção do grafo característico deste problema)




### Código

```python
# Conversão de um mapa de um ficheiro num grafo

# 1º - construir a matriz do mapa
def lerFicheiroMapaMatriz():
    ficheiro = open("circuito.txt")
    mapa = ficheiro.readlines()
    return mapa

# 2º - 
def criarGrafoMapa (mapa)

```

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
        self.g=Grafo(directed=True) # é um grafo DIRECIONADO, pois não podemos voltar uma ação para trás
        self.start=start
        self.goal=goal
        self.balde1=cap1   # capacidade do balde 1
        self.balde2=cap2   # capacidade do balde 2

    # Partindo do estado inicial, utilizando as ações possíveis como transições construir o grafo
    def cria_grafo(self):
        # Criar um grafo partindo do estado inicial, com todas as transições posiveis
        estados = []
        estados.append(self.start)
        visitados = []
        visitados.append(self.start)
        
        while estados != [] :
            estado = estados.pop()
            expansao = self.expande(estado)
            for e in expansao:
                self.g.add_edge(estado,e,1) # 1 -> custo
                if e not in visitados:
                    estados.append(e)
                    visitados.append(e)
            
            
        for e in self.g.getNodes():
            self.g.add_heuristica()

    # Dado um estado, expande para outros mediante as açoes possiveis
    def expande(self,estado):
        lista=[]
        # ver as capacidades ATUAIS
        cap1 = int(estado[1])
        cap2 = int(estado[3]) # vírgula é o 2
        
        if cap1 > 0:
            lista.append(self.esvazia1(estado))
        if cap2 > 0:
            lista.append(self.esvazia2(estado))
        if cap1 + cap2 <= self.balde1:
            lista.append(self.despeja21(estado))
        if cap1 + cap2 <= self.balde2:
            lista.append(self.despeja12(estado))
        if cap1 < self.balde1:
            lista.append(self.enche1(estado))
        if cap2 < self.balde2:
            lista.append(self.enche2(estado))
        
        return lista

    # Devolve o estado resultante de esvaziar o primeiro balde
    def esvazia1(self, nodo):
        res = "(0," + nodo[3] + ")"
        return res

    # Devolve o estado resultante de esvaziar o segundo balde
    def esvazia2(self, nodo):
        res = "(" + nodo[1] + ",0)"
        return res

    # Devolve o estado resultante de encher totalmente o primeiro balde da torneira
    def enche1(self, nodo):
        res = "(" + str(cap1) + "," + nodo[3] + ")"
        return res

    # Devolve o estado resultante de encher totalmente o segundo balde da torneira
    def enche2(self, nodo):
        res = "(" + nodo[1] + "," + str(cap2) + ")"
        return res

    # Devolve o estado resultante de despejar o balde 1 no balde 2
    def despeja12(self, nodo):
        cap1 = int(nodo[1])
        cap2 = int(nodo[3]) # 2 é a vírgula, 0 é ( , 4 é )
        if cap1 + cap2 <= self.balde2:
            cap2 = cap1 + cap2
            cap1 = 0
        else:
            falta2 = self.balde2 - cap2
            cap2 = self.balde2
            cap1 = cap1 - falta2
        res = "(" + str(cap1) + "," + str(cap2) + ")"
        return res

    # Devolve o estado resultante de despejar o balde 2 no balde 1
    def despeja21(self, nodo):
        cap1 = int(nodo[1])
        cap2 = int(nodo[3]) # 2 é a vírgula, 0 é ( , 4 é )
        if cap1 + cap2 <= self.balde1:
            cap1 = cap1 + cap2
            cap2 = 0
        else:
            falta1 = self.balde1 - cap1
            cap1 = self.balde1
            cap2 = cap2 - falta1
        res = "(" + str(cap1) + "," + str(cap2) + ")"
        return res

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

    # Encontra a solução utilizando DFS (recorre à classe grafo e node implementada antes
    def solucaoDFS(self,start,goal):
        res=self.g.procura_DFS(start,goal,path=[], visited=set())
        return (res)

    # Encontra a solução utilizando BFS (recorre à classe grafo e node implementada antes
    def solucaoBFS(self,start,goal):
        return self.g.procura_BFS(start,goal)

    ##################################################################################
    # Dados dois estados e1 e e2, devolve a ação que origina a transição de e1 para e2
    ##################################################################################
    def mostraA(self,e1,e2):
        e1_x = int(str(e1)[1])
        e1_y = int(str(e1)[3])
        e2_x = int(str(e2)[1])
        e2_y = int(str(e2)[3])

        if e1_x> 0 and e2_x==0 and e1_y==e2_y:
            # Despejar balde1
            return "Despejar balde 1"
        elif e1_y> 0 and e2_y==0 and e1_x==e2_x:
            # Despejar balde2
            return "Despejar balde2"
        elif e1_y==e2_y and e1_x<e2_x:
            # Encher balde 1
            return "Encher balde 1"
        elif e1_x==e2_x and e1_y < e2_y:
            # Encher balde 2
            return "Encher balde 2"
        elif e1_x > e2_x and e2_y > e2_x:
             # Despejar balde 1 no balde 2
            return "Despejar balde 1 no balde 2"
        elif e2_x > e1_x and e1_x < e2_x:
             # Despejar balde 2 no balde 1
            return "Despejar balde 2 no balde 1"

    ########################################################
    # Imprimir sequência de ações para um caminho encontrado
    ########################################################
    def imprimeA(self,caminho):
        lista_acoes=[]
        i=0
        while i+1 < len(caminho):
            lista_acoes.append(self.mostraA(caminho[i], caminho[i+1]))
            i=i+1
        return lista_acoes
  

def main(): # Todos os estados são feitos como STRINGS

    problema=Balde()
    problema.cria_grafo()
    saida = -1

    while saida != 0:
        print("1-Imprimir grafo ")
        print("2-Desenhar Grafo")
        print("3-Imprimir  nodos de Grafo")
        print("4-Imprimir arestas de Grafo")
        print("5-DFS")
        print("6-BFS")
        print("7 -Outra solução ")
        print("0-Saír")

        saida = int(input("introduza a sua opcao-> "))
        if saida == 0:
            print("saindo.......")
        elif saida == 1:
            print(problema.g.m_graph)
            l=input("prima enter para continuar")
        elif saida == 2:
            problema.g.desenha()
        elif saida == 3:
            print(problema.g.m_graph.keys())
            l = input("prima enter para continuar")
        elif saida == 4:
            print(problema.g.imprime_aresta())
            l = input("prima enter para continuar")
        elif saida == 5:
            inicio=input("Nodo inicial->")
            fim = input("Nodo final->")
            caminho=problema.solucaoDFS( inicio, fim)
            print(caminho)
            if caminho != None:
               a = caminho[0]
               lista=problema.imprimeA(a)
               print(lista)
            l = input("prima enter para continuar")
        elif saida == 6:
            inicio = input("Nodo inicial->")
            fim = input("Nodo final->")
            caminho=problema.solucaoBFS(inicio,fim)
            print(caminho)
            if caminho != None:
                a = caminho[0]
                lista = problema.imprimeA(a)
                print(lista)
            l = input("prima enter para continuar")
        elif saida == 7:
            inicio = input("Nodo inicial->")
            fim = input("Nodo final->")
            caminho = problema.encontraDFS(inicio, fim)
            print(caminho)
            if caminho != None:
                a = caminho[0]
                lista = problema.imprimeA(a)
                print(lista)
            l = input("prima enter para continuar")
        else:
            print("you didn't add anything")
            l = input("prima enter para continuar")

if __name__ == "__main__":
    main()
