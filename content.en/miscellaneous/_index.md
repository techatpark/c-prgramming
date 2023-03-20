---
title: 'Miscellaneous'
weight: 22
---

The topics discussed in this chapter were either too large or far too removed from the mainstream C programming for inclusion in the earlier chapters. These topics provide certain useful programming features, and could prove to be of immense help in certain programming strategies. In this chapter, we would examine enumerated data types, the **typedef** keyword, typecasting, bit fields, function pointers, functions with variable number of arguments and unions.

### Enumerated Data Type
The enumerated data type gives you an opportunity to invent your own data type and define what values the variable of this data type can take. This can help in making the program listings more readable, which can be an advantage when a program gets complicated or when more than one programmer would be working on it. Using enumerated data type can also help you reduce programming errors.

As an example, one could invent a data type called **mar\_status** which can have four possible values—single, married, divorced or widowed. Don’t confuse these values with variable names; married, for instance, has the same relationship to the variable **mar\_status** as the number 15 has with a variable of type **int**.

The format of the **enum** definition is similar to that of a structure. Here’s how the example stated above can be implemented.

enum mar\_status { single, married, divorced, widowed } ; enum mar\_status person1, person2 ;

Like structures, this declaration has two parts:

- The first part declares the data type and specifies its possible values. These values are called ‘enumerators’.

- The second part declares variables of this data type.

Now we can give values to these variables:

person1 = married ; person2 = divorced ;

Remember, we can’t use values that aren’t in the original declaration.

### T

Thus, the following expression would cause an error:

person1 = unknown ;

Internally, the compiler treats the enumerators as integers. Each value on the list of permissible values corresponds to an integer, starting with 0. Thus, in our example, single is stored as 0, married is stored as 1, divorced as 2 and widowed as 3.

This way of assigning numbers can be overridden by the programmer by initializing the enumerators to different integer values as shown below.

enum mar\_status { single = 100, married = 200, divorced = 300, widowed = 400 } ; enum mar\_status person1, person2 ;

### Uses of Enumerated Data Type

Enumerated variables are usually used to clarify the operation of a program. For example, if we need to use employee departments in a payroll program, it makes the listing easier to read if we use values like Assembly, Manufacturing, Accounts rather than the integer values 0, 1, 2, etc. The following program illustrates the point I am trying to make:

\# include <stdio.h> # include <string.h> int main( ) { enum emp\_dept { assembly, manufacturing, accounts, stores } ; struct employee { char name\[ 30 \] ; int age ; float bs ; enum emp\_dept department ; } ; struct employee e ;

strcpy ( e.name, "Lothar Mattheus" ) ; e.age = 28 ; e.bs = 5575.50 ; e.department = manufacturing ; printf ( "Name = %s\\n", e.name ) ; printf ( "Age = %d\\n", e.age ) ; printf ( "Basic salary = %f\\n", e.bs ) ; printf ( "Dept = %d\\n", e.department ) ; if ( e.department == accounts ) printf ( "%s is an accounant\\n", e.name ) ; else printf ( "%s is not an accounant\\n", e.name ) ; return 0 ; }

And here is the output of the program...

Name = Lothar Mattheus Age = 28 Basic salary = 5575.50 Dept = 1 Lothar Mattheus is not an accountant

Let us now dissect the program. We first defined the data type **enum emp\_dept** and specified the four possible values, namely, assembly, manufacturing, accounts and stores. Then we defined a variable **department** of the type **enum emp\_dept** in a structure. The structure **employee** has three other elements containing employee information.

The program first assigns values to the variables in the structure. The statement,

e.department = manufacturing ;

assigns the value manufacturing to **e.department** variable. This is much more informative to anyone reading the program than a statement like,

e.department = 1 ;

The next part of the program shows an important weakness of using **enum** variables... there is no way to use the enumerated values directly in input/output functions like **scanf( )** and **printf( )**.

