
__FACTOS__ : rio(minho) -> Minho é um rio
             pai(pedro, raquel) -> Pedro é PAI da Raquel

__REGRAS__ : neto(N,A):- filho(N,P),(descendente(P,A,_);  ->  
descendente(P,_,A)).

__QUESTÕES__ : 
?-pai(P, raquel). -> P é pai da raquel?
?-pai(pedro, raquel).
?-neto(rui, A).
