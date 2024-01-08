
**Javascript is a Lexically Scoped language.**

**Lexical Scoping** - In Lexical scoping  all the scopes are determined prior to execution i.e. during compilation.
Ex -
 ```js
var name = "Priyanshu";
       function fun(question){
           console.log(name , question) ;
       }
       function gun(){
           var name = "Ishu";
           fun("Hi"); 
       }
       gun();
```
 This would print Priyanshu Hi.
    Scope resolution will be done as it  discussed in the [[Scopes]].

**Dynamic Scoping** - In dynamic scoping scope resolution is done during the execution phase.
EX- **If**javascript were to be a language which supports Dynamic scoping then 
```js
var name = "Priyanshu";
       function fun(question){
           console.log(name , question) ;
       }
       function gun(){
           var name = "Ishu";
           fun("Hi"); 
       }
       gun();
       This would print Ishu Hi.
```


Some Example - 
```js
1.  var fun = 123;
	function fun(){
	      return 'fun2';
	}
	console.log(fun);
```
	This snippet prints 123 as expected. 

 ```js
2. var fun = 123;
	function fun(){
	      return 'fun2';
	}
	console.log(fun());
```
   This will throw  an error Undefined Function.
	This is because during the parsing phase as the name of variable fun and function fun are the same hence when the complier come to the function fun during parsing then fun would be already  be in the global scope and hence function fun would not be allocated any scope.
	Hence on calling is undefined function error is thrown.

 ```js
 3. var fun;
	function fun(){
	      return 'fun2';
	}
	console.log(fun);
```
This will not print fun2 but will display [ Function: fun]
	This is because variable fun was not assigned any value. 
	But console.log(fun()); will print fun2.

```js
4. var fun = 123;
	 var fun =  function (){
	      return 'fun2';
	}
	console.log(fun);
	This will print [Function: fun] whereas 
	console.log(fun()); will print fun2.
```
This line **var fun function()** is called function Expression and will be discussed in detail in [[Function Expression]].
 