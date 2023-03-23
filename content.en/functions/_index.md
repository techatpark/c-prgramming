---
title: 'Functions'
weight: 2
---

   

an is an intelligent species, but still cannot perform all of life’s tasks all alone. He has to rely on others. You may call a mechanic

to fix up your bike, hire a gardener to mow your lawn, or rely on a store to supply you groceries every month. A computer program (except for the simplest one) finds itself in a similar situation. It cannot handle all the tasks by itself. Instead, it requests other program-like entities— called ‘functions’ in C—to get its tasks done. In this chapter we will study these functions. We will look at a variety of features of these functions, starting with the simplest one and then working towards those that demonstrate the power of C functions.

**What is a Function?** A function is a self-contained block of statements that perform a coherent task of some kind. Every C program can be thought of as a collection of these functions. As we noted earlier, using a function is something like hiring a person to do a specific job for you. Sometimes the interaction with this person is very simple; sometimes it’s complex.

Suppose you have a task that is always performed exactly in the same way—say a bimonthly servicing of your motorbike. When you want it to be done, you go to the service station and say, “It’s time, do it now”. You don’t need to give instructions, because the mechanic knows his job. You don’t need to be told how the job is done. You assume the bike would be serviced in the usual way, the mechanic does it and that’s that.

Let us now look at a simple C function that operates in much the same way as the mechanic. Actually, we will be looking at two things—a function that calls or activates the function and the function itself.

\# include <stdio.h> void message( ) ; /\* function prototype declaration \*/ int main( ) { message( ) ; /\* function call \*/ printf ( "Cry, and you stop the monotony!\\n" ) ; return 0 ; } void message( ) /\* function definition \*/ { printf ( "Smile, and the world smiles with you...\\n" ) ; }

### M

And here’s the output...

Smile, and the world smiles with you... Cry, and you stop the monotony!

Here, we have defined two functions—**main( )** and **message( )**. In fact, we have used the word **message** at three places in the program. Let us understand the meaning of each.

The first is the function prototype declaration and is written as:

void message( ) ;

This prototype declaration indicates that **message( )** is a function which after completing its execution does not return any value. This ‘does not return any value’ is indicated using the keyword **void**. It is necessary to mention the prototype of every function that we intend to define in the program.

The second usage of **message** is…

void message( ) { printf ( "Smile, and the world smiles with you...\\n" ) ; }

This is the function definition. In this definition right now we are having only **printf( )**, but we can also use **if**, **for**, **while**, **switch**, etc., within this function definition.

The third usage is…

message( ) ;

Here the function **message( )** is being called by **main( )**. What do we mean when we say that **main( )** ‘calls’ the function **message( )**? We mean that the control passes to the function **message( )**. The activity of **main( )** is temporarily suspended; it falls asleep while the **message( )** function wakes up and goes to work. When the **message( )** function runs out of statements to execute, the control returns to **main( )**, which comes to life again and begins executing its code at the exact point where it left off. Thus, **main( )** becomes the ‘calling’ function, whereas **message( )** becomes the ‘called’ function.

If you have grasped the concept of ‘calling’ a function you are prepared for a call to more than one function. Consider the following example:

\# include <stdio.h> void italy( ) ; void brazil( ) ; void argentina( ) ; int main( ) { printf ( "I am in main\\n" ) ; italy( ) ; brazil( ) ; argentina( ) ; return 0 ; } void italy( ) { printf ( "I am in italy\\n" ) ; } void brazil( ) { printf ( "I am in brazil\\n" ) ; } void argentina( ) { printf ( "I am in argentina\\n" ) ; }

The output of the above program when executed would be as under:

I am in main I am in italy I am in brazil I am in argentina

A number of conclusions can be drawn from this program:

- A C program is a collection of one or more functions.

- If a C program contains only one function, it must be **main( )**.

- If a C program contains more than one function, then one (and only one) of these functions must be **main( )**, because program execution always begins with **main( )**.

