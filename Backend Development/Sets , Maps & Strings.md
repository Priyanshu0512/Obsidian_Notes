
## Sets 

- Sets are iterable Data structures which only stores uniques values. On peculiar thing about sets is that once data is entered into the set it cannot be retrieved but can only be checked for its existence in the set. 
- Some common methods of sets are as follows 

```js
const orderSet = new Set (['pizza', 'pasta']);
const orderSet2 = new Set('age'); // { 'a' ,'g' ,'e'} 


orderSet.size; // Returns the size of the set.
orderSet.has('pizza') // Returns a boolean checking for existence of argument.
orderSet.add('cheese') // Adds the argument to the set.
ordrSet.delete('pasta') // Deletes the entered argument in the set.
orderSet.clear() // Deletes all the elements in the set.

//DeStructuring object
console.log([...orderSet]) // ['pizza','pasta']
```


### Maps 

- Maps are iterable Data Structures which stores key values pair.
- The advantages of Maps over normal objects is that in Maps the Keys need not necessarily be strings. It can be any array , boolean or anything else.
- Some common methods of sets are as follows 

```js 
const rest = new Map();

rest.set('name' , 'pizza'); // This returns the Map. This is similar to add.
rest.get('name'); // Retrieves the value of the mentioned key. It key is not present then it returns undefined.
rest.has('name'); // Returns boolean depending on the presence of the mentioned key.
rest.delete('name') // Returns booleand depending upon the completion of the deletion process.
rest.size;
rest.clear(); // Returns undefined. 

// Convert Object to Map 
const hoursMap = new Map( Object.entries(objecjName));

// DeStructing Maps
console.log(...rest) // [ 'name', 'pizza' ] 

```

- Since Maps can have keys of any data type hence it could be used to incorporate some business logic. An example of it is in the snippet below.

```js

const question = new Map([
  ["question", "Which is the best programming language"],
  [1, "C"],
  [2, "Java"],
  [3, "Javascript"],
  ["correct", 3],
  [true, "Correct Answer"],
  [false, "Wrong Answer"],
]);

for (const [key, value] of question) {
  if (typeof key == "number") {
    console.log(`${key}. ${question.get(key)}`);
  }
}

const Answer = 3;
console.log(question.get(question.get("correct") === Answer));

Output - 
1. C
2. Java
3. Javascript
Correct Answer

```


### Strings

- When a string method is called then the string is converted to a String object on with the string methods are called. 
- Some common String methods are as followed

```js 
const str= new String("priyanshu") // typeof str is object.

str.indexOf('a');
str.lastIndexOf('b'); // It not present then returns -1.
str.slice(startingIndex, endingIndex) // Works like the substring function.
str.toLowerCase();
str.toUpperCase();
str.trim(); // Clears leading white spaces.
str.replace('a', 'b');
str.includes('ans'); // Returns boolean
str.startsWith('p') // Returns boolean
str.endsWith('u');
str.spilt('+'); // Returns an array by splitting the string at the mentioned literal.
[...something].join(' ');
str.padStart(lengthOfString, 'Padding symbol');
str.padEnd(lenghtOfString, 'Padding symbol');

```

**Regular Expression** - In order to replace all the characters in the string regular expressions are used.

```js
const str3 = "door door door";
console.log(str3.replace(/door/g, "gate")); // gate gate gate
```