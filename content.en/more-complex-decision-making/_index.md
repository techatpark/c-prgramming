---
title: 'More Complex Decision Making'
weight: 4
---

   
We all face situations in real-life where the action that we carry out is based on multiple conditions. For example, I will join a

company if the company allocates a metro location, gives me a good pay package and permits a joining period of 4 weeks. In programming too action performed may be based on result of multiple conditions. Such programming situations can be handled elegantly using Logical Operators. This chapter also explores the use of another type of operators called Conditional Operators.

**Use of Logical Operators** C allows usage of three logical operators, namely, &&, || and !. These are to be read as ‘AND’, ‘OR’ and ‘NOT’, respectively.

There are several things to note about these logical operators. Most obviously, two of them are composed of double symbols: **||** and **&&**. Don’t use the single symbol **|** and **&**. These single symbols also have a meaning. They are bitwise operators, which we would examine in Chapter 21.

The first two operators, **&&** and **||**, allow two or more conditions to be combined in an **if** statement. Let us see how they are used in a program. Consider the following example:

**Example 4.1:** The marks obtained by a student in 5 different subjects are input through the keyboard. The student gets a division as per the following rules:

Percentage above or equal to 60 - First division Percentage between 50 and 59 - Second division Percentage between 40 and 49 - Third division Percentage less than 40 - Fail

Write a program to calculate the division obtained by the student.

There are two ways in which we can write a program for this example. These methods are given below.

/\* Method – I \*/ # include <stdio.h> int main( ) { int m1, m2, m3, m4, m5, per ; printf ( "Enter marks in five subjects " ) ;

### W

scanf ( "%d %d %d %d %d", &m1, &m2, &m3, &m4, &m5 ) ; per = ( m1 + m2 + m3 + m4 + m5 ) \* 100 / 500 ; if ( per >= 60 ) printf ( "First division\\n" ) ; else { if ( per >= 50 ) printf ( "Second division\\n" ) ; else { if ( per >= 40 ) printf ( "Third division\\n" ) ; else printf ( "Fail\\n" ) ; } } return 0 ; }

This is a straight-forward program. Observe that the program uses nested **if-else**s. Though the program works fine, it has three disadvantages:

- As the number of conditions go on increasing the level of indentation also goes on increasing. As a result, the whole program creeps to the right. So much so that entire program is not visible on the screen. So if something goes wrong with the program locating what is wrong where becomes difficult.

- Care needs to be exercised to match the corresponding **if**s and **else**s.

- Care needs to be exercised to match the corresponding pair of braces.

All these three problems can be eliminated by usage of ‘Logical Operators’. The following program illustrates this:

/\* Method – II \*/ # include <stdio.h> int main( ) {

int m1, m2, m3, m4, m5, per ; printf ( "Enter marks in five subjects " ) ; scanf ( "%d %d %d %d %d", &m1, &m2, &m3, &m4, &m5 ) ; per = ( m1 + m2 + m3 + m4 + m5 ) / 500 \* 100 ; if ( per >= 60 ) printf ( "First division\\n" ) ; if ( ( per >= 50 ) && ( per < 60 ) ) printf ( "Second division\\n" ) ; if ( ( per >= 40 ) && ( per < 50 ) ) printf ( "Third division\\n" ) ; if ( per < 40 ) printf ( "Fail\\n" ) ; return 0 ; }

As can be seen from the second **if** statement, the **&&** operator is used to combine two conditions. ‘Second division’ gets printed if both the conditions evaluate to true. If one of the conditions evaluate to false then the whole thing is treated as false.

Two distinct advantages can be cited in favor of this program:

- The matching (or do I say mismatching) of the **if**s with their corresponding **else**s gets avoided, since there are no **else**s in this program.

- In spite of using several conditions, the program doesn't creep to the right. In the previous program the statements went on creeping to the right. This effect becomes more pronounced as the number of conditions goes on increasing. This would make the task of matching the **if**s with their corresponding **else**s and matching of opening and closing braces much more difficult.

There is a negative side to the program too. Even if the first condition turns out to be true, still all other conditions are checked. This will

