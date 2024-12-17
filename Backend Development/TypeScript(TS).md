---

---

## Types of Languages

#### 1. Loosely Typed Languages

-  `Runtime Type Association`: Data types are associated with values at runtime. Unlike strongly typed languages, type information is not strictly bound during compilation but rather at the time of execution.
-  `Dynamic Type Changes`: Variables can change types during execution, offering more adaptability. This flexibility allows for a dynamic approach to variable assignments and operations.
-  `Runtime Error Discovery`: Type errors may be discovered during runtime, potentially leading to unexpected behaviour's. This characteristic provides more freedom but requires careful handling.
-  **Examples of Loosely Typed Languages**: JavaScript, Python, Ruby.

#### 2. Strongly Typed Languages

-  `Compile-Time Enforcement`: The data type of a variable is strictly enforced during compilation. This means that the compiler checks and ensures that variables are used in a way that is consistent with their types at compile time.
-  `Type Safety`: The compiler or interpreter guarantees that operations are performed only on compatible types. This ensures that type-related errors are caught early in the development process.
- `Early Error Detection`: Type errors are identified and addressed at compile-time, providing early feedback to developers. This leads to increased reliability and reduces the likelihood of runtime errors.
-  **Examples of Strongly Typed Languages:** Java, C#, TypeScript

---
## Why TypeScript??

### 1. Static Typing

- TypeScript introduces static typing, allowing developers to declare the types of variables, parameters, and return values at compile-time.
- Static typing helps catch potential errors during development, offering a level of code safety that may not be achievable in pure JavaScript.
### 2. Compatibility with JavaScript

- TypeScript is a superset of JavaScript, meaning that any valid JavaScript code is also valid TypeScript code.
- Developers can gradually adopt TypeScript in existing JavaScript projects without the need for a full rewrite.
### 3.Interfaces and Type Declarations

- TypeScript introduces concepts like interfaces and type declarations, enabling developers to define clear contracts for their code.
- Interfaces help document the shape of objects, making it easier to understand and maintain the code.
---
### Execution of TypeScript Code 

 1.`TypeScript Compiler (tsc)`-
- The TypeScript Compiler (tsc) is a command-line tool that processes TypeScript code.
- Developers run tsc to initiate the compilation process.
 
 2.`Compilation Process`-
- The TypeScript Compiler parses and analyses the TypeScript code, checking for syntax errors and type-related issues.
- It generates equivalent JavaScript code, typically in one or more .js or .jsx files.
 
3.`Generated JavaScript Code`- 
- The output JavaScript code closely resembles the original TypeScript code but lacks TypeScript-specific constructs like type annotations.
- TypeScript features that aren't present in JavaScript (e.g., interfaces) are often transpiled or emitted in a way that doesn't affect runtime behaviour .

4.`Runtime Environment`
- In the chosen runtime environment, the JavaScript code is interpreted or compiled by the JavaScript engine (e.g., V8 in Chrome, SpiderMonkey in Firefox).
- Just-in-time (JIT) compilation or interpretation occurs to convert the code into machine code that the computer's processor can execute.


In addition to the TypeScript Compiler (**`tsc`**), several alternative tools have gained popularity for their efficiency, speed, and additional features when transpiling TypeScript to JavaScript. Here are a couple of noteworthy ones:

1. `esbuild`: a highly performant JavaScript bundler and minifier, but it also supports TypeScript.
2. `swc (Speedy Web Compiler)`: a fast and low-level JavaScript/TypeScript compiler.

```Bash
npm init -y
npx tsc --init //Generates  tsconfig.json
tsc -b // 
```

>  The `-b` flag tells TypeScript to build the project based on the configuration in `tsconfig.json`. This generates a JavaScript file (`index.js`) from the TypeScript source (`a.ts`).


![[Pasted image 20240829193020.png]]

### Basic Types in Typescript

 In TypeScript, basic types serve as the building blocks for defining the data types of variables. Here's an overview of some fundamental types provided by TypeScript:
 
1.  `Number` - Represents numeric values.
2. `String` -Represents textual data (sequences of characters).
3. `Boolean`- Represents true or false values.
4. `Null`- Represents the absence of a value.
5. `Undefined`-  Represents a variable that has been declared but not assigned a value.
6. `any` - Represents any type of value.

```Typescript
let age: number = 25;
let name: string = "John";
let isStudent: boolean = true;
let myVar: null = null;
let myVar: undefined = undefined;
```

Giving type to function passed as a callback

```Typescript
function run(abc: () => void) {
  setTimeout(abc, 1000);
}

run(function () {
  console.log("hi there");
});
```

