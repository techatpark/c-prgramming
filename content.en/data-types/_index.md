---
title: 'Data Types'
weight: 11
---

   

s seen in the first chapter, the primary data types could be of three varieties—**char**, **int**, and **float**. It may seem odd to many, how C

programmers manage with such a tiny set of data types. Fact is, the C programmers aren’t really deprived. They can derive many data types from these three types. In fact, the number of data types that can be derived in C, is in principle, unlimited. A C programmer can always invent whatever data type he needs, as we would see later in Chapter 17.

Not only this, the primary data types themselves can be of several types. For example, a **char** can be an **unsigned** **char** or a **signed** **char**. Or an **int** can be a **short** **int** or a **long** **int**. Sufficiently confusing? Well, let us take a closer look at these variations of primary data types in this chapter.

To fully define a variable, one needs to mention not only its type but also its storage class. In this chapter we would also explore the different storage classes and their relevance in C programming.

**Integers, _long_ and _short_** We had seen earlier that the range of an Integer constant depends upon the compiler. For a 16-bit compiler like Turbo C or Turbo C++ the range is –32768 to 32767. For a 32-bit compiler like Visual Studio or gcc the range would be –2147483648 to +2147483647. Here a 16-bit compiler means that when it compiles a C program it generates machine language code that is targeted towards working on a 16-bit microprocessor like Intel 8086/8088. As against this, a 32-bit compiler like Visual Studio generates machine language code that is targeted towards a 32-bit microprocessor like Intel Pentium. Note that this does not mean that a program compiled using Turbo C would not work on 32-bit processor. It would run successfully but at that time the 32-bit processor would work as if it were a 16-bit processor. This happens because a 32-bit processor provides support for programs compiled using 16-bit compilers. If this backward compatibility support is not provided the 16-bit program would not run on it. This is precisely what happens on the new Intel Itanium processors (64-bit), which have withdrawn support for 16-bit code.

Remember that out of the two/four bytes used to store an integer, the highest bit (16th/32nd bit) is used to store the sign of the integer. This bit is 1 if the number is negative and 0 if the number is positive.

### A

C offers a variation of the integer data type that provides what are called **short** and **long** integer values. The intention of providing these variations is to provide integers with different ranges wherever possible. Though not a rule, **short** and **long** integers would usually occupy two and four bytes respectively. Each compiler can decide appropriate sizes depending on the operating system and hardware, for which it is being written, subject to the following rules:

- **short**s are at least 2 bytes big

- **long**s are at least 4 bytes big

- **short**s are never bigger than **int**s

- **int**s are never bigger than **long**s

Figure 11.1 shows the sizes of different integers based upon the compiler used.

### Compiler short int long

16-bit (Turbo C/C++) 32-bit (Visual Studio, gcc)

2 2

2 4

4 4

Figure 11.1

**long** variables which hold **long** integers are declared using the keyword **long**, as in,

long int i ; long int abc ;

**long** integers cause the program to run a bit slower, but the range of values that we can use is expanded tremendously. The value of a **long** integer typically can vary from -2147483648 to +2147483647. More than this you should not need unless you are taking a world census.

If there are such things as **long**s, symmetry requires **short**s as well— integers that need less space in memory and thus help speed up program execution. **short** integer variables are declared as,

short int j ; short int height ;

C allows the abbreviation of **short** **int** to **short** and of **long** **int** to **long**. So the declarations made above can be written as,

long i ; long abc ; short j ; short height ;

Naturally, most C programmers prefer this short-cut.

Sometimes, we come across situations where the constant is small enough to be an **int**, but still we want to give it as much storage as a **long**. In such cases, we add the suffix ‘L’ or ‘l’ at the end of the number, as in 23L.

**Integers, _signed_ and _unsigned_** Sometimes, we know in advance that the value stored in a given integer variable will always be positive—when it is being used to only count things, for example. In such a case we can declare the variable to be **unsigned**, as in,

unsigned int num\_students ;

With such a declaration, the range of permissible integer values (for a 32-bit compiler) will shift from the range –2147483648 to +2147483647 to the range 0 to 4294967295. Thus, declaring an integer as **unsigned** almost doubles the size of the largest possible value that it can otherwise take. This so happens because on declaring the integer as **unsigned**, the left-most bit is now free and is not used to store the sign of the number. Note that an **unsigned** integer still occupies two bytes. This is how an **unsigned** integer can be declared:

unsigned int i ; unsigned i ;

Like an **unsigned** **int**, there also exists a **short unsigned int** and a **long** **unsigned** **int**. By default, a **short** **int** is a **signed** **short** **int** and a **long** **int** is a **signed** **long** **int**.

**Chars, _signed_ and _unsigned_** Parallel to **signed** and **unsigned** **int**s (either **short** or **long**), there also exist **signed** and **unsigned** **char**s, both occupying one byte each, but having different ranges. To begin with, it might appear strange as to how a **char** can have a sign. Consider the statement

char ch = 'A' ;

Here what gets stored in **ch** is the binary equivalent of the ASCII / Unicode value of ‘A’ (i.e. binary of 65). And if 65’s binary can be stored, then -54’s binary can also be stored (in a **signed** **char**).

A **signed** **char** is same as an ordinary **char** and has a range from -128 to +127; whereas, an **unsigned** **char** has a range from 0 to 255. Let us now see a program that illustrates this range:

\# include <stdio.h> int main( ) { char ch = 291 ; printf ( "\\n%d %c\\n", ch, ch ) ; return 0 ; }

What output do you expect from this program? Possibly, 291 and the character corresponding to it. Well, not really. Surprised? The reason is that **ch** has been defined as a **char**, and a **char** cannot take a value bigger than +127. Hence when value of **ch** exceeds +127, an appropriate value from the other side of the range is picked up and stored in **ch**. This value in our case happens to be 35, hence 35 and its corresponding character #, gets printed out.

Here is another program that would make the concept clearer.

\# include <stdio.h> int main( ) {

char ch ; for ( ch = 0 ; ch <= 255 ; ch++ ) printf ( "%d %c\\n", ch, ch ) ; return 0 ; }

This program should output ASCII values and their corresponding characters. Well, No! This is an indefinite loop. The reason is that **ch** has been defined as a **char**, and a **char** cannot take values bigger than +127. Hence when value of **ch** is +127 and we perform **ch++** it becomes -128 instead of +128. -128 is less than 255, hence the condition is still satisfied. Here onwards **ch** would take values like -127, -126, -125, .... -2, -1, 0, +1, +2, ... +127, -128, -127, etc. Thus the value of **ch** would keep oscillating between -128 to +127, thereby ensuring that the loop never gets terminated. How do you overcome this difficulty? Would declaring **ch** as an **unsigned** **char** solve the problem? Even this would not serve the purpose since when **ch** reaches a value 255, **ch++** would try to make it 256 which cannot be stored in an **unsigned** **char**. Thus the only alternative is to declare **ch** as an **int**. However, if we are bent upon writing the program using **unsigned** **char**, it can be done as shown below. The program is definitely less elegant, but workable all the same.

\# include <stdio.h> int main( ) { unsigned char ch ; for ( ch = 0 ; ch <= 254 ; ch++ ) printf ( "%d %c\\n", ch, ch ) ; printf ( "%d %c\\n", ch, ch ) ; return 0 ; }

**Floats and Doubles** A **float** occupies four bytes in memory and can range from -3.4e38 to +3.4e38. If this is insufficient, then C offers a **double** data type that

occupies 8 bytes in memory and has a range from -1.7e308 to +1.7e308. A variable of type **double** can be declared as,

double a, population ;

If the situation demands usage of real numbers that lie even beyond the range offered by **double** data type, then there exists a **long** **double** that can range from -1.7e4932 to +1.7e4932. A **long** **double** occupies 10 bytes in memory.

You would see that most of the times in C programming, one is required to use either **char**s or **int**s and cases where **float**s, **double**s or **long** **double**s would be used are indeed rare.

Let us now write a program that puts to use all the data types that we have learnt in this chapter. Go through the following program carefully, which shows how to use these different data types. Note the format specifiers used to input and output these data types.

\# include <stdio.h> int main( ) { char c ; unsigned char d ; int i ; unsigned int j ; short int k ; unsigned short int l ; long int m ; unsigned long int n ; float x ; double y ; long double z ; /\* char \*/ scanf ( "%c %c", &c, &d ) ; printf ( "%c %c\\n", c, d ) ; /\* int \*/ scanf ( "%d %u", &i, &j ) ; printf ( "%d %u\\n", i, j ) ;

