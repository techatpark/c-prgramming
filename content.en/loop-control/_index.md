---
title: 'Loop Control'
weight: 5
---

   

he programs that we have developed so far used either a sequential or a decision control instruction. In the first one, the calculations

were carried out in a fixed order; while in the second, an appropriate set of instructions were executed depending upon the outcome of the condition(s) being tested.

These programs were of limited nature, because when executed, they always performed the same series of actions, in the same way, exactly once. Almost always, if something is worth doing, it’s worth doing more than once. You can probably think of several examples of this from real life, such as eating a good dinner or going for a movie. Programming is the same; we frequently need to perform an action over and over, often with variations in the details each time. The mechanism, which meets this need, is the ‘Loop Control Instruction’, and loops are the subject of this chapter.

**Loops** The versatility of the computer lies in its ability to perform a set of instructions repeatedly. This involves repeating some portion of the program either a specified number of times or until a particular condition is being satisfied. This repetitive operation is done through a loop control instruction.

There are three methods by way of which we can repeat a part of a program. They are:

- Using a **for** statement (b) Using a **while** statement (c) Using a **do-while** statement

Each of these methods is discussed in the following pages.

**The _while_ Loop** It is often the case in programming that you want to repeat something a fixed number of times. Perhaps you want to calculate gross salaries of ten different persons, or you want to convert temperatures from Centigrade to Fahrenheit for 15 different cities. The **while** loop is ideally suited for this.

Let us look at a simple example that uses a **while** loop to calculate simple interest for 3 sets of values of principal, number of years and rate of interest. The flowchart shown in Figure 5.1 would help you to understand the operation of the **while** loop.

### T

START

INPUT p, n, r

STOP

is count <= 3

Yes

No

si = p \* n \* r / 100

PRINT si

count = 1

count = count + 1

Figure 5.1

Let us now write a program that implements the logic of this flowchart.

/\* Calculation of simple interest for 3 sets of p, n and r \*/ # include <stdio.h> int main( ) { int p, n, count ; float r, si ; count = 1 ; while ( count <= 3 ) { printf ( "\\nEnter values of p, n and r " ) ; scanf ( "%d %d %f", &p, &n, &r ) ; si = p \* n \* r / 100 ; printf ( "Simple interest = Rs. %\\nf", si ) ; count = count + 1 ;

} return 0 ; }

And here are a few sample runs of the program...

Enter values of p, n and r 1000 5 13.5 Simple interest = Rs. 675.000000 Enter values of p, n and r 2000 5 13.5 Simple interest = Rs. 1350.000000 Enter values of p, n and r 3500 5 3.5 Simple interest = Rs. 612.500000

The program executes all statements after the **while** 3 times. The logic for calculating the simple interest is written in these statements and they are enclosed within a pair of braces. These statements form the ‘body’ of the **while** loop. The parentheses after the **while** contain a condition. So long as this condition remains true the statements in the body of the **while** loop keep getting executed repeatedly. To begin with, the variable **count** is initialized to 1 and every time the simple interest logic is executed, the value of **count** is incremented by one. The variable **count** is often called either a ‘loop counter’ or an ‘index variable’.

The operation of the **while** loop is illustrated in Figure 5.2.

START

STOP

test

Tru e

False

body of loop

initialise

increment

Figure 5.2

### Tips and Traps

The general form of **while** is as shown below.

initialize loop counter ; while ( test loop counter using a condition ) { do this ; and this ; increment loop counter ; }

Note the following points about **while...**

- The statements within the **while** loop would keep getting executed till the condition being tested remains true. When the condition becomes false, the control passes to the first statement that follows the body of the **while** loop.

- In place of the condition there can be any other valid expression. So long as the expression evaluates to a non-zero value the statements within the loop would get executed.

- The condition being tested may use relational or logical operators as shown in the following examples:

while ( i <= 10 ) while ( i >= 10 && j <= 15 ) while ( j > 10 && ( b < 15 || c < 20 ) )

- The statements within the loop may be a single line or a block of statements. In the first case, the braces are optional. For example,

while ( i <= 10 ) i = i + 1 ;

is same as

while ( i <= 10 ) { i = i + 1 ; }

- Almost always, the while must test a condition that will eventually become false, otherwise the loop would be executed forever, indefinitely.

\# include <stdio.h> int main( ) { int i = 1 ; while ( i <= 10 ) printf ( "%d\\n", i ) ; return 0 ; }

This is an indefinite loop, since **i** remains equal to 1 forever. The correct form would be as under:

\# include <stdio.h> int main( ) { int i = 1 ; while ( i <= 10 ) { printf ( "%d\\n", i ) ; i = i + 1 ; } return 0 ; }

- Instead of incrementing a loop counter, we can decrement it and still manage to get the body of the loop executed repeatedly. This is shown below.

\# include <stdio.h> int main( ) { int i = 5 ; while ( i >= 1 ) { printf ( "Make the computer literate!\\n" ) ; i = i - 1 ; } }

- It is not necessary that a loop counter must only be an **int**. It can even be a **float**.

\# include <stdio.h> int main( ) { float a = 10.0 ; while ( a <= 10.5 ) { printf ( "Raindrops on roses..." ) ; printf ( "...and whiskers on kittens\\n" ) ; a = a + 0.1 ; } return 0 ; }

- Even floating point loop counters can be decremented. Once again, the increment and decrement could be by any value, not necessarily 1.

- What will be the output of the following program:

\# include <stdio.h> int main( ) { int i = 1 ; while ( i <= 10 ) ; { printf ( "%d\\n", i ) ; i = i + 1 ; } return 0 ; }