The **printf( )** function is not smart enough to perform the translation; the department is printed out as 1 and not manufacturing. Of course, we can write a function to print the correct enumerated values, using a **switch** statement, but that would reduce the clarity of the program. Even with this limitation, however, there are many situations in which enumerated variables are god sent!

### Are Enums Necessary?

Is there a way to achieve what was achieved using Enums in the previous program? Yes, using macros as shown below.

\# include <string.h> # define ASSEMBLY 0 # define MANUFACTURING 1 # define ACCCOUNTS 2 # define STORES 3 int main( ) { struct employee { char name\[ 30 \] ; int age ; float bs ; int department ; } ; struct employee e ; strcpy ( e.name, "Lothar Mattheus" ) ; e.age = 28 ; e.bs = 5575.50 ; e.department = MANUFACTURING ; return 0 ; }

If the same effect—convenience and readability can be achieved using macros then why should we prefer enums? Because, macros have a global scope, whereas, scope of enum can either be global (if declared outside all functions) or local (if declared inside a function).

**Renaming Data types with _typedef_** There is one more technique, which, in some situations, can help to clarify the source code of a C program. This technique is to make use of the **typedef** declaration. Its purpose is to redefine the name of an existing variable type.

For example, consider the following statement in which the type **unsigned long int** is redefined to be of the type **TWOWORDS**:

typedef unsigned long int TWOWORDS ;

Now we can declare variables of the type **unsigned long int** by writing,

TWOWORDS var1, var2 ;

instead of

unsigned long int var1, var2 ;

Thus, **typedef** provides a short and meaningful way to call a data type. Usually, uppercase letters are used to make it clear that we are dealing with a renamed data type.

While the increase in readability is probably not great in this example, it can be significant when the name of a particular data type is long and unwieldy, as it often is with structure declarations. For example, consider the following structure declaration:

struct employee { char name\[ 30 \] ; int age ; float bs ; } ; struct employee e ;

This structure declaration can be made more handy to use when renamed using **typedef** as shown below.

struct employee { char name\[ 30 \] ; int age ;

float bs ; } ; typedef struct employee EMP ; EMP e1, e2 ;

Thus, by reducing the length and apparent complexity of data types, **typedef** can help to clarify source listing and save time and energy spent in understanding a program.

The above **typedef** can also be written as

typedef struct employee { char name\[ 30 \] ; int age ; float bs ; } EMP ; EMP e1, e2 ;

**typedef** can also be used to rename pointer data types as shown below.

struct employee { char name\[ 30 \] ; int age ; float bs ; } typedef struct employee \* PEMP ; PEMP p ; p -> age = 32 ;

**Typecasting** Sometimes we are required to force the compiler to explicitly convert the value of an expression to a particular data type. This would be clear from the following example:

\# include <stdio.h> int main( ) { float a ; int x = 6, y = 4 ; a = x / y ;

printf ( "Value of a = %f\\n", a ) ; return 0 ; }

And here is the output...

Value of a = 1.000000

The answer turns out to be 1.000000 and not 1.5. This is because, 6 and 4 are both integers and hence **6 / 4** yields an integer, 1. This 1 when stored in **a** is converted to 1.000000 . But what if we don’t want the quotient to be truncated? One solution is to make either **x** or **y** as **float**. Let us say that other requirements of the program do not permit us to do this. In such a case what do we do? Use typecasting. The following program illustrates this:

\# include <stdio.h> int main( ) { float a ; int x = 6, y = 4 ; a = ( float ) x / y ; printf ( "Value of a = %f\\n", a ) ; return 0 ; }

And here is the output...

Value of a = 1.500000

This program uses typecasting. This consists of putting a pair of parentheses around the name of the data type. In this program we said,

a = ( float ) x / y ;

The expression ( **float** ) causes the variable **x** to be converted from type **int** to type **float** before being used in the division operation.

Here is another example of typecasting:

\# include <stdio.h> int main( ) { float a = 6.35 ;

printf ( "Value of a on type casting = %d\\n", ( int ) a ) ; printf ( "Value of a = %f\\n", a ) ; return 0 ; }

