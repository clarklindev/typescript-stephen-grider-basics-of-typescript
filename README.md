# Typescript - StephenGrider - Basics of Typescript

### NOTE: Section 01 to Section 09 - Basics of Typescript

- Basics of Typescript -77 lessons (77 lessons (5h 41min))
- NOTE: this section has been extracted to its own repository: [typescript-stephengrider-basics-of-typescript](https://github.com/clarklindev/typescript-stephengrider-basics-of-typescript)
- this section is also covered in courses:
  - [microservices-with-node-js-and-react](https://www.udemy.com/course/microservices-with-node-js-and-react/) - section 25: appendix B - basics of typescript
    - [my git repository](https://github.com/clarklindev/microservices-stephengrider-with-node-and-react)
  - [typescript-the-complete-developers-guide](https://www.udemy.com/course/typescript-the-complete-developers-guide) - section 01 to section 09
    - [my git repository](https://github.com/clarklindev/typescript-stephengrider-typescript-complete-developers-guide)
  - [react-and-typescript-build-a-portfolio-project](https://www.udemy.com/course/react-and-typescript-build-a-portfolio-project) - section 26: Appendix:Typescript
    - [my git repository](https://github.com/clarklindev/typescript-stephengrider-typescript-portfolio)

---

## Table of contents

### Section 01 to Section 09 - basics of typescript

- [Section 01 - Getting started with TypeScript](#section-01---getting-started-with-typescript)
- [Section 02 - What is a Type System](#section-02---what-is-a-type-system)
- [Section 03 - Type Annotations in Action](#section-03---type-annotations-in-action)
- [Section 04 - Annotations with Functions and Objects](#section-04---annotations-with-functions-and-objects)
- [Section 05 - Mastering Typed Arrays](#section-05---mastering-typed-arrays)
- [Section 06 - Tuples in TypeScript](#section-06---tuples-in-typescript)
- [Section 07 - The All Important Interface](#section-07---the-all-important-interface)
- [Section 08 - Building Functionality with Classes](#section-08---building-functionality-with-classes)
- [Section 09 - Design Patterns with TypeScript](#section-09---design-patterns-with-typescript)

---

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

## Section 02 - What is a type system

12. Do Not Skip - Course Overview (4min)

### learning Typescript:

- syntax + features
  - focus on this first, then design patterns
- design patterns with TS (FOCUS OF COURSE)
  - eg. how to use interfaces to write re-usable code

### course goals

- Syntax + features - section 2 - understanding basic types in TS
- Syntax + features - section 3 - Function typing + annotations
- Syntax + features - Type definition files
- Syntax + features - arrays in TS
- Syntax + features - modules systems
- Syntax + features - classes + refresher on OOP
- design pattern - Projects

- for each of the topics
  - definition
  - why?
  - examples
  - when to use

---

13. Types (5min)

- Type -> easy way to refer to the different properties and functions that a value has

14. More on Types (6min)

- 2 categories of types:
  - primitive types -> string, number, boolean, void, undefined, null, symbol
  - Object types -> functions, arrays, classes, objects
- Types - used by typescript compiler to analyze code for errors
- Types - allow other devs to understand what data values are in the codebase

## Features

- TODO FEATURE: Make interfaces for axios response.data objects
- TODO FEATURE: make use of 'as TYPE' to type some data to an interface
- TODO FEATURE: give type annotations to function parameters ( parameters are what you can pass to a function and arguments are actually values passed in a function)
- TODO FEATURE: Tuples (mutiple values(with different type - ONLY the values) for each entry in array) - no attributes, order is critical
- TODO FEATURE: Type alias

```ts
type Drink = [string, boolean, number];

//same as
const pepsi: Drink;
```

## Notes

- type annotation vs type inference
  - same line initialization and assignment - value has automatic inference (typescript figures out whats the type)
- 3 senarios for adding annotations

  1. when function returns any type (eg. response from axios call / JSON.parse() etc when typescript cant figure out return type)
  2. delayed initialization (when variable declaration and value assignment not on same line)
  3. when inferance doesnt work - (eg. variable is reassigned a value with different type)

15. Examples of Types (5min)

- autocomplete once we assigned type as Date

```ts
const date = new Date();
```

- Class

```ts
class Color {}
const red = new Color();
```

16. Where Do We Use Types? (1min)

- where are types used -> everywhere

---

## Section 03 - Type annotations in action

### - array of type string:

```ts
  let colors:string[] (string array)
```

### classes

- classes
  ```ts
  class Car {}
  let car: Car = new Car();
  ```

### Object literal

- object literal

```ts
let point: { x: number; y: number } = {
  x: 20,
  y: 23,
};
```

### Functions

- function annotation - (what arguments going into function, what we return)
  1. function varible annotation: const x:(i: number) => void
  2. function annotations (everything on right side of =) = (function inputs / function return types):
  - type inference only for return type of function (not the arguments)
  - we always annotate return type (this is for arrow functions, named functions, anonymous functions assigned to variable type) because there are times when we can forget to return something...and typecript will infer return as 'void'
  - :void return type for return null or undefined
  - :never return type is when we ONLY throw errors and dont return something so there is no way function will complete

```ts
const logNumber: (i: number) => void = (i: number) => {};
```

-- interface

```ts
interface Todo {
  id: number;
  title: string;
  completed: boolean;
}

axios.get(url).then((response) => {
  const todo = response.data as Todo; //TYPESCRIPT: as interface
});
```

17. Type Annotations and Inference (2min)
18. Annotations with Variables (5min)
19. Object Literal Annotations (7min)
20. Annotations Around Functions (6min)
21. Understanding Inference (4min)
22. The 'Any' Type (8min)
23. Fixing the 'Any' Type (2min)
24. Delayed Initialization (3min)
25. When Inference Doesn't Work (5min)

## Section 04 - Annotations with functions and objects

26. More on Annotations Around Functions (5min)
27. Inference Around Functions (6min)
28. Annotations for Anonymous Functions (2min)
29. Void and Never (3min)
30. Destructuring with Annotations (4min)
31. Annotations Around Objects (7min)

## Section 05 - Mastering Typed Arrays

32. Arrays in Typescript (5min)
33. Why Typed Arrays? (5min)
34. Multiple Types in Arrays (3min)
35. When to Use Typed Arrays (1min)

## Section 06 - Tuples in Typescript

36. Tuples in Typescript (4min)
37. Tuples in Action (5min)
38. Why Tuples? (3min)

## Section 07 - The all important interface

39. Interfaces (1min)
40. Long Type Annotations (5min)
41. Fixing Long Annotations with Interfaces (5min)
42. Syntax Around Interfaces (4min)
43. Functions in Interfaces (5min)
44. Code Reuse with Interfaces (4min)
45. General Plan with Interfaces (3min)

## Section 08 - Building functionality with classes

46. Classes (4min)
47. Basic Inheritance (3min)
48. Instance Method Modifiers (7min)
49. Fields in Classes (6min)
50. Fields with Inheritance (4min)
51. Where to Use Classes (1min)

## Section 09 - Design Patterns with Typescript

52. Updated Parcel Instructions (1min)
53. App Overview (3min)
54. Bundling with Parcel (5min)
55. Project Structure (3min)
56. IMPORTANT Info About Faker Installation (1min)
57. Generating Random Data (5min)
58. Type Definition Files (5min)
59. Using Type Definition Files (6min)
60. Export Statements in Typescript (5min)
61. Defining a Company (5min)
62. Note on Generating an API Key (1min)
63. Adding Google Maps Support (8min)
64. Required Update for New @types Library (1min)
65. Google Maps Integration (4min)
66. Exploring Type Definition Files (3min)
67. Hiding Functionality (6min)
68. Why Use Private Modifiers? Here's Why (8min)
69. Adding Markers (9min)
70. Duplicate Code (3min)
71. One Possible Solution (7min)
72. Restricting Access with Interfaces (6min)
73. Implicit Type Checks (3min)
74. Showing Popup Windows (7min)
75. Updating Interface Definitions (7min)
76. Optional Implements Clauses (6min)
77. App Wrapup (8min)

---