- There is no limit on the number of functions that might be present in a C program.

- Each function in a program is called in the sequence specified by the function calls in **main( )**.

- After each function has done its thing, control returns to **main(** **)**. When **main( )** runs out of statements and function calls, the program ends.

As we have noted earlier, the program execution always begins with **main( ).** Except for this fact, all C functions enjoy a state of perfect equality. No precedence, no priorities, nobody is nobody’s boss. One function can call another function it has already called but has in the meantime left temporarily in order to call a third function which will sometime later call the function that has called it, if you understand what I mean. No? Well, let me illustrate with an example.

\# include <stdio.h> void italy( ) ; void brazil( ) ; void argentina( ) ; int main( ) { printf ( "I am in main\\n" ) ; italy( ) ; printf ( "I am finally back in main\\n" ) ; return 0 ; } void italy( ) { printf ( "I am in italy\\n" ) ; brazil( ) ; printf ( "I am back in italy\\n" ) ; } void brazil( ) { printf ( "I am in brazil\\n" ) ; argentina( ) ; } void argentina( ) { printf ( "I am in argentina\\n" ) ;

}

And the output would look like...

I am in main I am in italy I am in brazil I am in argentina I am back in italy I am finally back in main

Here, **main( )** calls other functions, which in turn call still other functions. Trace carefully the way control passes from one function to another. Since the compiler always begins the program execution with **main( )**, every function in a program must be called directly or indirectly by **main( )**. In other words, the **main( )** function drives other functions.

Let us now summarize what we have learnt so far.

- A function gets called when the function name is followed by a semicolon ( ; ). For example,

argentina( ) ;

- A function is defined when function name is followed by a pair of braces ( { } ) in which one or more statements may be present. For example,

void argentina( ) { statement 1 ; statement 2 ; statement 3 ; }

- Any function can be called from any other function. Even **main( )** can be called from other functions. For example,

\# include <stdio.h> void message( ) ; int main( ) {

message( ) ; return 0 ; } void message( ) { printf ( "Can't imagine life without C\\n" ) ; main( ) ; }

- A function can be called any number of times. For example,

\# include <stdio.h> void message( ) ; int main( ) { message( ) ; message( ) ; return 0 ; } void message( ) { printf ( "Jewel Thief!!\\n" ) ; }

- The order in which the functions are defined in a program and the order in which they get called need not necessarily be same. For example,

\# include <stdio.h> void message1( ) ; void message2( ) ; int main( ) { message1( ) ; message2( ) ; return 0 ; } void message2( ) { printf ( "But the butter was bitter\\n" ) ; }

void message1( ) { printf ( "Mary bought some butter\\n" ) ; }

Here, even though **message1( )** is getting called before **message2( )**, still, **message1( )** has been defined after **message2( )**. However, it is advisable to define the functions in the same order in which they are called. This makes the program easier to understand.

- A function can call itself. Such a process is called ‘recursion’. We would discuss this aspect of C functions in Chapter 10.

- A function can be called from another function, but a function cannot be defined in another function. Thus, the following program code would be wrong, since **argentina( )** is being defined inside another function, **main( )**:

int main( ) { printf ( "I am in main\\n" ) ; void argentina( ) { printf ( "I am in argentina\\n" ) ; } }

- There are basically two types of functions:

Library functions Ex. **printf( )**, **scanf( )**, etc. User-defined functions Ex. **argentina( )**, **brazil( )**, etc.

As the name suggests, library functions are nothing but commonly required functions grouped together and stored in a Library file on the disk. These library of functions come ready-made with development environments like Turbo C, Visual Studio, NetBeans, gcc, etc. The procedure for calling both types of functions is exactly same.

### Why use Functions?

Why write separate functions at all? Why not squeeze the entire logic into one function, **main( )**? Two reasons:

- Writing functions avoids rewriting the same code over and over. Suppose you have a section of code in your program that calculates area of a triangle. If later in the program you want to calculate the area of a different triangle, you won’t like it if you are required to write the same instructions all over again. Instead, you would prefer to jump to a ‘section of code’ that calculates area and then jump back to the place from where you left off. This section of code is nothing but a function.

- By using functions it becomes easier to write programs and keep track of what they are doing. If the operation of a program can be divided into separate activities, and each activity placed in a different function, then each could be written and checked more or less independently. Separating the code into modular functions also makes the program easier to design and understand.

What is the moral of the story? Don’t try to cram the entire logic in one function. It is a very bad style of programming. Instead, break a program into small units and write functions for each of these isolated subdivisions. Don’t hesitate to write functions that are called only once. What is important is that these functions perform some logically isolated task.

**Passing Values between Functions** The functions that we have used so far haven’t been very flexible. We call them and they do what they are designed to do. Like our mechanic who always services the motorbike in exactly the same way, we haven’t been able to influence the functions in the way they carry out their tasks. It would be nice to have a little more control over what functions do, in the same way it would be nice to be able to tell the mechanic, ‘Also change the engine oil, I am going for an outing’. In short, now we want to communicate between the ‘calling’ and the ‘called’ functions.

The mechanism used to convey information to the function is the ‘argument’. You have unknowingly used the arguments in the **printf( )** and **scanf( )** functions; the format string and the list of variables used inside the parentheses in these functions are arguments. The arguments are sometimes also called ‘parameters’.

Consider the following program. In this program, in **main( )** we receive the values of **a**, **b** and **c** through the keyboard and then output the sum of **a**, **b** and **c**. However, the calculation of sum is done in a different function called **calsum( )**. If sum is to be calculated in **calsum( )** and

values of **a**, **b** and **c** are received in **main( )**, then we must pass on these values to **calsum( )**, and once **calsum( )** calculates the sum, we must return it from **calsum( )** back to **main( )**.

/\* Sending and receiving values between functions \*/ # include <stdio.h> int calsum ( int x, int y, int z ) ; int main( ) { int a, b, c, sum ; printf ( "Enter any three numbers " ) ; scanf ( "%d %d %d", &a, &b, &c ) ; sum = calsum ( a, b, c ) ; printf ( "Sum = %d\\n", sum ) ; return 0 ; } int calsum ( int x, int y, int z ) { int d ; d = x + y + z ; return ( d ) ; }

And here is the output...

Enter any three numbers 10 20 30 Sum = 60

There are a number of things to note about this program:

- In this program, from the function **main( )**, the values of **a**, **b** and **c** are passed on to the function **calsum( )**, by making a call to the function **calsum( )** and mentioning **a**, **b** and **c** in the parentheses:

sum = calsum ( a, b, c ) ;

In the **calsum( )** function these values get collected in three variables **x**, **y** and **z**:

int calsum ( int x, int y, int z )

- The variables **a**, **b** and **c** are called ‘actual arguments’, whereas the variables **x**, **y** and **z** are called ‘formal arguments’. Any number of arguments can be passed to a function being called. However, the type, order and number of the actual and formal arguments must always be same.

Instead of using different variable names **x**, **y** and **z**, we could have used the same variable names **a**, **b** and **c**. But the compiler would still treat them as different variables since they are in different functions.

- Note the function prototype declaration of **calsum( )**. Instead of the usual **void**, we are using **int**. This indicates that **calsum( )** is going to return a value of the type **int**. It is not compulsory to use variable names in the prototype declaration. Hence we could as well have written the prototype as:

int calsum ( int, int, int ) ;

In the definition of **calsum** too, **void** has been replaced by **int**.

- In the earlier programs, the moment closing brace ( **}** ) of the called function was encountered, the control returned to the calling function. No separate **return** statement was necessary to send back the control.

