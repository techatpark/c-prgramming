---
title: 'Recursion'
weight: 10
---

   

here is one important feature associated with functions in C. It is known as recursion. Though a bit difficult to understand, it is often

the most direct way of programming a complicated logic. This chapter explores recursion in detail.

**Recursion** In C, it is possible for the functions to call themselves. A function is called ‘recursive’ if a statement within the body of a function calls the same function. Sometimes called ‘circular definition’, recursion is thus the process of defining something in terms of itself.

Let us now see a simple example of recursion. Suppose we want to calculate the factorial value of an integer. As we know, the factorial of a number is the product of all the integers between 1 and that number. For example, 4 factorial is 4 \* 3 \* 2 \* 1. This can also be expressed as 4! = 4 \* 3! where ‘!’ stands for factorial. Thus factorial of a number can be expressed in the form of itself. Hence this can be programmed using recursion. However, before we try to write a recursive function for calculating factorial let us take a look at the non-recursive function for calculating the factorial value of an integer.

\# include <stdio.h> int factorial ( int ) ; int main( ) { int a, fact ; printf ( "Enter any number " ) ; scanf ( "%d", &a ) ; fact = factorial ( a ) ; printf ( "Factorial value = %d\\n", fact ) ; return 0 ; } int factorial ( int x ) { int f = 1, i ; for ( i = x ; i >= 1 ; i-- ) f = f \* i ;

### T

return ( f ) ; }

And here is the output...

Enter any number 3 Factorial value = 6

Work through the above program carefully, till you understand the logic of the program properly. Recursive factorial function can be understood only if you are thorough with the above logic.

Following is the recursive version of the function to calculate the factorial value:

\# include <stdio.h> int rec ( int ) ; int main( ) { int a, fact ; printf ( "Enter any number " ) ; scanf ( "%d", &a ) ; fact = rec ( a ) ; printf ( "Factorial value = %d\\n", fact ) ; return 0 ; } int rec ( int x ) { int f ; if ( x == 1 ) return ( 1 ) ; else f = x \* rec ( x - 1 ) ; return ( f ) ; }

And here is the output for four runs of the program…

Enter any number 1 Factorial value = 1 Enter any number 2 Factorial value = 2 Enter any number 3 Factorial value = 6 Enter any number 5 Factorial value = 120

Let us understand this recursive factorial function thoroughly. In the first run when the number entered through **scanf( )** is 1, let us see what action does **rec( )** take. The value of **a** (i.e., 1) is copied into **x**. Since **x** turns out to be 1, the condition **if ( x == 1 )** is satisfied and hence 1 (which indeed is the value of 1 factorial) is returned through the **return** statement.

When the number entered through **scanf( )** is 2, the **( x == 1 )** test fails, so we reach the statement,

f = x \* rec ( x - 1 ) ;

And here is where we meet recursion. How do we handle the expression **x \* rec ( x - 1 )**? We multiply **x** by **rec ( x - 1 )**. Since the current value of **x** is 2, it is same as saying that we must calculate the value (2 \* rec ( 1 )). We know that the value returned by **rec ( 1 )** is 1, so the expression reduces to (2 \* 1), or simply 2. Thus the statement,

x \* rec ( x - 1 ) ;

evaluates to 2, which is stored in the variable **f**, and is returned to **main( )**, where it is duly printed as

Factorial value = 2

Now perhaps you can see what would happen if the value of **a** is 3, 4, 5 and so on.

In case the value of **a** is 5, **main( )** would call **rec( )** with 5 as its actual argument, and **rec( )** will send back the computed value. But before sending the computed value, **rec( )** calls **rec( )** and waits for a value to be returned. It is possible for the **rec( )** that has just been called to call yet another **rec( )**, the argument **x** being decreased in value by 1 for each of these recursive calls. We speak of this series of calls to **rec( )** as being

different invocations of **rec( )**. These successive invocations of the same function are possible because the C compiler keeps track of which invocation calls which. These recursive invocations end finally when the last invocation gets an argument value of 1, which the preceding invocation of **rec( )** now uses to calculate its own **f** value and so on up the ladder. So we might say what happens is,

rec ( 5 ) returns ( 5 times rec ( 4 ), which returns ( 4 times rec ( 3 ), which returns ( 3 times rec ( 2 ), which returns ( 2 times rec ( 1 ), which returns ( 1 ) ) ) ) )

Foxed? Well, that is recursion for you in its simplest garbs. I hope you agree that it’s difficult to visualize how the control flows from one function call to another. Possibly Figure 10.1 would make things a bit clearer.

Assume that the number entered through **scanf( )** is 3. Using Figure 10.1 let’s visualize what exactly happens when the recursive function **rec( )** gets called. Go through the figure carefully. The first time when **rec( )** is called from **main( )**, **x** collects 3. From here, since **x** is not equal to 1, the **if** block is skipped and **rec( )** is called again with the argument **( x – 1 )**, i.e. 2. This is a recursive call. Since **x** is still not equal to 1, **rec( )** is called yet another time, with argument (2 - 1). This time as **x** is 1, control goes back to previous **rec( )** with the value 1, and **f** is evaluated as 2.

Similarly, each **rec( )** evaluates its **f** from the returned value, and finally 6 is returned to **main( )**. The sequence would be grasped better by following the arrows shown in Figure 10.1. Let it be clear that while executing the program, there do not exist so many copies of the function **rec( )**. These have been shown in the figure just to help you keep track of how the control flows during successive recursive calls.

from main( )

