---
aliases:
  - Declarative Programming
  - Paradigma Declarativo
tags:
  - programming-paradigms
  - computer-science
references:
  - "[[Documentação - Next.js]]"
---
A **Programação Declarativa** é o paradigma em que o desenvolvedor descreve **o que** deseja exibir ou obter como resultado, deixando para a linguagem, biblioteca ou *runtime* a responsabilidade de decidir os passos internos necessários para chegar lá.
## Modelo Mental (vs. [[Programação Imperativa]])

Na analogia da pizza, a programação declarativa equivale a pedir a pizza especificando o resultado esperado, sem precisar ditar cada etapa do preparo, em contraste direto com a [[Programação Imperativa]], que detalha o procedimento passo a passo.
## Uso em Interfaces de Usuário ([[React]])

Na construção de interfaces web, a abordagem declarativa costuma acelerar o desenvolvimento e simplificar a manutenção. Em vez de manipular o [[DOM]] manualmente com chamadas sequenciais (`createElement`, `createTextNode`, `appendChild`), bibliotecas declarativas como o [[React]] permitem declarar diretamente o elemento desejado (usando [[JSX]]):

```jsx
root.render(<h1>Develop. Preview. Ship.</h1>);
```

- **Trade-off:** reduz código repetitivo e facilita raciocinar sobre o estado da interface em qualquer instante, em troca de delegar o controle fino das atualizações a uma camada de abstração intermediária.