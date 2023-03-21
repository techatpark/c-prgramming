---
title: 'Case Control'
weight: 7
---
   
In real life, we are often faced with situations where we are required to make a choice between a number of alternatives rather than only one or two. For example, which school to join or which hotel to visit, or still harder, which girl to marry. Serious C programming is same; the choice we are asked to make is more complicated than merely selecting between two alternatives. C provides a special control statement that allows us to handle such cases effectively; rather than using a series of **if** statements. This control instruction is, in fact, the topic of this chapter. Towards the end of the chapter, we would also study a keyword called **goto**, and understand why we should avoid its usage in C programming.

**Decisions using _switch_** The control statement that allows us to make a decision from the number of choices is called a **switch**, or more correctly a **switch-case- default**, since these three keywords go together to make up the control statement. They most often appear as follows:

```C
switch ( integer expression ) 
{ 
    case constant 1 : do this ; 
    case constant 2 : do this ; 
    case constant 3 : do this ; 
    default : do this ; 
}
```

The integer expression following the keyword **switch** is any C expression that will yield an integer value. It could be an integer constant like 1, 2 or 3, or an expression that evaluates to an integer. The keyword **case** is followed by an integer or a character constant. Each constant in each **case** must be different from all the others. The “do this” lines in the above form of **switch** represent any valid C statement.

What happens when we run a program containing a **switch**? First, the integer expression following the keyword **switch** is evaluated. The value it gives is then matched, one-by-one, against the constant values that follow the **case** statements. When a match is found, the program executes the statements following that **case**, and all subsequent **case** and **default** statements as well. If no match is found with any of the **case**

### I

statements, only the statements following the **default** case are executed. A few examples will show how this control instruction works.

Consider the following program:

\# include <stdio.h> int main( ) { int i = 2 ; switch ( i ) { case 1 : printf ( "I am in case 1 \\n" ) ; case 2 : printf ( "I am in case 2 \\n" ) ; case 3 : printf ( "I am in case 3 \\n" ) ; default : printf ( "I am in default \\n" ) ; }

return 0 ; }

The output of this program would be:

I am in case 2 I am in case 3 I am in default

The output is definitely not what we expected! We didn’t expect the second and third line in the above output. The program prints case 2 and case 3 and the default case. Well, yes. We said the **switch** executes the case where a match is found and all the subsequent **case**s and the **default** as well.

If you want that only case 2 should get executed, it is upto you to get out of the **switch** then and there by using a **break** statement. The following example shows how this is done. Note that there is no need for a **break** statement after the **default**, since on reaching the **default** case, the control comes out of the **switch** anyway.

\# include <stdio.h>

int main( ) { int i = 2 ; switch ( i ) { case 1 : printf ( "I am in case 1 \\n" ) ; break ; case 2 : printf ( "I am in case 2 \\n" ) ; break ; case 3 : printf ( "I am in case 3 \\n" ) ; break ; default : printf ( "I am in default \\n" ) ; } return 0 ; }

The output of this program would be:

I am in case 2

The operation of **switch** is shown in Figure 7.1 in the form of a flowchart for a better understanding.

START

STOP

case 1 Yes

No

statement 1

case 2

case 3

case 4

Yes

Yes

Yes

statement 2

statement 3

statement 4

No

No

No

Figure 7.1

### The Tips and Traps

A few useful tips about the usage of **switch** and a few pitfalls to be avoided:

- The earlier program that used **switch** may give you the wrong impression that you can use only cases arranged in ascending order, 1, 2, 3 and default. You can, in fact, put the cases in any order you please. Here is an example of scrambled case order:

\# include <stdio.h> int main( ) { int i = 22 ;

switch ( i ) { case 121 : printf ( "I am in case 121 \\n" ) ; break ; case 7 : printf ( "I am in case 7 \\n" ) ; break ; case 22 : printf ( "I am in case 22 \\n" ) ; break ; default : printf ( "I am in default \\n" ) ; } return 0 ; }

The output of this program would be:

I am in case 22

- You are also allowed to use **char** values in **case** and **switch** as shown in the following program:

\# include <stdio.h> int main( ) { char c = 'x' ; switch ( c ) { case 'v' : printf ( "I am in case v \\n" ) ; break ; case 'a' : printf ( "I am in case a \\n" ) ; break ; case 'x' : printf ( "I am in case x \\n" ) ; break ; default :

printf ( "I am in default \\n" ) ; } return 0 ; }

The output of this program would be:

I am in case x

In fact here when we use ‘v’, ‘a’, ‘x’ they are actually replaced by the ASCII values (118, 97, 120) of these character constants.

- At times we may want to execute a common set of statements for multiple **case**s. The following example shows how this can be achieved:

\# include <stdio.h> int main( ) { char ch ; printf ( "Enter any one of the alphabets a, b, or c " ) ; scanf ( "%c", &ch ) ; switch ( ch ) { case 'a' : case 'A' : printf ( "a as in ashar\\n" ) ; break ; case 'b' : case 'B' : printf ( "b as in brain\\n" ) ; break ; case 'c' : case 'C' : printf ( "c as in cookie\\n" ) ; break ; default : printf ( "wish you knew what are alphabets\\n" ) ; return 0 ;

} }

Here, we are making use of the fact that once a **case** is satisfied; the control simply falls through the **switch** till it doesn’t encounter a **break** statement. That is why if an alphabet **a** is entered, the **case ’a’** is satisfied and since there are no statements to be executed in this **case**, the control automatically reaches the next **case**, i.e., **case** **’A’** and executes all the statements in this **case**.

- Even if there are multiple statements to be executed in each **case**, there is no need to enclose them within a pair of braces (unlike **if** and **else**).

- Every statement in a **switch** must belong to some **case** or the other. If a statement doesn’t belong to any **case**, the compiler won’t report an error. However, the statement would never get executed. For example, in the following program, the **printf( )** never goes to work:

\# include <stdio.h> int main( ) { int i, j ; printf ( "Enter value of i" ) ; scanf ( "%d", &i ) ; switch ( i ) { printf ( "Hello\\n" ) ; case 1 : j = 10 ; break ; case 2 : j = 20 ; break ; } return 0 ; }

- If we have no **default** case, then the program simply falls through the entire **switch** and continues with the next instruction (if any,) that follows the closing brace of **switch**.

- Is **switch** a replacement for **if**? Yes and no. Yes, because it offers a better way of writing programs as compared to **if**, and no, because, in certain situations, we are left with no choice but to use **if**. The disadvantage of **switch** is that one cannot have a case in a **switch** which looks like:

case i <= 20 :

All that we can have after the case is an **int** constant or a **char** constant or an expression that evaluates to one of these constants. Even a **float** is not allowed.

The advantage of **switch** over **if** is that it leads to a more structured program and the level of indentation is manageable, more so, if there are multiple statements within each **case** of a **switch**.

- We can check the value of any expression in a **switch**. Thus, the following **switch** statements are legal:

switch ( i + j \* k ) switch ( 23 + 45 % 4 \* k ) switch ( a < 4 && b > 7 )

Expressions can also be used in cases provided they are constant expressions. Thus, **case 3 + 7** is correct, however, **case a + b** is incorrect.

- The **break** statement when used in a **switch** takes the control outside the **switch**. However, use of **continue** will not take the control to the beginning of **switch** as one is likely to believe. This is because **switch** is not a looping statement unlike **while**, **for** or **do- while**.

- In principle, a **switch** may occur within another, but in practice, this is rarely done. Such statements would be called nested **switch** statements.

- The **switch** statement is very useful while writing menu driven programs. This aspect of **switch** is discussed in the exercise at the end of this chapter.

**_switch_ versus _if-else_ Ladder** There are some things that you simply cannot do with a **switch**. These are:

- A float expression cannot be tested using a **switch**.

- Cases can never have variable expressions (for example, it is wrong to say **case a +3 :** ).

- Multiple cases cannot use same expressions. Thus the following **switch** is illegal:

switch ( a ) { case 3 : ... case 1 + 2 : ... }