This approach is fine if the called function is not going to return any meaningful value to the calling function. In the above program, however, we want to return the sum of **x**, **y** and **z**. Therefore, it is necessary to use the **return** statement.

The **return** statement serves two purposes:

(1) On executing the **return** statement, it immediately transfers the control back to the calling function.

(2) It returns the value present in the parentheses after **return**, to the calling function. In the above program, the value of sum of three numbers is being returned.

- There is no restriction on the number of **return** statements that may be present in a function. Also, the **return** statement need not always be present at the end of the called function. The following program illustrates these facts:

int fun( )

{ int n ; printf ( "Enter any number " ) ; scanf ( "%d", &n ) ; if ( n >= 10 && n <= 90 ) return ( n ) ; else return ( n + 32 ) ; }

In this function, different **return** statements will be executed depending on whether **n** is between 10 and 90 or not.

- Whenever the control returns from a function, the sum being returned is collected in the calling function by assigning the called function to some variable. For example,

sum = calsum ( a, b, c ) ;

- All the following are valid **return** statements.

return ( a ) ; return ( 23 ) ; return ;

In the last statement, a garbage value is returned to the calling function since we are not returning any specific value. Note that, in this case, the parentheses after **return** are dropped. In the other **return** statements too, the parentheses can be dropped.

- A function can return only one value at a time. Thus, the following statements are invalid:

return ( a, b ) ; return ( x, 12 ) ;

There is a way to get around this limitation, which would be discussed later in this chapter, when we learn pointers.

- If the value of a formal argument is changed in the called function, the corresponding change does not take place in the calling function. For example,

\# include <stdio.h> void fun ( int ) ; int main( ) { int a = 30 ; fun ( a ) ; printf ( "%d\\n", a ) ; return 0 ; } void fun ( int b ) { b = 60 ; printf ( "%d\\n", b ) ; }

The output of the above program would be:

60 30

Thus, even though the value of **b** is changed in **fun( ),** the value of **a** in **main( )** remains unchanged. This means that when values are passed to a called function, the values present in actual arguments are not physically moved to the formal arguments; just a photocopy of values in actual argument is made into formal arguments.

**Scope Rule of Functions** Look at the following program:

\# include <stdio.h> void display ( int ) ; int main( ) { int i = 20 ; display ( i ) ; return 0 ; } void display ( int j ) { int k = 35 ;

printf ( "%d\\n", j ) ; printf ( "%d\\n", k ) ; }

In this program, is it necessary to pass the value of the variable **i** to the function **display( )**? Will it not become automatically available to the function **display( )**? No. Because, by default, the scope of a variable is local to the function in which it is defined. The presence of **i** is known only to the function **main( )** and not to any other function. Similarly, the variable **k** is local to the function **display( )** and hence it is not available to **main( )**. That is why to make the value of **i** available to **display( )**, we have to explicitly pass it to **display( )**. Likewise, if we want **k** to be available to **main( )**, we will have to return it to **main( )** using the **return** statement. In general, we can say that the scope of a variable is local to the function in which it is defined.

**Order of Passing Arguments** Consider the following function call:

fun (a, b, c, d ) ;

In this call, it doesn’t matter whether the arguments are passed from left to right or from right to left. However, in some function calls, the order of passing arguments becomes an important consideration. For example:

int a = 1 ; printf ( "%d %d %d\\n", a, ++a, a++ ) ;

It appears that this **printf( )** would output 1 2 2.

This however is not the case. Surprisingly, it outputs 3 3 1. This is because, in C during a function call the arguments are passed from right to left. That is, firstly 1 is passed through the expression **a++** and then **a** is incremented to 2. Then result of **++a** is passed. That is, **a** is incremented to 3 and then passed. Finally, latest value of **a**, i.e., 3, is passed. Thus in right to left order, 1, 3, 3 get passed. Once **printf( )** collects them, it prints them in the order in which we have asked it to get them printed (and not the order in which they were passed). Thus 3 3 1 gets printed.

