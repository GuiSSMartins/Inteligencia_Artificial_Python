
### ATENÇÃO: deve-se colocar . (ponto final) em factos e regras
### Pode-se colocar ; (ponto e vírgula) quando queremos que o programa procure por várias alternativas

__FACTOS__ : rio(minho). -> Minho é um rio
             
             pai(pedro, raquel). -> Pedro é PAI da Raquel

__REGRAS__ : neto(N,A):- filho(N,P),(descendente(P,A,_); descendente(P,_,A)).  ->  Dizer que "N é neto de A" é o mesmo que dizer que "N é filho de P" e que "P é descendente de A"

__QUESTÕES__ : 

?-pai(P, raquel). -> P é pai da raquel? (não é dado resposta)

?-pai(pedro, raquel).

?-neto(rui, A).

?-localizacao(madrid,espanha).   yes  ->  Madrid é uma localização de Espanha?  SIM.

?-atravessa(mondego,coimbra).  no     ->  O rio Mondego atravessa Coimbra? NÃO.

---------------------------------------
```prolog
?-localizacao(X,espanha).
X=madrid <cr>
yes
  
?- atravessa(tejo,C).
C=lisboa  <cr>
yes

?-localizacao(X,Y).
X=porto Y=portugal <cr>
yes

?-localizacao(X,portugal),atravessa(R,X).
X=porto R=douro <cr>
yes

% E se fossem pedidas alternativas com o ; ?

?-localizacao(X,portugal),atravessa(R,X).
X=porto R=douro ;
X=lisboa R=tejo ;
X=caminha R=minho

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
```
--------------------------------------------
