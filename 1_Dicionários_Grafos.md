# Algoritmos sobre prafos em Python

Os grafos em _python_ são represenatdos por _Dicionários_ (explicação no final deste _md_)



------------------------------------------------------

## Dicionários

O _Dicionário_ corresponde a uma tabela que mapeia um
tipo de objectos (a chave) noutro (o valor). 

A chave tem de ser de um tipo imutável (string, número ou tuplo). O
valor pode ser de qualquer tipo.

Um _Dicionário_ é uma tabela _hash_ em que não existe uma ordem das chaves.

```python
# Criar e Aceder a dados de um DIcionário
>>> estudantes = {19777: 'Pedro', 20200: 'Liza', 21999: 'Zanga'}
>>> estudantes[19777] # 'Pedro'

# Modificar valor de uma chave do Dicionário
>>> estudantes[20202]='Chico'
>>> estudantes # {19777: 'Pedro', 21999: 'Zanga', 20202: 'Chico'}

# Devolve uma lista dos pares do Dicionário
>>> estudantes.items() # dict_items([(19777, 'Pedro'), (21999, 'Zanga'), (20202, 'Chico')])

# Apagar elemento de um Dicionário
>>> del estudantes[20200]
>>> estudantes # {19777: 'Pedro', 21999: 'Zanga'}
```
