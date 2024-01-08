Matlab is a high performance software package for numerical calculations. Matlab stands for Matrix laboratory.It also provides the over 50 toolboxes which have special functions written in them for applications like symbolic calculation and image processing etc.
Examples of toolboxes - neural networks simulink, image processing and bioinformatics.

### Different Matlab windows.
- command window - This is the default windows in which you are placed when you open Matlab. It is characterised by the Matlab command prompt >> . It is here where all the command including the user written commands are executed.
- current directory pane - It shows all the files present in the current directory.
- Workspace pane - This sub-window list all the variables you have generated till now along with their type and size.
- command history pane - all the command types in the matlab prompt in the command window are listed here. It list commands across multiple sessions. command in the history pane can be executed by double clicking on them.
- Editor windows - This is where you write edit and create you own programs and save them in files called M-files.

 **Input-Output**
 The fundamental data type in matlab is an array.Though it encompasses several data-types like integer double matrix, character string , structures and cells. 
 Note - There is not need to define the dimensions of the array or matrix.

Matlab is a case-sensitive language.However you can turn off this case sensitivity with casesen command. Though it is not recommended.

Output - The output of every command is displayed on the command window unless until it is being suppressed by the user using a semicolon at the end of the command. Semicolon does not suppresses the  output of the graphics and on-line help command.

File-Types
- M-files - They are standard ASCII text files with .m extension to the filename.There are two types of M-files namely script and function files.All inbuilt functions reside in the m-files which are precompiled.
- Mat-files - These are the binary files with .mat extension to the filename. Mat files are created when you save data with the save command. The data is written in a special format which can only be read by matlab. They can be created on one machine and can be read by matlab on some other machine with different floating point format retaining as much accuracy as possible.
- Mex-files - These are the matlab callable fortran ,c , java programs with .mex extension to the filename.
- P-files - These are the complied .m files which .p extension to the filename. They can be executed in the matlab directly without being parsed or complied. These files are used to give application created to different people without giving them the source code(m files). They are created using the pcode command.

**Format** 
- long - display 15 places after the decimal
- long e - displays 15 places after the decimal followed by the exponential
- long g - displays a total of 15 digits
- shorts - displays 4 places after the decimal 
- short e - displays 4 places after the decimal followed by the exponential
- short g - displays a total of 5 digits.


**General Command** 
- who- Lists all the variables in workspace
- whos - List all the variables in workspace along with their size.
- what - Lists all the M , Mat , Mex files in the current working directory.
- clear - Clears the workspace all variables are removed
- clear all - Clear the entire workspace all the functions and variables are removed .
-  clear x y z - Removes only the variables mentioned.
- clc - clears the command windows. Cursor moves to the top
- clf - clears the figure window
- home - scrolls the command windows to place the cursor on the top
- mlock fun - Locks the mentioned function so that clear cannot remove it.
- munlock fun - unlocks the mentioned function so the clear can remove it.
- pwd - Displays the current working directory.
- mkdir - makes a new directory.
- getpath - Gets or sets the Matlab search path.
- date - Tells you the current data as a string in the format DD-MM-YYYY
- clock - gives you the time as a vector in the format Y M D H M S
- quit/exit - This command is used to quit matlab.
- ^c - This command is used to terminate the running matlab program.

**Complex Number** - Matlab recognise  i and j as imaginary numbers 
and complex number can be written as 5+7i and 5+7* i . Matlab recognises the later by default as imaginary whereas the second format it assumed to be imaginary only and only if i has not being assigned any value.

**Matrix Manipulation** 
- Matrix having only one column and row is called a vector
- matrix having one column and n elements is called a column vector
- matrix having one row and n elements is called a row vector.
- matrix with a single element is called a scalar.

- Defining a matrix - a= [1 2 3 ; 4 5 6 ; 7 8 9 ]
- Extracting an element - b = a(2,3) 
- replacing an element - a(i ,j) = k
- extracting all the elements of a row - c=a(:,j)
- extracting all the elements of a column - c=a(i,:)
- extracting all the elements of rows and column between a and b - 
    c=a(:,a:b)
- extracting all the elements of the columns and rows between m and n - 
    c=a(m:n,:)
- extracting all the elements between column a to b and rows m to n - 
    c=a(m:n,a:b)
- extracting selective elements of the certain rows and columns - 
    c=a([m n q],[p r q]) - it basically prints the intersecting elements
