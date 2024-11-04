## Section 01 - getting started with typescript

1. How to Get Help (1min)

- @ste_grider
- udemy Q&a

2. Join Our Community! (1min)
3. Course Resources (1min)
4. Typescript Overview (6min)

- adding a type-system
- catch errors during development
- adding 'type annotations'
- no performance optimizations

### running the code

- typescript (js + annotations) -> typescript compiler -> js

5. Environment Setup (8min)

- install typescript compiler -> `npm install -g typescript ts-node`

  - ts-node -> allows compile AND run code using single command
  - `tsc --help`
  - vscode typescript add-on
  - install vs-code prettier
  - add .prettierrc

  ```.prettierrc
  {
  "tabWidth": 2,
  "useTabs": false,
  "printWidth": 80,
  "semi": true,
  "singleQuote": true,
  "trailingComma": "es5"
  }
  ```

  - enable format on save:
    `CTRL + ,` -> search and enable 'Format On Save'

6. Important Axios and TypeScript Version Information (1min)

- when using latest axios need types: `npm install --save-dev @types/node`
- TS 5.6 has breaking changes (ts-node not nsync)
- install typscript v5.5 `npm install -g typescript@5.5`
  - this fixes `Cannot use import statement outside a module` errors

7. A First App (5min)

### A basic api fetching data

- see project files: [/tutorial-stephengrider-typescript-01-basic-example](./tutorial-stephengrider-typescript-01-basic-example)
- TODO: make a network request to fetch some JSON and print the result
- TODO: create a project folder
  - i've named mine: `tutorial-stephengrider-typescript-01-basic-example`
  - go into folder
- TODO: create node project `npm init -y`
- TODO: create index.js

### installs

- install axios
- install ts-node
- install typescript

```shell
npm i axios
npm i --save-dev ts-node typescript
```

### fetch data using json typicode (jsonplaceholder.typicode.com)

- https://jsonplaceholder.typicode.com/todos
- https://jsonplaceholder.typicode.com/todos/1

8. Executing Typescript Code (5min)

```shell
# compile -> creates index.js
tsc index.ts
```

```ts
import axios from 'axios';
const url = 'https://jsonplaceholder.typicode.com/todos/1';

axios.get(url).then((response) => {
  console.log(response.data);
});
```

# run the js

```shell
node index.js
```

- expected output:

```cmd
{ userId: 1, id: 1, title: 'delectus aut autem', completed: false }
```

```json
// package.json
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "tsc index.ts",
    "dev": "node index.js",
    "start": "ts-node index.ts"
  },
```

- ts-node (compile + run)
- NOTE: running ts-node on its own does not create output .js file (like with tsc)

9. One Quick Change (4min)

- makes some mistakes in code: passing wrong variable names
- does not have type checking

10. Catching Errors with Typescript (7min)

- below is the finished code (with Typescript)
- added an interface: defining structure of an object

```js
//index.ts
import axios from 'axios';

const url = "https://jsonplaceholder.typicode.com/todos/1";

//TYPESCRIPT: interface
interface Todo{
  id: number;
  title: string;
  completed: boolean;
}

axios.get(url).then(response => {
  const todo = response.data as Todo;  //TYPESCRIPT: as interface

  const id = todo.id;
  const title = todo.title;
  const completed = todo.completed;

  logTodo(id, title, completed);

});

//TYPESCRIPT: give type annotations to function parameters
const logTodo = (id:number, title: string, completed:boolean) => {
  console.log(`${id} ${title} ${completed}`)
}
```

11. Catching More Errors! (5min)

- created the logTodo function
- error was the order of arguments passed in
  - FIX: give the arguments types so it picks up if wrong prop passed-in