increase the time of execution of the program. This can be avoided using the **else if** clause discussed in the next section.

### The _else if_ Clause

There is one more way in which we can write program for Example 4.1. This involves usage of **else if** blocks as shown below.

/\* else if ladder demo \*/ # include <stdio.h> int main( ) { int m1, m2, m3, m4, m5, per ; per = ( m1+ m2 + m3 + m4+ m5 ) / 500 \* 100 ; if ( per >= 60 ) printf ( "First division\\n" ) ; else if ( per >= 50 ) printf ( "Second division\\n" ) ; else if ( per >= 40 ) printf ( "Third division\\n" ) ; else printf ( "fail\\n" ) ; return 0 ; }

You can note that this program reduces the indentation of the statements. In this case, every **else** is associated with its previous **if**. The last **else** goes to work only if all the conditions fail. Also, if a condition is satisfied, other conditions below it are not checked. Even in **else if** ladder, the last **else** is optional.

Note that the **else if** clause is nothing different. It is just a way of rearranging the **else** with the **if** that follows it. This would be evident if you look at the following code:

/\* code using ifs \*/ if ( i == 2 ) printf ( "With you…" ) ; else {

if ( j == 2 ) printf ( "…All the time" ) ; }

/\* code using if - else if - else \*/ if ( i == 2 ) printf ( "With you…" ) ; else if ( j == 2 ) printf ( "…All the time " ) ;

Another place where logical operators are useful is when we want to write programs for complicated logics that ultimately boil down to only two answers. For example, consider the following example:

**Example 4.2:** A company insures its drivers in the following cases:

 If the driver is married.

 If the driver is unmarried, male & above 30 years of age.

 If the driver is unmarried, female & above 25 years of age.

In all other cases, the driver is not insured. If the marital status, sex and age of the driver are the inputs, write a program to determine whether the driver should be insured or not.

Here after checking a complicated set of instructions the final output of the program would be one of the two—either the driver should be insured or the driver should not be insured. As mentioned above, since these are the only two outcomes this problem can be solved using logical operators. But before we do that, let us write a program that does not make use of logical operators.

/\* Insurance of driver - without using logical operators \*/ # include <stdio.h> int main( ) { char sex, ms ; int age ; printf ( "Enter age, sex, marital status " ) ; scanf ( "%d %c %c", &age, &sex, &ms ) ; if ( ms == 'M' ) printf ( "Driver should be insured\\n" ) ;

else { if ( sex == 'M' ) { if ( age > 30 ) printf ( "Driver should be insured\\n" ) ; else printf ( "Driver should not be insured\\n" ) ; } else { if ( age > 25 ) printf ( "Driver should be insured\\n" ) ; else printf ( "Driver should not be insured\\n" ) ; } } return 0 ; }

From the program it is evident that we are required to match several **if**s and **else**s and several pairs of braces. In a more real-life situation there would be more conditions to check leading to the program creeping to the right. Let us now see how to avoid these problems by using logical operators.

As mentioned above, in this example, we expect the answer to be either ‘Driver should be insured’ or ‘Driver should not be insured’. If we list down all those cases in which the driver is insured, then they would be:

- Driver is married.

- Driver is an unmarried male above 30 years of age.

- Driver is an unmarried female above 25 years of age.

Since all these cases lead to the driver being insured, they can be combined together using **&&** and **||** as shown in the program below.

/\* Insurance of driver - using logical operators \*/ # include <stdio.h> int main( ) { char sex, ms ;

int age ; printf ( "Enter age, sex, marital status " ) ; scanf ( "%d %c %c", &age, &sex, &ms ) ; if ( ( ms == 'M') || ( ms == 'U' && sex == 'M' && age > 30 ) || ( ms == 'U' && sex == 'F' && age > 25 ) ) printf ( "Driver should be insured\\n" ) ; else printf ( "Driver should not be insured\\n" ) ; return 0 ; }

In this program, it is important to note that:

 The driver will be insured only if one of the conditions enclosed in parentheses evaluates to true.

 For the second pair of parentheses to evaluate to true, each condition in the parentheses separated by && must evaluate to true.

 Even if one of the conditions in the second parentheses evaluates to false, then the whole of the second parentheses evaluates to false.

 The last two of the above arguments apply to third pair of parentheses as well.