- adding rows - 
    u=[ 10 11 12]
    a=[a; u]
- adding columns - 
    u = [ 10; 11; 12]
    a =[a u]
- deleting rows - a(1,:) =[]
- deleting columns - a(:,1) = []
This also works a([a b],:) =[]

**Special Matrixes** 

- Identity matrix - A matrix whose all diagonal elements are 1 and all non-diagonal elements are 0. 
     I = eye - This returns a scalar 1.
     I = eye(m) - This creates a identity matrix of dimensions mxm
     I = eye(m, n) - This creates a identity matrix of dimensions of mxn with ones only on the main diagonal. 
     I =eye(size(A)) - Creates an identity matrix of the size of matrix A.

- Zeroes matrix - A matrix containing all zeroes in it is called a null matrix.
     z= zeroes - Returns a scalar 0
     z= zeroes(m, n) - Creates a zero matrix of dimensions mxn
     z= zeroes(m) - Creates a zero matrix of dimension of mxm
     z= zeroes(size(A)) - Creates a zeroes matrix of the size of matrix A.

- Ones matrix - A matrix containing all ones in it is called a ones matrix. 
    o = ones - Returns a scalar 1
    o = ones (m,n) - Creates a ones matrix of dimension mxn
    o = ones(size(A)) - Creates a ones matrix of size of matrix A 
    o = ones (m) - Creates a ones matrix of dimensions mxm
    o = ones (m,n,p) - Creates a 3-D ones matrix 


### Matrix Operations 

-  diag(A) - Returns a column vector of the diagonal elements of the matrix A 
    Note - If is a row/column vectors(n) them it return a matrix nxn of  will all the elements being of the diagonal and all other elements being zero.
- diag(A,k) - 
   k=0 default value(Principal  diagonal)
   k=positive(upper off diagonal elements)
   k= negative(lower off diagonal elements)
- rot90(A) - rotates the matrix anti-clockwise by 90 degrees
- rot90(A,k) - rotates the matrix k times 
    k = positve(anti-clockwise)
    k=negative(clockwise)
- fliplr(A) - Flips the matrix left to right and right to left
- flipud(A) - Flips the matrix from up to down and down to up
- tril(A) - returns the lower  triangular matrix
- tril(a,k) - Returns the elements on and below the kth diagonal.
- triu(A) - returns the upper triangular matrix
- triu(A,k) - Returns the elements on and above the kth diagonal.
- reshpae(A,p,q) - Returns a reshaped matrix of dimensions pxq provide mxn=pxq.
   Note  - Reshaping is done column-wise

### Array
Any set of numbers arranged in a rectangular pattern is called an array.
1-D arrays are also called row/ column vectors.

In matlab there are two types of arithmetic operations 
- matrix operations - Operators are same as normal operators.
- array operations - It performs element by element operations.
     Ex - a./b (right division), a.+b (addition)

**Creating Vectors** - 
- Fixed Spacing (h) - v=a:h:b where a is initial value , h is increment and b is  the final value. 
    Note - By default the increment is 1 if nothing is mentioned. 
- Fixed no of points - v= linspace(a, b, n) where a is initial value b is final value and n is total number of elements in the vector. h=(b-a)/(n-1)
    Note - Default value of n is 100

**Operators** - 
- Relational operators are used to compare two scalar, matrices, vectors and strings.
    Note - When complex numbers are compared then <, >, >=, <= compare only the real operand while == and ~= compare both real and imaginary parts.

**Logical Functions** 
 - ischar(A) - Returns 1 if A is a character array else 0.
 - isempty(A) - Returns 1 if A is a empty array.
 - isinf(A) - Returns an array of dimensions of A with ones where inf was present and zeroes elsewhere.
 - isnan(A)- Returns an array of dimensions same as A which ones where NaN was present and zeroes everywhere else.
 - isnumeric(A) - Returns 1 if A is a numeric array else 0
 - isreal(A) - Returns 1 if A has no elements with imaginary parts else returns 0.

**Round off function** - 
- ceil - rounds off towards positive infinity
- floor - rounds off towards negative infinity 
- fix - rounds off towards zero
- round - rounds off to nearest integer

**Conversions** - 
- int2str - converts the integer to string. If the number is not an integer then it rounds off the number and then converts it to a string
- num2str - converts the number to string.