---
title: 'More Complex Repetitions'
weight: 6
---

   
The programs that we have developed so far used either a sequential or a decision control instruction. In the first one, the calculations

were carried out in a fixed order; while in the second, an appropriate set of instructions were executed depending upon the outcome of the condition(s) being tested.

**The _for_ Loop** Perhaps one reason why few programmers use **while** is that they are too busy using the **for**, which is probably the most popular looping instruction. The **for** allows us to specify three things about a loop in a single line:

- Setting a loop counter to an initial value.

- Testing the loop counter to determine whether its value has reached the number of repetitions desired.

- Increasing the value of loop counter each time the body of the loop has been executed.

The general form of **for** statement is as under:

for ( initialize counter ; test counter ; increment counter ) { do this ; and this ; and this ; }

Let us now write down the simple interest program using **for**. Compare this program with the one that we wrote using **while**. The flowchart is also given in Figure 6.1 for a better understanding.

### T

START

STOP

Yes

No

si = p \* n \* r / 100

count = 1

count = count + 1

is count <= 3

INPUT p, n, r

PRINT si

Figure 6.1

/\* Calculation of simple interest for 3 sets of p, n and r \*/ # include <stdio.h> int main( ) { int p, n, count ; float r, si ; for ( count = 1 ; count <= 3 ; count = count + 1 ) { printf ( "Enter values of p, n, and r " ) ; scanf ( "%d %d %f", &p, &n, &r ) ; si = p \* n \* r / 100 ; printf ( "Simple Interest = Rs.%f\\n", si ) ; } return 0 ; }

If you compare this program with the one written using **while**, you can observe that the three steps—initialization, testing and incrementation—required for the loop construct have now been incorporated in the **for** statement.

Let us now examine how the **for** statement gets executed:

 When the **for** statement is executed for the first time, the value of **count** is set to an initial value 1.

 Next the condition **count <= 3** is tested. Since **count** is 1, the condition is satisfied and the body of the loop is executed for the first time.

 Upon reaching the closing brace of **for**, control is sent back to the **for** statement, where the value of **count** gets incremented by 1.

 Again the test is performed to check whether the new value of **count** exceeds 3.

 If the value of **count** is less than or equal to 3, the statements within the braces of **for** are executed again.

 The body of the **for** loop continues to get executed till **count** doesn’t exceed the final value 3.

 When **count** reaches the value 4, the control exits from the loop and is transferred to the statement (if any) immediately after the body of **for**.

Figure 6.2 would help in further clarifying the concept of execution of the **for** loop.

START

STOP

test

True

False

body of loop

initialize

increment

Figure 6.2

It is important to note that the initialization, testing and incrementation part of a **for** loop can be replaced by any valid expression. Thus the following **for** loops are perfectly ok.

for ( i = 10 ; i ; i -- ) printf ( "%d ", i ) ; for ( i < 4 ; j = 5 ; j = 0 ) printf ( "%d ", i ) ; for ( i = 1; i <=10 ; printf ( "%d ", i++ ) ) ; for ( scanf ( "%d", &i ) ; i <= 10 ; i++ ) printf ( "%d", i ) ;

Let us now write down the program to print numbers from 1 to 10 in different ways. This time we would use a **for** loop instead of a **while** loop.

- # include <stdio.h> int main( ) { int i ; for ( i = 1 ; i <= 10 ; i = i + 1 ) printf ( "%d\\n", i ) ; return 0 ; }

Note that the initialization, testing and incrementation of loop counter is done in the **for** statement itself. Instead of **i = i + 1**, the statements **i++** or **i += 1** can also be used.

Since there is only one statement in the body of the **for** loop, the pair of braces have been dropped. As with the **while**, the default scope of **for** is the immediately next statement after **for**.

- # include <stdio.h> int main( ) { int i ; for ( i = 1 ; i <= 10 ; ) { printf ( "%d\\n", i ) ; i = i + 1 ; }

return 0 ; }

Here, the incrementation is done within the body of the **for** loop and not in the **for** statement. Note that, in spite of this, the semicolon ( ; ) after the condition is necessary.