Thus, we can conclude that the **&&** and **||** are useful in the following programming situations:

- When it is to be checked in which range does a value fall.

- When after testing several conditions, the outcome is only one of the two answers. (This problem is often called yes/no problem).

In some programming situations we may combine the usage of **if— else if—else** and logical operators. This is demonstrated in the following program.

**Example 4.3:** Write a program to calculate the salary as per the following table:

### Gender Years of Service Qualifications Salary

Male >= 10 Post-Graduate 15000

\>= 10 Graduate 10000

< 10 Post-Graduate 10000

< 10 Graduate 7000

Female >= 10 Post-Graduate 12000

\>= 10 Graduate 9000

< 10 Post-Graduate 10000

< 10 Graduate 6000

Figure 4.1

\# include <stdio.h> int main( ) { char g ; int yos, qual, sal = 0 ; printf ( "Enter Gender, Years of Service and Qualifications ( 0 = G, 1 = PG ):" ) ; scanf ( "%c%d%d", &g, &yos, &qual ) ; if ( g == 'm' && yos >= 10 && qual == 1 ) sal = 15000 ; else if ( ( g == 'm' && yos >= 10 && qual == 0 ) || ( g == 'm' && yos < 10 && qual == 1 ) ) sal = 10000 ; else if ( g == 'm' && yos < 10 && qual == 0 ) sal = 7000 ; else if ( g == 'f' && yos >= 10 && qual == 1 ) sal = 12000 ; else if ( g == 'f' && yos >= 10 && qual == 0 ) sal = 9000 ; else if ( g == 'f' && yos < 10 && qual == 1 ) sal = 10000 ; else if ( g == 'f' && yos < 10 && qual == 0 ) sal = 6000 ;

printf ( "\\nSalary of Employee = %d\\n", sal ) ; return 0 ; }

I hope you can follow the implementation of this program on your own.

### The ! Operator

So far we have used only the logical operators **&&** and **||**. The third logical operator is the NOT operator, written as **!**. This operator reverses the result of the expression it operates on. For example, if the expression evaluates to a non-zero value, then applying **!** operator to it results into a 0. Vice versa, if the expression evaluates to zero then on applying **!** operator to it makes it 1, a non-zero value. The final result (after applying **!**) 0 or 1 is considered to be false or true, respectively. Here is an example of the NOT operator applied to a relational expression.

! ( y < 10 )

This means ‘not **y** less than 10’. In other words, if **y** is less than 10, the expression will be false, since **(** **y < 10 )** is true. We can express the same condition as **(** **y >= 10 )**.

The NOT operator is often used to reverse the logical value of a single variable, as in the expression

if ( ! flag )

This is another way of saying:

if ( flag == 0 )

Does the NOT operator sound confusing? Avoid it if you want, as the same thing can be achieved without using the NOT operator.

### Hierarchy of Operators Revisited

Since we have now added the logical operators to the list of operators we know, it is time to review these operators and their priorities. Figure 4.2 summarizes the operators we have seen so far. The higher the position of an operator is in the table, higher is its priority. (A full- fledged precedence table of operators is given in Appendix B.)

### Operators

! \* / % + - < > <= >= == != && || =

### Type

Logical NOT Arithmetic and modulus Arithmetic Relational Relational Logical AND Logical OR Assignment

Figure 4.2

**A Word of Caution** Can you guess what will be the output of the following program?

\# include <stdio.h> int main( ) { int i ; printf ( "Enter value of i " ) ; scanf ( "%d", &i ) ; if ( i = 5 ) printf ( "You entered 5\\n" ) ; else printf ( "You entered something other than 5\\n" ) ; return 0 ; }

Well, here is the output of two runs of this program...

Enter value of i 200 You entered 5 Enter value of i 9999 You entered 5