And here is the output...

Value of a on type casting = 6 Value of a = 6.350000

Note that the value of **a** doesn’t get permanently changed as a result of typecasting. Rather it is the value of the expression that undergoes type conversion whenever the cast appears.

**Bit Fields** If in a program a variable is to take only two values 1 and 0, we really need only a single bit to store it. Similarly, if a variable is to take values from 0 to 3, then two bits are sufficient to store these values. And if a variable is to take values from 0 through 7, then 3 bits will be enough, and so on.

Why waste an entire integer when one or two or three bits will do? Well, for one thing, there aren’t any 1 bit or 2 bit or 3 bit data types available in C. However, when there are several variables whose maximum values are small enough to pack into a single memory location, we can use ‘bit fields’ to store several values in a single integer. To demonstrate how bit fields work, let us consider an example. Suppose we want to store the following data about an employee. Each employee can:

- Be male or female (b) Be single, married, divorced or widowed (c) Have one of the eight different hobbies (d) Can choose from any of the fifteen different schemes proposed by

the company to pursue his/her hobby.

This means we need 1 bit to store gender, 2 to store marital status, 3 for hobby, and 4 for scheme (with one value used for those who are not desirous of availing any of the schemes). We need 10 bits altogether, which means we can pack all this information into a single integer, since an integer is 16 bits long.

To do this using bit fields, we declare the following structure:

struct employee { unsigned gender : 1 ; unsigned mar\_stat : 2 ; unsigned hobby : 3 ; unsigned scheme : 4 ; } ;

The colon ( : ) in the above declaration tells the compiler that we are talking about bit fields and the number after it tells how many bits to allot for the field.

Once we have established a bit field, we can reference it just like any other structure element, as shown in the program given below.

\# include <stdio.h> # define MALE 0 ; # define FEMALE 1 ; # define SINGLE 0 ; # define MARRIED 1 ; # define DIVORCED 2 ; # define WIDOWED 3 ; int main( ) { struct employee { unsigned gender : 1 ; unsigned mar\_stat : 2 ; unsigned hobby : 3 ; unsigned scheme : 4 ; } ; struct employee e ; e.gender = MALE ; e.mar\_status = DIVORCED ; e.hobby = 5 ; e.scheme = 9 ; printf ( "Gender = %d\\n", e.gender ) ;

printf ( "Marital status = %d\\n", e.mar\_status ) ; printf ( "Bytes occupied by e = %d\\n", sizeof ( e ) ) ; return 0 ; }

And here is the output...

Gender = 0 Marital status = 2 Bytes occupied by e = 2

**Pointers to Functions** Every type of variable that we have discussed so far, with the exception of register, has an address. We have seen how we can reference variables of the type **char, int, float,** etc., through their addresses—that is by using pointers. Pointers can also point to C functions. And why not? C functions have addresses. If we know the function’s address, we can point to it, which provides another way to invoke it. Let us see how this can be done.

\# include <stdio.h> void display( ) ; int main( ) { printf ( "Address of function display is %u\\n", display ) ; display( ) ; /\* usual way of invoking a function \*/ return 0 ; } void display( ) { puts ( "Long live viruses!!\\n" ) ; }

The output of the program would be:

Address of function display is 1125 Long live viruses!!

Note that, to obtain the address of a function, all that we have to do is mention the name of the function, as has been done in the **printf( )**

statement above. This is similar to mentioning the name of the array to get its base address.

Now let us see how using the address of a function, we can manage to invoke it. This is shown in the program given below.

/\* Invoking a function using a pointer to a function \*/ # include <stdio.h> void display( ) ; int main( ) { void ( \*func\_ptr )( ) ; func\_ptr = display ; /\* assign address of function \*/ printf ( "Address of function display is %u", func\_ptr ) ; ( \*func\_ptr )( ) ; /\* invokes the function display( ) \*/ return 0 ; } void display( ) { puts ( "\\nLong live viruses!!" ) ; }