(a), (b) and (c) above may lead you to believe that these are obvious disadvantages with a **switch**, especially since there weren’t any such limitations with **if-else**. Then why use a **switch** at all? For speed—**switch** works faster than an equivalent **if-else** ladder. How come? This is because the compiler generates a jump table for a **switch** during compilation. As a result, during execution it simply refers the jump table to decide which case should be executed, rather than actually checking which case is satisfied. As against this, **if-else**s are slower because the conditions in them are evaluated at execution time. Thus a **switch** with 10 cases would work faster than an equivalent **if-else** ladder. If the 10th **case** is satisfied then jump table would be referred and statements for the 10th **case** would be executed. As against this, in an **if-else** ladder 10 conditions would be evaluated at execution time, which makes it slow. Note that a lookup in the jump table is faster than evaluation of a condition, especially if the condition is complex.

**The _goto_ Keyword** Avoid **goto** keyword! It makes a C programmer’s life miserable. There is seldom a legitimate reason for using **goto**, and its use is one of the reasons that programs become unreliable, unreadable, and hard to debug. And yet many programmers find **goto** seductive.

In a difficult programming situation, it seems so easy to use a **goto** to take the control where you want. However, almost always, there is a more elegant way of writing the same program using **if**, **for**, **while**, **do- while** and **switch**. These constructs are far more logical and easy to understand.

The big problem with **goto**s is that when we do use them we can never be sure how we got to a certain point in our code. They obscure the flow of control. So as far as possible skip them. You can always get the job done without them. Trust me, with good programming skills **goto** can always be avoided. This is the first and last time that we are going to use **goto** in this book. However, for sake of completeness of the book, the following program shows how to use **goto**:

\# include <stdio.h> # include <stdlib.h> int main( ) { int goals ; printf ( "Enter the number of goals scored against India" ) ; scanf ( "%d", &goals ) ; if ( goals <= 5 ) goto sos ; else { printf ( "About time soccer players learnt C\\n" ) ; printf ( "and said goodbye! adieu! to soccer\\n" ) ; exit ( 1 ) ; /\* terminates program execution \*/ } sos : printf ( "To err is human!\\n" ) ; return 0 ; }

And here are two sample runs of the program...

Enter the number of goals scored against India 3

To err is human! Enter the number of goals scored against India 7 About time soccer players learnt C and said goodbye! adieu! to soccer

A few remarks about the program would make the things clearer.

- If the condition is satisfied the **goto** statement transfers control to the label **sos**, causing **printf( )** following **sos** to be executed.

- The label can be on a separate line or on the same line as the statement following it, as in,

sos : printf ( "To err is human!\\n" ) ;

- Any number of **goto**s can take the control to the same label.

- The **exit( )** function is a standard library function which terminates the execution of the program. It is necessary to use this function since we don't want the statement

printf ( "To err is human!\\n" ) ;

to get executed after execution of the **else** block.

- The only programming situation in favour of using **goto** is when we want to take the control out of the loop that is contained in several other loops. The following program illustrates this:

\# include <stdio.h> int main( ) { int i, j, k ; for ( i = 1 ; i <= 3 ; i++ ) { for ( j = 1 ; j <= 3 ; j++ ) { for ( k = 1 ; k <= 3 ; k++ ) { if ( i == 3 && j == 3 && k == 3 ) goto out ; else

printf ( "%d %d %d\\n", i, j, k ) ; } } } out : printf ( "Out of the loops at last!\\n" ) ; return 0 ; }

Go through the program carefully and find out how it works. Also write a program to implement the same logic without using **goto**.

### Summary

- Ramesh’s basic salary is input through the keyboard. His dearness allowance is 40% of basic salary, and house rent allowance is 20% of basic salary. Write a program to calculate his gross salary.

- The

- When we need to choose one amongst number of alternatives, a **switch** statement is used.

- The **switch** keyword is followed by an integer or an expression that evaluates to an integer.

- The **case** keyword is followed by an integer or a character constant.

- The control falls through all the cases unless the fall is stopped using a **break** statement.

- The usage of the **goto** keyword should be avoided as it usually disturbs the normal flow of execution.

### Exercise

**\[A\]** What will be the output of the following programs:

- # include <stdio.h> int main( ) { char suite = 3 ; switch ( suite ) { case 1 :

