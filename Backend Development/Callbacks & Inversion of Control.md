**Higher Order Functions**  - Functions which take another functions as an argument are called HOF's or Functions which consume another functions.

```js
function hof(x, fn){
console.log("HI Calling the passed function:",fn);
fn();
console.log("Again inside the HOF");
}

hof(10,function exec(){
console.log("Inside the passed funciton");
});
```

Use Case - 
```js
let arr = [1,2,4,534,3,4533,5423,200,4,43];
console.log(arr.sort());//sorts the array in lexicographical manner by default. 

arr.sort(function comp(a,b){
return a-b; // If comparator functions give negative then a is placed before b. (a<b)
})
console.log(arr);
```
Here a comparator function comp is being passed to sort function to implement the increasing order sorting in the sort function.

**Callbacks** - The functions passed during functions call are called as callback functions or the functions which are passed as an argument to an HOF.

```js
function callback(x,fn){
  for(let i=0;i<x;i++){
  console.log(i);
  }
fn(x*2);
}

callback(5,function exec(x){ //function exec is a callback.
console.log(x);
});
```

**Problems with callbacks -** 
1. Callback Hell - It is nesting of callbacks inside another callbacks. Refer to [callbackhell.com] to get an idea about callback hell. It is sort of a readability problem.
2. **Inversion of control** - It is passing of the control of the callback function to an HOF and how this callback will be handled inside the HOF.
```js
function callback(x,fn){
//Someone else implemented this HOF function.
fn(x*2);
fn(x*2);  
}

callback(5,function exec(x){
console.log(x);//Someone else is using the HOF with their callback implementation.

});
```
Here the callback is being called twice in the HOF instead of one.

The Problem of inversion of control can be eliminated by use of [[Promises in Javascript]].