- # include <stdio.h> int main( ) { int i = 1 ; for ( ; i <= 10 ; i = i + 1 ) printf ( "%d\\n", i ) ; return 0 ; }

Here the initialization is done in the declaration statement itself, but still the semicolon before the condition is necessary.

- # include <stdio.h> int main( ) { int i = 1 ; for ( ; i <= 10 ; ) { printf ( "%d\\n", i ) ; i = i + 1 ; } return 0 ; }

Here, neither the initialization, nor the incrementation is done in the **for** statement, but still the two semicolons are necessary.

- # include <stdio.h> int main( ) { int i ; for ( i = 0 ; i++ < 10 ; ) printf ( "%d\\n", i ) ; return 0 ; }

Here, the comparison as well as the incrementation is done through the same expression, **i++ < 10**. Since the **++** operator comes after **i**, first comparison is done, followed by incrementation. Note that it is necessary to initialize **i** to 0.

- # include <stdio.h> int main( ) { int i ; for ( i = 0 ; ++i <= 10 ; ) printf ( "%d\\n", i ) ; return 0 ; }

Here again, both, the comparison and the incrementation are done through the same expression, **++i <= 10**. Since **++** precedes **i** firstly incrementation is done, followed by comparison. Note that it is necessary to initialize **i** to 0.

### Nesting of Loops

The way **if** statements can be nested, similarly **while**s and **for**s can also be nested. To understand how nested loops work, look at the program given below.

/\* Demonstration of nested loops \*/ # include <stdio.h> int main( ) { int r, c, sum ; for ( r = 1 ; r <= 3 ; r++ ) /\* outer loop \*/ { for ( c = 1 ; c <= 2 ; c++ ) /\* inner loop \*/ { sum = r + c ; printf ( "r = %d c = %d sum = %d\\n", r, c, sum ) ; } } return 0 ; }

When you run this program, you will get the following output:

r = 1 c = 1 sum = 2 r = 1 c = 2 sum = 3 r = 2 c = 1 sum = 3 r = 2 c = 2 sum = 4 r = 3 c = 1 sum = 4 r = 3 c = 2 sum = 5

Here, for each value of **r**, the inner loop is cycled through twice, with the variable **c** taking values from 1 to 2. The inner loop terminates when the value of **c** exceeds 2, and the outer loop terminates when the value of **r** exceeds 3.

As you can see, the body of the outer **for** loop is indented, and the body of the inner **for** loop is further indented. These multiple indentations make the program easier to understand.

Instead of using two statements, one to calculate **sum** and another to print it out, we can compact them into one single statement by saying:

printf ( "r = %d c = %d sum = %d\\n", r, c, r + c ) ;

The way **for** loops have been nested here, similarly, two **while** loops can also be nested. Not only this, a **for** loop can occur within a **while** loop, or a **while** within a **for**.

### Multiple Initializations in the _for_ Loop

The initialization expression in the **for** loop can contain more than one statement separated by a comma. For example,

for ( i = 1, j = 2 ; j <= 10 ; j++ )

Multiple statements can also be used in the incrementation expression of **for** loop; i.e., you can increment (or decrement) two or more variables at the same time. Similarly multiple conditions are allowed in the test expression. These conditions must be linked together using logical operators && and/or ||.

**The _break_ Statement** We often come across situations where we want to jump out of a loop instantly, without waiting to get back to the condition. The keyword **break** allows us to do this. When **break** is encountered inside any loop, control automatically passes to the first statement after the loop. A

**break** is usually associated with an **if**. Let’s consider the following example:

**Example 6.1:** Write a program to determine whether a number is prime or not. A prime number is said to be prime if it is divisible only by 1 or itself.

All we have to do to test whether a number is prime or not, is to divide it successively by all numbers from 2 to one less than itself. If remainder of any of these divisions is zero, the number is not a prime. If no division yields a zero then the number is a prime number. Following program implements this logic:

\# include <stdio.h> int main( ) { int num, i ; printf ( "Enter a number " ) ; scanf ( "%d", &num ) ; i = 2 ; while ( i <= num - 1 ) { if ( num % i == 0 ) { printf ( "Not a prime number\\n" ) ; break ; } i++ ; } if ( i == num ) printf ( "Prime number\\n" ) ; }

In this program, the moment **num % i** turns out to be zero, (i.e., **num** is exactly divisible by **i**), the message “Not a prime number” is printed and the control breaks out of the **while** loop. Why does the program require the **if** statement after the **while** loop at all? Well, there are two possibilities the control could have reached outside the **while** loop:

- It jumped out because the number proved to be not a prime.

- The loop came to an end because the value of **i** became equal to **num**.

When the loop terminates in the second case, it means that there was no number between 2 to **num - 1** that could exactly divide **num**. That is, **num** is indeed a prime. If this is true, the program should print out the message “Prime number”.

The keyword **break**, breaks the control only from the **while** in which it is placed. Consider the following program, which illustrates this fact:

\# include <stdio.h> int main( ) { int i = 1 , j = 1 ; while ( i++ <= 100 ) { while ( j++ <= 200 ) { if ( j == 150 ) break ; else printf ( "%d %d\\n", i, j ) ; } } return 0 ; }

In this program when **j** equals 150, **break** takes the control outside the inner **while** only, since it is placed inside the inner **while**.

**The _continue_ Statement** In some programming situations, we want to take the control to the beginning of the loop, bypassing the statements inside the loop, which have not yet been executed. The keyword **continue** allows us to do this. When **continue** is encountered inside any loop, control automatically passes to the beginning of the loop.

A **continue** is usually associated with an **if**. As an example, let's consider the following program:

\# include <stdio.h>

int main( ) { int i, j ; for ( i = 1 ; i <= 2 ; i++ ) { for ( j = 1 ; j <= 2 ; j++ ) { if ( i == j ) continue ; printf ( "%d %d\\n", i, j ) ; } } return 0 ; }

The output of the above program would be...

1 2 2 1

Note that when the value of **i** equals that of **j**, the **continue** statement takes the control to the **for** loop (inner) bypassing the rest of the statements pending execution in the **for** loop (inner).

**The _do_\-_while_ Loop** The **do-while** loop looks like this:

do { this ; and this ; and this ; and this ; } while ( this condition is true ) ;

There is a minor difference between the working of **while** and **do-while** loops. This difference is the place where the condition is tested. The **while** tests the condition before executing any of the statements within the **while** loop. As against this, the **do-while** tests the condition after

having executed the statements within the loop. Figure 6.3 would clarify the execution of **do-while** loop still further.

START

STOP

test True

False

body of loop

initialize

increment

Figure 6.3

This means that **do-while** would execute its statements at least once, even if the condition fails for the first time. The **while**, on the other hand will not execute its statements if the condition fails for the first time. This difference is brought about more clearly by the following program:

\# include <stdio.h> int main( ) { while ( 4 < 1 ) printf ( "Hello there \\n" ) ; return 0 ; }

Here, since the condition fails the first time itself, the **printf( )** will not get executed at all. Let's now write the same program using a **do-while** loop.

\# include <stdio.h> int main( ) {

do { printf ( "Hello there \\n" ) ; } while ( 4 < 1 ) ; return 0 ; }

In this program, the **printf( )** would be executed once, since first the body of the loop is executed and then the condition is tested.

**The Odd Loop** The loops that we have used so far executed the statements within them a finite number of times. However, in real life programming, one comes across a situation when it is not known beforehand how many times the statements in the loop are to be executed. This situation can be programmed as shown below.

/\* Execution of a loop an unknown number of times \*/ # include <stdio.h> int main( ) { char another ; int num ; do { printf ( "Enter a number " ) ; scanf ( "%d", &num ) ; printf ( "square of %d is %d\\n", num, num \* num ) ; printf ( "Want to enter another number y/n " ) ; fflush ( stdin ) ; scanf ( "%c", &another ) ; } while ( another == 'y' ) ; return 0 ; }

And here is the sample output...

Enter a number 5 square of 5 is 25 Want to enter another number y/n y

Enter a number 7 square of 7 is 49 Want to enter another number y/n n