/\* short int \*/ scanf ( "%d %u", &k, &l ) ; printf ( "%d %u\\n", k, l ) ; /\* long int \*/ scanf ( "%ld %lu", &m, &n ) ; printf ( "%ld %lu\\n", m, n ) ; /\* float, double, long double \*/ scanf ( "%f %lf %Lf", &x, &y, &z ) ; printf ( "%f %lf %Lf\\n", x, y, z ) ; }

The essence of all the data types that we have learnt so far has been captured in Figure 11.2.

### Data Type Range Bytes Format

signed char

unsigned char

short signed int

short unsigned int

signed int

unsigned int

long signed int

long unsigned int

float

double

long double

\-128 to +127

0 to 255

\-32768 to +32767

0 to 65535

\-2147483648 to +2147483647

0 to 4294967295

\-2147483648 to +2147483647

0 to 4294967295

\-3.4e38 to +3.4e38

\-1.7e308 to +1.7e308

\-1.7e4932 to +1.7e4932

1

1

2

2

4

4

4

4

4

8

10

%c

%c

%d

%u

%d

%u

%ld

%lu

%f

%lf

%Lf

Note: The sizes and ranges of int, short and long are compiler dependent. Sizes in this figure are for 32-bit compiler.

Figure 11.2

**A Few More Issues…** Having seen all the variations of the primary types let us take a look at some more related issues.

- We saw earlier that size of an integer is compiler dependent. This is even true in case of **char**s and **float**s. Also, depending upon the microprocessor for which the compiler targets its code the accuracy of floating point calculations may change. For example, the result of 22.0/7.0 would be reported more accurately by Visual Studio compiler as compared to TC/TC++ compilers. This is because TC/TC++ targets its compiled code to 8088/8086 (16-bit) microprocessors. Since these microprocessors do not offer floating point support, TC/TC++ performs all float operations using a software piece called Floating Point Emulator. This emulator has limitations and hence produces less accurate results. Also, this emulator becomes part of the EXE file, thereby increasing its size. In addition to this increased size there is a performance penalty since this bigger code would take more time to execute.

- If you look at ranges of **char**s and **int**s there seems to be one extra number on the negative side. This is because a negative number is always stored as 2’s compliment of its binary. For example, let us see how -128 is stored. Firstly, binary of 128 is calculated (10000000), then its 1’s compliment is obtained (01111111). A 1’s compliment is obtained by changing all 0s to 1s and 1s to 0s. Finally, 2’s compliment of this number, i.e. 10000000, gets stored. A 2’s compliment is obtained by adding 1 to the 1’s compliment. Thus, for -128, 10000000 gets stored. This is an 8-bit number and it can be easily accommodated in a **char**. As against this, +128 cannot be stored in a **char** because its binary 010000000 (left-most 0 is for positive sign) is a 9-bit number. However +127 can be stored as its binary 01111111 turns out to be a 8-bit number.

- What happens when we attempt to store +128 in a **char**? The first number on the negative side, i.e. -128 gets stored. This is because from the 9-bit binary of +128, 010000000, only the right-most 8 bits get stored. But when 10000000 is stored the left-most bit is 1 and it is treated as a sign bit. Thus the value of the number becomes -128 since it is indeed the binary of -128, as can be understood from (b) above. Similarly, you can verify that an attempt to store +129 in a

**char** results in storing -127 in it. In general, if we exceed the range from positive side we end up on the negative side. Vice versa is also true. If we exceed the range from negative side we end up on positive side.

**Storage Classes in C** We have already said all that needs to be said about constants, but we are not finished with variables. To fully define a variable, one needs to mention not only its ‘type’ but also its ‘storage class’. In other words, not only do all variables have a data type, they also have a ‘storage class’.

We have not mentioned storage classes yet, though we have written several programs in C. We were able to get away with this because storage classes have defaults. If we don’t specify the storage class of a variable in its declaration, the compiler will assume a storage class depending on the context in which the variable is used. Thus, variables have certain default storage classes.

