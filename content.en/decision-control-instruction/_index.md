---
title: 'Decision Control Instruction'
weight: 3
---

   

We all need to alter our actions in the face of changing circumstances. If the weather is fine, then I will go for a stroll. If

the highway is busy, I would take a diversion. If the pitch takes spin, we would win the match. If you join our WhatsApp group, I would send you interesting videos. If you like this book, I would write the next edition. You can notice that all these decisions depend on some condition being met.

C language too must be able to perform different sets of actions depending on the circumstances. C has three major decision making instructions—the **if** statement, the **if-else** statement, and the **switch** statement. A fourth, somewhat less important structure is the one that uses conditional operators. In this chapter, we will explore **if** and the **if- else** statement. Conditional operators would be dealt with in Chapter 4 and **switch** statement in Chapter 7.

**Decisions! Decisions!** In the programs written in Chapters 1 and 2, we have used sequence control instruction in which the various statements are executed sequentially, i.e., in the same order in which they appear in the program. In fact, to execute the instructions sequentially, we don’t have to do anything at all. That is, by default, the instructions in a program are executed sequentially. However, in serious programming situations, seldom do we want the instructions to be executed sequentially. Many a time, we want a set of instructions to be executed in one situation, and an entirely different set of instructions to be executed in another situation. This kind of situation is dealt with in C programs using a decision control instruction. As mentioned earlier, a decision control instruction can be implemented in C using:

- The **if** statement (b) The **if-else** statement (c) The conditional operators

Now let us learn each of these and their variations in turn.

**The _if_ Statement** C uses the keyword **if** to implement the decision control instruction. The general form of **if** statement looks like this:

if ( this condition is true ) execute this statement ;

### W

The keyword **if** tells the compiler that what follows is a decision control instruction. The condition following the keyword **if** is always enclosed within a pair of parentheses. If the condition, whatever it is, is true, then the statement is executed. If the condition is not true, then the statement is not executed; instead the program skips past it. But how do we express the condition itself in C? And how do we evaluate its truth or falsity? As a general rule, we express a condition using C’s ‘relational’ operators. The relational operators allow us to compare two values to see whether they are equal to each other, unequal, or whether one is greater than the other. Figure 3.1 shows how they look and how they are evaluated in C.

### this expression

x == y x != y x < y x > y x <= y x >= y

### is true if

x is equal to y x is not equal to y x is less than y x is greater than y x is less than or equal to y x is greater than or equal to y

Figure 3.1

The relational operators should be familiar to you except for the equality operator **\==** and the inequality operator **!=**. Note that **\=** is used for assignment, whereas, **\==** is used for comparison of two quantities. Here is a simple program that demonstrates the use of **if** and the relational operators.

/\* Demonstration of if statement \*/ # include <stdio.h> int main( ) { int num ; printf ( "Enter a number less than 10 " ) ; scanf ( "%d", &num ) ; if ( num < 10 ) printf ( "What an obedient servant you are !\\n" ) ;

return 0 ; }

On execution of this program, if you type a number less than 10, you get a message on the screen through **printf( )**. If you type some other number the program doesn’t do anything. The flowchart given in Figure 3.2 would help you understand the flow of control in the program.

START

PRINT Enter a num less than 10

INPUT num

PRINT What an obedient servant you are !

STOP

is num < 10

YesNo

Figure 3.2

To make you comfortable with the decision control instruction, one more example has been given below. Study it carefully before reading further. To help you understand it easily, the program is accompanied by an appropriate flowchart shown in Figure 3.3.

**Example 3.1:** While purchasing certain items, a discount of 10% is offered if the quantity purchased is more than 1000. If quantity and price per item are input through the keyboard, write a program to calculate the total expenses.

START

INPUT qty, rate

STOP

is qty > 1000

YesNo

dis = 0

dis = 10

PRINT tot

tot = qty \* rate – qty \* rate \* dis / 100

Figure 3.3

/\* Calculation of total expenses \*/ # include <stdio.h> int main( ) { int qty, dis = 0 ; float rate, tot ; printf ( "Enter quantity and rate " ) ; scanf ( "%d %f", &qty, &rate) ; if ( qty > 1000 ) dis = 10 ; tot = ( qty \* rate ) - ( qty \* rate \* dis / 100 ) ; printf ( "Total expenses = Rs. %f\\n", tot ) ;