In this program, the **do-while** loop would keep getting executed till the user continues to answer **y**. The moment user answers **n**, the loop terminates, since the condition ( **another == 'y'** ) fails. Note that this loop ensures that statements within it are executed at least once even if **n** is supplied first time itself.

Perhaps you are wondering what for have we used the function **fflush( )**. The reason is to get rid of a peculiarity of **scanf( )**. After supplying a number when we hit the Enter key, **scanf( )** assigns the number to variable **num** and keeps the Enter key unread in the keyboard buffer. So when it’s time to supply Y or N for the question ‘Want to enter another number (y/n)’, **scanf( )** will read the Enter key from the buffer thinking that user has entered the Enter key. To avoid this problem, we use the function **fflush( )**. It is designed to remove or ‘flush out’ any data remaining in the buffer. The argument to **fflush( )** must be the buffer which we want to flush out. Here we have used ‘stdin’, which means buffer related with standard input device, i.e., keyboard.

Though it is simpler to program such a requirement using a **do-while** loop, the same functionality if required, can also be accomplished using **for** and **while** loops as shown below.

/\* odd loop using a for loop \*/ # include <stdio.h> int main( ) { char another = 'y' ; int num ; for ( ; another == 'y' ; ) { printf ( "Enter a number " ) ; scanf ( "%d", &num ) ; printf ( "square of %d is %d\\n", num, num \* num ) ; printf ( "Want to enter another number y/n " ) ; fflush ( stdin ) ; scanf ( "%c", &another ) ; } return 0 ; }

/\* odd loop using a while loop \*/ # include <stdio.h> int main( ) { char another = 'y' ; int num ; while ( another == 'y' ) { printf ( "Enter a number " ) ; scanf ( "%d", &num ) ; printf ( "square of %d is %d\\n", num, num \* num ) ; printf ( "Want to enter another number y/n " ) ; fflush ( stdin ) ; scanf ( " %c", &another ) ; } return 0 ; }

**break** and **continue** are used with **do-while** just as they would be in a **while** or a **for** loop. A **break** takes you out of the **do-while** bypassing the conditional test. A **continue** sends you straight to the test at the end of the loop.

### Summary

- Unlike a **while** loop, in a **for** loop the initialization, test and incrementation are written in a single line.

- A **break** statement takes the execution control out of the loop.

- A **continue** statement skips the execution of the statements after it and takes the control through the next cycle of the loop.

- A **do-while** loop is used to ensure that the statements within the loop are executed at least once.

- The operators +=, -=, \*=, /=, %= are compound assignment operators. They modify the value of the operand to the left of them.

### Exercise

**\[A\]** What will be the output of the following programs:

- # include <stdio.h> int main( ) { int i = 0 ; for ( ; i ; ) printf ( "Here is some mail for you\\n" ) ; return 0 ; }

- # include <stdio.h> int main( ) { int i ; for ( i = 1 ; i <= 5 ; printf ( "%d\\n", i ) ) ; i++ ; return 0 ; }

- # include <stdio.h> int main( ) { int i = 1, j = 1 ; for ( ; ; ) { if ( i > 5 ) break ; else j += i ; printf ( "%d\\n", j ) ; i += j ; return 0 ; } }

**\[B\]** Answer the following:

- The three parts of the loop expression in the **for** loop are:

the i\_\_\_\_\_\_\_\_\_\_\_\_ expression the t\_\_\_\_\_\_\_\_\_\_\_\_ expression

the i\_\_\_\_\_\_\_\_\_\_\_\_ expression

- The **break** statement is used to exit from:

1\. An **if** statement 2. A **for** loop 3. A program 4. The **main( )** function

- A **do-while** loop is useful when we want that the statements within the loop must be executed:

1\. Only once 2. At least once 3. More than once 4. None of the above

- In what sequence the initialization, testing and execution of body is done in a **do-while** loop

1\. Initialization, execution of body, testing 2. Execution of body, initialization, testing 3. Initialization, testing, execution of body 4. None of the above

- Which of the following is not an infinite loop?

