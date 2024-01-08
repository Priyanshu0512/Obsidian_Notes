Numpy is faster than lists because it uses fixed type -
 in numpy the value is by defalut stored in binary form in INT32 format(4bytes) which also can be decreased depending upon the value of the input.
 whereas in list the a lot of additional data needs to be stored which is  
  1. size
  2. reference count
  3. object value
  4. object type
due to this operating upon list takes a much longer time than using its counterpart(numpy
numpy  also uses contiguous  memory i.e. all the information stored is in a sequence in the same addresss in the memory while in the case of lists the information in scattered at different locations.
Advantages of contiguous memory-
 1. Effective Cache utilization
 2. All memory units have a SIMD vector processing units which is used to perform computation on contiguous memory.SIMD stand for Single Instruction Multiple Data.
Initilization of Array - name of variable = np.array([1,2,3], dtype='int16')
In order to get the dimensions of an array 
    name of variable.ndim
To get the shape use .shape
To get the memory taken by each elemet in  the array use  .itemsize
To get the data type use .dtype
To get total number of elements use  .size
To get the total size use .nbytes or .itemsize* .size
To get a sepecific row a[0, :]
To get a specific element a[1,5]
Work outside in  in a 3-D array to get a particular element.
a.[1,5]=20 - This replaces the element in second row and 6th column with 20.
To get the all zero matrix np.zeros(Shape)
To get the all ones matriz np.ones(shape)
To get the matrix filed with some other number np.full((shape),value to be filled)
To get the matrix like some other matrix np.full_like(name of the matrix whose shape has to be replicated , value to be filled)
To fill the array with random decimal number np.random.rand(shape) A tuple will not accpeted in this case.
To give a tuple as an input use np.random.random_sample(a.shape)
To get matrix with random integers np.random.randint( 7, size=(4,2))
To get an identity matrix use np.identity(size)
To repeat an array horizontally or vertically np.repeat(arr, number of times, axis =0)
axis=0 means y-axis. 
axis=1 means x-axis
if an array b to another array a b=a them on changing the items of b will also change content of a  as both points towards the same array Hence in order to make a copy use b=a.copy()
In order to  perform arthimatic operations on each element 
a +-/* number also a+=2
sin of all values np.sin(a)
To multiply two matrices np.matmul(a,b)
To get determinant of  a  matrix np.linalg.det(c)
To get the minimun value in a matrix use np.min(stats, axis=0,1)
To reshape an array after= before.reshape(new shape)
To stack arrays vertically np.vstack([v1,v2]) for horizontally stacking use .hstack
To load data from a file use np.genfromtxt('name of the file', delimiter=',')
filedata >50 returns a matrix of  true or false depending upon the result.
filedata[filedata>50] - returns matrix will elements greater than 50.
((filedata>50) & (filedata<100))

