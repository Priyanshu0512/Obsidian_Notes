
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