- Which keyword is used to take the control to the beginning of the loop?

- How many times the **while** loop in the following C code will get executed?

1\. int i = 1 ; while ( 1 ) { i++ ; }

2\. for ( ; ; ) ;

3\. int t = 0, f ; while ( t ) { f = 1 ; }

4\. int y, x = 0 ; do { y = x ; } while ( x == 0 ) ;

\# include <stdio.h> int main( ) { int j = 1 ; while ( j <= 255 ) ; { printf ( "%c %d ", j, j ) ; j++; } return 0 ; }

- Which of the following statements is true for the following program?

\# include <stdio.h> int main( ) { int x=10, y = 100%90 ; for ( i = 1 ; i <= 10 ; i++ ) ; if ( x != y ) ; printf ( "x = %d y = %d\\n", x, y ) ; return 0 ; }

1\. The **printf( )** function is called 10 times. 2. The program will produce the output x=10 y=10. 3. The ; after the **if (x!=y)** would not produce an error. 4. The program will not produce any output. 5. The **printf( )** function is called infinite times.

- Which of the following statement is true about a **for** loop used in a C program?

1\. **for** loop works faster than a **while** loop. 2. All things that can be done using a **for** loop can also be done

using a **while** loop. 3. **for ( ; ; )** implements an infinite loop. 4. **for** loop can be used if we want statements in a loop to get

executed at least once. 5. **for** loop works faster than a **do-while** loop.

**\[C\]** Attempt the following:

- Write a program to print all prime numbers from 1 to 300. (Hint: Use nested loops, **break** and **continue**)

- Write a program to fill the entire screen with a smiling face. The smiling face has an ASCII value 1.

- Write a program to add first seven terms of the following series

using a **for** loop:

- Write a program to generate all combinations of 1, 2 and 3 using **for** loop.

- A machine is purchased which will produce earning of Rs. 1000 per year while it lasts. The machine costs Rs. 6000 and will have a salvage value of Rs. 2000 when it is condemned. If 9 percent per annum can be earned on alternate investments, write a program to determine what will be the minimum life of the machine to make it a more attractive investment compared to alternative investment?

- Write a program to print the multiplication table of the number entered by the user. The table should get displayed in the following form:

29 \* 1 = 29 29 \* 2 = 58

…

- According to a study, the approximate level of intelligence of a person can be calculated using the following formula:

i = 2 + ( y + 0.5 x )

Write a program that will produce a table of values of **i**, **y** and **x**, where **y** varies from 1 to 6, and, for each value of **y**, **x** varies from 5.5 to 12.5 in steps of 0.5.

- When interest compounds **q** times per year at an annual rate of **r** % for **n** years, the principal **p** compounds to an amount **a** as per the following formula

a = p ( 1 + r / q ) nq

Write a program to read 10 sets of **p, r, n** & **q** and calculate the corresponding **a**s.

1

1!

2

2!

3

3! ……

.

- The natural logarithm can be approximated by the following series.

If **x** is input through the keyboard, write a program to calculate the sum of first seven terms of this series.

- Write a program to generate all Pythogorean Triplets with side length less than or equal to 30.

- Population of a town today is 100000. The population has increased steadily at the rate of 10 % per year for last 10 years. Write a program to determine the population at the end of each year in the last decade.

- Ramanujan number is the smallest number that can be expressed as sum of two cubes in two different ways. Write a program to print all such numbers up to a reasonable limit.

- Write a program to print 24 hours of day with suitable suffixes like AM, PM, Noon and Midnight.

(m) Write a program to produce the following output:

1

2 3

4 5 6

7 8 9 10

(n) Write a program to produce the following output:

A B C D E F G F E D C B A

A B C D E F F E D C B A

A B C D E E D C B A

A B C D D C B A

A B C C B A

A B B A

A A

(o) Write a program to produce the following output:

.... 1

2

1 1

2

1 1

2

1 1 4 3 2

  

  

  



  

   



  

  



_x_

_x_

_x_

_x_

_x_

_x_

_x_

_x_ 

1

1 1

1 2 1

1 3 3 1

1

4 6 4 1