**Using Library Functions** Consider the following program:

\# include <stdio.h> # include <math.h> int main( ) { float a = 0.5 ; float w, x, y, z ; w = sin ( a ) ; x = cos ( a ) ; y = tan ( a ) ; z = pow ( a, 2 ) ; printf ( "%f %f %f %f\\n", w, x, y, z ) ; return 0 ; }

Here we have called four standard library functions—**sin( )**, **cos( )**, **tan( )** and **pow( )**. As we know, before calling any function, we must declare its prototype. This helps the compiler in checking whether the values being passed and returned are as per the prototype declaration. But since we didn’t define the library functions (we merely called them), we do not know the prototype declarations of library functions. Hence, when the library of functions is provided, a set of ‘.h’ files is also provided. These files contain the prototype declarations of library functions. But why multiple files? Because the library functions are divided into different groups and one file is provided for each group. For example, prototypes of all input/output functions are provided in the file ‘stdio.h’, prototypes of all mathematical functions are provided in the file ‘math.h’, etc.

Prototypes of functions **sin( )**, **cos( )**, **tan( )** and **pow( )** are declared in the file ‘math.h’. To make these prototypes available to our program we need to **#include** the file ‘math.h’. You can even open this file and look at the prototypes. They would appear as shown below.

double sin ( double ) ; double cos ( double ) ; double tan ( double ) ; double pow ( double, double ) ;

Here **double** indicates a real number. We would learn more about **double** in Chapter 11.

Whenever we wish to call any library function we must include the header file which contains its prototype declaration.

**One Dicey Issue** Now consider the following program:

\# include <stdio.h> int main( ) { int i = 10, j = 20 ; printf ( "%d %d %d\\n", i, j ) ; printf ( "%d\\n", i, j ) ; return 0 ; }

This program gets successfully compiled, even though there is a mismatch in the format specifiers and the variables in the list used in **printf( )**. This is because, **printf( )** accepts _variable_ number of arguments (sometimes 2 arguments, sometimes 3 arguments, etc.), and even with the mismatch above, the call still matches with the prototype of **printf( )** present in ‘stdio.h’. At run-time, when the first **printf( )** is executed, since there is no variable matching with the last specifier **%d**, a garbage integer gets printed. Similarly, in the second **printf( )**, since the format specifier for **j** has not been mentioned, its value does not get printed.

**Return Type of Function** Suppose we want to find out square of a floating point number using a function. This is how this simple program would look like:

\# include <stdio.h> float square ( float ) ; int main( ) { float a, b ; printf ( "Enter any number " ) ; scanf ( "%f", &a ) ; b = square ( a ) ; printf ( "Square of %f is %f\\n", a, b ) ; return 0 ;

} float square ( float x ) { float y ; y = x \* x ; return ( y ) ; }

And here are three sample runs of this program...

Enter any number 3 Square of 3 is 9.000000 Enter any number 1.5 Square of 1.5 is 2.250000 Enter any number 2.5 Square of 2.5 is 6.250000

Since we are returning a **float** value from this function we have indicated the return type of the **square( )** function as **float** in the prototype declaration as well as in the function definition. Had we dropped **float** from the prototype and the definition, the compiler would have assumed that **square( )** is supposed to return an integer value.

### Summary

- To avoid repetition of code and bulky programs functionally related statements are isolated into a function.

- Function declaration specifies the return type of the function and the types of parameters it accepts.

- Function definition defines the body of the function.

- Variables declared in a function are not available to other functions in a program. So, there won’t be any clash even if we give same name to the variables declared in different functions.

- In C order of passing arguments to a function is from right to left.

### Exercise

**\[A\]** What will be the output of the following programs:

- # include <stdio.h> void display( ) ;

int main( ) { printf ( "Learn C\\n" ) ; display( ) ; return 0 ; } void display( ) { printf ( "Followed by C++, C# and Java!\\n" ) ; main( ) ; }

