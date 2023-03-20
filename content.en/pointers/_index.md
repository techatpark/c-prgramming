---
title: 'Pointers'
weight: 9
---

which feature of C do beginners find most difficult to understand? The answer is easy: pointers. Other languages have pointers but few use them so frequently as C does. And why not? It is C’s clever use of pointers that makes it the excellent language it is. This chapter is devoted to pointers and their usage in function calls. Let us begin with the function calls.

**Call by Value and Call by Reference** By now, we are well familiar with how to call functions. But, if you observe carefully, whenever we called a function and passed something to it we have always passed the ‘values’ of variables to the called function. Such function calls are called ‘calls by value’. By this what we mean is, on calling a function, we are passing values of variables to it. The examples of call by value are shown below:

```
sum = calsum ( *a, b, c ) ; 
f = factr ( a ) ;
```

We have also learnt that variables are stored somewhere in memory. So instead of passing the value of a variable, can we not pass the location number (also called address) of the variable to a function? If we were able to do so, it would become a ‘call by reference’. What purpose a ‘call by reference’ serves we would find out a little later. First we must equip ourselves with knowledge of how to make a ‘call by reference’. This feature of C functions needs at least an elementary knowledge of a concept called ‘pointers’. So let us first acquire the basics of pointers after which we would take up this topic once again.

### An Introduction to Pointers
The difficulty beginners have with pointers has much to do with C’s pointer terminology than the actual concept. For instance, when a C programmer says that a certain variable is a “pointer”, what does that mean? It is hard to see how a variable can point to something, or in a certain direction.

It is hard to get a grip on pointers just by listening to programmer’s jargon. In our discussion of C pointers, therefore, we will try to avoid this difficulty by explaining pointers in terms of programming concepts we already understand. The first thing we want to do is to explain the rationale of C’s pointer notation.

### W

**Pointer Notation** Consider the declaration,

int i = 3 ;

This declaration tells the C compiler to:

- Reserve space in memory to hold the integer value.

- Associate the name **i** with this memory location.

- Store the value 3 at this location.

We may represent **i**’s location in memory by the memory map shown in Figure 9.1.

3

65524

i location name

value at location

location number

Figure 9.1

We see that the computer has selected memory location 65524 as the place to store the value 3. The location number 65524 is not a number to be relied upon, because some other time the computer may choose a different location for storing the value 3. The important point is, **i**’s address in memory is a number.

We can print this address number through the following program:

\# include <stdio.h> int main( ) { int i = 3 ; printf ( "Address of i = %u\\n", &i ) ; printf ( "Value of i = %d\\n", i ) ; return 0 ; }

The output of the above program would be:

Address of i = 65524 Value of i = 3

Look at the first **printf( )** statement carefully. ‘&’ used in this statement is C’s ‘address of’ operator. The expression **&i** returns the address of the variable **i**, which in this case happens to be 65524. Since 65524 represents an address, there is no question of a sign being associated with it. Hence it is printed out using **%u**, which is a format specifier for printing an unsigned integer. We have been using the ‘&’ operator all the time in the **scanf( )** statement.

The other pointer operator available in C is ‘**\*’**, called ‘value at address’ operator. It gives the value stored at a particular address. The ‘value at address’ operator is also called ‘indirection’ operator.

Observe carefully the output of the following program:

\# include <stdio.h> int main( ) { int i = 3 ; printf ( "Address of i = %u\\n", &i ) ; printf ( "Value of i = %d\\n", i ) ; printf ( "Value of i = %d\\n", \*( &i ) ) ; return 0 ; }

The output of the above program would be:

Address of i = 65524 Value of i = 3 Value of i = 3

Note that printing the value of **\*( &i )** is same as printing the value of **i**.

The expression **&i** gives the address of the variable **i**. This address can be collected in a variable, by saying,

j = &i ;

But remember that **j** is not an ordinary variable like any other integer variable. It is a variable that contains the address of other variable (**i** in this case). Since **j** is a variable, the compiler must provide it space in the

memory. Once again, the memory map shown in Figure 9.2 would illustrate the contents of **i** and **j**.

3 65524

65524 65522

i j