return 0 ; }

Here is some sample interaction with the program.

Enter quantity and rate 1200 15.50 Total expenses = Rs. 16740.000000

Enter quantity and rate 200 15.50 Total expenses = Rs. 3100.000000

In the first run of the program, the condition evaluates to true, as 1200 (value of **qty**) is greater than 1000. Therefore, the variable **dis**, which was earlier set to 0, now gets a new value 10. Using this new value, total expenses are calculated and printed.

In the second run, the condition evaluates to false, as 200 (the value of **qty**) isn’t greater than 1000. Thus, **dis**, which is earlier set to 0, remains 0, and hence the expression after the minus sign evaluates to zero, thereby offering no discount.

Is the statement **dis = 0** necessary? The answer is yes, since in C, a variable, if not specifically initialized, contains some unpredictable value (garbage value).

### The Real Thing

We mentioned earlier that the general form of the **if** statement is as follows:

if ( condition ) statement ;

Here the expression can be any valid expression including a relational expression. We can even use arithmetic expressions in the **if** statement. For example all the following **if** statements are valid.

if ( 3 + 2 % 5 ) printf ( "This works" ) ; if ( a = 10 ) printf ( "Even this works" ) ; if ( -5 )

printf ( "Surprisingly even this works" ) ;

Note that in C a non-zero value is considered to be true, whereas a 0 is considered to be false. In the first **if**, the expression evaluates to **5** and since **5** is non-zero it is considered to be true. Hence the **printf( )** gets executed.

In the second **if**, 10 gets assigned to **a** so the **if** is now reduced to **if ( a )** or **if ( 10 )**. Since 10 is non-zero, it is true hence again **printf( )** goes to work.

In the third **if**, -5 is a non-zero number, hence true. So again **printf( )** goes to work. In place of -5 even if a float like 3.14 were used it would be considered to be true. So the issue is not whether the number is integer or float, or whether it is positive or negative. Issue is whether it is zero or non-zero.

### Multiple Statements within _if_

It may so happen that in a program we want more than one statement to be executed if the expression following **if** is satisfied. If such multiple statements are to be executed, then they must be placed within a pair of braces, as illustrated in the following example:

**Example 3.2:** The current year and the year in which the employee joined the organization are entered through the keyboard. If the number of years for which the employee has served the organization is greater than 3, then a bonus of Rs. 2500/- is given to the employee. If the years of service are not greater than 3, then the program should do nothing.

/\* Calculation of bonus \*/ # include <stdio.h> int main( ) { int bonus, cy, yoj, yos ; printf ( "Enter current year and year of joining " ) ; scanf ( "%d %d", &cy, &yoj ) ; yos = cy - yoj ; if ( yos > 3 ) {

bonus = 2500 ; printf ( "Bonus = Rs. %d\\n", bonus ) ; } return 0 ; }

Observe that here the two statements to be executed on satisfaction of the condition have been enclosed within a pair of braces. If a pair of braces is not used, then the C compiler assumes that the programmer wants only the immediately next statement after the **if** to be executed on satisfaction of the condition. In other words, we can say that the default scope of the **if** statement is the immediately next statement after it. Figure 3.4 would help you understand the flow of control in the program.

START

INPUT cy, yoj

STOP

is yos > 3

YesNo

yos = cy - yoj

bonus = 2500

PRINT bonus

Figure 3.4

**The _if-else_ Statement** The **if** statement by itself will execute a single statement, or a group of statements, when the expression following **if** evaluates to true. It does nothing when the expression evaluates to false. Can we execute one group of statements if the expression evaluates to true and another group of statements if the expression evaluates to false? Of course! This is what is the purpose of the **else** statement that is demonstrated in the following example:

**Example 3.3:** In a company an employee is paid as under:

If his basic salary is less than Rs. 1500, then HRA = 10% of basic salary and DA = 90% of basic salary. If his salary is either equal to or above Rs. 1500, then HRA = Rs. 500 and DA = 98% of basic salary. If the employee's salary is input through the keyboard write a program to find his gross salary.