rec ( int x ) {

int f ;

if ( x == 1 ) return ( 1 ) ;

else f = x \* rec ( x - 1 ) ;

return ( f ) ; }

to main( )

rec ( int x ) {

int f ;

if ( x == 1 ) return ( 1 ) ;

else f = x \* rec ( x - 1 ) ;

return ( f ) ; }

rec ( int x ) {

int f ;

if ( x == 1 ) return ( 1 ) ;

else f = x \* rec ( x - 1 ) ;

return ( f ) ; }

Figure 10.1

Recursion may seem strange and complicated at first glance, but it is often the most direct way to code an algorithm, and once you are familiar with recursion, the clearest way of doing so.

**Recursion and Stack** There are different ways in which data can be organized. For example, if you are to store five numbers then we can store them in five different variables, an array, a linked list, a binary tree, etc. All these different ways of organizing the data are known as data structures. The compiler uses one such data structure called stack for implementing normal as well as recursive function calls.

A stack is a Last In First Out (LIFO) data structure. This means that the last item to get stored on the stack (often called Push operation) is the first one to get out of it (often called as Pop operation). You can compare this to the stack of plates in a cafeteria—the last plate that goes on the stack is the first one to get out of it. Now let us see how the stack works in case of the following program:

\# include <stdio.h> int add ( int, int ) ; int main( ) { int a = 5, b = 2, c ; c = add ( a, b ) ; printf ( "sum = %d\\n", c ) ; return 0 ;

} int add ( int i, int j ) { int sum ; sum = i + j ; return sum ; }

In this program, before transferring the execution control to the function **add( )**, the values of parameters **a** and **b** are pushed on the stack. Following this, the address of the statement **printf( )** is pushed on the stack and the control is transferred to **add( )**. It is necessary to push this address on the stack. In **add( )**, the values of **a** and **b** that were pushed on the stack are referred as **i** and **j**. Once inside **add( )**, the local variable **sum** gets pushed on the stack. When value of **sum** is returned, **sum** is popped off from the stack. Next, the address of the statement where the control should be returned, is popped off from the stack. Using this address, the control returns to the **printf( )** statement in **main( )**. Before execution of **printf( )** begins, the two integers that were earlier pushed on the stack are now popped off.

How the values are being pushed and popped even though we didn’t write any code to do so? Simple—the compiler, on encountering the function call, would generate code to push the parameters and the address. Similarly, it would generate code to clear the stack when the control returns back from **add( )**. Figure 10.2 shows the contents of the stack at different stages of execution.

Empty stack When call to **add( )** is met

Before transferring control to **add( )**

Copy of a

Copy of b

5

2

5

2

xxxx

Copy of a

Copy of b

Address of **printf( )**

After control reaches **add( )**

5

2

xxxx

7

j

i

sum

Address

While returning control from **add( )**

5

2

xxxx

On returning control from **add( )**

Figure 10.2

Note that in this program, popping of **sum** and address is done by **add( )**, whereas, popping of the two integers is done by **main( )**. When it is done this way, it is known as ‘cdecl Calling Convention’. There are other calling conventions as well, where instead of **main( )**, **add( )** itself clears the two integers. The calling convention also decides whether the parameters being passed to the function are pushed on the stack in left- to-right or right-to-left order. The standard calling convention always uses the right-to-left order. Thus, during the call to **add( )** firstly value of **b** is pushed to the stack, followed by the value of **a**.

The recursive calls are no different. Whenever we make a recursive call the parameters and the return address gets pushed on the stack. The stack gets unwound when the control returns from the called function. Thus during every recursive function call we are working with a fresh set of parameters.

Also, note that while writing recursive functions, you must have an **if** statement somewhere in the recursive function to force the function to return without recursive call being executed. If you don’t do this and you call the function, you will fall in an indefinite loop, and the stack will keep on getting filled with parameters and the return address each time there is a call. Soon the stack would become full and you would get a

run-time error indicating that the stack has become full. This is a very common error while writing recursive functions. My advice is to use **printf( )** statement liberally during the development of recursive function, so that you can watch what is going on and can abort execution if you see that you have made a mistake.

### Summary

- When a function calls itself from within its body it is known as a recursive function.

- A fresh set of variables are created every time a function gets called (normally or recursively).

- Understanding how a recursive function is working becomes easy if you make several copies of the same function on paper and then perform a dry run of the program.

- Adding too many functions and calling them frequently may slow down the program execution.

### Exercise

**\[A\]** What will be the output of the following programs:

- # include <stdio.h> int main( ) { printf ( "C to it that C survives\\n" ) ; main( ) ; return 0 ; }

- # include <stdio.h> int main( ) { int i = 0 ; i++ ; if ( i <= 5 ) { printf ( "C adds wings to your thoughts\\n" ) ; exit ( 0 ) ; main( ) ; } return 0 ;

}

**\[B\]** Attempt the following:

- A 5-digit positive integer is entered through the keyboard, write a recursive and a non-recursive function to calculate sum of digits of the 5-digit number.

- A positive integer is entered through the keyboard, write a program to obtain the prime factors of the number. Modify the function suitably to obtain the prime factors recursively.

- Write a recursive function to obtain the first 25 numbers of a Fibonacci sequence. In a Fibonacci sequence the sum of two successive terms gives the third term. Following are the first few terms of the Fibonacci sequence:

1 1 2 3 5 8 13 21 34 55 89...

- A positive integer is entered through the keyboard, write a function to find the binary equivalent of this number :

(1) Without using recursion (2) Using recursion

- Write a recursive function to obtain the running sum of first 25 natural numbers.