Figure 9.2

As you can see, **i**’s value is 3 and **j**’s value is **i**’s address.

But wait, we can’t use **j** in a program without declaring it. And since **j** is a variable that contains the address of **i**, it is declared as,

int \*j ;

This declaration tells the compiler that **j** will be used to store the address of an integer value. In other words, **j** points to an integer. How do we justify the usage of **\*** in the declaration,

int \*j ;

Let us go by the meaning of **\***. It stands for ‘value at address’. Thus, **int \*j** would mean, the value at the address contained in **j** is an **int**.

Here is a program that demonstrates the relationships we have been discussing.

\# include <stdio.h> int main( ) { int i = 3 ; int \*j ; j = &i ; printf ( "Address of i = %u\\n", &i ) ; printf ( "Address of i = %u\\n", j ) ; printf ( "Address of j = %u\\n", &j ) ; printf ( "Value of j = %u\\n", j ) ; printf ( "Value of i = %d\\n", i ) ;

printf ( "Value of i = %d\\n", \*( &i ) ) ; printf ( "Value of i = %d\\n", \*j ) ; return 0 ; }

The output of the above program would be:

Address of i = 65524 Address of i = 65524 Address of j = 65522 Value of j = 65524 Value of i = 3 Value of i = 3 Value of i = 3

Work through the above program carefully, taking help of the memory locations of **i** and **j** shown earlier. This program summarizes everything that we have discussed so far. If you don’t understand the program’s output, or the meanings of **&i**, **&j**, **\*j** and **\*( &i )**, re-read the last few pages. Everything we say about pointers from here onwards will depend on your understanding these expressions thoroughly.

Look at the following declarations:

int \*alpha ; char \*ch ; float \*s ;

Here, **alpha, ch** and **s** are declared as pointer variables, i.e., variables capable of holding addresses. Remember that, addresses (location nos.) are always going to be whole numbers, therefore pointers always contain whole numbers. Now we can put these two facts together and say—pointers are variables that contain addresses, and since addresses are always whole numbers, pointers would always contain whole numbers.

The declaration **float \*s** does not mean that **s** is going to contain a floating-point value. What it means is, **s** is going to contain the address of a floating-point value. Similarly, **char \*ch** means that **ch** is going to contain the address of a char value. Or in other words, the value at address stored in **ch** is going to be a **char**.

The concept of pointers can be further extended. Pointer, we know is a variable that contains address of another variable. Now this variable

itself might be another pointer. Thus, we now have a pointer that contains another pointer’s address. The following example should make this point clear:

\# include <stdio.h> int main( ) { int i = 3, \*j, \*\*k ; j = &i ; k = &j ; printf ( "Address of i = %u\\n", &i ) ; printf ( "Address of i = %u\\n ", j ) ; printf ( "Address of i = %u\\n ", \*k ) ; printf ( "Address of j = %u\\n ", &j ) ; printf ( "Address of j = %u\\n ", k ) ; printf ( "Address of k = %u\\n ", &k ) ; printf ( "Value of j = %u\\n ", j ) ; printf ( "Value of k = %u\\n ", k ) ; printf ( "Value of i = %d\\n ", i ) ; printf ( "Value of i = %d\\n ", \* ( &i ) ) ; printf ( "Value of i = %d\\n ", \*j ) ; printf ( "Value of i = %d\\n ", \*\*k ) ; return 0 ; }

The output of the above program would be:

Address of i = 65524 Address of i = 65524 Address of i = 65524 Address of j = 65522 Address of j = 65522 Address of k = 65520 Value of j = 65524 Value of k = 65522 Value of i = 3 Value of i = 3 Value of i = 3 Value of i = 3

Figure 9.3 would help you in tracing out how the program prints the above output.

Remember that when you run this program, the addresses that get printed might turn out to be something different than the ones shown in Figure 9.3. However, with these addresses too, the relationship between **i**, **j** and **k** can be easily established.

3 65524

65524 65522

i j

65522

65520

k

Figure 9.3

Observe how the variables **j** and **k** have been declared,

int i, \*j, \*\*k ;