The output of the program would be:

Address of function display is 1125 Long live viruses!!

In **main( )**, we declare the function **display( )** as a function returning nothing. But what are we to make of the declaration,

void ( \*func\_ptr )( ) ;

that comes in the next line? We are obviously declaring something that, like **display( )**, will return nothing, but what is it? And why is **\*func\_ptr** enclosed in parentheses?

If we glance down a few lines in our program, we see the statement,

func\_ptr = display ;

so we know that **func\_ptr** is being assigned the address of **display( )**. Therefore, **func\_ptr** must be a pointer to the function **display( )**. Thus, all that the declaration

void ( \*func\_ptr )( ) ;

means is, that **func\_ptr** is a pointer to a function, which returns nothing. And to invoke the function, we are just required to write the statement,

( \*func\_ptr )( ) ; /\* or simply, func\_ptr( ) ; \*/

Pointers to functions are certainly awkward and off-putting. And why use them at all when we can invoke a function in a much simpler manner? What is the possible gain of using this esoteric feature of C? There are two possible uses:

- In implementing callback mechanisms used popularly in Windows programming.

- In binding functions dynamically, at run-time in C++ programming.

These topics are beyond the scope of this book. If you want to explore them further you can refer the book “Let Us C++” or “Test Your C++ Skills” by Yashavant Kanetkar.

**Functions Returning Pointers** The way functions return an **int**, a **float**, a **double** or any other data type, it can even return a pointer. However, to make a function return a pointer, it has to be explicitly mentioned in the calling function as well as in the function definition. The following program illustrates this:

int \*fun( ) ; int main( ) { int \*p ; p = fun( ) ; return 0 ; } int \*fun( ) { static int i = 20 ; return ( &i ) ; }

This program just indicates how an integer pointer can be returned from a function. Beyond that, it doesn’t serve any useful purpose. This

concept can be put to use while handling strings. For example, look at the following program which copies one string into another and returns the pointer to the target string:

char \*copy ( char \*, char \* ) ; int main( ) { char \*str ; char source\[ \] = "Jaded" ; char target\[ 10 \] ; str = copy ( target, source ) ; printf ( "%s\\n", str ) ; return 0 ; } char \*copy ( char \*t, char \*s ) { char \*r ; r = t ; while ( \*s != '\\0' ) { \*t = \*s ; t++ ; s++ ; } \*t = '\\0' ; return ( r ) ; }

Here we have sent the base addresses of **source** and **target** strings to **copy( )**. In the **copy( )** function, the **while** loop copies the characters in the source string into the target string. Since during copying **t** is continuously incremented, before entering into the loop, the initial value of **t** is safely stored in the character pointer **r**. Once copying is over, this character pointer **r** is returned to **main( )**.

**Functions with Variable Number of Arguments** We have used **printf( )** so often without realizing how it works properly irrespective of how many arguments we pass to it. How do we go about writing such routines that can take variable number of arguments? And what have pointers got to do with it? There are three macros available in the file “**stdarg.h**” called **va\_start**, **va\_arg** and **va\_list** which allow us to handle this situation. These macros provide a method for accessing the arguments of the function when a function takes a fixed number of arguments followed by a variable number of arguments. The fixed number of arguments are accessed in the normal way, whereas the optional arguments are accessed using the macros **va\_start** and **va\_arg**. Out of these macros, **va\_start** is used to initialize a pointer to the beginning of the list of optional arguments. On the other hand, the macro **va\_arg** is used to advance the pointer to the next argument.

Let us put these concepts into action using a program. Suppose we wish to write a function **findmax( )** which would find out the maximum value from a set of values, irrespective of the number of values passed to it. Here is how we can do it…

\# include <stdio.h> # include <stdarg.h> int findmax ( int, … ) ; int main( ) { int max ; max = findmax ( 5, 23, 15, 1, 92, 50 ) ; printf ( "maximum = %d\\n", max ) ; max = findmax ( 3, 100, 300, 29 ) ; printf ( "maximum = %d\\n", max ) ; return 0 ; } int findmax ( int tot\_num, … ) { int max, count, num ; va\_list ptr ;

