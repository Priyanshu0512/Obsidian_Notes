Types of languages 
1. Imperative languages - In these kinds of languages each and every step needs to be given to the program to get the required task done.
2. Declarative languages - In these kinds of languages only the operation which needs to be performed needs to be given to program. The implementation of how that task needs to be performed is handled internally by the language. Ex- mysql
3. pseudo-Declarative Implementation - These are not as such programming languages in itself but are Imperative languages but with the use of  some coding practice we can mimic the declarative behaviour on a broader and higher level.


**Iterators** - Iterators is an object which defines a sequence and potentially returns a value upon its termination.It is like a stream of data automatically being provided upon calling it.
Custom implementation of an iterator
```js
function fetchNextElement(array){
    let index=0;
    function next(){
        if(index >= array.length){
            return undefined;
        }
        const nextElement =array[index];
        index++;
        return nextElement;
    }
    return {next};

}

const elementFetcher = fetchNextElement([1,2,3,4,5,6]);
console.log(elementFetcher.next());
console.log(elementFetcher.next());
console.log(elementFetcher.next());
console.log(elementFetcher.next());
console.log(elementFetcher.next());
console.log(elementFetcher.next());
console.log(elementFetcher.next());
console.log(elementFetcher.next());
/*
Output 
1
2
3
4
5
6
undefined
undefined
*
```

In the above snippet the fetchNextElement returns the {next} object to elementFetcher and upon calling it due to closure property it remember the index and increments it on every call to return the array element.

**Inbuilt Iterator in array prototypes**
```js 
arr=[1,2,3,4]
iterator=arr[Symbol.iterator]();   
Array Iterator {}[[Prototype]]
iterator.next();
{value: 1, done: false}
iterator.next();
{value: 2, done: false}
iterator.next();
{value: 3, done: false}
iterator.next();
{value: 4, done: false}
iterator.next();
{value: undefined, done: true}
```
Every array has an Symbol.iterator which returns an array iterator  object with next() function.
This iterator has two keys - 
value - It stores the currently value being extracted.
done - The done key stores whether end of the array has been reached or not and returns true or false accordingly.

**Note** - Done key is necessary to represent end of an array instead of returning undefined in value as arrays in javascript are heterogeneous in nature and therefore they might contains a value which is itself undefined.

# Generators

While custom iterators are a useful tool, their creation requires careful programming due to the need to explicitly maintain their internal state. **Generator functions** provide a powerful alternative: they allow you to define an iterative algorithm by writing a single function whose execution is not continuous. Generator functions are written using the [`function*`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*) syntax.

**Note - Generators do not start the function execution when called upon but they return a special type of iterator called as Generator.
**

```js
function* generator(){
    console.log("Inside the generator function");
    yield 1;
    yield 2;
    console.log("Still Inside");
    yield 3;
}

const iter=generator();

console.log(iter.next());
console.log(iter.next());
console.log(iter.next());
console.log(iter.next());
/*
Output
Inside the generator function
{ value: 1, done: false }
{ value: 2, done: false }
Still Inside
{ value: 3, done: false }
{ value: undefined, done: true }
*
```

Generator function are special types of functions which can stop their execution and some point down in their code execute commands outside their scope and return back to executing there code.
**This to and fro of chain of execution can be achieved using the yield keyword.** Whenever in the execution the yield keyword is encountered then the function returns an iterator object which value same as after the yield keyword and done the key to represent whether all the function have been executed in the generator function or not.
Note - If inside the generator function return keyword is encountered then it ends the function then and there.

Example - 
```js
function* makeRangeIterator(start = 0, end = Infinity, step = 1) {
    let iterationCount = 0;
    for (let i = start; i < end; i += step) {
      iterationCount++;
      yield i;
    }
    return iterationCount;
}```


# Async Await

Custom implementation of Async await using generator functions
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
        console.log("Starting to write to the file the data ",data);
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


function* steps(){
    const downloadData= yield downloader("xyz.com");
    console.log("Downloaded data is " ,downloadData);
    const filewritten = yield writeToFile(downloadData);
    console.log("Data Written to the file ", filewritten);
    const uploadResponse = yield uploader(filewritten);
    console.log("Successfully uploaded the data to the          URL", uploadResponse);
    return uploadResponse;
}

const iter= steps();
const future = iter.next();
future.value.then(doAfterReceiving);

function doAfterReceiving(value){
    let future= iter.next(value);
    if(future.done) return;
    future.value.then(doAfterReceiving);
}
/*
Output
Starting to download from xyz.com
Downloading the Data.....
Downloading Completed
Downloaded data is  ABCD
Starting to write to the file the data  ABCD
Writing to the file....
Written to the file successfully
Data Written to the file  data.txt
Starting to upload the file data.txt
Uploading Completed
Successfully uploaded the data to the URL abc.com*
```

With Async Await
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
        console.log("Starting to write to the file the data ",data);
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


async function steps(){
    const downloadData = await downloader("xyz.com");
    console.log("Downloaded data is " ,downloadData);
    const filewritten = await writeToFile(downloadData);
    console.log("Data Written to the file ", filewritten);
    const uploadResponse = await uploader(filewritten);
    console.log("Successfully uploaded the data to the         URL", uploadResponse);
    return uploadResponse;
}

steps();
```

While using an async function the .next() iterator sort of implementation is handled automatically.
Note - Any function which async before it automatically becomes an promise bases function.Also await keyword is allowed only inside async function with an exception.

Basically what happens is that these async functions with await are completed asynchronously. Whenever the await keyword is encountered the execution comes out of the async function and goes back inside when the call-stack is empty and all global piece of code has been executed. The resolves promise is comes from micro-task queue to the call-stack and the execution of async functions again starts.

**Handling Rejection in Async Await** 
```js
async function steps(){
    try{
        const downloadData= await downloader("xyz.com");
        return downloadData;
    }
    catch(error){
        console.log("Successfully Handled the error",              error)
    }
    finally{
        console.log("Ending");
    }
}
steps();
/*
Output
Starting to download from xyz.com
Downloading the Data.....
Downloading Completed
Successfully Handled the error ABCD
Ending
/* 
```

**Managing Multiple Promises Using Promise.all**
```js
function downloader(url,time){
    return new Promise(function exec(resolve,reject){
        console.log("Starting to download the data                 from",url);
        setTimeout(function exe(){
            const content ="ABCD";
            console.log("Download Completed");
            resolve(content);
        },time);
    });
}

const p1 = downloader("xyz.com",1000);
const p2 = downloader("xyz2.com",2000);
const p3 = downloader("xyz3.com",3000);
Promise.all([p1,p2,p3]).then(function fulfilhandler(value){
    console.log(value);
})
/*
Output
Starting to download the data from xyz.com
Starting to download the data from xyz2.com
Starting to download the data from xyz3.com
Download Completed
Download Completed
Download Completed
[ 'ABCD', 'ABCD', 'ABCD' ]
*
```

Note -Promise.all fulfilhandler is executed only when all the promises are resolved and returns single promise.It rejects if any of the promise rejects.
**Refer to Promise.all page of MDN .**
