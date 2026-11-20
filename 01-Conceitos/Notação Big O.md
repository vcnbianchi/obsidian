---
aliases:
  - Big O
  - Complexidade de Tempo
  - Complexidade Algoritmica
tags:
  - algorithms
  - computer-science
  - math
references:
  - "[[Livro - Entendendo Algoritmos]]"
---
A **Notação Big O** descreve a rapidez com que o tempo de execução (ou consumo de memória) de um algoritmo cresce à medida que o tamanho da entrada ($n$) aumenta.

- **Foco em operações, não em segundos:** Ela não mede o tempo em milissegundos (que depende do hardware), mas sim a **taxa de crescimento do número de operações**.
- **Análise de Pior Caso:** Por padrão, o Big O expressa a garantia de limite superior, isto é, a pior situação possível para aquele algoritmo.

## Principais Ordens de Complexidade

| Notação | Nome | Exemplo Clássico | Operações p/ $n = 128$ |
| :--- | :--- | :--- | :---: |
| $O(1)$ | Tempo Constante | Acesso por índice em [[Array]] | $1$ |
| $O(\log n)$ | Tempo Logarítmico | [[Busca Binária]] | $7$ |
| $O(n)$ | Tempo Linear | [[Busca Simples]] | $128$ |
| $O(n \log n)$ | Linearítmico | [[Quicksort]] (caso médio) | $896$ |
| $O(n^2)$ | Tempo Quadrático | [[Selection Sort]] | $16.384$ |
| $O(n!)$ | Tempo Fatorial | Problema do Caixeiro Viajante | $3,85 \times 10^{215}$ |