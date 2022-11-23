
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
?-rio_português(Rio). %Mostra todas respostas possíveis à questão (Rio -> MAIUSCULAS)
Rio=douro
yes

% Na chamada à regra, do lado esquerdo, Rio e R atravessam a ser a mesma variável atravessa(R,C) tem sucesso com R=douro e C=porto
% A chamada seguinte já é feita com C já instanciada com porto, na prática essa chamada é feita como sendo localizacao(porto,portugal)
% Quando se atinge o ponto a regra tem sucesso
```
