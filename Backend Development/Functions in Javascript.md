A function is a black box which takes a input and processes it to give an output.

Functions are of two types
1. User defined functions
2. In-built functions

Defining a Function
     Syntax - 
   ```js
 function functionName(input1, input2){
    //logic
    return argument; 
    }
    ex- function isEven(num){
    if(num%2 == 0){
         return true;
     }
     else{
        return false
     }
    }
```

In console.log console is a function which has a log keys in which it has the function which prints the entered value.
**console.log returns undefined.** 
*In javascript if user does not return a value manually then the function by default returns undefined. In javascript ever function returns something.*

**Arguments and Parameters**

```js
 function add (x,y){
    let c = x+y;
    return c;
}

let a= 10;
let b= 20;
let result = add(a,b);
console.log(result);
```

Here x and y are called parameters whereas a and b are arguments.Arguments are passed and parameters are expected.
Note- If the number of arguments passed are more than the number of parameters then the intials arguments will be passed only.

**Higher Order Functions** - Functions which take another function as an argument or return a function are called higher order function.
Ex- 
```js
     function f( x , fn){
        console.log(x);
        console.log(fn);
        fn(); 
    }
    f(10, function exec(){
       console.log("I am a expression passed to a HOF.");
    })
```


arr.sort( )- The default implementation of .sort is to sort the given values in lexicographical manner. 
In ordr to sort the values in a specific manner as the .sort is a HOF there a comparator function can be passed to specify the way of sorting.
For sorting in ascending order 
arr.sort(function(a,b){
    return a-b;
})


### Functions returning Functions

```js
const greet = function (greet) {
  return function innerGreet(name) {
    console.log(`${greet} ${name}`);
  };
};

greet("Hi")("Connor"); // Output Hi Connor 

// In terms of arrow functions
const greet = (greet) => (name) => console.log(`${greet} ${name}`);

greet("Hi")("Connor"); // Output Hi Connor 

```


### Call Method

- Call method is used to specify where the this keyword should point to.

```js
const lufthansa = {
  airline: "lufthansa",
  iataCode: "LH",
  bookings: [],
  book(flightNum, name) {
    console.log(
      `${name} booked a seat on ${this.airline} flight${this.iataCode}${flightNum}`
    );
    this.bookings.push({ flight: `${this.iataCode}${flightNum}`, name });
  },
};

lufthansa.book("23", "Priyanshu");

const indigo = {
  airline: "indigo",
  iataCode: "IN",
  bookings: [],
};

const book = lufthansa.book; // Now Book is like a normal function and not a mehthod.

// book("27", "Connor"); 

book.call(indigo, "27", "Connor");
book.call(lufthansa, "27", "Connor");
console.log(indigo.bookings);
console.log(lufthansa.bookings);
```

- Now `book("27", "Connor"); ` in this function call book is a normal function therefore in its function body  this keyword points to undefined in `strict mode` and when it tries to access the bookings property on `undifined` it throws and error.
- While using the `call()` the object name is mentioned to which the this keyword should point to hence changing the pointing state of the this keyword. 

### Apply Method 

 - It works in a similar way to call method but it takes  an array of arguments instead of individual argument's.

### Bind Method

- Bind method does not calls the function immediately but it bind the `this` keyword to the mentioned object.
```js
const bookIn = book.bind(indigo);
const booKIn29 = book.bind(indigo, 29); // partial application 

bookIn("28", "Connor");
booKIn29("Priyanshu");
console.log(indigo.bookings);

Output 

[
  { flight: 'IN28', name: 'Connor' },
  { flight: 'IN29', name: 'Priyanshu' }
]
```

- `Bind` method is also used for partial application wherein the values of the arguments to be passed are fixed in advance using the bind() method call. 
**Note - The first argument of the bind method is pointing direction of the this keyword.**
- In case of partial application if this keyword is not to be used then it is industry practice to point it to `null`.