Surprised? You have entered 200 and 9999, and still you find in either case the output is ‘You entered 5’. This is because we have written the condition wrongly. We have used the assignment operator **\=** instead of the relational operator **==**. As a result, the condition gets reduced to **if (**

**5 )**, irrespective of what you supply as the value of **i**. And remember that in C, ‘truth’ is always non-zero, whereas, ‘falsity’ is always zero. Therefore, **if ( 5 )** always evaluates to true and hence the result.

Another common mistake while using the **if** statement is to write a semicolon (**;**) after the condition, as shown below.

\# include <stdio.h> int main( ) { int i ; printf ( "Enter value of i " ) ; scanf ( "%d", &i ) ; if ( i == 5 ) ; printf ( "You entered 5\\n" ) ; return 0 ; }

The ; makes the compiler to interpret the statement as if you have written it in following manner:

if ( i == 5 ) ; printf ( "You entered 5\\n" ) ;

Here, if the condition evaluates to true, the ; (null statement, which does nothing on execution) gets executed, following which the **printf( )** gets executed. If the condition fails, then straightaway the **printf( )** gets executed. So, irrespective of whether the condition evaluates to true or false, **printf( )** is bound to get executed. Remember that compiler would not point out this as an error, since as far as the syntax is concerned, nothing has gone wrong, but the logic has certainly gone awry. Moral is, beware of such pitfalls.

The following figure summarizes the working of all the three logical operators.

### Operands Results

### x y !x !y x && y x || y

0 0 1 1 0 0

0 non-zero 1 0 0 1

non-zero 0 0 1 0 1

non-zero non-zero 0 0 1 1

Figure 4.3

**The Conditional Operators** The conditional operators **?** and **:** are sometimes called ternary operators since they take three arguments. In fact, they form a kind of foreshortened if-then-else. Their general form is,

expression 1 ? expression 2 : expression 3

What this expression says is: “if **expression 1** is true (that is, if its value is non-zero), then the value returned will be **expression 2**, otherwise the value returned will be **expression 3**”. Let us understand this with the help of a few examples.

- int x, y ; scanf ( "%d", &x ) ; y = ( x > 5 ? 3 : 4 ) ;

This statement will store 3 in **y** if **x** is greater than 5, otherwise it will store 4 in y.

The equivalent **if-else** form would be,

if ( x > 5 ) y = 3 ; else y = 4 ;

- char a ; int y ; scanf ( "%c", &a ) ; y = ( a >= 65 && a <= 90 ? 1 : 0 ) ;

Here 1 would be assigned to **y** if **a >=65 && a <=90** evaluates to true, otherwise 0 would be assigned.

The following points may be noted about the conditional operators:

- It’s not necessary that the conditional operators should be used only in arithmetic statements. This is illustrated in the following examples:

Ex.: int i ; scanf ( "%d", &i ) ; ( i == 1 ? printf ( "Amit" ) : printf ( "All and sundry" ) ) ; Ex.: char a = 'z' ; printf ( "%c", ( a >= 'a' ? a : '!' ) ) ;

- The conditional operators can be nested as shown below.

int big, a, b, c ; big = ( a > b ? ( a > c ? 3: 4 ) : ( b > c ? 6: 8 ) ) ;

- Check out the following conditional expression:

a > b ? g = a : g = b ;

This will give you an error ‘Lvalue Required’. The error can be overcome by enclosing the statement in the **:** part within a pair of parentheses. This is shown below.

a > b ? g = a : ( g = b ) ;

In absence of parentheses, the compiler believes that **b** is being assigned to the result of the expression to the left of second **\=**. Hence it reports an error.

The limitation of the conditional operators is that after the **?** or after the **:** , only one C statement can occur. In practice, rarely does this requirement exist. Therefore, in serious C programming, conditional operators aren’t as frequently used as the **if-else**.

### Summary

- If the outcome of an if-else ladder is only one of two answers then the ladder should be replaced either with an else-if clause or by logical operators.

- **&&** and **||** are binary operators, whereas, **!** is a unary operator.

- In C every test expression is evaluated in terms of zero and non- zero values. A zero value is considered to be false and a non-zero value is considered to be true.

- Conditional operators can be used as an alternative to if-else statement if there is a single statement in the ‘if block’ and a single statement in the ‘else block’.

