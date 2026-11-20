---
aliases:
  - Selection Sort
  - Ordenação por Seleção
tags:
  - algorithms
  - computer-science
  - algo-selection
references:
  - "[[Livro - Entendendo Algoritmos]]"
---
O **Selection Sort** é um algoritmo de ordenação simples que percorre uma coleção repetidas vezes, selecionando o menor (ou maior) elemento restante a cada passagem e movendo-o para a posição ordenada.
## Por que a complexidade é $O(n^2)$?
1. Na primeira passagem, o algoritmo verifica $n$ elementos para achar o menor.
2. Na segunda passagem, verifica $n - 1$ elementos, depois $n - 2$, até $1$.
3. Embora a média de itens verificados por etapa seja $\frac{1}{2} \times n$ (resultando em $O(n \times \frac{1}{2}n)$), a [[Notação Big O]] **ignora constantes multiplicativas** como $\frac{1}{2}$. Portanto, realizar uma operação $O(n)$ por $n$ vezes resulta em **$O(n^2)$**.