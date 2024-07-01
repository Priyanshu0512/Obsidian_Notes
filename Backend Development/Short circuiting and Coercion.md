**Abstract Operations** - These are some set of algorithms that are present in the ECMAScript docs but they are not available for usage in ECMAScript i.e. They are there to help the documentations only. What this basically means is that in ECMAScript there are a lot of things that are done by the language internally. To explain what the language is doing internally these abstract operations are mentioned in the documentation.

**Coercion**(type-conversion) - The inter-conversion done by javascript while evaluating the expression is called coercion.
The detailed working of the logic gates are in the [[Operators in Javascript]].
This conversion can be manually done by the user which is called **explicit type-casting** or if the language based on certain rules automatically converts the types then it is called **implicit type-casting**.This implicit type-conversion is called **coercion**.

Coercion or type-conversion only happens to valid data-types in javascript.

**1. ToNumber(argument)** - 1. Undefined - Returns NaN. 2. Null - Returns +0. 3. Boolean - If true Returns 1 , if false returns +0. 4. Number - Returns the argument. 5. Symbol - Throws a TypeError Exception. 6. String - It converts the string into a number if possible otherwise it returns NaN. If a number is entered in Hexadecimal or Octal form then it is converts to the type of the argument with which is it being used.
Ex- console.log(1-"0xa"); Returns -9 and it converts the Hexadecimal value to binary which is 10 and then performs subtraction. 7. Object - ToNumber(ToPrimitive(argument, hint Number))

**2. ToPrimitive(input, preferred type)** -
It converts the input to an non-object type.But if the object is capable of being converted to multiple non-object types then it gives priority to the preferred type in conversion.
If input is already a primitive it returns the input else if it is an object then -
Step 1. If preferred type is none, hint -"default"
Step 2. If preferred type is String, hint -"string"
Step 3. If preferred type is Number,hint -"number"
NOTE - If the hint is default then generally it behaves like a Number if its preferred type is not changed due to some overiding or the above three statements. 4. After all these steps its calls **OrdinarytoPrimitive(input,hint)**

**3.OrdinarytoPrimitive(input,hint)** -It input is a object(as sent be ToPrimitive) then it does the following conversions else it throws an TypeError exception.
Step 1. Type(hint) is String and its value is either `"string"` or `"number"`.
Step 2. If hint is `"string"`, then 1. Let methodNames be « `"toString"`, `"valueOf"` ».
Step 3. Else, 1. Let methodNames be « `"valueOf"`, `"toString"` ».
Step 4. For each name in methodNames in List order, do 1. Let method be  Get(O, name). 2. If IsCallable(method) is true, then 1. Let result be  Call(method, O). 2. If Type(result) is not Object, return result.
Step 5. Throws a TypeError Exception
NOTE- By default toString()- returns a string [object Object]

**3.ToBoolean(argument)** -

1.  Undefined - false
2.  Null - false
3.  Boolean - return the argument.
4.  Number - If the argument is +0, -0 or NaN is returns false otherwise it returns true.
5.  String - If it is an empty string i.e. its length is zero then it returns false else is returns true.
6.  Symbol - true
7.  Object - true

    \*\*In javacript only null undefined +0,-0 , NaN and false are the only falsy value.

**Abstract Equality Comparison** -
It compares betweens two values(x == y) and produces true or false.This is performed using the following steps in order.
Step1- If type of x and y are equal then it called Strict equality operator.
Step2- If x is null and y is undefined or vice-versa then it returns true.
Step3- If typeof(x) is a Number and typeof(y) is a String or vice-versa then it returns result of x== ToNumber(y)
or ToNumber(x) == y respectively.
Step4- If typeof(x) is a Boolean or vice-versa then it returns result of ToNumber(x) == y or x == ToNumber(y) respectively.
Step5- If the typeof(x) is a String,Symbol or Number and typeof(y) is object and vice-versa then it returns x == ToPrimitive(y) or ToPrimitive(x) == y respectively.
Step6 - Else it Returns false.

**Strict Equality Conversion** - If compares (x === y) and Returns either true or false depending upon the comparison result.
Step1- If the typeof or x and y are different then it returns false.
Step2- If typeof x is a Number then 1. if x is NaN returns false. 2. if y is NaN returns false. 3. if x is the same number as y returns false. 4. if x is +0 and y is -0 or vice-versa then it returns true. 5. Else it returns false.
Step3- Returns SameValueNonNumber(x, y)

**SameValueNonNumber(x, y)**- 1. It assets that x is not a number and typeof x and y are both same. 2. If type(x) is either undefined or null returns true. 3. If type(x) is a string then it returns true if both the strings x and y are exactly similar otherwise false. 4. If type(x) is boolean then it returns true if both are either true or false else it returns false. 5. If type(x) is a symbol then if both x and y are same symbol then it returns true else it returns false. 6. If x and y havethe same object value(**same memory objects**) then it returns true else it returns false.

**4. ToString**(argument)- 1. Undefined - "undefined" 2. Null - "null" 3. boolean - True and False gets converted to "true" and "false" respectively. 4. String - Returns argument 5. Symbol - Throws **TypeError** Exception. 6. Object - ToString(ToPrimitive(argument,hint string)) 7. Number - Returns NumbertoString(argument)

**Corner Cases in Coerion** - 1. Both +0 and -0 are converted to 0 when converted to a string. 2. When a empty array is converted to a string then it gives empty string but when an empty object is converted to string it returns [ object Object].
Ex- console.log("" + []) - prints (empty strings).
console.log("" + {}) - prints [object Object] 3. console.log("" + [1,2,3]) - prints 1,2,3
console.log("" + [null, undefined])- prints , (ignores null and undefined)
console.log("" + [1, 2 ,null, 4])- prints 1,2,,4
console.log([] -1)- prints -1
console.log([""] -1 )- prints -1
console.log(["0"-1])- prints -1 4. console.log(0-"010")- prints -10 ( Any number inside a string which starts with zero gets interpreted to decimal number system)
console.log(0-"O10")- prints NaN
console.log(0- 010)- prints -8 converts to octal as it starts with zero.
console.log(0 -"0xb") prints -11
console.log(0 - 0xb) prints -11

**How to check whether something is NaN?**
As NaN is never equal to another NaN to resolve this situation there is a function called **isNaN(argument)**.
It converts the incoming input to a number by applying ToNumber abstract operation
Ex- console.log(isNaN("sanket"))- prints true

But Number.isNaN(number)-(does not do coercion)
Step1- if type(number) is not a number returns false.
Step2- if number is NaN then it returns true else it returns false.

**How to differentiate between -0 and +0?**
let x =-0;
console.log(Object.is(x,-0)); prints false
console.log(Object.is(x, 0)); prints true
**OR**

**Boxing**- Boxing is wrapping primitive value in an object. When the user tries to access object like properties for the argument which is a primitive then it converts the argument for that instance to an object.
Ex - 1.toString() - Throws an exception
but (1).toString() or
Number(1).toString() or
x = 1;
X.toString() - Returns 10
