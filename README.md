Download Link: https://assignmentchef.com/product/solved-csci-1200-data-structures-homework-3-dynamic-matrices
<br>
In this assignment you will build a custom class named <em>Matrix</em>, which will mimic traditional matrices (the plural of matrix). You will not be expected to have intimate knowledge of matrices, but if you are curious you can read more about them online: <a href="https://en.wikipedia.org/wiki/Matrix_(mathematics)">https://en.wikipedia.org/wiki/Matrix_(mathematics)</a>

Matrices are used in many di↵erent applications, and over the years many optimizations, tricks, and numerical methods have been developed to quickly handle matrix operations and solve more complicated problems.

Building this data structure will give you practice with pointers, dynamic array allocation and deallocation, 2D pointers, and class design. The implementation of this data structure will involve writing one new class. You are not allowed to use any of the STL container classes in your implementation or use any additional classes or structs. You will need to make use of the new and delete keywords. Please read the entire handout before beginning your implementation. Also, be sure to review the <a href="http://www.cs.rpi.edu/academics/courses/spring17/ds/lectures/08_vector_implementation.pdf">Lecture</a> <a href="http://www.cs.rpi.edu/academics/courses/spring17/ds/lectures/08_vector_implementation.pdf">8</a> notes and our implementation of the Vec class mimicking STL’s vector. You may also want to review our discussion of 2D dynamic arrays from <a href="http://www.cs.rpi.edu/academics/courses/spring17/ds/lectures/06_memory.pdf">Lecture</a> <a href="http://www.cs.rpi.edu/academics/courses/spring17/ds/lectures/06_memory.pdf">6</a><a href="http://www.cs.rpi.edu/academics/courses/spring17/ds/lectures/06_memory.pdf">.</a>

<h1>The Data Structure</h1>

A matrix is a two-dimensional arrangement of numbers. In this assignment we will assume every matrix contains doubles. We refer to the size of a matrix with <em>m </em>rows and <em>n </em>columns as an <em>m</em>⇥<em>n </em>matrix. For example, shown below is a 4⇥3 matrix:

We will represent the data inside our Matrix class by using a two-dimensional array. Because a matrix may be any size, you will need to use dynamic memory for this task. The same matrix shown above can be represented like so:

We will denote <em>a<sub>i,j </sub></em>as the value in matrix <em>A </em>that is in row <em>i </em>and column <em>j</em>. So a general matrix can be described as:

<h1>Basic Functionality</h1>

The private section of your class will be fairly small, and the main challenge will be working with the dynamic memory as you implement features to make the class functional. You can implement these methods in any order; we start by mentioning a few that will make debugging easier.

The first thing we suggest is writing a constructor that takes two unsigned ints: a <em>rows </em>count and a <em>columns count</em>, and a double <em>fill </em>value. The constructor should create a data representation of a <em>rows</em>⇥<em>columns </em>matrix with every value initialized to <em>fill</em>. If either dimension is 0, the resulting matrix should be of size 0⇥0.

Your class must support the equality operator == and the inequality operator !=. Two matrices are considered to be equal if they have the same value in every position. In other words, matrices <em>A </em>and <em>B </em>are equal if and only if (8<em>i,j</em>|<em>i </em>2 {0<em>,</em>1<em>,…,m </em>2<em>,m </em>1}<em>,j </em>2 {0<em>,</em>1<em>,…,n </em>2<em>,n </em>1})<em>a<sub>i,j </sub></em>= <em>b<sub>i,j</sub></em>. 8 is a common shorthand for “for all,” so 8<em>i,j </em>means “for every value of i and j.” 2 is a common shorthand for “in”.

Since a matrix has two dimensions, you will need to implement <em>num </em><em>rows() </em>and <em>num </em><em>cols() </em>which return the number of rows and the number of columns in the matrix respectively.

We may want to change a previously filled matrix to an empty one, so you must write a <em>clear() </em>method as well. This method should reset the number of rows and columns to 0, and deallocate any memory currently held by the Matrix.

Naturally we want to be able to access data stored in the Matrix class. To do so we will implement a “safe” accessor called <em>get()</em>, which takes in a row, a column, and a double. If the row and column are within the bounds of the matrix, then the value at <em>a<sub>row,col </sub></em>should be stored in the double, and the function should return true. Otherwise the function should return false.

A complementary, but similar task to accessing data is to be able to set a value at a particular position in the matrix. This is done through a safe modifier called <em>set()</em>. This function also takes in a row, column, and a double value. <em>set() </em>returns false if the position is out of bounds, and true if the position is valid. If the position is valid, the function should also set <em>a<sub>row,col </sub></em>to the value of the double that was passed in.

<h1>Overloaded Output Operator</h1>

At some point, it is probably a good idea to write a method to do output for us. Unlike previous classes where we wrote a method to do the printing, we will instead rely on a non-member overload of the <em>operator&lt;&lt;</em>. We have practiced overloading other operators for calls to std::sort() before, and this will be similar. Outside of the Matrix class definition, but still in your .cpp and .h files, you should write the following operator: std::ostream&amp; operator&lt;&lt; (std::ostream&amp; out, const Matrix&amp; m)

