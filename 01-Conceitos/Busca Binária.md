---
aliases:
  - Binary Search
tags:
  - algorithms
  - algo-search
  - computer-science
references:
  - "[[Livro - Entendendo Algoritmos]]"
---
A **Busca Binária** é um algoritmo de busca que encontra a posição de um item dividindo repetidamente a metade da lista que pode conter o elemento, até reduzir as localizações possíveis a apenas uma.

>[!warning] Pré-requisito
>A coleção de dados **precisa estar ordenada** e suportar acesso aleatório (como um [[Array]]). Se a lista não estiver ordenada, o algoritmo falha.

## Algoritmo

1. Defina dois ponteiros de índice: `baixo = 0` e `alto = tamanho - 1`.
2. Enquanto `baixo` for menor ou igual a `alto`:
   - Calcule o índice central: `meio = (baixo + alto) / 2` (arredondado para baixo).
   - Inspecione o `chute = lista[meio]`.
   - Se `chute == item`, retorne `meio`.
   - Se `chute > item` (muito alto), descarte a metade superior: `alto = meio - 1`.
   - Se `chute < item` (muito baixo), descarte a metade inferior: `baixo = meio + 1`.
3. Se o laço terminar sem retorno, o item não existe na coleção.

## Complexidade

- **Tempo (Pior Caso):** $O(\log n)$. Em uma lista de $1.024$ elementos, exige no máximo $\log_2(1024) = 10$ verificações (contra $1.024$ na [[Busca Simples]]).
- **Espaço:** $O(1)$ na versão iterativa.