From C compiler’s point of view, a variable name identifies some physical location within the computer where the string of bits representing the variable’s value is stored. There are basically two kinds of locations in a computer where such a value may be kept— Memory and CPU registers. It is the variable’s storage class that determines in which of these two types of locations, the value is stored.

Moreover, a variable’s storage class tells us:

- Where the variable would be stored.

- What will be the initial value of the variable, if initial value is not specifically assigned.(i.e. the default initial value).

- What is the scope of the variable; i.e. in which functions the value of the variable would be available.

- What is the life of the variable; i.e. how long would the variable exist.

There are four storage classes in C:

- Automatic storage class (b) Register storage class (c) Static storage class

- External storage class

Let us examine these storage classes one by one.

### Automatic Storage Class

The features of a variable defined to have an automatic storage class are as under:

Storage: Memory. Default value: An unpredictable value, often called a garbage value. Scope: Local to the block in which the variable is defined. Life: Till the control remains within the block in which the

variable is defined.

Following program shows how an automatic storage class variable is declared, and the fact that if the variable is not initialized, it contains a garbage value.

\# include <stdio.h> int main( ) { auto int i, j ; printf ( "%d %d\\n", i, j ) ; return 0 ; }

The output of the above program could be...

1211 221

where, 1211 and 221 are garbage values of **i** and **j**. When you run this program, you may get different values, since garbage values are unpredictable. So always make it a point that you initialize the automatic variables properly, otherwise you are likely to get unexpected results. Note that the keyword for this storage class is **auto**, and not automatic.

Scope and life of an automatic variable is illustrated in the following program.

\# include <stdio.h> int main( ) { auto int i = 1 ; { auto int i = 2 ; { auto int i = 3 ; printf ( "%d ", i ) ; } printf ( "%d ", i ) ; } printf ( "%d\\n", i ) ; return 0 ; }

The output of the above program would be:

3 2 1

Note that the Compiler treats the three **i**’s as totally different variables, since they are defined in different blocks. All three **i**’s are available to the innermost **printf( )**. This is because the innermost **printf( )** lies in all the three blocks (a block is all statements enclosed within a pair of braces) in which the three **i**’s are defined. This **printf( )** prints 3 because when all three **i**’s are available, the one which is most local (nearest to **printf( )**) is given a priority.

Once the control comes out of the innermost block, the variable **i** with value 3 is lost, and hence the **i** in the second **printf( )** refers to **i** with value 2. Similarly, when the control comes out of the next innermost block, the third **printf( )** refers to the **i** with value 1.

Understand the concept of life and scope of an automatic storage class variable thoroughly before proceeding with the next storage class.

### Register Storage Class

The features of a variable defined to be of **register** storage class are as under:

Storage: CPU registers. Default value: Garbage value. Scope: Local to the block in which the variable is defined. Life: Till the control remains within the block in which the

variable is defined.

A value stored in a CPU register can always be accessed faster than the one that is stored in memory. Therefore, if a variable is used at many places in a program, it is better to declare its storage class as **register**. A good example of frequently used variables is loop counters. We can name their storage class as **register**.

\# include <stdio.h> int main( ) { register int i ; for ( i = 1 ; i <= 10 ; i++ ) printf ( "%d\\n", i ) ; return 0 ; }

Here, even though we have declared the storage class of **i** as **register**, we cannot say for sure that the value of **i** would be stored in a CPU register. Why? Because the number of CPU registers are limited, and they may be busy doing some other task. What happens in such an event... the variable works as if its storage class is **auto**.

Not every type of variable can be stored in a CPU register. For example, if the microprocessor has 16-bit registers then they cannot hold a **float** value or a **double** value, which require 4 and 8 bytes respectively. However, if you use the **register** storage class for a **float** or a **double** variable, you won’t get any error messages. All that would happen is the compiler would treat the variables to be of **auto** storage class.

### Static Storage Class

The features of a variable defined to have a **static** storage class are as under:

Storage: Memory. Default value: Zero. Scope: Local to the block in which the variable is defined. Life: Value of the variable persists between different

function calls.

Compare the two programs and their output given in Figure 11.3 to understand the difference between the **automatic** and **static** storage classes.

