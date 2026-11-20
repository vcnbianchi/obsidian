---
aliases:
  - JavaScript XML
tags:
  - react
  - javascript
  - web-dev
  - frontend
references:
  - "[[Documentação - Next.js]]"
---
O **JSX (*JavaScript XML*)** é uma extensão de sintaxe para [[JavaScript]] que permite descrever elementos de interface de usuário com uma notação semelhante ao [[HTML]], muito utilizada no [[React]].

Além do conhecimento de [[HTML]] e [[JavaScript]], adotar JSX exige observar três regras específicas.
## As Três Regras do JSX

1. **Retorno de elemento único:** uma função/componente só pode retornar um único elemento raiz. Quando múltiplos elementos irmãos são necessários, envolva-os em um elemento pai (como uma `<div>`) ou em um *Fragment* (`<>...</>`).
2. **Fechamento obrigatório:** todas as tags devem ser explicitamente fechadas, incluindo tags sem filhos (ex: `<Header />`, `<br />`).
3. **`camelCase` na maioria dos atributos:** propriedades e atributos seguem o padrão `camelCase` do [[JavaScript]] e evitam palavras reservadas da linguagem, por exemplo, `className` no lugar de `class`.

## Expressões [[JavaScript]] com Chaves

Em JSX, chaves (`{...}`) permitem transitar entre o domínio de marcação e o domínio [[JavaScript]]. Qualquer **expressão** [[JavaScript]] que produza um valor pode ser embutida dentro de chaves — tanto no conteúdo de elementos quanto em atributos — e ser avaliada dinamicamente:

- **Variáveis e propriedades:** inserção direta de valores em texto ou atributos (ex.: `<h1>{title}</h1>`).
- **Chamadas de função e métodos de [[Array]]:** transformação de coleções em múltiplos elementos de interface (ex.: `.map()` retornando itens de lista), permitindo alternar repetidamente entre [[JavaScript]] e JSX no mesmo bloco.

```jsx
const title = 'Develop. Preview. Ship.';
const names = ['Ada Lovelace', 'Grace Hopper', 'Margaret Hamilton'];

const page = (
  <div>
    <h1>{title}</h1>
    <ul>
      {names.map((name) => (
        <li>{name}</li>
      ))}
    </ul>
  </div>
);
```

>[!tip] Expressões vs. instruções (*statements*)
>As chaves `{...}` aceitam apenas **expressões** que retornam um valor (como variáveis, operadores ternários e `.map()`), e não instruções imperativas como `for` ou `if/else` diretamente embutidas na marcação.

## Compilação para o Navegador

Navegadores não interpretam JSX nativamente. Executar código contendo marcação como `<h1>Develop. Preview. Ship.</h1>` diretamente em um script [[JavaScript]] gera `Uncaught SyntaxError: Unexpected token '<'`.

Para que o navegador consiga executar o código, é necessário um compilador [[JavaScript]], como o [[Babel]], para transformar o JSX em chamadas JavaScript válidas.

Em um ambiente simples no navegador (sem etapa prévia de build), isso pode ser feito carregando `@babel/standalone` e configurando a tag `<script>`:

- `type="text/babel"`: sinaliza ao [[Babel]] que o bloco precisa ser compilado.
- `data-presets="react"`: habilita a transformação de sintaxe JSX.
- `data-type="module"`: preserva o comportamento de [[ES Modules]] para que instruções `import` continuem funcionando.

```html
<html>
  <head>
    <script type="importmap">
      {
        "imports": {
          "react": "https://esm.sh/react@latest?dev",
          "react-dom/client": "https://esm.sh/react-dom@latest/client?dev",
          "react/jsx-runtime": "https://esm.sh/react@latest/jsx-runtime?dev"
        }
      }
    </script>
    <script src="https://unpkg.com/@babel/standalone@latest/babel.min.js"></script>
  </head>
  <body>
    <div id="app"></div>
    <script type="text/babel" data-type="module" data-presets="react">
      import React from 'react';
      import { createRoot } from 'react-dom/client';

      const domNode = document.getElementById('app');
      const root = createRoot(domNode);
      root.render(<h1>Develop. Preview. Ship.</h1>);
    </script>
  </body>
</html>
```