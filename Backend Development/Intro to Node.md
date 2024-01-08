In Order to solve the problem of different browsers providing different runtime feature and handling them differently a sort separate runtime was created by extracting of mimicking the features of browser runtime.
     In 2009 Ryan Dahl created Node.js which enable the user to directly run the javascript runtime into the terminal.

**Javascript runtime is nothing but additional set of resources which are been provided which are not native to Ecmascript.**

Note - Node js not only adds but also removes the functionality which are not  required to processed in to the terminal . It brings JS features into the terminal so as to interact which OS based features.
Event loops, micro and macro task queues and callback queues are all provided by runtime to handle the asynchronous nature of the javascript.

# Components of Node.js

1. V8 Engine developed by google.( One of the fastest JS Engine.)
2. JS API's/Functions
3. libuv - It is an multi platform C library that provides supports for asynchronous I/O operations based on event loops.It makes Node js compatible and non-blocking for all operating systems.
4. Bindings - These are special programs that facilitate the interactions between Node js and libuv library.

**Globals** - They are JS objects and variable etc. which are available everywhere to access.
The return of setTimeout in the node environment a setTimeOut object whereas in the browsers it is a number.
Note - In certain configurations all globals are not available for use.Also global object should not be changed.

[[Module Pattern in Node]]

Using the File System (fs)module file system can be accessed and
manipulated. It is be can accessed for both promise and callback based syntaxes in the following ways- 
    For Promise based syntax -
    import * as fs from 'node:fs/promises';
    For Callback bases syntax - 
    import * as fs from 'node:fs';

**Top level await** - Await can be used on its own (outside the async function)  at the top level of the module. It means that a  modules with child modules having await will wait for child modules to complete their execution after which it will start executing , all the while not blocking the other child modules from loading.

In order to read file lines the following syntax in used 
1. In ES6 moduleing top level await is used in the following way. 
      ```js
 import { open } from 'node:fs/promises';

 const file = await open('./some/file/to/read');

 for await (const line of file.readLines()) {
  console.log(line);
}
```
2. In CJS moduleing and IIFE is being implemented in the following way.
    ```js
  const { open } = require('node:fs/promises');

 (async () => {
  const file = await open('./some/file/to/read');

  for await (const line of file.readLines()) {
    console.log(line);
  }
})();
```

To used to the Readfile method following syntax has to be followed.
```js
import { readFile } from 'node:fs/promises';
try {
  const filePath = new URL('./package.json', import.meta.url);
  const contents = await readFile(filePath, { encoding: 'utf8' });
  console.log(contents);
} catch (err) {
  console.error(err.message);
}
```

Here **import.meta.url** gives the absolute file path.()

In order to write to a HTML file using templeted string following can be done:-
```js
const data = {
       name : "Priyanshu",
       work : "Delhi Technological University",
       age : "20"
}
for (const [key, value] of Object.entries(data)){
       contents = contents.replace(`{${key}}`,value)
}
console.log(contents);
```

Here the Object.entries(data) is an helper function which returns an a 2-D array(in this case) where the first entry of first subarray will be the key and second entry will be the value like- 
```js
[
  [ 'name', 'Priyanshu' ],
  [ 'work', 'Delhi Technological University' ],
  [ 'age', '20' ]
]
```
Function like Object.keys(data) anad Object.values() are also available and they work in the same manner as above but give only keys and values repectively.
What is happening in the above function is that the object is being iterated over and the contents in the HTML file are being replaced whereever it finds the the mentioned template i.e. {${key}} with the corresponding value.
**Note - for...of syntax is an better way to iterate over something as a whole as it prevents humans errors of entering the wrong iterating values in looping statement.**

In order to create a HTML file write content to it writeFile command is used in the following way.
```js
import {readFile, writeFile} from 'fs/promises';
const filePath = new URL('./index.html', import.meta.url);
let contents = await readFile(filePath, { encoding: 'utf8' });
const data = {
     name : "Priyanshu",
     work : "Delhi Technological University",
     age : "20"
}
await writeFile(new URL('./newindex.html', import.meta.url) ,contents);
```
Here if the file is not present then the file will be created.

**Streams in Node.js**

When there is an huge amount of data to be handled with then instead of downloading or operating upon the data as a whole operations are perfomred on chuncks of data to reduce the system load.
Using the **pipe** function data from one stream can be piped to some other streams. In this way huge amount of data can be piped to different streams and reduce the system load significantly.

process.stdout is an output stream using which console.log is internally implemented. There is write function in it which prints the contents to the terminal. The difference between process.stdout.write and console.log is that console.log changes to a new line after printing its contents.(Similar to println and print in Java)
Note- Streams based functions are not avaliable with promise based syntax.

```js
const readstrema = fs.createReadStream(__dirname+'/run.txt');
```
Above line creates Readstream and __ dirname gives the path to the current file.
```js
const filewritestream= fs.createWriteStream(__dirname +'/write.txt');
```
While the above line creates a write stream to the mentioned file.

Below is snippet of write stream of data to both a file and print the data to the terminal while transforming the contents to uppercase.
```js
const fs = require('fs');
const TransformStream = require('stream').Transform;
const readstream = fs.createReadStream(__dirname+'/run.txt');
const filewritestream= fs.createWriteStream(__dirname +'/write.txt');
const transformedstream = new TransformStream({
     transform(chunk,encoding, cb){
         this.push(chunk.toString().toUpperCase())
     setTimeout(cb, 3000)
    }
})
const writestream = process.stdout;
const outputstream= readstream.pipe(transformedstream);
outputstream.pipe(writestream);
outputstream.pipe(filewritestream);
```

Note- Including Transform stream has a bit of different syntax as mentioned below.

Note - In order to run the node in watch mode in the dev key of the package.json file of the project write **node --watch path-of-file**
or if using nodemon write **npx nodemon path-of-file**.