va\_start ( ptr, tot\_num ) ; max = va\_arg ( ptr, int ) ; for ( count = 1 ; count < tot\_num ; count++ ) { num = va\_arg ( ptr, int ) ; if ( num > max ) max = num ; } return ( max ) ; }

Note how the **findmax( )** function has been declared. The ellipses ( … ) indicate that the number of arguments after the first argument would be variable.

Here we are making two calls to **findmax( )**, first time to find maximum out of 5 values and second time to find maximum out of 3 values. Note that for each call the first argument is the count of arguments that follow the first argument. The value of the first argument passed to **findmax( )** is collected in the variable **tot\_num**. **findmax( )** begins with a declaration of a pointer **ptr** of the type **va\_list**. Observe the next statement carefully.

va\_start ( ptr, tot\_num ) ;

This statement sets up **ptr** such that it points to the first variable argument in the list. If we are considering the first call to **finndmax( )**, **ptr** would now point to 23. The statement **max = va\_arg ( ptr, int )** would assign the integer being pointed to by **ptr** to **max**. Thus 23 would be assigned to **max**, and **ptr** would now start pointing to the next argument, i.e.,15. The rest of the program is fairly straightforward. We just keep picking up successive numbers in the list and keep comparing them with the latest value in **max**, till all the arguments in the list have been scanned. The final value in **max** is then returned to **main( )**.

How about another program to fix your ideas? This one calls a function **display( )** which is capable of printing any number of arguments of any type.

\# include <stdio.h> # include <stdarg.h>

void display ( int, int, … ) ; int main( ) { display ( 1, 2, 5, 6 ) ; display ( 2, 4, 'A', 'a', 'b', 'c' ) ; display ( 3, 3, 2.5, 299.3, -1.0 ) ; return 0 ; } void display ( int type, int num, … ) { int i, j ; char c ; float f ; va\_list ptr ; va\_start ( ptr, num ) ; switch ( type ) { case 1 : for ( j = 1 ; j <= num ; j++ ) { i = va\_arg ( ptr, int ) ; printf ( "%d ", i ) ; } break ; case 2 : for ( j = 1 ; j <= num ; j++ ) { c = va\_arg ( ptr, char ) ; printf ( "%c ", c ) ; } break ; case 3 : for ( j = 1 ; j <= num ; j++ ) { f = ( float ) va\_arg ( ptr, double ) ; printf ( "%f ", f ) ; } } printf ( "\\n" ) ;

}

Here we pass two fixed arguments to the function **display( )**. The first one indicates the data type of the arguments to be printed and the second indicates the number of such arguments to be printed. Once again, through the statement **va\_start ( ptr, num )** we set up **ptr** such that it points to the first argument in the variable list of arguments. Then depending upon whether the value of type is 1, 2 or 3, we print out the arguments as **int**s, **char**s or **float**s.

In all calls to **display( )** the second argument indicates how many values are we trying to print. Contrast this with **printf( )**. To it we never pass an argument indicating how many value are we trying to print. Then how does **printf( )** figure this out? Simple. It scans the format string and counts the number of format specifiers that we have used in it to decide how many values are being printed.

**Unions** Unions are derived data types, the way structures are. Unions and structures look alike, but are engaged in totally different activities.

Both structures and unions are used to group a number of different variables together. But while a structure enables us treat a number of different variables stored at different places in memory, a union enables us to treat the same space in memory as a number of different variables. That is, a union offers a way for a section of memory to be treated as a variable of one type on one occasion, and as a different variable of a different type on another occasion.

You might wonder why it would be necessary to do such a thing, but we will be seeing several very practical applications of unions soon. First, let us take a look at a simple example.

/\* Demo of union at work \*/ # include <stdio.h> int main( ) { union a { short int i ; char ch\[ 2 \] ; } ; union a key ;

