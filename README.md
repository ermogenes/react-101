# React-101

Primeiros passos com React e React Native

Pré-requisitos

- HTML, CSS, JavaScript
- Git e GitHub

Software:

- [VsCode](https://code.visualstudio.com/download)
- [Node.js](https://nodejs.org/)

## JavaScript

Referências:

- https://developer.mozilla.org/en-US/docs/Web/JavaScript
- https://javascript.info/

Ferramentas:

- https://codesandbox.io/
- [ESLint VsCode extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- [Prettier VsCode extension](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

Tópicos:

- [Optional chaining `?.`](https://javascript.info/optional-chaining)

```js
// Retorna undefined caso um valor não exista dentro de um objeto
let x;
console.log(x.foo); // exception: Cannot read properties of undefined (reading 'foo')
console.log(x?.foo); // undefined

// A variável deve estar declarada
console.log(y.foo); // exception: y is not defined
console.log(y?.foo); // exception: y is not defined
```

- [Null coalesce](https://javascript.info/nullish-coalescing-operator)

```js
let name = null;
let socialName;
let nickname = "n00b";

console.log(socialName ?? name ?? "Anonymous"); // "Anonymous"
console.log(socialName ?? nickname ?? name ?? "Anonymous"); // "n00b"
```

- [Condicional com `&&` (AND)](https://javascript.info/logical-operators#and-finds-the-first-falsy-value) e com [`?:` (`if` ternário)](https://javascript.info/ifelse#conditional-operator)

```js
const isPolite = true;

isPolite && console.log("hello"); // exibe "hello"
!isPolite && console.log("f@#$ u"); // não exibe nada

isPolite ? console.log("hello") : console.log("f@#$ u"); // exibe "hello"
```

- [Desestruturação](https://javascript.info/destructuring-assignment) e [Spread](https://javascript.info/rest-parameters-spread)

```js
// Desestruturando arrays
const data = ["SP", 2023];
const [local, year] = data;
console.log(`${local}, em ${year}`); // exibe "SP, em 2023"

// Desestruturando objetos
const user = { id: 1, age: 25, name: "Zé" };
const { id, name } = user;
console.log(id, name); // exibe "1 'Zé'"

// Invertendo valores com desestruturação
let a = 1;
let b = 2;
[b, a] = [a, b];
console.log(a, b); // exibe "2 1"
```

```js
// Spread em arrays
const data = ["SP", 2023, "outro valor qualquer"];
const [local, ...details] = data;
console.log(local); // exibe "SP"
console.log(details); // exibe [2023, "outro valor qualquer"]

// Spread em objetos
const user = { id: 1, age: 25, name: "Zé" };
const { id, ...userData } = user;
console.log(userData); // exibe {age: 25, name: 'Zé'}
```

- [Promises](https://javascript.info/promise-basics) e [Fetch API](https://javascript.info/fetch)

```js
fetch("https://api.github.com/users/ermogenes") // retorna uma promise
  .then((response) => response.json()) // retorna outra promise
  .then((result) => console.log(result.company)); // exibe "Prodam"
```

- [Métodos funcionais (`map`, `filter`, ...)](https://javascript.info/array-methods)

```js
// Transforma cada item em um valor novo
["a", "b", "c"].map((n) => n.toUpperCase()); // ['A', 'B', 'C']

// Filtra o arranjo
[(1, 2, 3, 4, 5)].filter((x) => x % 2 == 0); // [2, 4]

// Encontra o índice de um valor
["a", "b", "c"].findIndex((n) => n === "b"); // 1
```

- [Módulos](https://javascript.info/modules-intro)

## React

Referências:

- https://react.dev/

Ferramentas:

- https://codesandbox.io/
- [Projeto local](https://react.dev/learn/start-a-new-react-project)
- [ES7+ React/Redux/React-Native snippets VsCode extension](https://marketplace.visualstudio.com/items?itemName=dsznajder.es7-react-js-snippets)

Tópicos:

- [Componentes](https://react.dev/learn#components) e [JSX](https://react.dev/learn#writing-markup-with-jsx)

[Ver no CodeSandbox](https://codesandbox.io/s/react-101-components-3bsyjg?file=/src/App.js)

`index.html`

```html
<!DOCTYPE html>
<html>
  <head>
    <title>React App</title>
  </head>

  <body>
    <div id="root"></div>
  </body>
</html>
```

`index.js`

```jsx
import { createRoot } from "react-dom/client";

import App from "./App";

const rootElement = document.getElementById("root");
const root = createRoot(rootElement);

root.render(<App />);
```

`App.js`

```jsx
const Titulo = () => {
  return <h1>Exemplo de uso de componentes</h1>;
};

const Texto = () => {
  return (
    <>
      <p>
        Lorem ipsum <em>dolor sit amet</em>, consectetur adipiscing elit.
      </p>
      <p>
        Donec sollicitudin ligula mauris, a ultricies lorem scelerisque quis.
        Mauris ac urna at elit aliquam hendrerit at sit amet purus.
      </p>
      <p>Sed nec leo et nisl cursus tempor.</p>
    </>
  );
};

export default function App() {
  return (
    <div>
      <Titulo />
      <p>Acima temos um componente. Abaixo, outro.</p>
      <Texto />
    </div>
  );
}
```

- [Estilos (`className`, `style`, ...)](https://react.dev/learn#adding-styles)

[Ver no CodeSandbox](https://codesandbox.io/s/react-101-estilos-t1wynk?file=/src/App.js)

`styles.css`

```css
.App {
  font-family: sans-serif;
  text-align: center;
}

code {
  background-color: #ccc;
  font-size: large;
}
```

`App.js`

```jsx
import "./styles.css";

export default function App() {
  return (
    <div className="App">
      <h1>Usando estilos</h1>
      <p>
        Usando <code>import</code> e <code>className</code>
      </p>
      <p style={{ color: "red", textDecoration: "underline" }}>
        Usando um objeto <code>style</code>
      </p>
    </div>
  );
}
```

- [Renderizando dados](https://react.dev/learn#displaying-data)

[Ver no CodeSandbox](https://codesandbox.io/s/react-101-renderizando-dados-f0r7hd?file=/src/App.js)

```jsx
const alinhamento = "center";
const corTexto = "#008800";

export default function App() {
  const texto = "Texto e atributo armazenados em variáveis";
  return (
    <div>
      <h1>Renderizando dados</h1>
      <p align={alinhamento} style={{ color: corTexto }}>
        {texto}
      </p>
    </div>
  );
}
```

- [Props](https://react.dev/learn#sharing-data-between-components)

[Ver no CodeSandbox](https://codesandbox.io/s/react-101-props-4vdlxd?file=/src/App.js)

```jsx
function EmojiDisplay(props) {
  const frameStyle = {
    // estilos omitidos, veja no código completo
  };

  return (
    <div style={frameStyle}>
      <span
        role="img"
        aria-label={props.label}
        title={props.label ?? "um emoji qualquer"}
      >
        {props.emoji ?? "❌"}
      </span>
    </div>
  );
}

export default function App() {
  return (
    <div>
      <h1>Props</h1>
      <EmojiDisplay emoji="😍" label="cuti cuti" />
      <EmojiDisplay emoji="💩" label="cocô" />
      <EmojiDisplay emoji="☕" label="razão de viver" />
      <EmojiDisplay />
    </div>
  );
}
```

- [Renderização condicional](https://react.dev/learn#conditional-rendering)

[Ver no CodeSandbox](https://codesandbox.io/s/react-101-renderizacao-condicional-6mkzr6?file=/src/App.js)

```jsx
function SayHello({ to, gender, isCute }) {
  const boasVindas = `Seja bem-vind${gender === "female" ? "a" : "o"}.`;
  return (
    <div>
      {to ? (
        <p>
          Olá, {to}! {boasVindas}
          {isCute && <span> :)</span>}
        </p>
      ) : (
        <p>Não falo com estranhos.</p>
      )}
    </div>
  );
}

export default function App() {
  return (
    <div>
      <h1>Renderização condicional</h1>
      <SayHello to="Maria" gender="female" isCute />
      <SayHello />
      <SayHello to="Mario" gender="male" />
    </div>
  );
}
```

- [Renderização de listas](https://react.dev/learn#rendering-lists)

[Ver no CodeSandbox](https://codesandbox.io/s/react-101-renderizacao-de-listas-fscci4)

```jsx
export default function App() {
  const fruits = [
    { name: "Banana", icon: "🍌" },
    { name: "Maça", icon: "🍎" },
    { name: "Laranja", icon: "🍊" },
    { name: "Morango", icon: "🍓" },
    { name: "Abacaxi", icon: "🍍" },
    { name: "Abacate", icon: "🥑" },
  ];

  fruits.sort((f1, f2) => f1.name.localeCompare(f2.name));

  return (
    <div>
      <h1>Renderização de listas</h1>
      <ul style={{ listStyleType: "none", padding: 0 }}>
        {fruits?.map((fruit, index) => (
          <li key={index}>
            <span>{fruit.icon}</span> {fruit.name}
          </li>
        ))}
      </ul>
    </div>
  );
}
```

- [Eventos](https://react.dev/learn#responding-to-events)

[Ver no CodeSandbox](https://codesandbox.io/s/react-101-eventos-oc9jkj?file=/src/App.js:0-298)

```jsx
export default function App() {
  const handleClick = (event) =>
    alert(`Voce clicou em ${event.target.innerText}!`);
  return (
    <div>
      <h1>Eventos</h1>
      <button onClick={() => alert("Você clicou em 1!")}>1</button>
      <button onClick={handleClick}>2</button>
    </div>
  );
}
```

- [State](https://react.dev/learn#updating-the-screen)

[Ver no CodeSandbox](https://codesandbox.io/s/react-101-state-eel9wm?file=/src/App.js:0-501)

```jsx
import { useState } from "react";

export default function App() {
  const [number, setNumber] = useState(51);

  const increment = () => setNumber(number + 1);
  const decrement = () => setNumber(number - 1);
  const valueChanged = (e) => setNumber(Number(e.target.value));

  return (
    <div>
      <h1>State</h1>
      <button onClick={decrement}>&lt;</button>
      <input type="number" value={number} onChange={valueChanged} />
      <button onClick={increment}>&gt;</button>
    </div>
  );
}
```

# TODO: Passando estado em propriedade

- [Context](https://react.dev/learn/passing-data-deeply-with-context)
- [Effect](https://react.dev/reference/react/useEffect)
- [Memoization](https://react.dev/reference/react/useMemo) e [Callbacks](https://react.dev/reference/react/useCallback)
- [Ref](https://react.dev/reference/react/useRef)

## React Native

Referências:

- https://reactnative.dev/

Ferramentas:

- https://snack.expo.dev/
- [Projeto local](https://reactnative.dev/docs/environment-setup)
- [React Native Tools VsCode extension](https://marketplace.visualstudio.com/items?itemName=msjsdiag.vscode-react-native)

Tópicos:

- [Componentes multiplataforma](https://reactnative.dev/docs/components-and-apis)
- [Estilos e `StyleSheet.create`](https://reactnative.dev/docs/style)
- [Flexbox](https://reactnative.dev/docs/flexbox)
- [Imagens](https://reactnative.dev/docs/images)
- [Toque](https://reactnative.dev/docs/handling-touches)
- [Navegação](https://reactnative.dev/docs/navigation) com [React Navigation](https://reactnavigation.org/docs/getting-started)

## Expo

Referências:

- https://docs.expo.dev/

Ferramentas:

- [Expo Snack](https://snack.expo.dev/)
- [Projeto local](https://docs.expo.dev/get-started/installation/)
- [Expo Go](https://docs.expo.dev/get-started/expo-go/) para [Android](https://play.google.com/store/apps/details?id=host.exp.exponent) e [iOS](https://apps.apple.com/app/expo-go/id982107779)
- [Expo Tools VsCode extension](https://marketplace.visualstudio.com/items?itemName=expo.vscode-expo-tools)
- [ngrok](https://ngrok.com/)

Gestão do projeto:

- [Projeto local](https://docs.expo.dev/get-started/installation/)
- [Executar no Expo Go (LAN)](https://docs.expo.dev/get-started/expo-go/)
- [Executar no Expo Go (Tunnel)](https://docs.expo.dev/more/expo-cli/#tunneling)
- [Build com EAS Build](https://docs.expo.dev/develop/development-builds/introduction/)
- [Deploy com EAS Submit](https://docs.expo.dev/submit/introduction/)
- [Prebuild](https://docs.expo.dev/more/expo-cli/#prebuild)
- [Build e deploy com AppCenter](https://learn.microsoft.com/pt-br/appcenter/)
- [Estrutura do projeto](https://docs.expo.dev/develop/project-structure/)

Outros:

- [SafeArea](https://docs.expo.dev/develop/user-interface/safe-areas/)
- [Local Storage](https://docs.expo.dev/develop/user-interface/store-data/)
- [Ícones](https://docs.expo.dev/guides/icons/)
- [OAuth](https://docs.expo.dev/guides/authentication/)

Utils:

- [Expo SDK](https://docs.expo.dev/versions/latest/)
  - [AuthSession](https://docs.expo.dev/versions/latest/sdk/auth-session/)
  - [AV (vídeo)](https://docs.expo.dev/versions/latest/sdk/av/)
  - [Crypto](https://docs.expo.dev/versions/latest/sdk/crypto/)
  - [Font](https://docs.expo.dev/versions/latest/sdk/font/)
  - [Linking](https://docs.expo.dev/versions/latest/sdk/linking/)
  - [Location](https://docs.expo.dev/versions/latest/sdk/location/)
  - [Notifications](https://docs.expo.dev/versions/latest/sdk/notifications/)
  - [Speech](https://docs.expo.dev/versions/latest/sdk/speech/)
  - [SplashScreen](https://docs.expo.dev/versions/latest/sdk/splash-screen/)
- [Expo Router](https://docs.expo.dev/guides/routing-and-navigation/)

## Outros

Navegação:

- [React Navigation](https://reactnavigation.org/docs/getting-started)
  - [Stack](https://reactnavigation.org/docs/native-stack-navigator)
  - [Tabs](https://reactnavigation.org/docs/bottom-tab-navigator)
  - [Drawer](https://reactnavigation.org/docs/drawer-navigator)
  - [Navegação](https://reactnavigation.org/docs/navigating)
  - [Parâmetros](https://reactnavigation.org/docs/params)
  - [Aninhamento](https://reactnavigation.org/docs/nesting-navigators)

UI:

- [NativeBase](https://docs.nativebase.io/)
- [React Native Paper](https://callstack.github.io/react-native-paper/docs/guides/getting-started)

Mapas:

- [React Native Maps](https://github.com/react-native-maps/react-native-maps)

Chat:

- [React Native Gifted Chat](https://github.com/FaridSafi/react-native-gifted-chat)
- [@flyerhq/react-native-chat-ui](https://github.com/flyerhq/react-native-chat-ui)

Utils:

- [Lodash](https://lodash.com/docs)
- [Day.js](https://day.js.org/)

Stores:

- [Redux](https://redux.js.org/)
- [Zustand](https://zustand-demo.pmnd.rs/)
