---
title: Entendendo Algoritmos
subtitle: Um guia ilustrado para programadores e outros curiosos
type:
  - book
author: Aditya Y. Bhargava
tags:
  - algorithms
  - data-structures
  - code
created at: 2026-11-17
updated at: 2026-11-17
---
Um algoritmo é um conjunto de instruções que realizam uma tarefa. O presente livro irá explicar e demonstrar diversos algoritmos essenciais para profissionais da Ciência da Computação, matemáticos ou outros interessados. Os algoritmos exemplares serão escritos em Python mas podem (e devem) ser implementados em outras linguagens de programação.
# Notação Big O

Sempre que falamos em um algoritmo, falamos sobre seu tempo de execução. O que define a escolher de um algoritmo em detrimento do outro é sua eficiência de tempo e espaço. Para exemplificar, podemos fazer a comparação entre dois algoritmos que possuem o mesmo propósito: Pesquisa Simples e Pesquisa Binária.

Enquanto que para uma lista de 1024 elementos, a Pesquisa Simples levaria, no pior caso (Big O), 1024 tentativas, isto é, o número máximo de tentativas, no pior caso, de uma Pesquisa Simples será sempre igual ao tamanho da lista, resultando em um algoritmo de tempo linear. Já a Pesquisa Binária levaria apenas 10, pois é um algoritmo de tempo logarítmico.
# Pesquisa Binária

O algoritmo "Pesquisa Binária" (Busca Binária) trata-se de um algoritmo de busca, assim como o nome sugere. Isto significa que o funcionamento básico do algoritmo é: buscar alguma informação alvo em alguma estrutura de dados, como uma lista, lista encadeada ou até mesmo em um banco de dados, e se encontrada, a localização do alvo é retornada, caso contrário, `None` é retornado.

Existem diversos tipos de algoritmos de busca diferentes, com implementações diferentes. Falando especificamente acerca da Pesquisa Binária, esta possui uma característica marcante: cada iteração elimina metade das possibilidades da lista, desde que a mesma esteja ordenada.
## Exemplo

Suponhamos que o objetivo seja encontrar um número entre 1 a 100 de modo que a cada chute a outra pessoa que sabe o número deve te informar se o número está muito alto ou muito baixo. Caso fôssemos usar a Pesquisa Simples começaríamos do número 1, seguido do número 2, 3, 4, 5 e assim por diante, eliminando apenas um número a cada iteração. 

Na Pesquisa Binária, no entanto, começamos pela metade, isso é, 50. Dessa forma se 50 for muito baixo, sabemos que o número só pode estar entre 51 e 100 descartando 50 números no processo (metade da lista). O mesmo comportamento seria visto caso o contrário fosse verdade, isto é, se o número estivesse muito alto.

A próxima iteração tentaria a metade das possibilidades existentes, isto é, o número 75. Portanto, no pior caso, ao invés de levarmos 100 iterações para descobrir o número correto, levaremos 7.
- Pesquisa Simples: 100, 99, 98, 97, 96, 95, ..., **1**.
- Pesquisa Binária: 100, 50, 25, 13, 7, 4, 2, **1**.
De maneira geral, para uma lista de $n$ números, a Pesquisa Binária precisa de $log_{2}n$ para encontrar o valor correto, enquanto a Pesquisa Simples precisa de $n$ etapas.

>[!note] Logaritmos na Notação Big O
>Usaremos a Notação Big O como métrica para medir o desempenho dos algoritmos, por isso, sempre que falamos em logaritmo e em Big O, consideramos $log$ como sendo $log_{2}$.
## Código

O algoritmo "Pesquisa Binária" pode ser implementado, em Python, da seguinte forma:

```python
def binary_search(array, target):
	idx_start = 0
	idx_end = len(array) - 1
	
	while idx_end <= idx_start:
		idx_mid = (idx_end + idx_start) / 2
		guess = array[idx_mid]
		
		if guess == target:
			return idx_mid
		if guess > target:
			idx_end = guess - 1
		else:
			idx_start = guess + 1
			
	return None
```