Here, **i** is an ordinary **int**, **j** is a pointer to an **int** (often called an integer pointer), whereas **k** is a pointer to an integer pointer. We can extend the above program still further by creating a pointer to a pointer to an integer pointer. In principle, you would agree that likewise there could exist a pointer to a pointer to a pointer to a pointer to a pointer. There is no limit on how far can we go on extending this definition. Possibly, till the point we can comprehend it. And that point of comprehension is usually a pointer to a pointer. Beyond this, one rarely requires to extend the definition of a pointer. But just in case...

**Back to Function Calls** Having had the first tryst with pointers, let us now get back to what we had originally set out to learn—the two types of function calls—call by value and call by reference. Arguments can generally be passed to functions in one of the two ways:

- sending the values of the arguments

- sending the addresses of the arguments

In the first method, the ‘value’ of each of the actual arguments in the calling function is copied into corresponding formal arguments of the

called function. With this method, the changes made to the formal arguments in the called function have no effect on the values of actual arguments in the calling function. The following program illustrates the ‘Call by Value’:

\# include <stdio.h> void swapv ( int x, int y ) ; int main( ) { int a = 10, b = 20 ; swapv ( a, b ) ; printf ( "a = %d b = %d\\n", a, b ) ; return 0 ; } void swapv ( int x, int y ) { int t ; t = x ; x = y ; y = t ; printf ( "x = %d y = %d\\n", x, y ) ; }

The output of the above program would be:

x = 20 y = 10 a = 10 b = 20

Note that values of **a** and **b** remain unchanged even after exchanging the values of **x** and **y**.

In the second method (call by reference), the addresses of actual arguments in the calling function are copied into the formal arguments of the called function. This means that, using these addresses, we would have an access to the actual arguments and hence we would be able to manipulate them. The following program illustrates this fact:

\# include <stdio.h> void swapr ( int \*, int \* ) ; int main( ) { int a = 10, b = 20 ; swapr ( &a, &b ) ;

printf ( "a = %d b = %d\\n", a, b ) ; return 0 ; } void swapr ( int \*x, int \*y ) { int t ; t = \*x ; \*x = \*y ; \*y = t ; }

The output of the above program would be:

a = 20 b = 10

Note that this program manages to exchange the values of **a** and **b** using their addresses stored in **x** and **y**.

Usually, in C programming, we make a call by value. This means that, in general, you cannot alter the actual arguments. But if desired, it can always be achieved through a call by reference.

Using a call by reference intelligently, we can make a function return more than one value at a time, which is not possible ordinarily. This is shown in the program given below.

\# include <stdio.h> void areaperi ( int, float \*, float \* ) ; int main( ) { int radius ; float area, perimeter ; printf ( "Enter radius of a circle " ) ; scanf ( "%d", &radius ) ; areaperi ( radius, &area, &perimeter ) ; printf ( "Area = %f\\n", area ) ; printf ( "Perimeter = %f\\n", perimeter ) ; return 0 ; } void areaperi ( int r, float \*a, float \*p )

{ \*a = 3.14 \* r \* r ; \*p = 2 \* 3.14 \* r ; }

And here is the output...

Enter radius of a circle 5 Area = 78.500000 Perimeter = 31.400000

Here, we are making a mixed call, in the sense, we are passing the value of **radius** but, addresses of **area** and **perimeter**. And since we are passing the addresses, any change that we make in values stored at addresses contained in the variables **a** and **p**, would make the change effective in **main( )**. That is why, when the control returns from the function **areaperi( )**, we are able to output the values of **area** and **perimeter**.

Thus, we have been able to indirectly return two values from a called function, and hence, have overcome the limitation of the **return** statement, which can return only one value from a function at a time.

**Conclusions** From the programs that we discussed here, we can draw the following conclusions:

- If we want that the value of an actual argument should not get changed in the function being called, pass the actual argument by value.

- If we want that the value of an actual argument should get changed in the function being called, pass the actual argument by reference.

- If a function is to be made to return more than one value at a time, then return these values indirectly by using a call by reference.

### Summary

- Pointers are variables which hold addresses of other variables.

- A pointer to a pointer is a variable that holds address of a pointer variable.

