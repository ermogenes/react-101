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

[Ver no CodeSandbox](https://codesandbox.io/s/beautiful-shadow-t1wynk?file=/src/App.js)

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

[Ver no CodeSandbox](https://codesandbox.io/s/rough-resonance-f0r7hd?file=/src/App.js)

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

- [Renderização condicional](https://react.dev/learn#conditional-rendering)
- [Renderização de listas](https://react.dev/learn#rendering-lists)
- [Eventos](https://react.dev/learn#responding-to-events)
- [State](https://react.dev/learn#updating-the-screen)
- [Props](https://react.dev/learn#sharing-data-between-components)
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
