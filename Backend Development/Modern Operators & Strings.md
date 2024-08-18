

### Destructing Objects 

```js
const { property1 , property2 ,property3 } = objectName;

// To change the names of th variables different from property name 

const { property1 : Name1 , property2: Name2 , property3 : Name3} = objectName;

// Giving Default Values 
const { property1 : Name1 = defaultValue , property2 : defaultValue};

// Mutating Variables 
 let a = 2;
 let b = 4;
 ({a, b} = object)
```

Giving default values to the property is helpful in cases when a particular property is being accessed by does not exists.

### (...) Spread Operator

It can only be using when building an array or passing argument's in the function.It also works on objects. It is used on the right side of the assignment operator.

```js
const arr = [1,3,4];
const newArr = [5,6, ...arr]; // newArr = [5,6,1,3,4];

console.log(arr) // Output- [1,3,4];
console.log(...arr) // Output - 1 3 4; Notice each element is separate.

//Copying Arrays
const copyArr = [ ...arr]; 
```

Note - While copying arrays in the above example it only creates a shallow copy of the array.


### Rest Pattern & Parameters
 It is opposite of the **Spread** Operator and is used on the left side of the assignment operator.
 It creates a new array of the remaining elements which are not extracted. Works also on Objects.
 **Note - The Rest pattern must be the last element of the array in which it is used.**
 
```js 
const [pizza , pasta , ...otherFood ] = [...menu];

const day = ["monday", "t", "w", "th", "f", "sat", "sun"];
const [m, , ...days] = [...day]; // Skipped element at index 1

console.log(m);
console.log(days);

 Output - 
 monday
[ 'w', 'th', 'f', 'sat', 'sun' ]


// Fucntions 
const add = function (...numbers) {
   console.log(numbers);
};

add(2, 3);
add(2, 4, 5);

```

Rest Pattern are frequently used with functions where the number of argument's are not known or they keep changing.

### Nullish Coalescing Operator(??)

- This operator was introduced in the ES20 and it considered only **Nullish** values which are `null` and `undefined` and skips `0` and `''`.
```js
const guest = 0;

console.log(guest || 10);  // Outputs = 10 (But logical should be 0 guests)
console.log(guest ?? 10);  // Outputs = 0 ( Considers only nullish values)
```

### Optional chaining (?.)
- This operator returns undefined if a nested property is being accessed which simply does not exist instead of giving an error message.
```js
console.log(restaurant.openingHours?.mon?.open)
// This will return undefined if openingHours does not exists and if it exists then  it checks if mon exists inside it or not.

console.log(restaurant.order?.(0,1)  || "Method does not exist") //also works on methods.
```

Without the use of Optional Chaining Operator if `mon` as property would not have existed then `undefined` would have been returned and the `open` property would be accessed on `undefined` which would have lead to an error message.