---
## The `tsconfig.json` File in TypeScript

The `tsconfig.json` file in TypeScript is a configuration file that provides settings for the TypeScript compiler (`tsc`).

Below are a bunch of options that you can change to change the compilation process in the `tsconfig.json` file:

####  1. Target Option in`tsconfig.json`

The `target` option in a `tsconfig.json` file specifies the ECMAScript target version to which the TypeScript compiler (`tsc`) will compile the TypeScript code. It allows you to define the lowest version of ECMAScript that your code should be compatible with. Here's an explanation and example usage:

- **ES5 (ECMAScript 5):**
    - When `target` is set to `"es5"`, the TypeScript compiler generates code compatible with ECMAScript 5, which is widely supported across browsers.

```json
{   "compilerOptions":
    {     "target": "es5",    
     // Other options...   
} }
```

- TypeScript Code:

```Typescript
const greet = (name: string) => `Hello, ${name}!`;
```

- Output

```js
"use strict";
var greet = function (name) { 
    return "Hello, ".concat(name, "!"); 
};

```

- **ES2020 (ECMAScript 2020):**
    - When `target` is set to `"es2020"`, the TypeScript compiler generates code compatible with ECMAScript 2020, incorporating the latest features.

```JSON
{   "compilerOptions": 
    {   "target": "es2020",    
	// Other options...  
    } 
}
```

- TypeScript Code:

```Typescript
const greet = (name: string) => `Hello, ${name}!`;
```

- Output:
```js
"use strict";
const greet = (name) => `Hello, ${name}!`;
```

> By setting the `target` option, you ensure that the generated JavaScript code adheres to the specified ECMAScript version, allowing you to control the level of compatibility and take advantage of the features available in newer ECMAScript versions.

#### 2. `rootDir:`

- The `rootDir` option in a `tsconfig.json` file specifies the root directory where the TypeScript compiler (`tsc`) should look for `.ts` files.
- It is considered a good practice to set `rootDir` to the source folder (`src`), indicating the starting point for TypeScript file discovery.

```JSON
{   "compilerOptions": 
    {     "rootDir": "src",   
      // Other options...   
    }
}
```

#### 3. `outDir`

- The `outDir` option defines the output directory where the TypeScript compiler will place the generated `.js` files.
- It determines the structure of the output directory relative to the `rootDir`.

```json
{   "compilerOptions":
    {     "outDir": "dist",     
    // Other options...   
    } 
}
```

> If `rootDir` is set to `"src"` and `outDir` is set to `"dist"`, the compiled files will be placed in the `dist` folder, mirroring the structure of the `src` folder.

#### 4. `noImplicitAny`

- The `noImplicitAny` option in a `tsconfig.json` file determines whether TypeScript should issue an error when it encounters a variable with an implicit `any` type.
- **Enabled (**`"noImplicitAny": true`**):**

```json
{   "compilerOptions": 
    {     "noImplicitAny": true,     
    // Other options...   
    } 
}
```

Example:

```typescript
Compilation Error: Implicit any type const greet = (name) => `Hello, ${name}!`;
```

#### 5.`removeComments`

- The `removeComments` option in a `tsconfig.json` file determines whether comments should be included in the final JavaScript output.
- **Enabled (**`**"removeComments": true**`**):**

```json
{   "compilerOptions": 
    {     "removeComments": true,     
    // Other options...   
    } 
}
```

> These options provide flexibility and control over the compilation process, allowing you to structure your project and handle type-related scenarios according to your preferences.

---
## Interfaces 

In TypeScript, an interface is a way to define a contract for the shape of an object.It basically allows you to declare the types of properties of the object. It is like a blueprint of the object hence it eliminates the requirements of declaring types whenever object is used anywhere else.

```typescript
interface User {
  firstName: string;
  lastName: string;
  email: string;
  age: number;
}

const user: Usere = {
  firstName: "harkirat",
  lastName: "singh",
  email: "email@gmail.com",
  age ?: 21, // Means the age property is optional.
};
```

>- By stating `const user: User`, you are explicitly indicating that the `user` object must adhere to the structure defined by the `User` interface.

Creating a react component that takes todos as an input and renders them.

```JSX
// Define an interface to specify the structure of a todo object
interface TodoType {
  title: string;
  description: string;
  done: boolean;
}

// Define the input prop for the Todo component
interface TodoInput {
  todo: TodoType;
}

// Create a React component 'Todo' that takes a 'todo' prop and renders it
function Todo({ todo }: TodoInput): JSX.Element {
  return (
    <div>
      <h1>{todo.title}</h1>
      <h2>{todo.description}</h2>
      {/* Additional rendering logic can be added for other properties */}
    </div>
  );
}
```

