Javascript is Asynchronous in nature and is single threaded but only for valid native ECMAscript code given by the standards.

Note - Since javascript is single thread and synchronous in nature native js code is blocking in nature whereas in other languages like java which are multi threaded they did not hamper the main thread on blocking code but redirect the task to a different thread to behave asynchronously.
```js
console.log("HI");
setTimeout(function exec(){console.log("Inside the setTimeout function")},5000);
console.log("End");

//Output
// HI
//End
//Inside the setTimeout function
```
Here js didn't  wait for the exec function to get completed and printed End.

Javascript in itself is not very powerful but when combined with a runtime like Node.js or  a browser runtime then they provide a whole set new functionality to javascript for various use cases.

```js
function timeConsumingByLoops(){
  console.log("Loop Starts")
  for(let i=0;i<10000000000;i++);
  console.log("Loop Ends");
}
function timeConsumingByRuntime(){
  console.log("Timer starts");
  setTimeout(function exec(){
     console.log("Timer Ends");
  },500);
}

console.log("Starts");
timeConsumingByLoops();
timeConsumingByRuntime();
timeConsumingByLoops();
console.log("End");

/* Output- 
Starts
Loop Starts
Loop Ends
Timer starts
Loop Starts
Loop Ends
End
Timer Ends
*/
```

**How Async behaviour is handled?**

Note - Any synchronous piece of code is never broken to execute any async function output.

**Callstack** - It is here where all the function calls are executed synchronously one by one
**Event loop** - It constantly checks whether all global piece of code has been executed and the callstack is empty.
**Event Queue** - It stores all the Async task which have been completed in the runtime waiting for being executed in the callstack.
```js
function timeConsumingByLoops(){
  console.log("Loop Starts")
  for(let i=0;i<10000000000;i++);
    console.log("Loop Ends");
}
function timeConsumingByRuntime0(){
  console.log("Timer-0 Starts");
  setTimeout(function exec(){
    console.log("Completed Timer-0");
    for(let i=0;i<10000000000;i++);
    },5000);
}
function timeConsumingByRuntime1(){
  console.log("Timer-1 Starts");
  setTimeout(function exec(){
    console.log("Completed Timer-1");
  },0);
}
function timeConsumingByRuntime2(){
  console.log("Timer-2 Starts");
  setTimeout(function exec(){
    console.log("Completed Timer-2");
  },200);
}

console.log("Starts");
timeConsumingByLoops();
timeConsumingByRuntime0();
timeConsumingByRuntime1();
timeConsumingByRuntime2();
timeConsumingByLoops();
console.log("End");
/* Output 
Starts
Loop Starts
Loop Ends
Timer-0 Starts
Timer-1 Starts
Timer-2 Starts
Loop Starts
Loop Ends
End
Completed Timer-1
Completed Timer-2
Completed Timer-0
*/
```
Note - If their is an blocking piece of code inside an async function which infinitely blocks then other async functions in event queue will never be executed.

**console.log** - It is not a native javascript feature and whether it runs synchronously or asynchronously is determined by the runtime.In Node.js environment console.log works synchronously for **files.**

```js 
y=setInterval(function exec(){console.log("Second One")},500);
clearInterval(y);//clears the interval
```

setInterval is used to execute the callbacks after the specified interval of time. In chrome this ID y is a number whereas in Node env this is an object.Therefore based on different environment different implementation of runtime functions is there.