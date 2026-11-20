---
aliases:
  - Busca Simples
  - Busca Linear
  - Linear Search
  - Busca Sequencial
tags:
  - algorithms
  - algo-search
  - computer-science
references:
  - "[[Livro - Entendendo Algoritmos]]"
---
A **Busca Simples** (formalmente conhecida como **Busca Linear** ou **Sequencial**) é o algoritmo de busca mais elementar: ele inspeciona cada elemento da coleção, um por um, do início ao fim, até encontrar o item desejado ou atingir o final da estrutura.
## Quando utilizar (Trade-offs vs. [[Busca Binária]])

- **Coleções não ordenadas:** Ao contrário da [[Busca Binária]], a Busca Simples **não exige que os dados estejam ordenados**. Se você só precisa fazer uma única busca em um [[Array]] bagunçado, rodar uma Busca Simples ($O(n)$) é mais rápido do que ordenar o array primeiro ($O(n \log n)$) para depois aplicar a Busca Binária.
- **Estruturas sem acesso aleatório:** É o único método de busca viável em uma [[Lista Encadeada]] padrão, já que a ausência de índices contíguos na memória obriga a percorrer os ponteiros sequencialmente.
## Funcionamento Passo a Passo

1. Comece no primeiro elemento da estrutura (`índice = 0` ou `nó = cabeça`).
2. Compare o elemento atual com o `item` buscado:
   - Se for igual, retorne a posição atual.
   - Se for diferente, avance para o próximo elemento.
3. Se chegar ao fim da estrutura sem encontrar o valor, retorne nulo/inexistente.

## Complexidade ([[Notação Big O]])

- **Tempo (Pior Caso):** $O(n)$. Se a lista tiver $n$ elementos e o item estiver na última posição (ou não existir), o algoritmo fará exatamente $n$ verificações. Em uma lista de $1$ bilhão de itens, são até $1$ bilhão de operações (contra apenas $30$ na [[Busca Binária]]).
- **Tempo (Melhor Caso):** $O(1)$. O item buscado é justamente o primeiro da lista.
- **Espaço:** $O(1)$. Não aloca memória extra proporcional à entrada.