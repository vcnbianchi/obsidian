---
aliases:
  - Imperative Programming
  - Paradigma Imperativo
tags:
  - programming-paradigms
  - computer-science
references:
  - "[[Documentação - Next.js]]"
---
A **Programação Imperativa** é o paradigma em que o desenvolvedor descreve explicitamente a sequência passo a passo de instruções que determinam **como** o computador deve executar uma tarefa ou atualizar o estado do sistema.
## Modelo Mental (vs. [[Programação Declarativa]])

Uma analogia clássica é o preparo de uma pizza: na abordagem imperativa, você dita passo a passo ao chef cada etapa necessária para fazer a pizza; na [[Programação Declarativa]], você apenas pede a pizza desejada sem se preocupar com as instruções internas de preparo.

| Aspecto              |   [[Programação Imperativa]]   |    [[Programação Declarativa]]     |
| :------------------- | :----------------------------: | :--------------------------------: |
| Foco principal       | **Como** fazer (passo a passo) |   **O que** obter (estado final)   |
| Controle da execução |  Explícito pelo desenvolvedor  | Abstraído pela biblioteca/runtime  |
| Exemplo em UI Web    |   Métodos diretos do [[DOM]]   | Componentes e [[JSX]] no [[React]] |
## Exemplo na Construção de Interfaces

Ao atualizar uma página web de forma imperativa, o código precisa localizar o elemento alvo no [[DOM]], instanciar manualmente cada nó, criar o texto e anexar cada elemento na ordem correta:

```javascript
const app = document.getElementById('app');
const header = document.createElement('h1');
const headerContent = document.createTextNode('Develop. Preview. Ship.');

header.appendChild(headerContent);
app.appendChild(header);
```

- **Trade-off:** garante controle direto sobre cada operação, mas tende a ficar verboso e mais difícil de manter conforme o número de estados e interações da interface aumenta, razão pela qual interfaces modernas costumam preferir a [[Programação Declarativa]].