- Assignment statements used with conditional operators must be enclosed within a pair of parentheses.

### Exe**r**cise

**\[A\]** If a = 10, b = 12, c = 0, find the values of the expressions in the following table:

### Expression

a != 6 && b > 5 a == 9 || b < 3 ! ( a < 10 ) ! ( a > 5 && c ) 5 && c != 8 || !c

### Value

1

**\[B\]** What will be the output of the following programs:

- # include <stdio.h> int main( ) { int i = 4, z = 12 ; if ( i = 5 || z > 50 ) printf ( "Dean of students affairs\\n" ) ; else printf ( "Dosa\\n" ) ;

return 0 ; }

- #include <stdio.h> int main( ) { int i = 4, j = -1, k = 0, w, x, y, z ; w = i || j || k ; x = i && j && k ; y = i || j && k ; z = i && j || k ; printf ( "w = %d x = %d y = %d z = %d\\n", w, x, y, z ) ; return 0 ; }

- # include <stdio.h> int main( ) { int x = 20, y = 40, z = 45 ; if ( x > y && x > z ) printf ( "biggest = %d\\n", x ) ; else if ( y > x && y > z ) printf ( "biggest = %d\\n", y ) ; else if ( z > x && z > y ) printf ( "biggest = %d\\n", z ) ; return 0 ; }

- # include <stdio.h> int main( ) { int i = -1, j = 1, k, l ; k = !i && j ; l = !i || j ; printf ( "%d %d\\n", i, j ) ; return 0 ; }

- # include <stdio.h> int main( ) { int i = -4, j, num ; j = ( num < 0 ? 0 : num \* num ) ;

printf ( "%d\\n", j ) ; return 0 ; }

- # include <stdio.h> int main( ) { int k, num = 30 ; k = ( num > 5 ? ( num <= 10 ? 100 : 200 ) : 500 ) ; printf ( "%d\\n", num ) ; return 0 ; }

**\[C\]** Point out the errors, if any, in the following programs:

- # include <stdio.h> int main( ) { int code, flag ; if ( code == 1 & flag == 0 ) printf ( "The eagle has landed\\n" ) ; return 0 ; }

- # include <stdio.h> int main( ) { char spy = 'a', password = 'z' ; if ( spy == 'a' or password == 'z' ) printf ( "All the birds are safe in the nest\\n" ) ; return 0 ; }

- # include <stdio.h> int main( ) { int i = 10, j = 20 ; if ( i = 5 ) && if ( j = 10 ) printf ( "Have a nice day\\n" ) ; return 0 ; }

- # include <stdio.h> int main( )

{ int x = 10, y = 20 ; if ( x >= 2 and y <= 50 ) printf ( "%d\\n", x ) ; return 0 ; }

- # include <stdio.h> int main( ) { int x = 2 ; if ( x == 2 && x != 0 ) ; printf ( "Hello\\n" ) ; else printf ( "Bye\\n" ) ; return 0 ; }

- # include <stdio.h> int main( ) { int i = 10, j = 10 ; if ( i && j == 10 ) printf ( "Have a nice day\\n" ) ; return 0 ;

}

- # include <stdio.h> int main( ) { int j = 65 ; printf ( "j >= 65 ? %d : %c\\n", j ) ; return 0 ; }

- # include <stdio.h> int main( ) { int i = 10, j ; i >= 5 ? j = 10 : j = 15 ; printf ( "%d %d\\n", i, j ) ; return 0 ; }

- # include <stdio.h> int main( ) { int a = 5, b = 6 ; ( a == b ? printf ( "%d\\n", a ) ) ; return 0 ; }

- # include <stdio.h> int main( ) { int n = 9 ; ( n == 9 ? printf ( "Correct\\n" ) ; : printf ( "Wrong\\n" ) ; ) ; return 0 ; }

**\[D\]** Attempt the following:

- Any year is entered through the keyboard, write a program to determine whether the year is leap or not. Use the logical operators **&&** and **||**.

- Any character is entered through the keyboard, write a program to determine whether the character entered is a capital letter, a small case letter, a digit or a special symbol.