This will allow us to print one or more outputs sequentially. All of the following code should work if your <em>operator&lt;&lt; </em>is implemented correctly:

Matrix m1; Matrix m2;

std::ofstream outfile(output_filename); //Assuming we already had the filename std::cout &lt;&lt; m1 &lt;&lt; m2 &lt;&lt; std::endl; outfile &lt;&lt; m1; outfile &lt;&lt; m2 &lt;&lt; std::endl;

std::cout &lt;&lt; “Done printing.” &lt;&lt; std::endl;

Let us assume in the above example that:

Then the output should look something like this:

0 x 0 matrix:

[ ]

3 x 2 matrix:

[ 3 5.21

-2 4

-18 1 ]

Done printing.

We will ignore whitespace, but we do expect that your operator outputs the elements of the matrix in the right order, that the size output comes before the matrix and follows the format shown below – one row per line, and spacing between elements. Note that even in these examples, the alignment is not ideal. We would rather you focus on the task of implementing the Matrix class correctly and handling memory properly instead of focusing on making the output pretty.

<h1>Simple Matrix Operations</h1>

To start with, we introduce some basic matrix operations. The first is the method <em>multiply </em><em>by coe cient()</em>, which takes a double called a coe cient. The method should multiply every element in the matrix by the coe cient. For example:

Another common operation is to swap two rows of a matrix. This will be accomplished by the method <em>swap </em><em>row()</em>, which takes two arguments of type unsigned int: a <em>s</em>ource row number and a <em>t</em>arget row number. If both rows are inside the bounds of the matrix, then the function should switch the values in the two rows and return true. Otherwise the function should return false.

For example:

<strong>NOTE</strong>: With the basic functions and swap row() done, the tests related to the provided <em>rref() </em>function in <em>matrix main.cpp </em>can be called. We do not explain the function in detail here, and you don’t need to know how it works, but computing the Reduced Row Echelon Form (RREF) can be used to find an inverse matrix, which is important in many fields. We use a simple to implement method called Gauss-Jordan Elimination, which you can read about here: <a href="https://en.wikipedia.org/wiki/Gaussian_elimination">https://en.wikipedia.org/wiki/Gaussian_elimination</a> . There are other techniques for finding the RREF that are better, but we chose this one for its simplicity.

It is common to need to “flip” a matrix, a process called transposition. You will need to write the <em>transpose() </em>method, which has a return type of void. Formally, transposition of <em>m</em>⇥<em>n </em>matrix <em>A </em>into <em>n</em>⇥<em>m </em>matrix <em>A<sup>T </sup></em>is defined as:

(8<em>i,j</em>|<em>i </em>2 {0<em>,</em>1<em>,…,m                 </em>2<em>,m            </em>1}<em>,j </em>2 {0<em>,</em>1<em>,…,n            </em>2<em>,n         </em>1})<em>a<sup>T</sup><sub>i,j </sub></em>= <em>a<sub>j,i</sub></em>

1       4 1   2             3

<em>m</em>1 =4       5      6 <em>,         m</em>1<em>.transpose</em>() =)422     535

3    6

<h1>Binary Matrix Operations</h1>

Binary matrix operations are ones that involve two matrices. To keep things simple, we will write them as methods (not operators) that are inside the class definition, so the current Matrix object will always be the “left-hand” matrix, <em>A</em>. You will be required to implement both <em>add() </em>and <em>subtract()</em>. Both functions take in just one argument, a second Matrix which we will refer to as <em>B</em>, and modify <em>A </em>if the dimensions of <em>A </em>and <em>B </em>match. If the dimensions match, the functions should return true, otherwise they should return false.

Addition of two matrices, <em>C </em>= <em>A </em>+ <em>B</em>, and subtraction of two matrices, <em>D </em>= <em>A                       B </em>are formally defined as:

(8<em>i,j</em>|<em>i </em>2 {0<em>,</em>1<em>,…,m </em>2<em>,m </em>1}<em>,j </em>2 {0<em>,</em>1<em>,…,n </em>2<em>,n </em>1})<em>C<sub>i,j </sub></em>= <em>a<sub>i,j </sub></em>+ <em>b<sub>i,j </sub></em>(8<em>i,j</em>|<em>i </em>2 {0<em>,</em>1<em>,…,m </em>2<em>,m </em>1}<em>,j </em>2 {0<em>,</em>1<em>,…,n </em>2<em>,n </em>1})<em>D<sub>i,j </sub></em>= <em>a<sub>i,j </sub>b<sub>i,j</sub></em>

Consider these two matrices:

<table>

 <tbody>

  <tr>

   <td></td>

  </tr>

 </tbody>

</table>

1    2    3                         4      16          25

<em>m</em>1 =<em>m</em>2 = 