The programs in Figure 11.3 consist of two functions **main( )** and **increment( )**. The function **increment( )** gets called from **main( )** thrice. Each time it prints the value of **i** and then increments it. The only difference in the two programs is that one uses an **auto** storage class for variable **i**, whereas the other uses **static** storage class.

#include <stdio.h> void increment( ) ; int main( ) {

increment( ) ; increment( ) ; increment( ) ; return 0 ;

} void increment( ) {

auto int i = 1 ; printf ( “%d\\n”, i ) ; i = i + 1 ;

}

#include <stdio.h> void increment( ) ; int main( ) {

increment( ) ; increment( ) ; increment( ) ; return 0 ;

} void increment( ) {

static int i = 1 ; printf ( “%d\\n”, i ) ; i = i + 1 ;

}

The output of the above programs would be:

1 1 1

1 2 3

Figure 11.3

Like **auto** variables, **static** variables are also local to the block in which they are declared. The difference between them is that **static** variables don’t disappear when the function is no longer active. Their values

persist. If the control comes back to the same function again, the **static** variables have the same values they had last time around.

In the above example, when variable **i** is **auto**, each time **increment( )** is called, it is re-initialized to one. When the function terminates, **i** vanishes and its new value of 2 is lost. The result: no matter how many times we call **increment( ),** **i** is initialized to 1 every time.

On the other hand, if **i** is **static**, it is initialized to 1 only once. It is never initialized again. During the first call to **increment( )**, **i** is incremented to 2. Because **i** is static, this value persists. The next time **increment(** **)** is called, **i** is not re-initialized to 1; on the contrary, its old value 2 is still available. This current value of **i** (i.e. 2) gets printed and then **i = i + 1** adds 1 to **i** to get a value of 3. When **increment( )** is called the third time, the current value of **i** (i.e. 3) gets printed and once again **i** is incremented. In short, if the storage class is **static**, then the statement **static** **int** **i =** **1** is executed only once, irrespective of how many times the same function is called.

Consider one more program.

\# include <stdio.h> int \* fun( ) ; int main( ) { int \*j ; j = fun( ) ; printf ( "%d\\n", \*j ) ; return 0 ; } int \*fun( ) { int k = 35 ; return ( &k ) ; }

Here we are returning an address of **k** from **fun( )** and collecting it in **j**. Thus **j** becomes pointer to **k**. Then using this pointer we are printing the value of **k**. This correctly prints out 35. Now try calling any function (even **printf( )** ) immediately after the call to **fun( )**. This time **printf( )**

prints a garbage value. Why does this happen? In the first case, when the control returned from **fun( )** though **k** went dead it was still left on the stack. We then accessed this value using its address that was collected in **j**. But when we precede the call to **printf( )** by a call to any other function, the stack is now changed, hence we get the garbage value. If we want to get the correct value each time then we must declare **k** as **static**. By doing this when the control returns from **fun( )**, **k** would not die.

All this having been said, a word of advice—avoid using **static** variables unless you really need them. Because their values are kept in memory when the variables are not active, which means they take up space in memory that could otherwise be used by other variables.

### External Storage Class

The features of a variable whose storage class has been defined as external are as follows:

Storage: Memory. Default value: Zero. Scope: Global. Life: As long as the program’s execution doesn’t come to

an end.

External variables differ from those we have already discussed in that their scope is global, not local. External variables are declared outside all functions, yet are available to all functions that care to use them. Here is an example to illustrate this fact.

\# include <stdio.h> int i ; void increment( ) ; void decrement( ) ; int main( ) { printf ( "\\ni = %d", i ) ; increment( ) ; increment( ) ;

decrement( ) ; decrement( ) ; return 0 ; }

void increment( ) { i = i + 1 ; printf ( "on incrementing i = %d\\n", i ) ; }

void decrement( ) { i = i - 1 ; printf ( "on decrementing i = %d\\n", i ) ; }

The output would be:

i = 0 on incrementing i = 1 on incrementing i = 2 on decrementing i = 1 on decrementing i = 0

As is obvious from the above output, the value of **i** is available to the functions **increment( )** and **decrement( )** since **i** has been declared outside all functions.

Look at the following program.

\# include <stdio.h> int x = 21 ; int main( ) { extern int y ; printf ( "%d %d\\n", x, y ) ; return 0 ; } int y = 31 ;

