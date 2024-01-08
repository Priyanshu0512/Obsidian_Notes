1. Promises are readability Enhancers.
2. They solve the problem of Inversion of control in callbacks.

In JS Promises are special types of objects that get returned immediately when called.They act as placeholder for the data we expect to get sometime in the future or Promise is a placeholder object for an eventually deferred computation.(possibly asynchronous).

In these Promise objects we can implement the functionality we want to execute when the future task is done.

**Creating a Promise** - 
1. Creation of Promise object is synchronous in nature.(Promise creation is native to javascript)
2. States of Promise object 
    1. Pending  state - When promise object is created this is the default state. It represents work in progress.
    2. Fulfilled state - It represents successful completion of operation.
    3. Rejected state - It represents that operation was not successful.

Promise are created using new keyword and it takes a callback(called executor function) with two parameters resolve and reject.
If resolve function is called Promise goes to a fulfilled state whereas on calling a reject function Promise goes to a rejected state. If either of them are not called then Promise remains in pending state forever.

Note - In Pending state the value property of promise object is undefined.
Otherwise it takes the value of argument with which resolve or reject function is called.It multiple arguments are called them only the first argument is considered. Also only first resolve or reject is considered in case of multiple rejects or resolves.
```js
function createNewPromise(x){
  return new Promise(function executor(resolve,reject){
     setTimeout(function exec(){
       if(x%2==0)
           resolve(x);
       else
           reject(x);
    },10);
  })
};
y=createNewPromise(6);
console.log(y);
```

Note - The executor callback is called immediately when promise is created.

**Consuming a Promise** - 
While consuming a Promise we can attach the functionality of when happens when the Promise is either rejected or resolved.
```js
function createNewPromise(x){
    return new Promise(function executor(resolve,reject){
      console.log("Inside the executor call - Starting");
      setTimeout(function exec(){
        if(x%2==0)
           resolve(x);
        else
           reject(x);
     },10000);
    console.log("At the end of the executor callback")
  })
};
console.log("Starting....");
const y=createNewPromise(6);
console.log("Waiting for the Promise to get either resolve or rejected");
console.log("Currently the Promise object is",y);

y.
then(
  function fulfillHandler(value){
    console.log("Inside the fulfill Handler");
    console.log("Promise resolves with value ", value);
    console.log("Promise after getting resolved",y)
},
  function rejectionHandler(){
    console.log("Inside the rejection Handler");
    console.log("Promise rejected with the value",value);
    console.log("Promise after getting rejected",y);
})
/* Output - 
Starting....
Inside the executor call - Starting
At the end of the executor callback
Waiting for the Promise to get either resolve or rejected
Currently the Promise object is Promise { <pending> }
Inside the fulfill Handler
Promise resolves with value  6
Promise after getting resolved Promise { 6 }
*/
```

.then  - It registers the handler function for the promise objects which are executed on promise rejection or resolution.It register the handlers despite the promise being resolved or rejected. It is just an registering statement.

The promise is object maintains two arrays -
 1. On fulfilment array 
 2. On rejection array 
 They store the multiple fulfilment and rejections handlers which are to be executed on promise rejection or resolution.

Apart from the Callstack , callback queue and event loop there is an another queue known as an Micro-task queue.(Macro-task queue)

**Micro-task Queue** - This queue stores all the fulfilment and rejection handlers which are to be executed once the callstack becomes empty and all global piece of code has been executed.
**Note - The event loop prioritises the function in micro-queue  over the callback queue.**

```js
function createPromise(num){
    return new Promise(function executor (resolve,reject){
        if(num==1)
            resolve(num);
        else
            reject(num);
     })
}

setTimeout(function exec(){
     console.log("Completed the timer");
},0)

const p=createPromise(1);
p.then(
    function fulfilhandler1(){
        console.log("Inside the fulfill handler 1");
     },
).then(
     function fulfilhander2(){
        console.log("Inside the fulfill handler 2");
     }
)

console.log("End");
/* Output 
End
Inside the fulfill handler 1
Inside the fulfill handler 2
Completed the timer
*
```

Example - 
```js
console.log("Start of the file");

function blockingloop(){
    for(let i=0;i<10000000;i++){}
}

let p1=Promise.resolve("resolved");
    p1.then(function fullfilled(value){
        console.log("Promise 1 has been ",value);
    blockingloop();
})

let p2=Promise.resolve("resolved");
    p2.then(function fullfilled(value){
        console.log("Promise 2 has been ",value);
    setTimeout(function exec(){
        console.log("Ok Done");
   });
})

let p3=Promise.resolve("resolved");
     p3.then(function fullfilled(value){
        console.log("Promise 3 has been ",value);
})

setTimeout(function timer2(){
    console.log("Timer 2 done");
},1000);

console.log("End of the file");
/* Output 
Start of the file
End of the file
Promise 1 has been  resolved
Promise 2 has been  resolved
Promise 3 has been  resolved
Timer 1 done
Timer 2 done
Ok Done
*
```


