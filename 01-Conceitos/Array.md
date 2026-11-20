---
aliases:
  - Arrays
  - Vetor
  - Vetores
tags:
  - data-structures
  - computer-science
references:
  - "[[Livro - Entendendo Algoritmos]]"
---
Um **Array** armazena uma coleção de elementos de forma **contígua (lado a lado) na memória RAM**.
## Comportamento na Memória e Trade-offs

- **Leitura instantânea (Acesso Aleatório):** Como os elementos estão em endereços sequenciais, o computador calcula a posição exata de qualquer índice instantaneamente (`endereco_base + indice * tamanho_tipo`). Isso permite algoritmos como a [[Busca Binária]].
- **Inserção e Realocação Custosas:** Se o espaço adjacente na memória estiver ocupado por outro programa e o array precisar crescer, é necessário realocar o bloco inteiro para outro endereço livre. Inserir no meio exige deslocar (*shift*) todos os elementos seguintes.
## Complexidade de Operações (vs. [[Lista Encadeada]])

| Operação                    | [[Array]] | [[Lista Encadeada]] |
| :-------------------------- | :-------: | :-----------------: |
| Leitura (Acesso por índice) |  $O(1)$   |       $O(n)$        |
| Inserção (no início/meio)   |  $O(n)$   |       $O(1)$        |
| Remoção (no início/meio)    |  $O(n)$   |       $O(1)$        |