4    5    6                        14    3<em>.</em>4    3<em>.</em>64159

<table>

 <tbody>

  <tr>

   <td></td>

  </tr>

 </tbody>

</table>

1 + 4       2 + 16           3 + 25                  5      18          28

<em>m</em>1 + <em>m</em>2 == 

4 + 14     5 + 3<em>.</em>4    6 + 3<em>.</em>64159           18    8<em>.</em>4    9<em>.</em>64159

<table>

 <tbody>

  <tr>

   <td></td>

  </tr>

 </tbody>

</table>

1      4      2      16          3     25                      3         14           22

<em>m</em>1                                         <em>m</em>2 == 

4      14    5      3<em>.</em>4    6     3<em>.</em>64159               10     1<em>.</em>6     2<em>.</em>35841

<h1>Harder Matrix Operations</h1>

If we want to get the contents of an entire row or column, it’s annoying to have to extract the values one by one using <em>get()</em>, especially since our implementation is a “safe” accessor so we can’t use some of the coding shortcuts we normally use. To fix this, you will implement two more accessors, <em>get </em><em>row() </em>and <em>get col()</em>. Both functions take one unsigned int and return a double*. For <em>get </em><em>row() </em>the argument is the number of row to retrieve, while for <em>get </em><em>col() </em>the argument is the number of the column to retrieve. If the requested row/column is outside of the matrix bounds, the method should return a pointer set to NULL.

The final method we expect you to implement, <em>quarter()</em>, is not a traditional matrix operation. The method takes no arguments and returns a Matrix* containing four Matrix elements in order: an <strong>U</strong>pper <strong>L</strong>eft (UL) quadrant, an <strong>U</strong>pper <strong>R</strong>ight (UR) quadrant, a <strong>L</strong>ower <strong>L</strong>eft (LL) quadrant, and finally a <strong>L</strong>ower <strong>R</strong>ight (LR) quadrant. All four quadrants should be the same size. Remember that when a function ends all local variables go out of scope and are destroyed, so you will need to be particularly careful about how you construct and return the quadrants. On the next page are two examples of the quarter operation:

<h1>Testing and Debugging</h1>

We provide a matrix main.cpp file with a wide variety of tests of the Matrix class. Some of these tests are initially commented out. We recommend that you get your class working on the basic tests, and then uncomment the additional tests as you implement and debug the remaining functionality. Study the provided test cases to understand the arguments and return values.

<em>Note: Do not edit the provided </em>matrix main.cpp <em>file, except to uncomment the provided test cases as you work through your implementation and to add your own test cases where specified.</em>

The assert() function is used throughout the test code. This is a function available in both C and C++ that will do nothing if the condition is true, and will cause an immediate crash if the condition is false. If the condition is false, your command line should show the assertion that failed immediate prior to the crash.

We recommend using a memory debugging tool to find memory errors and memory leaks. Information on installation and use of the memory debuggers “Dr. Memory” (available for Linux/MacOSX/Windows) and “Valgrind” (available for Linux/OSX) is presented on the course webpage:

<a href="http://www.cs.rpi.edu/academics/courses/spring17/ds/memory_debugging.php">http://www.cs.rpi.edu/academics/courses/spring17/ds/memory_debugging.php</a>

The homework submission server will also run your code with Dr. Memory to search for memory problems. Your program must be memory error free and memory leak free to receive full credit.

<h1>Your Task &amp; Provided Code</h1>

You must implement the Matrix class as described in this handout. Your class should be split between a .cpp and a .h file. You should also include some extra tests in the <em>StudentTest() </em>function in matrix main.cpp.

When implementing the class, pay particular attention to correctly implementing the copy constructor, assignment operator, and destructor. As you implement your classes, be careful with return types, the const keyword, and passing by reference.

If you have correctly implemented the Matrix class, then running the provided matrix main.cpp file with your class, should produce the output provided in sample output.txt. We are not going to be particularly picky about di↵erences in whitespace, but you should be making an e↵ort to try and match both spacing and newlines between our output and your output.

<h1>Submission</h1>

You will need to submit your matrix main.cpp,Matrix.cpp,Matrix.h, and README.txt file. Be aware that Submitty will be using an instructor copy of matrix main.cpp for most of the tests, so you must make sure your Matrix implementation can compile given the provided file.

Be sure to write your own new test cases and don’t forget to comment your code! Use the provided template README.txt file for notes you want the grader to read. Fill out the order notation section as well in the README.txt file.

<h1>Extra Credit Opportunity</h1>

For extra credit, you may implement another method in the Matrix class called <em>resize</em>. This method should take in three arguments: a number of rows, number of columns, and finally a fill value. The function should always change the internal matrix to be <em>rows</em>⇥<em>columns </em>in size, copying over any values that were in the bounds of the original matrix. If the new matrix is larger, any positions that are in the new matrix, but not the old one, should have the fill value.

If you do this, make sure to fill out the section about extra credit in your README.txt, and write some tests in <em>ExtraCreditTest()</em>.