/\* Calculation of gross salary \*/ # include <stdio.h> int main( ) { float bs, gs, da, hra ; printf ( "Enter basic salary " ) ; scanf ( "%f", &bs ) ; if ( bs < 1500 ) { hra = bs \* 10 / 100 ; da = bs \* 90 / 100 ; } else { hra = 500 ; da = bs \* 98 / 100 ; } gs = bs + hra + da ; printf ( "gross salary = Rs. %f\\n", gs ) ; return 0 ; }

Figure 3.5 would help you understand the flow of control in the program.

START

INPUT bs

STOP

is bs < 1500

YesNo

hra = 500 hra = bs \* 10 / 100

PRINT gs

da = bs \* 90 / 100da = bs \* 98 / 100

gs = bs + hra + da

Figure 3.5

A few points worth noting about the program...

- The group of statements after the **if** upto and not including the **else** is called an ‘if block’. Similarly, the statements after the **else** form the ‘else block’.

- Notice that the **else** is written exactly below the **if**. The statements in the if block and those in the else block have been indented to the right. This formatting convention is followed throughout the book to enable you to understand the working of the program better.

- Had there been only one statement to be executed in the if block and only one statement in the else block we could have dropped the pair of braces.

- As with the **if** statement, the default scope of **else** is also the statement immediately after the **else**. To override this default scope, a pair of braces, as shown in the above example, must be used.

### Nested _if-elses_

It is perfectly alright if we write an entire **if-else** construct within either the body of the **if** statement or the body of an **else** statement. This is called ‘nesting’of **if**s. This is shown in the following program:

/\* A quick demo of nested if-else \*/ # include <stdio.h> int main( ) { int i ; printf ( "Enter either 1 or 2 " ) ; scanf ( "%d", &i ) ; if ( i == 1 ) printf ( "You would go to heaven !\\n" ) ; else { if ( i == 2 ) printf ( "Hell was created with you in mind\\n" ) ; else printf ( "How about mother earth !\\n" ) ; } return 0 ; }

Note that the second **if-else** construct is nested in the first **else** statement. If the condition in the first **if** statement is false, then the condition in the second **if** statement is checked. If it is false as well, then the final **else** statement is executed.

You can see in the program how each time a **if-else** construct is nested within another **if-else** construct, it is also indented to add clarity to the program. Inculcate this habit of indentation; otherwise, you would end up writing programs which nobody (you included) can understand easily at a later date. Note that whether we indent or do not indent the

program, it doesn’t alter the flow of execution of instructions in the program.

In the above program, an **if-else** occurs within the ‘**else** block’ of the first **if** statement. Similarly, in some other program, an **if-else** may occur in the ‘**if** block’ as well. There is no limit on how deeply the **if**s and the **else**s can be nested.

### Forms of _if_

The **if** statement can take any of the following forms:

- if ( condition ) do this ;

- if ( condition ) { do this ; and this ; }

- if ( condition ) do this ; else do this ;

- if ( condition ) { do this ; and this ; } else { do this ; and this ; }

- if ( condition ) { if ( condition ) do this ; else { do this ;

and this ; } } else do this ;

- if ( condition ) do this ; else { if ( condition ) do this ; else { do this ; and this ; } }

### Summary

- There are three ways for taking decisions in a program. First way is to use the **if**\-**else** statement, second way is to use the conditional operators and third way is to use the **switch** statement.

- The condition associated with an if statement is built using relational operators <, >, <=, >=, == and !=.

- The default scope of **if** statement is only the next statement. So, to execute more than one statement they must be written in a pair of braces.

- An ‘**if** block’ need not always be associated with an ‘**else** block’. However, an ‘**else** block’ must always be associated with an **if**.

- An **if-else** statement can be nested inside another **if-else** statement.

### Exe**r**cise

**\[A\]** What will be the output of the following programs:

- # include <stdio.h> int main( ) {

int a = 300, b, c ; if ( a >= 400 ) b = 300 ; c = 200 ; printf ( "%d %d\\n", b, c ) ; return 0 ; }

