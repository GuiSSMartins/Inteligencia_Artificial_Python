# Resumos PYTHON 
(finalmente, demoraste muito a ficar atual UMinho)

### Comentários
```python
# A revolução no mundo da programação
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

# AVISO - Funções
Nem todas as funções modificam o conteúdo de uma variável. Mostram apenas um resultado!!!!
Se estiver entre parenteses 

### Funções uteis para _Strings_
```python
# Concatenação de Strings
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

# Indexação Negativa para aceder aos elementos pela ordem de trás para a frente.
 
>>> frutas[-1] # com frutas[-1] acede-se ao último elemento
'banana'
>>> frutas[-2]
'pêra'

# obter o último elemento de uma lista depois de ser removido
>>> frutas.pop()
'banana'
>>> frutas
['maçã', 'laranja', 'pêra']

# adicionar coisas no FINAL da lista
>>> frutas.append('uvas')
>>> frutas
['maçã', 'laranja', 'pêra', 'uvas']

# Uso de intervalos de indexação
>>> frutas[0:2]
['maçã', 'laranja']
>>> frutas[:3]
['maçã', 'laranja', 'ananás']
>>> frutas[2:]
['ananás', 'uvas']

>>> frutas.reverse # reverter os elementos da lista
```

### Tuplos
Igual a uma lista mas que é imutável a partir do momento em que é criado, i.e., não pode mudar. 

__ATENÇÃO__: Os tuplos são envolvidos em __parêntesis ()__ enquanto as listas são-no por __parêntesis retos []__ (ou mesmo sem parenteses!!!!!).

```python
>>> par = (3,5)
>>> par[0]
3
>>> outro_par = 5,5 # Na verdade, nem precisamos de parêntesis.
>>> outro_par
(5, 5)

>>> x,y = par
>>> x
3
>>> y
5
```

### Conjuntos (da Matemática Discreta)
É uma lista _não ordenada_ __sem elementos duplicados__.

```python
# COnversão Lista -> Conjunto (função set())
>>> formas = ['círculo','quadrado','triângulo','círculo']
>>> formas = set(formas)
>>> formas
{'triângulo', 'quadrado', 'círculo'}
```
