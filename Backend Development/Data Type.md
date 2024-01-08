There are a number of Data types in Javascript namely **Number, Boolean, String,  Symbol, Object, Undefined and Null.**
 1. Number- It can store any real value.
 3. String- They can be defined using a pair of Double quotes , single quotes or backticks.
 4. Boolean- Have only two values either true(1) or false(0).
 5. undefined- Something that does not have a value but can be defined later.
 6. object- If key-value pair need to be stored then objects are used for that purpose.
      Ex-
      ```js
    User1={
           name: "priyanshu",
           gender: "male",
           posts: {
           creation-date:"12/1/2023",
         . content: undefined,
                               }
      }
```
 6. Null- It represents empty value unlike undefined which represents a variable which has not been assigned any value yet.

Types of Data types-
1. Primitive - They are atomic in number . They can exist in themselves.Ex- boolean, interger etc.
2. Non-primitive - They are composition of other types.Ex- objects.


**Special Numbers in Javascript**
There are five special numbers in javascript +0, -0, NaN and +Infinity and -Infinity.
+0 and -0 - They are included in javascript to give quantities magnitude and direction. One practical implementation can be  like in the case of games. Suppose a character is deaccerlerating and when it comes to and halt them for again starting the motion in the same direction something like a +0 or an -0 will really come in handy for this purpose.

NaN- It stands for Not A Number.It can be helpful in situation where you are bound to return a number but there is not possible number to return.(basically invalid situation)
Ex- **10/null returns infinity but
       undefined/null returns NaN.**
 *NaN is the only number which is not equal to itself.*

String comparisions
let x = new String("abc"); This is an string object
let y = String("abc"); This is an String.
let z = "abc"; This is a String.
(x === y)- Returns false due to different types.
(y === z)- Returns true as both as string and have same values.
(x === z )- Returns false due to different types.