This is an indefinite loop, and it doesn’t give any output at all. The reason is, we have carelessly given a **;** after the **while**. It would make the loop work like this...

while ( i <= 10 ) ; { printf ( "%d\\n", i ) ;

i = i + 1 ; }

Since the value of **i** is not getting incremented, the control would keep rotating within the loop, eternally. Note that enclosing **printf( )** and **i = i +1** within a pair of braces is not an error. In fact we can put a pair of braces around any individual statement or set of statements without affecting the execution of the program.

### More Operators

There are several operators that are frequently used with **while**. To illustrate their usage, let us consider a problem wherein numbers from 1 to 10 are to be printed on the screen. The program for performing this task can be written using **while** in following different ways:

- # include <stdio.h> int main( ) { int i = 1 ; while ( i <= 10 ) { printf ( "%d\\n", i ) ; i = i + 1 ; } return 0 ; }

This is the most straight-forward way of printing numbers from 1 to 10.

- # include <stdio.h> int main( ) { int i = 1 ; while ( i <= 10 ) { printf ( "%d\\n", i ) ; i++ ; } return 0 ; }

Note that the increment operator **++** increments the value of **i** by 1, every time the statement **i++** gets executed. Similarly, to reduce the value of a variable by 1, a decrement operator **\--** is also available.

However, never use **n+++** to increment the value of **n** by 2, since there doesn’t exist an operator **+++** in C.

- # include <stdio.h> int main( ) { int i = 1 ; while ( i <= 10 ) { printf ( "%d\\n", i ) ; i += 1 ; } return 0 ; }

Note that **+=** is a compound assignment operator. It increments the value of **i** by 1. Similarly, **j = j + 10** can also be written as **j += 10**. Other compound assignment operators are **\-=, \*=, / =** and **%=**.

- # include <stdio.h> int main( ) { int i = 0 ; while ( i++ < 10 ) printf ( "%d\\n", i ) ; return 0 ; }

In the statement **while ( i++ < 10 )**, first the comparison of value of **i** with 10 is performed, and then the incrementation of **i** takes place. Since the incrementation of **i** happens after the comparison, here the **++** operator is called a post-incrementation operator. When the control reaches **printf( )**, **i** has already been incremented, hence **i** must be initialized to 0, not 1.

- # include <stdio.h> int main( ) {

int i = 0 ; while ( ++i <= 10 ) printf ( "%d\\n", i ) ; return 0 ; }

In the statement **while ( ++i <= 10 )**, first incrementation of **i** takes place, then the comparison of value of **i** with 10 is performed. Since the incrementation of **i** happens before the comparison, here the **++** operator is called a pre-incrementation operator.

### Summary

- The three type of loops available in C are **for**, **while**, and **do-while**.

- In a **while** loop there are three distinct steps of initialization, testing and incrementation of loop counter.

- The loop counter can be incremented or decremented by any suitable step value.

- There are two forms of ++ operator—pre-increment and post- increment.

- There are two forms of **\--** operator—pre-decrement and post- decrement.

### Exercise

**\[A\]** What will be the output of the following programs:

- # include <stdio.h> int main( ) { int i = 1 ; while ( i <= 10 ) ; { printf ( "%d\\n", i ) ; i++ ; } return 0 ; }

- # include <stdio.h> int main( )

{ int x = 4, y, z ; y = --x ; z = x-- ; printf ( "%d %d %d\\n", x, y, z ) ; return 0 ; }

- # include <stdio.h> int main( ) { int x = 4, y = 3, z ; z = x-- - y ; printf ( "%d %d %d\\n", x, y, z ) ; return 0 ; }

- # include <stdio.h> int main( ) { while ( 'a' < 'b' ) printf ( "malayalam is a palindrome\\n" ) ; return 0 ; }

- # include <stdio.h> int main( ) { int i ; while ( i = 10 ) { printf ( "%d\\n", i ) ; i = i + 1 ; } return 0 ; }

- # include <stdio.h> int main( ) { float x = 1.1 ; while ( x == 1.1 ) {

printf ( "%f\\n", x ) ; x = x – 0.1 ; } return 0 ; }

**\[B\]** Attempt the following:

- Write a program to calculate overtime pay of 10 employees. Overtime is paid at the rate of Rs. 12.00 per hour for every hour worked above 40 hours. Assume that employees do not work for fractional part of an hour.

- Write a program to find the factorial value of any number entered through the keyboard.

- Two numbers are entered through the keyboard. Write a program to find the value of one number raised to the power of another.

- Write a program to print all the ASCII values and their equivalent characters using a while loop. The ASCII values vary from 0 to 255.

- Write a program to print out all Armstrong numbers between 1 and 500. If sum of cubes of each digit of the number is equal to the number itself, then the number is called an Armstrong number. For example, 153 = ( 1 \* 1 \* 1 ) + ( 5 \* 5 \* 5 ) + ( 3 \* 3 \* 3 ).

- Write a program for a matchstick game being played between the computer and a user. Your program should ensure that the computer always wins. Rules for the game are as follows:

- There are 21 matchsticks.

- The computer asks the player to pick 1, 2, 3, or 4 matchsticks.

- After the person picks, the computer does its picking.

- Whoever is forced to pick up the last matchstick loses the game.

- Write a program to enter numbers till the user wants. At the end it should display the count of positive, negative and zeros entered.

- Write a program to receive an integer and find its octal equivalent.

- (Hint: To obtain octal equivalent of an integer, divide it continuously by 8 till dividend doesn’t become zero, then write the remainders obtained in reverse direction.)

- Write a program to find the range of a set of numbers entered through the keyboard. Range is the difference between the smallest and biggest number in the list.