Here, **x** and **y** both are global variables. Since both of them have been defined outside all the functions both enjoy external storage class. Note the difference between the following:

extern int y ; int y = 31 ;

Here the first statement is a declaration, whereas the second is the definition. When we declare a variable no space is reserved for it, whereas, when we define it space gets reserved for it in memory. We had to declare **y** since it is being used in **printf( )** before it’s definition is encountered. There was no need to declare **x** since its definition is done before its usage. Also remember that a variable can be declared several times but can be defined only once.

Another small issue—what will be the output of the following program?

\# include <stdio.h> int x = 10 ; void display( ) ; int main( ) { int x = 20 ; printf ( "%d\\n", x ) ; display( ) ; return 0 ; } void display( ) { printf ( "%d\\n", x ) ; }

Here **x** is defined at two places, once outside **main( )** and once inside it. When the control reaches the **printf( )** in **main(** **)** which **x** gets printed? Whenever such a conflict arises, it’s the local variable that gets preference over the global variable. Hence the **printf( )** outputs 20. When **display( )** is called and control reaches the **printf(** **)** there is no such conflict. Hence, this time, the value of the global **x**, i.e. 10 gets printed.

One last thing—a **static** variable can also be declared outside all the functions. For all practical purposes it will be treated as an **extern** variable. However, the scope of this variable is limited to the same file in which it is declared. This means that the variable would not be available to any function that is defined in a file other than the file in which the variable is defined.

### A Few Subtle Issues

Let us now look at some subtle issues about storage classes.

- All variables that are defined inside a function are normally created on the stack each time the function is called. These variables die as soon as control goes back from the function. However, if the variables inside the function are defined as static then they do not get created on the stack. Instead they are created in a place in memory called ‘Data Segment’. Such variables die only when program execution comes to an end.

- If a variable is defined outside all functions, then not only is it available to all other functions in the file in which it is defined, but is also available to functions defined in other files. In the other files the variable should be declared as extern. This is shown in the following program:

/\* PR1.C \*/ # include <stdio.h> # include <functions.c> int i = 35 ; int fun1( ) ; int fun2( ) ; int main( ) { printf ( "%d\\n", I ) ; fun1( ) ; fun2( ) ; return 0 ; }

/\* FUNCTIONS.C \*/ extern int i ; int fun1( ) { i++ ; printf ( "%d\\n", i ) ; return 0 ; } int fun2( ) { i-- ; printf ( "%d\\n", i ) ; return 0 ; }

The output of the program would be

35 36 35

However, if we place the word **static** in front of an external variable (**i** in our case) it makes the variable private and not accessible to use in any other file.

- In the following statements the first three are definitions, whereas, the last one is a declaration.

auto int i ; static int j ; register int k ; extern int l ;

### Which to Use When

Dennis Ritchie has made available to the C programmer a number of storage classes with varying features, believing that the programmer would be in a best position to decide which one of these storage classes should be used when. We can make a few ground rules for usage of

different storage classes in different programming situations with a view to:

- economise the memory space consumed by the variables (b) improve the speed of execution of the program

The rules are as under:

- Use **static** storage class only if you want the value of a variable to persist between different function calls.

- Use **register** storage class for only those variables that are being used very often in a program. Reason is, there are very few CPU registers at our disposal and many of them might be busy doing something else. Make careful utilization of the scarce resources. A typical application of **register** storage class is loop counters, which get used a number of times in a program.

- Use **extern** storage class for only those variables that are being used by almost all the functions in the program. This would avoid unnecessary passing of these variables as arguments when making a function call. Declaring all the variables as **extern** would amount to a lot of wastage of memory space because these variables would remain active throughout the life of the program.

- If you don’t have any of the express needs mentioned above, then use the **auto** storage class. In fact, most of the times, we end up using the **auto** variables. This is because once we have used the variables in a function and are returning from it, we don’t mind losing them.

### Summary

- We can use different variations of the primary data types, namely **signed** and **unsigned** **char**, **long** and **short** **int**, **float**, **double** and **long** **double**. There are different format specifications for all these data types when they are used in **scanf( )** and **printf( )** functions.

- The maximum value a variable can hold depends upon the number of bytes it occupies in memory.

