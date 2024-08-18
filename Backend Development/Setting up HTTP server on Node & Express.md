**127.0.0.1**  - It is a loopback Internet protocol address also known as localhost used to establish an IP connection to the same machine or the computer being used by the end user.

```js
const http =require('http'); //Required the HTTP module
//Using the createServer function we can create a basic HTTP server from the http module
// This function return a server object and takes a callback as an argument.
PORT = 5500;
// This function only creates a server but doesn't starts it.
const server =http.createServer(function listener(request,response){
    //This callback listener function kinds to listens to the every HTTP request we make.
    //request -> Through request we can get the details of the incoming HTTP request.
    //response -> we will be able to configure the response to an incoming HTTP request.
    // console.log("Incoming request details",request);
    // console.log("Response object details",response);
    if(request.url =='/home'){
        console.log(request.method);
        response.end("WELCOME TO HOME");
    }
    console.log("Request Received");
});

server.listen(PORT,function exec(){
    //This callback is executed on successful booting up of the server.
    console.log(`Server is up and running on PORT: ${PORT}`);
})```

Note - response.send does not exist in http module of node but is present in express.js
In order to send the data chunk by chunk use response.write() multiple times then end with response.end(). If response.end() is not used then the page will keeping loading waiting for more data to come.

Note - We cannot sent Post request from the URL bar of the browser but programatically we can.

**Server on Express**
```js
const express =require('express');
const app = express(); // Creates the server.
const PORT = 5500;

app.get('/home',(request,response)=>{
    response.send("Welcome to the Home");
});

app.post('/home',(request,response)=>{
    response.json({
        message: "HI",
    })
});

app.listen(PORT,()=>{ //Boots up the server.
    console.log(`The server is up and running of port ${PORT}`);
});```

In express we can manually configure the server for different types of request.

```js
const express =require('express');
const app = express(); // Creates the server.
const PORT = 5500;

const mylogger =(req,res,next) =>{
    console.log("Logging from middleware-1");
    next();
}
const mylogger2 =(req,res,next) =>{
    console.log("Logging from middleware-2");
    next();
}
let middleware = [mylogger,mylogger2];

app.get('/home',middleware ,(request,response)=>{
    console.log("Inside the last middleware");
    response.json({message: "Last Middleware"});
});

app.post('/home',(request,response)=>{
    response.json({
        message: "HI",
    })
});

app.listen(PORT,()=>{
    console.log(`The server is up and running of port ${PORT}`);
});
/*
Output from terminal
The server is up and running of port 5500
Logging from middleware-1
Logging from middleware-2
Inside the last middleware

Output on sending GET request
{
  "message": "Last Middleware"
}
```

**Express Router** - It creates a modular, mountable route handlers.A router instance is itself an middleware.

**app.use('/path',callback)** - This function mounts the specified middleware or function at the specified path. The middleware function is executed when the requested path matches the path.
Note- Whenever .use() is used the function or the properties gets applied to all the request in they match the patch.


### Global Catches 
In order to not expose the server data upon occurrence of an error global catches are present which are executed if error are encountered in the middle-wares  or in some other part of the code.
```js
app.use((err,req,res,next)=>{
// Error handling logic 
})
```
Note - This should be present in the last of the file in order to handle errors from all the routers above it. 


```js 
app.use(express.json())
```
The above line is used to specify the type of data that is incoming in the request body. 
This ensures that data is parsed according to its type.