key.i = 512 ; printf ( "key.i = %d\\n", key.i ) ; printf ( "key.ch\[ 0 \] = %d\\n", key.ch\[ 0 \] ) ; printf ( "key.ch\[ 1 \] = %d\\n", key.ch\[ 1 \] ) ; return 0 ; }

And here is the output...

key.i = 512 key.ch\[ 0 \] = 0 key.ch\[ 1 \] = 2

As you can see, first we declared a data type of the type **union a**, and then a variable **key** to be of the type **union a**. This is similar to the way we first declare the structure type and then the structure variables. Also, the union elements are accessed exactly the same way in which the structure elements are accessed, using a ‘**.’** operator. However, the similarity ends here. To illustrate this let us compare the following data types:

struct a { short int i ; char ch\[ 2 \] ; } ; struct a key ;

This data type would occupy 4 bytes in memory, 2 for **key.i** and 1 each for **key.ch\[ 0 \]** and **key.ch\[ 1 \]**, as shown in Figure 22.1.

1002 1003 1004 1005

key.i key.ch\[0\] key.ch\[1\]

Figure 22.1

Now we declare a similar data type, but instead of using a structure we use a union.

union a { short int i ; char ch\[ 2 \] ; } ; union a key ;

Representation of this data type in memory is shown in Figure 22.2.

key.i

key.ch\[0\] key.ch\[1\]

Figure 22.2

As shown in Figure 22.2, the union occupies only 2 bytes in memory. Note that the same memory locations that are used for **key.i** are also being used by **key.ch\[ 0 \]** and **key.ch\[ 1 \]**. It means that the memory locations used by **key.i** can also be accessed using **key.ch\[ 0 \]** and **key.ch\[ 1 \]**. What purpose does this serve? Well, now we can access the 2 bytes simultaneously (by using **key.i**) or the same 2 bytes individually (using **key.ch\[ 0 \]** and **key.ch\[ 1 \]**).

This is a frequent requirement while interacting with the hardware, i.e., sometimes we are required to access 2 bytes simultaneously and sometimes each byte individually. Faced with such a situation, using union is the answer, usually.

Perhaps you would be able to understand the union data type more thoroughly if we take a fresh look at the output of the above program. Here it is...

key.i = 512 key.ch\[ 0 \] = 0 key.ch\[ 1 \] = 2

Let us understand this output in detail. 512 is an integer, a 2 byte number. Its binary equivalent will be 0000 0010 0000 0000. We would expect that this binary number when stored in memory would look as shown in Figure 22.3.

0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 0

key.i

high byte low byte

key.ch\[0\] key.ch\[1\]

Figure 22.3

If the number is stored in this manner, then the output of **key.ch\[ 0 \]** and **key.ch\[ 1 \]** should have been 2 and 0, respectively. But, if you look at the output of the program written above, it is exactly the opposite. Why is it so? Because, in CPUs that follow little-endian architecture (Intel CPUs, for example), when a 2-byte number is stored in memory, the low byte is stored before the high byte. It means, actually 512 would be stored in memory as shown in Figure 22.4. In CPUs with big-endian architecture this reversal of bytes does not happen.

0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0

key.i

low byte high byte

key.ch\[0\] key.ch\[1\]

Figure 22.4

Now, we can see why value of **key.ch\[ 0 \]** is printed as 0 and value of **key.ch\[ 1 \]** is printed as 2.

One last thing. We can’t assign different values to the different union elements at the same time. That is, if we assign a value to **key.i**, it gets automatically assigned to **key.ch\[ 0 \]** and **key.ch\[ 1 \]**. Vice versa, if we assign a value to **key.ch\[ 0 \]** or **key.ch\[ 1 \]**, it is bound to get assigned to **key.i**. Here is a program that illustrates this fact.

