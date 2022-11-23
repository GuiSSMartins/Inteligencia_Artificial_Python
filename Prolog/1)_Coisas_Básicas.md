
### ATENÇÃO: deve-se colocar . (ponto final) em factos e regras
### Pode-se colocar ; (ponto e vírgula) quando queremos que o programa procure por várias alternativas
### MAIUSCULAS -> X -> Variáveis (podem tomar qualquer valor)
### Ver sempre as Bases de Conhecimento

__FACTOS__ : rio(minho). -> Minho é um rio
             
             pai(pedro, raquel). -> Pedro é PAI da Raquel

__REGRAS__ : neto(N,A):- filho(N,P),(descendente(P,A,_); descendente(P,_,A)).  ->  Dizer que "N é neto de A" é o mesmo que dizer que "N é filho de P" e que "P é descendente de A e de outra pessoa"

:- -> símbolo das regras (lado direito -> condições da regra)

, -> Conjunção (e) de regras

; -> disjunção (ou) de regras (Costuma ser RATOEIRA nos Testes)



__QUESTÕES__ : 

?-pai(P, raquel). -> P é pai da raquel? (não é dado resposta)

?-pai(pedro, raquel).

?-neto(rui, A).

?-localizacao(madrid,espanha).   yes  ->  Madrid é uma localização de Espanha?  SIM.

?-atravessa(mondego,coimbra).  no     ->  O rio Mondego atravessa Coimbra? NÃO.

---------------------------------------
```prolog
% As respostas vão estar no X (mostra todas respostas quando apresenta o "yes")

?-localizacao(X,espanha).
X=madrid <cr>
yes
  
?- atravessa(tejo,C).
C=lisboa  <cr>
yes

?-localizacao(X,Y).
X=porto Y=portugal <cr>
yes

?-localizacao(X,portugal),atravessa(R,X). % , vígula -> conjunção
X=porto R=douro <cr>
yes

% E se fossem pedidas alternativas com o ; ?

?-localizacao(X,portugal),atravessa(R,X). % Mostram-se todas as respostas à questão
X=porto R=douro ;
X=lisboa R=tejo ;
X=caminha R=minho
yes

?-localizacao(X,portugal);localizacao(X,espanha).
X=porto <cr>
yes

% E se fossem pedidas alternativas com o ; ?

?-localizacao(X,portugal);localizacao(X,espanha).
X=porto ;
X=lisboa ;
X=coimbra ;
X=caminha ;
X=madrid ;
X=barcelona ; 
X=zamora ;
X=orense ;
X=toledo
yes

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% not - NEGAÇÃO

?-not(localizacao(porto,portugal)).
no

?-not(atravessa(mondego,coimbra)).
yes


```
--------------------------------------------

### Exemplos de regras

```prolog
filho(X,Y):-homem(X),
(descendente(X,Y,_);descendente(X,_,Y)).

potência(_,0,1):-!. % cut -> quando chegar a esta condição, deve parar a procura
potência(X,N,P):- N1 is N-1,
                  potência(X,N1,P1),
                  P is X*P1.

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

a :- b. 
b :- c. 
c :- d. 

Resposta paar a questão -a    ->    b.

```

--------------------------------------------

```prolog
rio_português(R):-atravessa(R,C),localizacao(C,portugal).
mesmo_rio(C1,C2):-atravessa(R,C1),atravessa(R,C2),C1\==C2.

?-rio_português(Rio). %Mostra todas respostas possíveis à questão (Rio -> MAIUSCULAS)
Rio=douro
yes

% Na chamada à regra, do lado esquerdo, Rio e R atravessam a ser a mesma variável atravessa(R,C) tem sucesso com R=douro e C=porto
% A chamada seguinte já é feita com C já instanciada com porto, na prática essa chamada é feita como sendo localizacao(porto,portugal)
% Quando se atinge o ponto a regra tem sucesso
```

