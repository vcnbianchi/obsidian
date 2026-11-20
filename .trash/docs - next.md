![[learn-props.avif]]Os elementos HTML comuns possuem atributos que podem ser usados ​​para transmitir informações que alteram o comportamento desses elementos. Por exemplo, alterar o `src`atributo de um `<img>`elemento altera a imagem exibida. Alterar o `href`atributo de uma `<a>`tag <a> altera o destino do link.

Da mesma forma, você pode passar informações como propriedades para componentes React. Essas propriedades são chamadas de propriedades `props`. Considere, por exemplo, as possíveis variações de um botão:

Semelhante a uma função JavaScript, você pode criar componentes que aceitam argumentos personalizados (ou props) que alteram o comportamento do componente ou o que é exibido visualmente quando ele é renderizado na tela. Em seguida, você pode passar essas props dos componentes pai para os componentes filhos.

**Observação:** No React, os dados fluem na árvore de componentes. Isso é chamado de _fluxo de dados unidirecional_ . O estado, que será discutido no próximo capítulo, pode ser passado de componentes pai para componentes filhos como props.

Exemplos:

```html
function HomePage() {
  return (
    <div>
      <Header title="React" />
    </div>
  );
}

function Header(props) {
  return <h1>Develop. Preview. Ship.</h1>;
}
```

Se você `console.log()`observar as propriedades (props), verá que se trata de um **objeto** com uma propriedade chamada "title".

function Header(props) {
  console.log(props); // { title: "React" }
  return <h1>Develop. Preview. Ship.</h1>;
}

Como `props` é um objeto, você pode usar a desestruturação de objetos para nomear explicitamente os valores de `props` dentro dos parâmetros da sua função:

function Header({ title }) {
  console.log(title); // "React"
  return <h1>{title}</h1>;
}

É comum ter dados que precisam ser exibidos como uma lista. Você pode usar métodos de array para manipular seus dados e gerar elementos de interface do usuário com estilo idêntico, mas que contenham informações diferentes.

Por exemplo:

function HomePage() {
  const names = ['Ada Lovelace', 'Grace Hopper', 'Margaret Hamilton'];
 
  return (
    <div>
      <Header title="Develop. Preview. Ship." />
      <ul>
        {names.map((name) => (
          <li>{name}</li>
        ))}
      </ul>
    </div>
  );
}

Observe como você usou chaves para transitar entre os domínios "JavaScript" e "JSX".

Se você executar esse código, o React exibirá um aviso sobre uma `key`propriedade ausente. Isso ocorre porque o React precisa de algo para identificar exclusivamente os itens em um array, para saber quais elementos atualizar no DOM.

Você pode usar os nomes por enquanto, já que eles são únicos no momento, mas é recomendável usar algo que seja garantidamente único, como um ID de item.

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