printf ( "Diamond\\n" ) ; case 2 : printf ( "Spade\\n" ) ; default : printf ( "Heart\\n" ) ; } printf ( "I thought one wears a suite\\n" ) ; return 0 ; }

- # include <stdio.h> int main( ) { int c = 3 ; switch ( c ) { case '3' : printf ( "You never win the silver prize\\n" ) ; break ; case 3 : printf ( "You always lose the gold prize\\n" ) ; break ; default : printf ( "Of course provided you win a prize\\n" ) ; } return 0 ; }

- # include <stdio.h> int main( ) { int i = 3 ; switch ( i ) { case 0 : printf ( "Customers are dicey\\n" ) ; case 1 + 0 : printf ( "Markets are pricey\\n" ) ; case 4 / 2 : printf ( "Investors are moody\\n" ) ; case 8 % 5 : printf ( "At least employees are good\\n" ) ;

} return 0 ; }

- # include <stdio.h> int main( ) { int k ; float j = 2.0 ; switch ( k = j + 1 ) { case 3 : printf ( "Trapped\\n" ) ; break ; default : printf ( "Caught!\\n" ) ; } return 0 ; }

- # include <stdio.h> int main( ) { int ch = 'a' + 'b' ; switch ( ch ) { case 'a' : case 'b' : printf ( "You entered b\\n" ) ; case 'A' : printf ( "a as in ashar\\n" ) ; case 'b' + 'a' : printf ( "You entered a and b\\n" ) ; } return 0 ; }

- # include <stdio.h> int main( ) { int i = 1 ; switch ( i - 2 ) {

case -1 : printf ( "Feeding fish\\n" ) ; case 0 : printf ( "Weeding grass\\n" ) ; case 1 : printf ( "Mending roof\\n" ) ; default : printf ( "Just to survive\\n" ) ; } return 0 ; }

**\[B\]** Point out the errors, if any, in the following programs:

- # include <stdio.h> int main( ) { int suite = 1 ; switch ( suite ) ; { case 0 ; printf ( "Club\\n" ) ; case 1 ; printf ( "Diamond\\n" ) ; } return 0 ; }

- # include <stdio.h> int main( ) { int temp ; scanf ( "%d", &temp ) ; switch ( temp ) { case ( temp <= 20 ) : printf ( "Ooooooohhhh! Damn cool!\\n" ) ; case ( temp > 20 && temp <= 30 ) : printf ( "Rain rain here again!\\n" ) ; case ( temp > 30 && temp <= 40 ) : printf ( "Wish I am on Everest\\n" ) ; default : printf ( "Good old nagpur weather\\n" ) ;

} return 0 ; }

- # include <stdio.h> int main( ) { float a = 3.5 ; switch ( a ) { case 0.5 : printf ( "The art of C\\n" ) ; break ; case 1.5 : printf ( "The spirit of C\\n" ) ; break ; case 2.5 : printf ( "See through C\\n" ) ; break ; case 3.5 : printf ( "Simply c\\n" ) ; } return 0 ; }

- # include <stdio.h> int main( )

{ int a = 3, b = 4, c ; c = b – a ; switch ( c ) { case 1 || 2 : printf ( "God give me a chance to change things\\n" ) ; break ; case a || b : printf ( "God give me a chance to run my show\\n" ) ; break ; } return 0 ; }

**\[C\]** Write a menu driven program which has following options:

1\. Factorial of a number

2\. Prime or not 3. Odd or even 4. Exit

Once a menu item is selected the appropriate action should be taken and once this action is finished, the menu should reappear. Unless the user selects the ‘Exit’ option the program should continue to run.

Hint: Make use of an infinite **while** and a **switch** statement.

**\[D\]** Write a program to find the grace marks for a student using **switch**. The user should enter the class obtained by the student and the number of subjects he has failed in. Use the following logic:

- If the student gets first class and the number of subjects he failed in is greater than 3, then he does not get any grace. Otherwise the grace is of 5 marks per subject.

- If the student gets second class and the number of subjects he failed in is greater than 2, then he does not get any grace. Otherwise the grace is of 4 marks per subject.

- If the student gets third class and the number of subjects he failed in is greater than 1, then he does not get any grace. Otherwise the grace is of 5 marks.