- # include <stdio.h> int check ( int ) ; int main( ) { int i = 45, c ; c = check ( i ) ; printf ( "%d\\n", c ) ; return 0 ; } int check ( int ch ) { if ( ch >= 45 ) return ( 100 ) ; else return ( 10 \* 10 ) ; }

- # include <stdio.h> float circle ( int ) ; int main( ) { float area ; int radius = 1 ; area = circle ( radius ) ; printf ( "%f\\n", area ) ; return 0 ; } float circle ( int r ) { float a ;

a = 3.14 \* r \* r ; return ( a ) ; }

- #include <stdio.h> int main( ) { void slogan( ) ; int c = 5 ; c = slogan( ) ; printf ( "%d\\n", c ) ; return 0 ; } void slogan( ) { printf ( "Only He men use C!\\n" ) ; }

**\[B\]** Point out the errors, if any, in the following programs:

- # include <stdio.h> int addmult ( int, int ) int main( ) { int i = 3, j = 4, k, l ; k = addmult ( i, j ) ; l = addmult ( i, j ) ; printf ( "%d %d\\n", k, l ) ; return 0 ; } int addmult ( int ii, int jj ) { int kk, ll ; kk = ii + jj ; ll = ii \* jj ; return ( kk, ll ) ; }

- # include <stdio.h> void message( ) ; int main( ) { int a ;

a = message( ) ; return 0 ; } void message( ) { printf ( "Viruses are written in C\\n" ) ; return ; }

- # include <stdio.h> int main( ) { float a = 15.5 ; char ch = 'C' ; printit ( a, ch ) ; return 0 ; } printit ( a, ch ) { printf ( "%f %c\\n", a, ch ) ; }

- # include <stdio.h> void message( ) ; int main( ) { message( ) ; message( ) ; return 0 ; } void message( ) ; { printf ( "Praise worthy and C worthy are synonyms\\n" ) ; }

- # include <stdio.h> int main( ) { let\_us\_c( ) { printf ( "C is a Cimple minded language !\\n" ) ; printf ( "Others are of course no match !\\n" ) ;

} return 0 ; }

- # include <stdio.h> void message( ) ; int main( ) { message ( message( ) ) ; return 0 ; } void message( ) { printf ( "It’s a small world after all…\\n" ) ; }

**\[C\]** Answer the following:

- Is this a correctly written function:

int sqr ( int a ) ; { return ( a \* a ) ; }

- State whether the following statements are True or False:

1\. The variables commonly used in C functions are available to all the functions in a program.

2\. To return the control back to the calling function we must use the keyword **return**.

3\. The same variable names can be used in different functions without any conflict.

4\. Every called function must contain a **return** statement.

5\. A function may contain more than one **return** statements.

6\. Each **return** statement in a function may return a different value.

7\. A function can still be useful even if you don’t pass any arguments to it and the function doesn’t return any value back.

8\. Same names can be used for different functions without any conflict.

9\. A function may be called more than once from any other function.

10\. It is necessary for a function to return some value.

**\[D\]** Answer the following:

- Write a function to calculate the factorial value of any integer entered through the keyboard.

- Write a function **power ( a, b )**, to calculate the value of **a** raised to **b**.

- Write a general-purpose function to convert any given year into its Roman equivalent. Use these Roman equivalents for decimal numbers: 1 – I, 5 – V, 10 – X, 50 – L, 100 – C, 500 – D, 1000 – M.

Example:

Roman equivalent of 1988 is mdcccclxxxviii. Roman equivalent of 1525 is mdxxv.

- Any year is entered through the keyboard. Write a function to determine whether the year is a leap year or not.

- A positive integer is entered through the keyboard. Write a function to obtain the prime factors of this number.

For example, prime factors of 24 are 2, 2, 2 and 3, whereas prime factors of 35 are 5 and 7.