- By default all the variables are **signed**. We can declare a variable as **unsigned** to accommodate bigger value without increasing the bytes occupied.

- We can make use of proper storage classes like **auto**, **register**, **static** and **extern** to control four properties of a variable—storage, default initial value, scope and life.

### Exercise

**\[A\]** What will be the output of the following programs: (a) # include <stdio.h>

int main( ) { int i ; for ( i = 0 ; i <= 50000 ; i++ ) printf ( "%d\\n", i ) ; return 0 ; }

- # include <stdio.h> int main( ) { float a = 13.5 ; double b = 13.5 ; printf ( "%f %lf\\n", a, b ) ; return 0 ; }

- # include <stdio.h> int i = 0 ; void val( ) ; int main( ) { printf ( "main's i = %d\\n", i ) ; i++ ; val( ) ; printf ( "main's i = %d\\n", i ) ; val( ) ; return 0 ; } void val( ) {

i = 100 ; printf ( "val's i = %d\\n", i ) ; i++ ; }

- # include <stdio.h> int f ( int ) ; int g ( int ) ; int main( ) { int x, y, s = 2 ; s \*= 3 ; y = f ( s ) ; x = g ( s ) ; printf ( "%d %d %d\\n", s, y, x ) ; return 0 ; } int t = 8 ; int f ( int a ) { a += -5 ; t -= 4 ; return ( a + t ) ; } int g ( int a ) { a = 1 ; t += a ; return ( a + t ) ; }

- # include <stdio.h> int main( ) { static int count = 5 ; printf ( "count = %d\\n", count-- ) ; if ( count != 0 ) main( ) ;

return 0 ; }

- # include <stdio.h> int g ( int ) ; int main( ) { int i, j ; for ( i = 1 ; i < 5 ; i++ ) { j = g ( i ) ; printf ( "%d\\n", j ) ; } return 0 ; } int g ( int x ) { static int v = 1 ; int b = 3 ; v += x ; return ( v + x + b ) ; }

- # include <stdio.h> int main( ) { func( ) ; func( ) ; return 0 ; } void func( ) { auto int i = 0 ; register int j = 0 ; static int k = 0 ; i++ ; j++ ; k++ ; printf ( "%d % d %d\\n", i, j, k ) ; }

- # include <stdio.h> int x = 10 ;

int main( ) { int x = 20 ; { int x = 30 ; printf ( "%d\\n", x ) ; } printf ( "%d\\n", x ) ; return 0 ; }

**\[B\]** Point out the errors, if any, in the following programs:

- # include <stdio.h> int main( ) { long num ; num = 2 ; printf ( "%d\\n", num ) ; return 0 ; }

- # include <stdio.h> int main( ) { char ch = 200 ; printf ( "%d\\n", ch ) ; return 0 ; }

- # include <stdio.h> int main( ) { unsigned a = 25 ; long unsigned b = 25l ; printf ( "%lu %u\\n", a, b ) ; return 0 ; }

- # include <stdio.h> int main( ) {

long float a = 25.345e454 ; unsigned double b = 25 ; printf ( "%lf %d\\n", a, b ) ; return 0 ; }

- # include <stdio.h> static int y ; int main( ) { static int z ; printf ( "%d %d\\n", y, z ) ; return 0 ; }

**\[C\]** State whether the following statements are True or False:

- Storage for a register storage class variable is allocated each time the control reaches the block in which it is present.

- An extern storage class variable is not available to the functions that precede its definition, unless the variable is explicitly declared in these functions.

- The value of an automatic storage class variable persists between various function invocations.

- If the CPU registers are not available, the register storage class variables are treated as static storage class variables.

- The register storage class variables cannot hold float values.

- If we try to use register storage class for a **float** variable the compiler will report an error message.

- If the variable **x** is defined outside all functions and a variable **x** is also defined as a local variable of some function, then the global variable gets preference over the local variable.

- The default value for automatic variable is zero.

- The life of static variable is till the control remains within the block in which it is defined.

- If a global variable is to be defined, then the **extern** keyword is necessary in its declaration.

- The address of register variable is not accessible.

- A variable that is defined outside all functions can also have a static **storage** class.

(m) One variable can have multiple storage classes.

