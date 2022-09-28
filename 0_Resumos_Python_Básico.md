# Resumos PYTHON 
(finalmente, demoraste muito a ficar atual UMinho)

### Comentários
```python
# A revolução no mundo da progarmação
```

## Tópicos básicos de programação

- __Nomes de variáveis__ (_exemplos_): _filho, somaNumeros, jogar_… (lowerCase + HigerCase)
- __Strings__ (_entre aspas simples_ '' OU _duplas_ ""): ‘Miguel', "Miguel", ‘Abraço', '@$%'
- __Inteiros e Reais__: 12,-34, 22342, 13435.24, -2454 ** 0.5
- __Operações matemáticas__: +, -, *, /, % (resto da divisão inteira), ** (potencia)
- __Valores & Operadores Lógicos__: True, False;     ==, !=;      not, and, or

```python
>>> not (1==0)
True

>>> (2==4-2) and (2==3)
False

>>> (2==4-2) or (2==3)
True
```

```python
# Escrever coisas no ecrã
print(10*2) 
```

### Funções uteis para _Strings_
```python
>>> "artificial" + " " + "intelligence"
'artificial intelligence'

>>> 'artificial'.upper()
'ARTIFICIAL'

>>> 'HELP'.lower()
'help'

>>> len('Help') # length - dá o comprimento da String
4

>>> "a-maria-e-o-manel".split('-') # dividir uma string numa lista consoante o caracter recebido
['a', 'maria', 'e', 'o', 'manel']
```

## Estruturas de Dados

### Listas
```python
>>> frutas = ['maçã','laranja','pêra','banana']
>>> frutas[0]
'maçã'
>>> outrasFrutas = ['kivi','morangos']
>>> frutas + outrasFrutas # + para concatenar listas
['maçã', 'laranja', 'pêra', 'banana', 'kivi', 'morangos']
```
