
- Arrays in Js are mutable even though if declared with const.

```js
 const years = [2001,2002,2003];
 console.log(years+10);

 Output - 2001,2002,200310 (concatenation)
```

**Basic array methods**
- `.push(argument)`- Adds element to the end of the array. Returns the length of the new array.
- `.unshift(argument)` - Adds the element to the start of the array and return new length.
- `.pop()` - Removes the last element of the array. It return the removed element.
-  `.shift()` - Removes the first element of the array and returns the removed element.
- `.includes(argument)` - Returns true or false based on the presence on the argument in the array. It checks with strict equality operator.
- `.indexOf(argument)` - Return the index of the argument if present else returns -1.


## Objects 

- The properties of an object can be accessed in two ways 
   1. `.` - Dot operator -> It requires the exact property name to be accessed.
   2. `[]` - Bracket Notation -> It can contain an expression which results in a property name.

- If a property is accessed which is simply not present in the object it returns `undefined.`
- In order to create a property in an object use the following syntax 
```js
const object.location = "Something";
or 
const object['location'] = "Something";
```

**Note :- A function associated with a Object is called a Method.**

```js
const obj1 = {
   name: 'something'
}
const obj2 = Object.assign({},obj1);
```
This method only creates a shallow copy of the object mentioned and not a complete clone of the object. What this means is that only the first level properties are only copied and if nested reference objects are present then they will keep pointing to the original memory address.


### Enhanced Object Literals

- In order to include and external object literal into an object literal only the name of the incoming object literal needs to be written which any key value pair to be included.
```js
 const obj1 ={
    name: "someting"
 }

 const obj2 ={
    age : 21,
    obj1, // Instead of obj1 = obj1, 
 }
```

- When creating a function expression inside the object the `function` keyword need not be written.
```js
const obj1 = {
add(a , b){
    console.log(a+b);
    }
}
```

- Property names can also be computed.\

**Looping over Objects** 

- `Ojbect.keys(objectName)` - Returns an array containing all the key names.
- `Object.values(objectName)` - Returns an array containing all the values in the object.
- `Object.entries(objectName)` -  Returns an array which contains key value pairs  of the object in form of the array.