**How Promise  resolve the problem of Inversion of Control?**
In Promise based syntax the callback which is to be execute on completion of some task is executed from where the request was initially made. 
     Also when a promise can only be resolved or rejected once only here the problem of multiple instance of a callback being executed is also eliminated.
     Further more in callbacks the task which needs to executed after the completion of piece code needed to be written then and their only but in promises they are handled by the  user according to their needs.

**.then** - It returns another promise object either in resolved state or in rejected state depending upon the resolution of the promise it had.
Note - In .then chaining whatever is being returned from the fulfilHandler or rejectionHandler becomes the value of promise object returned by .then which is passed on to the next .then chained.
Note - If nothing is returned by the Handler then undefined is returned by default.
Primitive values if returned are considered to be already resolved promises.
Example - 
```js 
Promise.resolve("foo")
    .then((string)=>
        new Promise((resolve,reject)=>{
            setTimeout(()=>{
                string+="bar";
                resolve(string);
             },10000);
     }),
)
.then((string)=>{
     setTimeout(()=>{
         string +="baz";
         console.log(string);
    },1);
    return string;
})
.then((string)=>{
    console.log(string);
});

/*Output
foobar
foobarbaz
*
```

**Callback Based Code Implementation with Promises** 
1. Callback bases implementation
```js 
function downloader(url,download){
    console.log("Starting to download the data from ",       url);
    console.log("Downloading the Data.....");
    setTimeout(function exec(){
        const content="ABCD";
        console.log("Downloading completed");
        download(content);
    },5000);
}

function writeToFile(data,write){
    console.log("Starting to write file the data",data);
    console.log("Writing to the file.....");
    setTimeout(function exex2(){
        const filename="data.txt";
        console.log("Written to file successfully");
        write(filename);
    },5000);
}

function uploader(data,filename, upload){
    console.log("Starting to upload the file",filename,"    with the data " ,data);
    setTimeout(function exec3(){
        const newurl = "abc.com";
        console.log("Uploading Completed");
        upload(newurl);
    },5000);
}

downloader("xyz.com",function download(data){
    console.log("Successfully downloaded the content which is ", data);
    writeToFile(data,function write(filename){
        console.log("Successfully Written the data to the file", filename);
        uploader(data,filename,function upload(newurl){
            console.log("Successfully uploaded the data to the URL", newurl);
        })
    })
})
/* Output
Starting to download the data from  xyz.com
Downloading the Data.....
Downloading completed
Successfully downloaded the content which is  ABCD
Starting to write file the data ABCD
Writing to the file.....
Written to file successfully
Successfully Written the data to the file data.txt
Starting to upload the file data.txt  with the data  ABCD
Uploading Completed
Successfully uploaded the data to the URL abc.com
*
```

2. Promise bases Implementation
```js
function downloader(url){
    return new Promise(function download(resolve,reject){
        console.log("Starting to download from",url);
        console.log("Downloading the Data.....");
        setTimeout(function exec(){
            const content ="ABCD";
            resolve(content);
            console.log("Downloading Completed");
        },5000)
    })
}

function writeToFile(data){
    return new Promise(function write(resolve,reject){
        console.log("Starting to write to the file the             data ",data);
    console.log("Writing to the file....");
    setTimeout(function exec(){
        const filename= "data.txt";
        resolve(filename);
        console.log("Written to the file successfully");
   },5000)
  })
}

function uploader(filename){
    return new Promise(function upload(resolve,reject){
    console.log("Starting to upload the file",filename);
    setTimeout(function exec(){
        const newurl="abc.com";
        resolve(newurl);
        console.log("Uploading Completed");
        })
    })
}

downloader("xyx.com")
.then(
    function fulfilhandler1(content){
      console.log("Successfully downloaded the data which        is",content);
      return writeToFile(content);
})
.then(
     function fulfilhandler2(filename){
        console.log("Successfully written the data to the          file ",filename);
        return uploader(filename);
})
.then(
     function fulfilhandler3(newurl){
         console.log("Successfully Uploaded the data to             the new url", newurl);
})
/*
Output
Starting to download from xyx.com
Downloading the Data.....
Downloading Completed
Successfully downloaded the data which is  ABCD
Starting to write to the file the data  ABCD
Writing to the file....
Written to the file successfully
Successfully written the data to the file  data.txt
Starting to upload the file data.txt
Uploading Completed
Successfully Uploaded the data to the new url abc.com
*/
```

Example 2 - 
```js
function* generator(){
    console.log("Inside the Generator");
    const x=10;
    yield 9;
    const y= x+(yield 30);
    console.log("Value of y is ", y);
}

console.log("Start");
const iter = generator();
console.log(iter.next());
console.log(iter.next());
console.log(iter.next(15));
console.log("End");
/*
Output
Start
Inside the Generator
{ value: 9, done: false }
{ value: 30, done: false }
Value of y is  25
{ value: undefined, done: true }
End
*
```