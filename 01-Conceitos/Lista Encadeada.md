---
aliases:
  - Linked List
tags:
  - data-structures
  - computer-science
references:
  - "[[Livro - Entendendo Algoritmos]]"
---
Uma **Lista Encadeada** (*Linked List*) armazena elementos em qualquer endereço disponível da memória RAM, conectando-os através de **ponteiros** (cada nó guarda o valor do item e o endereço de memória do próximo elemento).
## Comportamento na Memória e Trade-offs

- **Inserção e Remoção Rápidas:** Para adicionar ou remover um item, nunca é necessário mover dados na memória; basta alterar o endereço para o qual o ponteiro do nó anterior aponta.
- **Leitura Sequencial Obrigatória:** Não é possível pular direto para o índice `i` porque os endereços são espalhados. Para ler o último item, é obrigatório percorrer todos os ponteiros desde o primeiro nó ($O(n)$).
## Complexidade de Operações

- **Leitura:** $O(n)$ (Acesso sequencial).
- **Inserção / Remoção** (tendo o ponteiro do nó): $O(1)$.