The following table shows the range of ASCII values for various characters:

### Characters

A – Z a – z 0 – 9 special symbols

### ASCII Values

65 – 90 97 – 122 48 – 57 0 - 47, 58 - 64, 91 - 96, 123 - 127

- A certain grade of steel is graded according to the following conditions:

- Hardness must be greater than 50 (ii) Carbon content must be less than 0.7 (iii) Tensile strength must be greater than 5600

The grades are as follows:

Grade is 10 if all three conditions are met Grade is 9 if conditions (i) and (ii) are met Grade is 8 if conditions (ii) and (iii) are met Grade is 7 if conditions (i) and (iii) are met Grade is 6 if only one condition is met Grade is 5 if none of the conditions are met

Write a program, which will require the user to give values of hardness, carbon content and tensile strength of the steel under consideration and output the grade of the steel.

- If the three sides of a triangle are entered through the keyboard, write a program to check whether the triangle is valid or not. The triangle is valid if the sum of two sides is greater than the largest of the three sides.

- If the three sides of a triangle are entered through the keyboard, write a program to check whether the triangle is isosceles, equilateral, scalene or right angled triangle.

- In boxing the weight class of a boxer is decided as per the following table. Write a program that receives weight as input and prints out the boxer’s weight class.

### Boxer Class

Flyweight Bantamweight Featherweight Middleweight Heavyweight

### Weight in Pounds

< 115 115 - 121 122 - 153 154 – 189 >= 190

- In digital world colors are specified in Red-Green-Blue (RGB) format, with values of R, G, B varying on an integer scale from 0 to 255. In print publishing the colors are mentioned in Cyan-Magenta-Yellow- Black (CMYK) format, with values of C, M, Y, and K varying on a real scale from 0.0 to 1.0. Write a program that converts RGB color to CMYK color as per the following formulae:

 255/,255/,255/Re _BlueGreendMaxWhite_ 

Note that if the RGB values are all 0, then the CMY values are all 0 and the K value is 1.

- Write a program that receives month and date of birth as input and prints the corresponding Zodiac sign based on the following table:

### Sun Sign

Capricorn Aquarius Pisces Aries Taurus Gemini Cancer Leo Virgo Libra Scorpio Sagittarius

### From - To

December 22 - January 19 January 20 - February 17 February 18 - March 19 March 20 - April 19 April 20 - May 20 May 21 - June 20 June 21 - July 22 July 23 - August 22 August 23 - September 22 September 23 - October 22 October 23 - November 21 November 22 - December 21

- The Body Mass Index (BMI) is defined as ratio of the weight of a person (in kilograms) to the square of the height (in meters). Write a program that receives weight and height, calculates the BMI, and reports the BMI category as per the following table:

 

  

  

_White_

_dWhite Cyan_

255/Re

 

  

  

_White_

_GreenWhite Magenta_

255/

 

  

  

_White_

_BlueWhite Yellow_

255/

_WhiteBlack_ 1

### BMI Category

Starvation Anorexic Underweight Ideal Overweight Obese Morbidly Obese

### BMI

< 15 15.1 to 17.5 17.6 to 18.5 18.6 to 24.9 25 to 25.9 30 to 30.9 >= 40

**\[E\]** Attempt the following:

- Using conditional operators determine:

(1) Whether the character entered through the keyboard is a lower case alphabet or not.

(2) Whether a character entered through the keyboard is a special symbol or not.

- Write a program using conditional operators to determine whether a year entered through the keyboard is a leap year or not.

- Write a program to find the greatest of the three numbers entered through the keyboard. Use conditional operators.

- Write a program to receive value of an angle in degrees and check whether sum of squares of sine and cosine of this angle is equal to 1.

- Rewrite the following program using conditional operators.

\# include <stdio.h> int main( ) { float sal ; printf ( "Enter the salary" ) ; scanf ( "%f", &sal ) ; if ( sal >= 25000 && sal <= 40000 ) printf ( "Manager\\n" ) ; else if ( sal >= 15000 && sal < 25000 ) printf ( "Accountant\\n" ) ;

else printf ( "Clerk\\n" ) ; return 0 ; }