- The & operator fetches the address of the variable in memory.

- The \* operator lets us access the value present at an address in memory with an intension of reading it or modifying it.

- A function can be called either by value or by reference.

- Pointers can be used to make a function return more than one value simultaneously in an indirect manner.

### Exercise

**\[A\]** What will be the output of the following programs:

- # include <stdio.h> void fun ( int, int ) ; int main( ) { int i = 5, j = 2 ; fun ( i, j ) ; printf ( "%d %d\\n", i, j ) ; return 0 ; } void fun ( int i, int j ) { i = i \* i ; j = j \* j ; }

- # include <stdio.h> void fun ( int \*, int \* ) ; int main( ) { int i = 5, j = 2 ; fun ( &i, &j ) ; printf ( "%d %d\\n", i, j ) ; return 0 ; } void fun ( int \*i, int \*j ) { \*i = \*i \* \*i ; \*j = \*j \* \*j ; }

- # include <stdio.h> int main( )

{ float a = 13.5 ; float \*b, \*c ; b = &a ; /\* suppose address of a is 1006 \*/ c = b ; printf ( "%u %u %u\\n", &a, b, c ) ; printf ( "%f %f %f %f %f\\n", a, \*(&a), \*&a, \*b, \*c ) ; return 0 ; }

**\[B\]** Point out the errors, if any, in the following programs:

- # include <stdio.h> void pass ( int, int ) ; int main( ) { int i = 135, a = 135, k ; k = pass ( i, a ) ; printf ( "%d\\n", k ) ; return 0 ; } void pass ( int j, int b ) int c ; { c = j + b ; return ( c ) ; }

- # include <stdio.h> void jiaayjo ( int , int ) int main( ) { int p = 23, f = 24 ; jiaayjo ( &p, &f ) ; printf ( "%d %d\\n", p, f ) ; return 0 ; } void jiaayjo ( int q, int g ) { q = q + q ; g = g + g ; }

- # include <stdio.h> void check ( int ) ; int main( ) { int k = 35, z ; z = check ( k ) ; printf ( "%d\\n", z ) ; return 0 ; } void check ( m ) { int m ; if ( m > 40 ) return ( 1 ) ; else return ( 0 ) ; }

- # include <stdio.h> void function ( int \* ) ; int main( ) { int i = 35, \*z ; z = function ( &i ) ; printf ( "%d\\n", z ) ; return 0 ; } void function ( int \*m ) { return ( \*m + 2 ) ; }

**\[C\]** Attempt the following:

- Write a function that receives 5 integers and returns the sum, average and standard deviation of these numbers. Call this function from **main( )** and print the results in **main( )**.

- Write a function that receives marks received by a student in 3 subjects and returns the average and percentage of these marks. Call this function from **main( )** and print the results in **main( )**.

- Write a C function to evaluate the series

 )!7/()!5/()!3/()sin( 753 _xxxxx_

up to 10 terms.

- Given three variables **x**, **y**, **z** write a function to circularly shift their values to right. In other words if x = 5, y = 8, z = 10, after circular shift y = 5, z = 8, x =10. Call the function with variables **a**, **b**, **c** to circularly shift values.

- If the lengths of the sides of a triangle are denoted by **a**, **b**, and **c**, then area of triangle is given by

))()(( _cSbSaSSarea_ 

where, S = ( a + b + c ) / 2. Write a function to calculate the area of the triangle.

- Write a function to compute the distance between two points and use it to develop another function that will compute the area of the triangle whose vertices are **A(x1, y1)**, **B(x2, y2)**, and **C(x3, y3)**. Use these functions to develop a function which returns a value 1 if the point **(x, y)** lines inside the triangle ABC, otherwise returns a value 0.

- Write a function to compute the greatest common divisor given by Euclid’s algorithm, exemplified for J = 1980, K = 1617 as follows:

1980 / 1617 = 1 1980 – 1 \* 1617 = 363 1617 / 363 = 4 1617 – 4 \* 363 = 165 363 / 165 = 2 363 – 2 \* 165 = 33 5 / 33 = 5 165 – 5 \* 33 = 0

Thus, the greatest common divisor is 33.