\# include <stdio.h> int main( ) { union a { short int i ; char ch\[ 2 \] ; } ; union a key ; key.i = 512 ; printf ( "key.i = %d\\n", key.i ) ; printf ( "key.ch\[ 0 \] = %d\\n", key.ch\[ 0 \] ) ; printf ( "key.ch\[ 1 \] = %d\\n", key.ch\[ 1 \] ) ; key.ch\[ 0 \] = 50 ; /\* assign a new value to key.ch\[ 0 \] \*/ printf ( "key.i = %d\\n", key.i ) ; printf ( "key.ch\[ 0 \] = %d\\n", key.ch\[ 0 \] ) ; printf ( "key.ch\[ 1 \] = %d\\n", key.ch\[ 1 \] ) ; return 0 ; }

And here is the output...

key.i = 512 key.ch\[ 0 \] = 0 key.ch\[ 1 \] = 2 key.i= 562 key.ch\[ 0 \] = 50 key.ch\[ 1 \] = 2

Before we move on to the next section, let us reiterate that a union provides a way to look at the same data in several different ways. For example, there can exist a union as shown below.

union b { double d ; float f\[ 2 \] ; short int i\[ 4 \] ; char ch\[ 8 \] ;

} ; union b data ;

In what different ways can the data be accessed from it? Sometimes, as a complete set of 8 bytes (**data.d**), sometimes as two sets of 4 bytes each (**data.f\[ 0 \]** and **data.f\[ 1 \]**), sometimes as four sets of 2 bytes each (**data.i\[ 0 \]**, **data.i\[ 1 \]**, **data.i\[ 2 \]** and **data.\[ 3 \]**) and sometimes as 8 individual bytes (**data.ch\[ 0 \]**, **data.ch\[ 1 \]... data.ch\[ 7 \]**).

Also note that there can exist a union, each of whose elements is of different size. In such a case, the size of the union variable will be equal to the size of the longest element in the union.

### Union of Structures

Just as one structure can be nested within another, a union too can be nested in another union. Not only that, there can be a union in a structure, or a structure in a union. Here is an example of stuctures nested in a union.

\# include <stdio.h> int main( ) { struct a { int i ; char c\[ 2 \] ; } ; struct b { int j ; char d\[ 2 \] ; } ; union z { struct a key ; struct b data ; } ; union z strange ; strange.key.i = 512 ; strange.data.d\[ 0 \] = 0 ; strange.data.d\[ 1 \] = 32 ;

printf ( "%d\\n", strange.key.i ) ; printf ( "%d\\n", strange.data.j ) ; printf ( "%d\\n", strange.key.c\[ 0 \] ) ; printf ( "%d\\n", strange.data.d\[ 0 \] ) ; printf ( "%d\\n", strange.key.c\[ 1 \] ) ; printf ( "%d\\n", strange.data.d\[ 1 \] ) ; return 0 ; }

And here is the output...

512 512 0 0 32 32

Just as we do with nested structures, we access the elements of the union in this program using the ‘**.’** operator twice. Thus,

strange.key.i

refers to the variable **i** in the structure **key** in the union **strange**. Analysis of the output of the above program is left to the reader.

**Utility of Unions** Suppose we wish to store information about employees in an organization. The items of information are as shown below.

Name Grade Age If Grade = HSK (Highly Skilled) hobbie name credit card no. If Grade = SSK (Semi Skilled) Vehicle no. Distance from Co.

Since this is dissimilar information we can gather it together using a structure as shown below.

struct employee { char n\[ 20 \] ; char grade\[ 4 \] ; int age ; char hobby\[ 10 \] ; int crcardno ; char vehno\[ 10 \] ; int dist ; } ; struct employee e ;

Though grammatically there is nothing wrong with this structure, it suffers from a disadvantage. For any employee, depending upon his/her grade, either the fields hobby and credit card no. or the fields vehicle number and distance would get used. Both sets of fields would never get used. This would lead to wastage of memory with every structure variable that we create, since every structure variable would have all the four fields apart from name, grade and age. This can be avoided by creating a **union** between these sets of fields. This is shown below.

