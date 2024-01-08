```js
function process(){
    let i=1;
    function innerprocess(){
        i+=1;
        return i;
    }
    return innerprocess;
}

let res = process();
console.log(res);
console.log(res());
console.log(res());
console.log(res());
/*
Output 
[Function: innerprocess]
2
3
4
*
```

In the above code snippet function process gets into the call-stack and returns function innerprocess into the variable res and gets removed from the callstack.
Now the question arises that how this function innerprocess is returning a value of i upon being called as function process has been removed from the call-stack which as the scope of i. 

**The answer to this is the closure property of the function innerprocess which remembers the memory address of the variables being used inside it despite them being not process inside its scope.**

The closure property can be found in the function prototype of the function in the scopes key of the object prototype.

**Note- The closure property remembers the memory address and does not create a copy of the variable.**