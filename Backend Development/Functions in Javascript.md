A function is a black box which takes a input and processes it to give an output.

Functions are of two types
1. User defined functions
2. In-built functions

Defining a Function
     Syntax - 
   ```js
 function functionName(input1, input2){
    //logic
    return argument; 
    }
    ex- function isEven(num){
    if(num%2 == 0){
         return true;
     }
     else{
        return false
     }
    }
```

In console.log console is a function which has a log keys in which it has the function which prints the entered value.
**console.log returns undefined.** 
*In javascript if user does not return a value manually then the function by default returns undefined. In javascript ever function returns something.*

**Arguments and Parameters**

```js
 function add (x,y){
    let c = x+y;
    return c;
}

let a= 10;
let b= 20;
let result = add(a,b);
console.log(result);
```

Here x and y are called parameters whereas a and b are arguments.Arguments are passed and parameters are expected.
Note- If the number of arguments passed are more than the number of parameters then the intials arguments will be passed only.

**Higher Order Functions** - Functions which take another function as an argument are called higher order function.
Ex- 
```js
     function f( x , fn){
        console.log(x);
        console.log(fn);
        fn(); 
    }
    f(10, function exec(){
       console.log("I am a expression passed to a HOF.");
    })
```


arr.sort( )- The default implementation of .sort is to sort the given values in lexicographical manner. 
In ordr to sort the values in a specific manner as the .sort is a HOF there a comparator function can be passed to specific the way of sorting.
For sorting in ascending order 
arr.sort(function(a,b){
    return a-b;
})