struct info1 { char hobby\[ 10 \] ; int crcardno ; } ; struct info2 { char vehno\[ 10 \] ; int dist ; } ; union info { struct info1 a ; struct info2 b ; } ; struct employee { char n\[ 20 \] ;

char grade\[ 4 \] ; int age ; union info f ; } ; struct employee e ;

**The _volatile_ Qualifier** When we define variables in a function the compiler may optimize the code that uses the variable. That is, the compiler may compile the code in a manner that will run in the most efficient way possible. The compiler achieves this by using a CPU register to store the variable’s value rather than storing it in stack.

However, if we declare the variable as volatile, then it serves as a warning to the compiler that it should not _optimize_ the code containing this variable. In such a case whenever we use the variable its value would be loaded from memory into register, operations would be performed on it and the result would be written back to the memory location allocated for the variable.

We can declare a volatile variable as:

volatile int j ;

Another place where we may want to declare a variable as volatile is when the variable is not within the control of the program and is likely to get altered from outside the program. For example, the variable

volatile float temperature ;

might get modified through the digital thermometer attached to the computer.

### Summary

- The enumerated data type and the **typedef** declaration add to the clarity of the program.

- Typecasting makes the data type conversions for specific operations.

- When the information to be stored can be represented using a few bits of a byte we can use bit fields to pack more information in a byte.

- Every C function has an address that can be stored in a pointer to a function. Pointers to functions provide one more way to call functions.

- We can write a function that receives a variable number of arguments.

- Unions permit access to same memory locations in multiple ways.

### Exercise

**\[A\]** What will be the output of the following programs:

- # include <stdio.h> int main( )

{ enum status { pass, fail, atkt } ; enum status stud1, stud2, stud3 ; stud1 = pass ; stud2 = fail ; stud3 = atkt ; printf ( "%d %d %d\\n", stud1, stud2, stud3 ) ; return 0 ; }

- # include <stdio.h> int main( )

{ printf ( "%f\\n", ( float ) ( ( int ) 3.5 / 2 ) ) ; return 0 ; }

- # include <stdio.h> int main( )

{ float i, j ; i = ( float ) 3 / 2 ; j = i \* 3 ; printf ( "%d\\n", ( int ) j ) ; return 0 ; }

**\[B\]** Point out the error, if any, in the following programs:

- # include <stdio.h>

int main( ) { typedef struct patient { char name\[ 20 \] ; int age ; int systolic\_bp ; int diastolic\_bp ; } ptt ; ptt p1 = { "anil", 23, 110, 220 } ; printf ( "%s %d\\n", p1.name, p1.age ) ; printf ( "%d %d\\n", p1.systolic\_bp, p1.diastolic\_bp ) ; return 0 ; }

- # include <stdio.h> void show( ) ;

int main( ) { void ( \*s )( ) ; s = show ; ( \*s )( ) ; s( ) ; return 0 ; } void show( ) { printf ( "don't show off. It won't pay in the long run\\n" ) ; }

- # include <stdio.h> void show ( int, float ) ;

int main( ) { void ( \*s )( int, float ) ; s = show ; ( \*s )( 10, 3.14 ) ; return 0 ; } void show ( int i, float f ) { printf ( "%d %f\\n", i, f ) ;

}

**\[C\]** Attempt the following:

- Create an array of four function pointers. Each pointer should point to a different function. Each of these functions should receive two integers and return a float. Using a loop call each of these functions using the addresses present in the array.

- Write a function that receives variable number of arguments, where the arguments are the coordinates of a point. Based on the number of arguments received, the function should display type of shape like a point, line, triangle, etc., that can be drawn.

- Write a program, which stores information about a date in a structure containing three members—day, month and year. Using bit fields the day number should get stored in first 5 bits of day, the month number in 4 bits of month and year in 12 bits of year. Write a program to read date of joining of 10 employees and display them in ascending order of year.

- Write a program to read and store information about insurance policy holder. The information contains details like gender, whether the holder is minor/major, policy name and duration of the policy. Make use of bit-fields to store this information.

