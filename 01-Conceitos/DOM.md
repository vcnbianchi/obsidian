---
aliases:
  - Document Object Model
  - Árvore DOM
tags:
  - html
  - javascript
  - web-dev
  - frontend
references:
  - "[[Documentação - Next.js]]"
---
O **DOM (*Document Object Model*)** é a representação em memória, estruturada como uma árvore de objetos, que o navegador constrói ao ler e interpretar um arquivo [[HTML]].
## Do [[HTML]] à Árvore de Objetos

Quando um usuário acessa uma página web, o servidor retorna um documento [[HTML]]. O navegador faz o *parsing* dessa marcação e traduz cada elemento em um objeto na árvore DOM, que passa a ser a base para a renderização na tela.

![[learn-html-and-dom.avif]]
## Manipulação via [[JavaScript]]

Através dos métodos da API do DOM em [[JavaScript]], é possível escutar eventos do usuário e manipular a interface dinamicamente, selecionando, criando, atualizando ou removendo nós, além de alterar seu conteúdo e estilo.

O exemplo abaixo cria e injeta um cabeçalho `<h1>` diretamente no DOM seguindo [[Programação Imperativa]]:

```html
<body>
  <div id="app"></div>
  <script type="text/javascript">
    const app = document.getElementById('app');
    const header = document.createElement('h1');
    const text = 'Develop. Preview. Ship.';
    const headerContent = document.createTextNode(text);

    header.appendChild(headerContent);
    app.appendChild(header);
  </script>
</body>
```
## Trade-offs da Manipulação Direta

- **Controle granular:** atuar diretamente sobre os métodos do DOM dispensa abstrações externas em scripts simples.
- **Baixa escalabilidade em UIs complexas:** descrever manualmente cada passo de atualização torna o código verboso e propenso a inconsistências de estado. Por isso, bibliotecas baseadas em [[Programação Declarativa]] como o [[React]] (via `react-dom`) abstraem a manipulação direta do DOM.