### Implementing Interfaces 

- One of the advantages of using `interfaces` is that they can be implemented using classes.

```Typescript
interface Person {
  name: string;
  age: number;
  greet(phrase: string): void; // function
}

class Employee implements Person {
  name: string;
  age: number;

  constructor(n: string, a: number) {
    this.name = n;
    this.age = a;
  }
  greet(phrase: string) {
    console.log(`${phrase} ${this.name}`);
  }
}

const e = new Employee("connor",21);
e.greet("hello"); // Prints hello connor
```

---
## Types 

- In TypeScript, **types** allow you to aggregate data together in a manner very similar to interfaces. They provide a way to define the structure of an object, similar to how interfaces do. 

```typescript

type User = { 
firstName: string,
lastName: string,
age?: number
}

```

### Features 

1. `Union` - Unions allow you to define a type that can be one of several types. This is useful when dealing with values that could have different types.

```typescript
type User = string | number;

function user(input: User) {
  console.log(typeof input);
}

user("22");
user(7);

// Prints
// string
// number
```

2. `Intersection` - Intersections allow you to create a type that has every property of multiple types or interfaces.

```typescript
type Person = {
  name: string;
  age: number;
};
interface Employee {
  name: string;
  department: string;
}

type Team = Person | Employee;

const team: Team = {
  name: "connor",
  department: "Physics",
  age: 21,
};

console.log(team);
// { name: 'connor', department: 'Physics', age: 21 }
```

---
### Interfaces Vs Types 

#### Major Differences

#### 1. Declaration Syntax:

- **Type:**
    - Uses the `type` keyword.
    - More flexible syntax, can represent primitive types, unions, intersections, and more.

- **Interface:**
    - Uses the `interface` keyword.
    - Typically used for defining the structure of objects.

#### 2. Extension and Merging: 

- **Type:**
    - Supports extending types.
    - Can't be merged; if you define another type with the same name, it will override the previous one.

- **Interface:**
    - Supports extending interfaces using the `extends` keyword.
    - Automatically merges with the same-name interfaces, combining their declarations.

#### 3. Declaration vs. Implementation:

- **Type:**
    - Can represent any type, including primitives, unions, intersections, etc.
    - Suitable for describing the shape of data.

- **Interface:**
    - Mainly used for describing the shape of objects.
    - Can also be used to define contracts for classes.

#### 4.Implementation for Classes:
- Interfaces can be used to define contracts for class implementations.
- Types are more versatile for creating complex types and reusable utility types.


### When to Use Which

- **Use Types:**
    - For advanced scenarios requiring union types, intersections, or mapped types.
    - When dealing with primitive types, tuples, or non-object-related types.
    - Creating utility types using advanced features like conditional types.

- **Use Interfaces:**
    - When defining the structure of objects or contracts for class implementations.
    - Extending or implementing other interfaces.
    - When consistency in object shape is a priority.


#### Arrays in Typescript

- It you want to access in typescript simply add `[]` after the type.

```typescript
function maxElement(arr : number[]) // arr is a array of numbers.
```

---
### Enums

- `Enums` in Typescript are a feature that allows you to define a set of named constants.

```typescript
enum Direction {
  Up, // 0 if 10 
  Down, // 1 if 20 
  Left, // 2 then 21
  Right, // 3 then 22
}

function keyPressed(key: Direction) {
  if (key == Direction.Up) {
    //Do someting
  }
}
```

Internal implementation in the js file.

```js
"use strict";
var Direction;
(function (Direction) {
    Direction[Direction["Up"] = 0] = "Up";
    Direction[Direction["Down"] = 1] = "Down";
    Direction[Direction["Left"] = 2] = "Left";
    Direction[Direction["Right"] = 3] = "Right";
})(Direction || (Direction = {}));
function keyPressed(key) {
    if (key == Direction.Up) {
    }
}
```

- If you want to gives values to the enums other the default values of 0,1,2..etc 

```typescript
enum Direction {
  Up = "up",
  Down = "down",
  Left = "left",
  Right = "right",
}
```

---
## Generics

- Generics enable you to create components that work with any data type while still providing compile-time  type safety.

```typescript
function element<T>(arr: T[]): T {
  return arr[0];
}

interface User {
  name: string;
  age?: number;
}
const el = element<User>([{ name: "connor" }]);
const el2 = element<number>([1, 2]);
console.log(el.name);
console.log(el2);
```

---
