An function declaration which does not start with the keyword **function** is called as a **Function Expression**.
Ex- 
 ```js
 1.   let a = function fun(){
          // body of the function
     }
     This is a named function expression.
2.  let a = function(){
     // body of the  function
   }
   This is  anoymous function expression.
3.  (function x(){
         // body of the function
     })
4. (function(){
         //body of the function
      }) 
5.  let y = () =>{
       //body of the function 
     }
     This is a fat body function.They will be discussed in the      [[Objects in Javascript]].
```

Why use named function expression?
 1. Using named function increases the readability of the code as function name in itself will depict the use case of that particular function
 2. While using recursive algorthims function cannot call itself it is not having a function name.
 3. During the call stack the function would not have any name in the call stack history and hence it would make it difficult to debug the code in case of errors.This is done using console.trace() function.

**IIFE** - It stands for **Immediately Invoked Function Expression**. These functions are called when they are declared.
Ex - 
```js
 (function x (y){
    console.log("hi",y);
})("Priyanshu");
This prints Hi Priyanshu
```

Function Expressions get the scope of the variable by which they are defined.
Ex - 
```js
 const f = function fun(){
     console.log("Hi");
}
```
This function can be called by 
f(); This will print Hi
but since function fun has been scoped to f therefore it can only be called using variable f and not by directly fun().fun() will throw function not defined error if called.