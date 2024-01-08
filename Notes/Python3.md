In python3 data-types are automactically assumed by the interpreter.
In boolean the two values True and False   the T and F are in capitals.
In order to take input from the user the following syntax is used-
(variable-name)= input('Message to be printed on the terminal')
In order to print something on the sreen only print has to be written.
Type casting can be used by  using the following syntax-
int(value or   name of the variable)
In order to print a  given charactrer or string multiple number of times-  print("Hello" * 10) This will print Hello 10 times.
In to print multiple lines of message ''' '''(triple quote needs to used)
course = "Enginnering"
print(course[ 2 ]) This will print the character at index 2.
print(course[ 2:5])This will print the character from index 2 to 5 excluding the character at index 5. If nothing is mentioned then it assumes values from the  zeroth index till the length of the string.
also if values are in negative are given then it denotes values from the end of the string.
len(variable name)- It is used to count the number of characters in the string.
variable.upper()/lower()-converts characters to upper or lowercase respectively.
.find('a')-returns the index of first occurence of the given characters.
.replace('part to be replaced','part to be in place of the replaced part')
'......' in variable name - returns a boolean value depending upon whether the entered string is in the mentioned variable.
// - This is also division sign but returns interger value instead of floating point number.
** - This is used exponentiation.
abs()- Returns absoluete value.
elif- Same as else if.
Logical operators-
  1. logical and - and
  2. logical or - or
  3. not - not
Relational operators - > < >= <= ==

while loops also have an optional else part but it has to be on the same level.
range(starting limit, ending limit, stepping factor) - stores values from starting to the ending limit while changing values by the stepping factor.
.append(value)- It adds the value at the end of the list.
.insert(index, value) - It adds the entered value at the specified index.
.clear()- Empties the list.
.remove(value)- Removes  the entered value.
.pop() - Removes the value at last index.
.index(value) - returns the index of the first occurence of value entered.
value in (list name)- returns true or false depending upon the presence of the value in the list.
None is returned when there is an absence of returned value.
.sort() -   Sorts the given list in ascending order.
.reverse() - It reverses the given list.
.copy() - Creates a copy of the given list.
A tuple is an ordered and unchangble container. It has access to only two methods .count and .index.
variable name separated by a comma = name of list or tuple - It assigns the values in tuple or list to the variables in a lexiographical manner.
Dictionaries can store mutiple forms of data in form of keys.Keys are case-sensitive.Syntax for the following is as follows:
Dictionary name ={
  "keys" : "vale for the key",
}
In order to print the value there are two ways-
 1. print(dictionary name.get("key name", default value if keys not present)(preferred)
 2. print(dictionary name["key"])

Functions are defined using def keyword
def function_name();
keyword arguments must always be preceeded by the positional arguments.
On calling a function which does not return's any value then none will be printed.
Error Handling - 
try:
  // instructions
except Error:
   // instructions if specified error is encountered.
Comments start with # .
Classes in Python start with the keyword class name it is recommended that class name should start in uppercase.
Various functions can be defined inside the class and can be called later and can be used as method to do certain opertions.
objects of an class can be created by using the following syntax-
object_name = class_name()
These created object can have certain attributes and can be defined in the following way-
object_name.attribute_name= value of the attribute
Construstor is the function that is called when an object of an class is created. Its syntax is-
def  _ _init_ _ (self, aruguments):
self keyword is used to refer to currently calling object.self keyword is exactly similar to this keyowrd in java.
A class can inherit the properties of its parent class by writing the name of the super class in the prototype of the child class.
Absoulete path starts from the root directory.
Relative path starts from the current directory.
pypi - python package index- collection of different libraries 
pip  command is used to install packages from pypi.org 