- # include <stdio.h> int main( ) { int a = 500, b, c ; if ( a >= 400 ) b = 300 ; c = 200 ; printf ( "%d %d\\n", b, c ) ; return 0 ; }

- # include <stdio.h> int main( ) { int x = 10, y = 20 ; if ( x == y ) ; printf ( "%d %d\\n", x, y ) ; return 0 ; }

- # include <stdio.h> int main( ) { int x = 3 ; float y = 3.0 ; if ( x == y ) printf ( "x and y are equal\\n" ) ; else printf ( "x and y are not equal\\n" ) ; return 0 ; }

- # include <stdio.h> int main( ) {

int x = 3, y, z ; y = x = 10 ; z = x < 10 ; printf ( "x = %d y = %d z = %d\\n", x, y, z ) ; return 0 ; }

- # include <stdio.h> int main( ) { int i = 65 ; char j = ’A’ ; if ( i == j ) printf ( "C is WOW\\n" ) ; else printf ( "C is a headache\\n" ) ; return 0 ; }

**\[B\]** Point out the errors, if any, in the following programs:

- # include <stdio.h> int main( ) { float a = 12.25, b = 12.52 ; if ( a = b ) printf ( "a and b are equal\\n" ) ; return 0 ; }

- # include <stdio.h> int main( )

{ int j = 10, k = 12 ; if ( k >= j ) { { k = j ; j = k ; } } return 0 ; }

- # include <stdio.h> int main( ) { if ( 'X' < 'x' ) printf ( "ascii value of X is smaller than that of x\\n" ) ; }

- # include <stdio.h> int main( ) { int x = 10 ; if ( x >= 2 ) then printf ( "%d\\n", x ) ; return 0 ; }

- # include <stdio.h> int main( ) { int x = 10, y = 15 ; if ( x % 2 = y % 3 ) printf ( "Carpathians\\n" ) ; }

- # include <stdio.h> int main( ) { int x = 30, y = 40 ; if ( x == y ) printf ( "x is equal to y\\n" ) ; elseif ( x > y ) printf ( "x is greater than y\\n" ) ; elseif ( x < y ) printf ( "x is less than y\\n" ) ; return 0 ; }

- # include <stdio.h> int main( ) { int a, b ; scanf ( "%d %d", a, b ) ; if ( a > b ) ;

printf ( "This is a game\\n" ) ; else printf ( "You have to play it\\n" ) ; return 0 ; }

**\[C\]** Attempt the following:

- If cost price and selling price of an item are input through the keyboard, write a program to determine whether the seller has made profit or incurred loss. Also determine how much profit he made or loss he incurred.

- Any integer is input through the keyboard. Write a program to find out whether it is an odd number or even number.

- Any year is input through the keyboard. Write a program to determine whether the year is a leap year or not.

(Hint: Use the % (modulus) operator)

- According to the Gregorian calendar, it was Monday on the date 01/01/01. If any year is input through the keyboard write a program to find out what is the day on 1st January of this year.

- A five-digit number is entered through the keyboard. Write a program to obtain the reversed number and to determine whether the original and reversed numbers are equal or not.

- If the ages of Ram, Shyam and Ajay are input through the keyboard, write a program to determine the youngest of the three.

- Write a program to check whether a triangle is valid or not, when the three angles of the triangle are entered through the keyboard. A triangle is valid if the sum of all the three angles is equal to 180 degrees.

- Write a program to find the absolute value of a number entered through the keyboard.

- Given the length and breadth of a rectangle, write a program to find whether the area of the rectangle is greater than its perimeter. For example, the area of the rectangle with length = 5 and breadth = 4 is greater than its perimeter.

- Given three points **(x1, y1)**, **(x2, y2)** and **(x3, y3)**, write a program to check if all the three points fall on one straight line.

- Given the coordinates **(x, y)** of center of a circle and its radius, write a program that will determine whether a point lies inside the circle,

on the circle or outside the circle. (Hint: Use **sqrt( )** and **pow( )** functions)

- Given a point **(x, y)**, write a program to find out if it lies on the X- axis, Y-axis or on the origin.