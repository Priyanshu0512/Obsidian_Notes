There are various kinds on operators in javascript.

Operand - Values on which the operation is going to be performed.

**1. Arithmetic Operators**
	   They include simple mathematical operators which are + , - , /  , * , %(modulus operator gives remainder).
	   In order to perform exponentiation ** is used followed by the power raised. 
	   Ex- console.log(y ** 2 );

**2. Assignment Operator **
      It is simply used to assign the value from the RHS to the LHS.
      Shorthand Operation - 
       a +=2 can be interpreted same as a = a+2. This will first  increment the value of a by 2 and assign the new value back to a.

 **3.Relational Operator **
      They take two Operand and take the first value and compare it with the second value and depending upon the condition they always  return a  true or false value. They are >, <, <=, >=.

 **4 Logical Operator**
     They work on the basic of logic gate.
     The operands given will be boolean operands.
     1.  AND Gate( && ) - If the first input is true then it return the second input else if the first input is false then it return the first input only.
     2. OR Gate( | | ) - If the first input is true then it return the first input is only else if the first input is false then it return the second input.
     3. NOT Gate( ! )- It reverses the true or false value and returns it.
 The concept of coercion is explained in this file.[[Short circuiting and Coercion ]]

 **5. Bitwise Operators**- Bitwise operators perform the corresponding operators on the operand bit by bit.
    1. Bitwise AND( & )
    2. Bitwise OR ( |  )
    3. Bitwise XOR( ^ )
    4. Bitwise NOT ( ~ )

 **6.Equality Operator** - They are of two types.
    1. Abstract Equality operator( == ) - It checks the type of both the operands if the types are same then it calls Strict Equality operator( === ). But is the types are not same then coercion occurs and then comparison is done.
    2. Strict Equality operator ( === ) - It also checks the types of both the operands. If the types are different it returns false but if the types are same value comparison occurs.

 Ex- (1== "1") returns true( It converts string to number and compares.)
  (1== "priyanshu") returns false ( priyanshu is converted to NaN and its not equal to number. )
  The details of both the equality are in [[Short circuiting and Coercion]].

**7.typeof operator** - This operator returns the type of  the data  given to it.
Syntax- typeof argument;
NOTE- Corner case- typeof null returns object instead of null.

**8.Unary Operator** - This operator only operate upon a single operand.
1. Postfix - It performs the operation and then increases/decreases the value.
2. Prefix - It first increases/decreases the value and then performs the operation.
There are two types on unary operators increment(++) and decrement(--). 
Also minus(-) and plus(+) are itself unary operators.

1. Unary plus(+)- It tries to convert the argument into a number if it is not already a number.If it cannot be converted to number then it returns NaN.
     Ex- let x= "22";
      y = +x;
      then typeof x; will return y to be a  number but will not change the type of original operand.
2. Unary plus(-)- It tries to convert the argument into a number if it is not already a number and then makes the result negative.
3. typeof - It is also a unary operator.

**9.Ternary operator** - 
    Syntax - (condition)? expression1 : expression2;