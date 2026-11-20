---
aliases:
  - React.js
  - ReactJS
tags:
  - react
  - javascript
  - web-dev
  - frontend
  - ui
references:
  - "[[Documentação - Next.js]]"
---
O **React** é uma biblioteca [[JavaScript]] baseada em [[Programação Declarativa]] para a construção de interfaces gráficas de usuário (*User Interfaces*) interativas.
## Filosofia e Pacotes Principais

- **Biblioteca não-opinativa:** fornece um conjunto de funções e APIs focadas em UI, sem impor arquitetura de rotas, busca de dados ou infraestrutura. Essa liberdade impulsionou o ecossistema e permitiu o surgimento de frameworks como o [[Next.js]], mas implica maior esforço de configuração ao escalar uma aplicação do zero.
- **Separação de responsabilidades em dois pacotes:**
  - `react`: núcleo da biblioteca (definição de componentes, estado e primitivas de UI).
  - `react-dom`: métodos específicos para integrar o React ao [[DOM]] do navegador.
## Montagem no [[DOM]]

Para conectar o React a uma página [[HTML]], seleciona-se um nó raiz do [[DOM]] com `createRoot()` e renderizam-se os elementos da aplicação com `root.render()`.

Em projetos didáticos ou sem *bundler*, é possível carregar `react` e `react-dom` diretamente de uma [[CDN]] (como `esm.sh`) utilizando [[ES Modules]] (`type="module"`) e [[Import Maps]] (`<script type="importmap">`), mapeando URLs externas para nomes curtos de pacotes:

```html
<html>
  <head>
    <script type="importmap">
      {
        "imports": {
          "react": "https://esm.sh/react@latest?dev",
          "react-dom/client": "https://esm.sh/react-dom@latest/client?dev"
        }
      }
    </script>
  </head>
  <body>
    <div id="app"></div>
    <script type="module">
      import React from 'react';
      import { createRoot } from 'react-dom/client';

      const domNode = document.getElementById('app');
      const root = createRoot(domNode);
      root.render(<h1>Develop. Preview. Ship.</h1>);
    </script>
  </body>
</html>
```

>[!tip] Versão de desenvolvimento (`?dev`)
>O sufixo `?dev` nas URLs da CDN carrega o build de desenvolvimento do React, que exibe avisos e mensagens de erro detalhadas no console do navegador.

>[!warning] Dependência de compilação para [[JSX]]
>O trecho `<h1>Develop. Preview. Ship.</h1>` dentro de `root.render()` não é [[JavaScript]] puro, mas sim [[JSX]]. Para executá-lo diretamente no navegador, é necessário um compilador como o [[Babel]].
## Conceitos Fundamentais

O modelo mental do React apoia-se em três conceitos centrais:

1. **Components** (Componentes)
2. **Props** (Propriedades)
3. **State** (Estado)

### Componentes (*Components*)

Interfaces de usuário podem ser decompostas em blocos menores, independentes e reutilizáveis chamados **componentes**. Como peças de LEGO, cada componente encapsula uma parte específica da interface e pode ser combinado para formar telas completas, se uma parte precisar mudar, atualiza-se apenas o componente responsável.

![[learn-components.avif]]

No React, componentes são **funções [[JavaScript]] que retornam elementos de interface** (escritos em [[JSX]]):

```html
<script type="text/babel" data-type="module" data-presets="react">
  import React from 'react';
  import { createRoot } from 'react-dom/client';

  const domNode = document.getElementById('app');

  function Header() {
    return <h1>Develop. Preview. Ship.</h1>;
  }

  const root = createRoot(domNode);
  root.render(<Header />);
</script>
```

>[!warning] Convenção de nomenclatura
>Nomes de componentes React **sempre** devem começar com letra maiúscula (*PascalCase*, como `Header`), para que o [[JSX]] os diferencie de tags [[HTML]] nativas (escritas em minúsculas, como `<h1>`).

### Propriedades (*Props*)

Assim como elementos [[HTML]] recebem atributos que alteram seu comportamento ou aparência (como `src` em `<img>` ou `href` em `<a>`), componentes React aceitam dados personalizados chamados **props** (*properties*). Como componentes são funções [[JavaScript]], as `props` funcionam de modo análogo a argumentos passados de um componente pai para um componente filho.

![[learn-props.avif]]

Por baixo dos panos, o React agrupa todas as propriedades passadas na chamada de um componente em um único **objeto** [[JavaScript]] entregue como primeiro parâmetro da função. Por isso, é prática idiomática usar **desestruturação de objetos** (*object destructuring*) diretamente na assinatura do componente para nomear explicitamente os valores esperados:

```jsx
function HomePage() {
  return (
    <div>
      <Header title="React" />
    </div>
  );
}

// Recebendo o objeto completo: props === { title: "React" }
function HeaderWithObject(props) {
  return <h1>{props.title}</h1>;
}

// Forma idiomática com desestruturação de objeto
function Header({ title }) {
  return <h1>{title}</h1>;
}
```

A interpolação de valores como `{title}` dentro da marcação ocorre por meio das expressões com chaves do [[JSX]].

>[!tip] Fluxo de dados unidirecional (*One-way data flow*)
>No React, os dados fluem em uma única direção pela árvore de componentes: sempre do componente pai para os componentes filhos por meio de `props`. Quando um componente mantém estado (*state*), esse estado também é propagado para baixo como `props`.

### Renderização de Listas e Propriedade `key`

Quando há uma coleção de dados a ser exibida com a mesma estrutura visual, utilizam-se métodos de [[Array]] do [[JavaScript]] — em especial `.map()` — dentro de expressões [[JSX]] para transformar cada elemento do array em um elemento de interface.

Ao renderizar listas dinamicamente, o React exige que cada item possua uma propriedade especial `key` com valor único entre os irmãos. Sem ela, o React exibe um aviso em desenvolvimento, pois utiliza a `key` para identificar de forma inequívoca qual item corresponde a cada nó no [[DOM]] ao calcular atualizações (reconciliação):

```jsx
function HomePage() {
  const names = ['Ada Lovelace', 'Grace Hopper', 'Margaret Hamilton'];

  return (
    <div>
      <Header title="Develop. Preview. Ship." />
      <ul>
        {names.map((name) => (
          <li key={name}>{name}</li>
        ))}
      </ul>
    </div>
  );
}
```

>[!warning] Escolha de valores para `key`
>Usar o próprio conteúdo textual do item (como `name` acima) só é seguro quando há garantia de unicidade na lista. Em aplicações reais, utilize sempre um identificador estável e garantidamente único para cada registro, como um `id` proveniente do banco de dados ou API.