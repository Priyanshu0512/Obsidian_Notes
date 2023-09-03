Scopes are used to define the visibility of variables and functions.

Variables and Functions can be used in the code in the following two ways:-
1. Either it will be getting some value assigned to it.
2. Or some value will be retrieved from it.


**Complier** - It goes through the entire code and find any errors in the program and will throw them. The code cannot be executed before these errors are corrected.
**Interpreter** -It goes through the code line by line with each line being executed at that instant only.The occurrence of first errors in the code stops the execution and execution cannot take place further till the error is resolved.

**Javascript is neither purely Complied nor purely Interpreted language.**
Javascript is executed is two phases:- 
  1. Parsing - Scope Resolution happens
  2. Execution


**Types of Scopes**
    1. Global Scope
    2. Function Scope 
    3. Block Scope
    4. Module

**1.Function Scope** - A Function creates a scope. A variable defined exclusively inside a function cannot be accessed from outside the function or used within other functions.
**2. Block Scope** - Block scopes are defined using the {} curly braces. **Block only scope let and const but is not valid for var declarations.**
Ex -
```js
{
 const x =1;
}
console.log(x) //Reference Error: x is not defined
 but 
 {
   var x=1;
 }
 console.log(x) - prints 1
```
**Var** - The var statement either declares function scope or Globally Scoped variable(not block scope).Var declarations are executed wherever they occur in the code before the code is executed.This is called **Hoisting**.
**Let** - The Let statement declares a block scoped local variable.

**Temporal Dead Zones is the region before the declaration of the block scope.** They exist for both const and let declarations.

**Const** - Const statement also declares a block scoped local variable.Const does not allows reassignment but allows updation of values.
Ex- 
      const x = 10;
      const x= 9; This throws an error
      But 
      const obj ={x: 9};
      obj.x = 10; This is allows as it only updates the values of key x and not a new object is being assigned.


**Parsing in Javascript**
In the parsing phase everytime we see a **Formal Declaration** a scope is assigned to it.

**Auto Globals**
During the parsing phase if a non-formal declaration is not then not scope resolution will be done for it. During the Execution phase this non-formal declaration will be taken one-scope out of the current scope and would automatically made a Global variable. This is called the concept of Auto Globals.
Note - This only works if the declaration has value assignment to it and is been called before the value of the declaration is been used anywhere in the program during the execution phase.

To Remove this functionality of Auto Globals javascript can be executed in two modes namely:- 
   1. Strict Mode 
   2. Non-Strict Mode(sloppy mode)

**Strict-Mode**
Javascript Strict Mode is a way to opt into a restricted variant of javascript. It advantages are as following- 
   1. It eliminates some silent erros of javascript by throwing errors.
   2. Fixes mistake which some javascript engines find hard for proper optimization.(performance optimizations)
   3. Prohibits some feature going to be introduced in future until they become stable.

To invoke strict mode for a function just write **"use strict";** or  before any other statement of the function or in the global scope to use strict mode globally.
Strict mode makes it impossible to create global accidentally.

Ex- 
console.log("Hi");
console.lo("World");
console.log("Hey");
This prints Hi and then throws an error as during the parsing phase console is a valid object and can have a function lo inside of it hence the code is parsed successfully but during the execution phase when it tries to access the lo function inside the console object then the function is not present in it and hence it throws an error but prints Hi.

console.log("Hi");
console..log("World");
console.log("Hey");
This will not print anything and directly throw an error as this is an syntactical error. During thr parsing phase it when it encounters .. this not an valid operation and hence it throws an error then and there.

Note- For Primitves double dotes(..) syntax is valid in javascript.
Ex- console.log(10..toString()); prints 10 
but console.log(10...toString()); It throws an error.
**.. is used to implement boxing if () are not used in decimal numbers.**
This .. operator has to be used while applying boxing to numbers so as to remove the ambuiguity where the user wanted to enter a decimal value or intentionally wnated to do boxing.

[[Lexical Vs Dynamic Scoping]].