-----------------------------------------------

### Predicado _cut_

Quando não é necessário encontrar todas as soluções possíveis pode ser usar o predicado cut: !
Permite indicar ao prolog objetivos já satisfeitos e que não precisam ser reconsiderados no processo de backtracking

```prolog
% EXEMPLOS

a1(X, Y) :- b(X), c(Y). 

b(1). 
b(2). 
b(3).
 
c(1). 
c(2). 
c(3). 

a1(X,Y).
X = Y, Y = 1 ;
X = 1, Y = 2 ;
X = 1, Y = 3 ;
X = 2, Y = 1 ;
X = Y, Y = 2 ;
X = 2, Y = 3 ;
X = 3, Y = 1 ;
X = 3, Y = 2 ;
X = Y, Y = 3.

------------------------

% Quando encontrar uma solução para X, mostra as soluções restantes Y, mas pará depois imediatamente a procura
a2(X, Y) :- b(X), !, c(Y). 

b(1). 
b(2). 
b(3).
 
c(1). 
c(2). 
c(3). 

a2(X,Y).
X = Y, Y = 1 ;
X = 1, Y = 2 ;
X = 1, Y = 3.
```
N+1 __Não__ é um Incremento.

### Operadores Lógicos
- , para a conjunção
- ; para a disjunção
- not para a negação

```prolog
% Exemplo
a.
b.
c:-fail. /* origina uma falha */
d.

% Questões:
?- a.
yes
?- c.
no
?- not(a).
no
?- not(c).
yes
?- a,b.
yes
?- a,c.
no
?- a;c.
yes
?- (a,c);(not(a);b).
yes
```

### Operadores Aritméticos e Relacionais (ATENÇÃO: letras MAIUSCULAS - são VARIAVEIS)
- Adição 				X + Y
- Subtracção 			X - Y
- Multiplicação 			X * Y
- Divisão 				X / Y
- Divisão inteira 			X // Y
- Resto da divisão inteira 		X mod Y
- Potência 				X ^ Y
- Simétrico 				- X

- Igualdade 		X==Y
- Diferença 		X\==Y
- Maior 			X>Y
- Menor 			X<Y
- Menor ou igual		X=<Y
- Maior ou igual 		X >= Y

### Atribuição
- = para a atribuição simbólica 		X=a (X=Y bidirecional)
- is para a atribuição numérica 		X is 5  (unidirecional)

__ERRO:__ N is N+1

### Recursividade
factorial(0,1):-!. % cut - para devolver valor

factorial(N,F):-N1 is N-1,factorial(N1,F1),F is N*F1.

?-factorial(3,F).
F = 6

### LISTAS
lista vazia: []

notação cabeça-cauda: [H|T]

Não têm de ser do memso tipo: [a,2,abc,[x,1,zzz]]

```prolog
?- [H|T]=[a,b,c,d].
H = a ,
T = [b,c,d]

?- [H|T]=[a,b,X].
H = a ,
T = [b,X] ,
X = _

?- [H|T]=[a].
H = a ,
T = []

?- [H|T]=[[a,b],3,[d,e]].
H = [a,b] ,
T = [3,[d,e]]

?- [H|T]=[].
no
```
### Alteração dinâmica de conhecimento
dynamic predicado/aridade

- asserta, assertz (acrescentar conhecimento)
- retract (retirar conhecimento)

```prolog
:-dynamic figura/2.

figura(hexágono,6).

cria_figuras:- 	assertz(figura(triângulo,3)),
		asserta(figura(quadrado,4)),
		assertz(figura(pentagono,5)).

----------------------------------------------

?- figura(F,NL).
F = hexágono ,
NL = 6

?- cria_figuras.
yes

?- figura(F,NL).
F = quadrado ,
NL = 4 ;

F = hexágono ,
NL = 6 ;

F = triângulo ,
NL = 3 ;

F = pentagono ,
NL = 5
```
