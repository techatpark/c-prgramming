---
title: 'C Instructions'
weight: 2
---

   

program is nothing but a set of instructions. The program behaves as per the instructions that we give in it. Different instructions help

us achieve different tasks in a program. In the last chapter we saw how to write simple C programs. In these programs knowingly or unknowingly we have used instructions to achieve the intended purpose of the program. In this chapter we would explore the instructions that we have used in these programs.

**Types of Instructions** There are basically three types of instructions in C:

- Type Declaration Instruction – This instruction is used to declare the type of variables used in a C program.

- Arithmetic Instruction – This instruction is used to perform arithmetic operations on constants and variables.

- Control Instruction – This instruction is used to control the sequence of execution of various statements in a C program.

Since, the elementary C programs would usually contain only the type declaration and the arithmetic instructions; we would discuss only these two instructions at this stage. The control instruction would be discussed in detail in the subsequent chapters.

**Type Declaration Instruction** This instruction is used to declare the type of variables being used in the program. Any variable used in the program must be declared before using it in any statement. The type declaration statement is written at the beginning of **main( )** function.

Ex.: int bas ; float rs, grosssal ; char name, code ;

There are several subtle variations of the type declaration instruction. These are discussed below:

- While declaring the type of variable we can also initialize it as shown below.

int i = 10, j = 25 ; float a = 1.5, b = 1.99 + 2.4 \* 1.44 ;

A

- The order in which we define the variables is sometimes important sometimes not. For example,

int i = 10, j = 25 ;

is same as

int j = 25, i = 10 ;

However,

float a = 1.5, b = a + 3.1 ;

is alright, but

float b = a + 3.1, a = 1.5 ;

is not. This is because here we are trying to use **a** before defining it.

- The following statements would work

int a, b, c, d ; a = b = c = 10 ;

However, the following statement would not work

int a = b = c = d = 10 ;

Once again we are trying to use **b** (to assign to **a**) before defining it.

**Arithmetic Instruction** A C arithmetic instruction consists of a variable name on the left hand side of = and variable names and constants on the right hand side of =. The variables and constants appearing on the right hand side of = are connected by arithmetic operators like **+, -, \*,** and **/**.

Ex.: int ad ; float kot, deta, alpha, beta, gamma ; ad = 3200 ; kot = 0.0056 ; deta = alpha \* beta / gamma + 3.2 \* 2 / 5 ;

Here,

**\*, /, -, +** are the arithmetic operators.

**\=** is the assignment operator.

2, 5 and 3200 are integer constants.

3.2 and 0.0056 are real constants.

**ad** is an integer variable.

**kot, deta, alpha, beta, gamma** are real variables.

The variables and constants together are called ‘operands’. While executing an arithmetic statement the operands on right hand side are operated upon by the ‘arithmetic operators’ and the result is then assigned, using the assignment operator, to the variable on left-hand side.

A C arithmetic statement could be of three types. These are as follows:

- Integer mode arithmetic statement – In this statement all operands are either integer variables or integer constants.

Ex.: int i, king, issac, noteit ; i = i + 1 ; king = issac \* 234 + noteit - 7689 ;

- Real mode arithmetic statement – In this statement all operands are either real constants or real variables.

Ex.: float qbee, antink, si, prin, anoy, roi ; qbee = antink + 23.123 / 4.5 \* 0.3442 ; si = prin \* anoy \* roi / 100.0 ;

- Mixed mode arithmetic statement – In this statement some operands are integers and some operands are real.

Ex.: float si, prin, anoy, roi, avg ; int a, b, c, num ; si = prin \* anoy \* roi / 100.0 ; avg = ( a + b + c + num ) / 4 ;

Though Arithmetic instructions look simple to use, one often commits mistakes in writing them. Let us take a closer look at these statements. Note the following points carefully:

- C allows only one variable on left-hand side of **\=**. That is, **z = k \* l** is legal, whereas **k \* l = z** is illegal.

- In addition to the division operator C also provides a modular division operator. This operator returns the remainder on dividing one integer with another. Thus the expression 10 / 2 yields 5, whereas, 10 % 2 yields 0. Note that the modulus operator (**%**) cannot be applied on a float. Also note that on using % the sign of the remainder is always same as the sign of the numerator. Thus -5 % 2 yields –1, whereas, 5 % -2 yields 1.

- An arithmetic instruction is at times used for storing character constants in character variables.

char a, b, d ; a = 'F' ; b = 'G' ; d = '+' ;

When we do this, the ASCII values of the characters are stored in the variables. ASCII codes are used to represent any character in memory. For example, ASCII codes of ‘F’ and ‘G’ are 01000110 and 01000111. ASCII values are nothing but the decimal equivalent of ASCII codes. Thus ASCII values of ‘F’ and ‘G’ are 70 and 71.

- Arithmetic operations can be performed on **int**s, **float**s and **char**s.

Thus the statements,

char x, y ; int z ; x = 'a' ; y = 'b' ; z = x + y ;

are perfectly valid, since the addition is performed on the ASCII values of the characters and not on characters themselves. The ASCII values of ‘a’ and ‘b’ are 97 and 98, and hence can definitely be added.

- No operator is assumed to be present. It must be written explicitly. In the following example, the multiplication operator after b must be explicitly written.

a = c.d.b(xy) usual arithmetic statement a = c \* d \* b \* ( x \* y ) C statement

- There is no operator in C to perform exponentiation operation. Exponentiation has to be carried out as shown below:

\# include <math.h> # include <stdio.h> int main( ) { float a ; a = pow ( 3.0, 2.0 ) ; printf ( "%f", a ) ; }

Here **pow( )** function is a standard library function. It is being used to raise 3.0 to the power of 2.0. The **pow( )** function works only with real numbers, hence we have used 3.0 and 2.0 instead of 3 and 2.

**#include <math.h>** is a preprocessor directive. It is being used here to ensure that the **pow( )** function works correctly. We would learn more about standard library functions in Chapter 6 and about preprocessor in Chapter 8.

You can explore other mathematical functions like **abs( )**, **sqrt( )**, **sin( )**, **cos( )**, **tan( )**, etc., declared in **math.h** on your own.

**Integer and Float Conversions** In order to effectively develop C programs, it will be necessary to understand the rules that are used for the implicit conversion of floating point and integer values in C. These are mentioned below. Note them carefully.

- An arithmetic operation between an integer and integer always yields an integer result.

- An operation between a real and real always yields a real result.

- An operation between an integer and real always yields a real result. In this operation the integer is first promoted to a real and then the operation is performed. Hence the result is real.

I think a few practical examples shown in Figure 2.1 would put the issue beyond doubt.

### Operation Result Operation Result

5 / 2 5.0 / 2 5 / 2.0 5.0 / 2.0

2 2.5 2.5 2.5

2 / 5 2.0 / 5 2 / 5.0 2.0 / 5.0

0 0.4 0.4 0.4

Figure 2.1

**Type Conversion in Assignments** It may so happen that the type of the expression on right hand side and the type of the variable on the left-hand side of an assignment operator may not be same. In such a case, the value of the expression is promoted or demoted depending on the type of the variable on left- hand side of =.

For example, consider the following assignment statements.

int i ; float b ; i = 3.5 ; b = 30 ;

Here in the first assignment statement, though the expression’s value is a **float** (3.5), it cannot be stored in **i** since it is an **int**. In such a case, the **float** is demoted to an **int** and then its value is stored. Hence what gets stored in **i** is 3. Exactly opposite happens in the next statement. Here, 30 is promoted to 30.0 and then stored in **b**, since **b** being a **float** variable cannot hold anything except a **float** value.

Instead of a simple expression used in the above examples, if a complex expression occurs, still the same rules apply. For example, consider the following program fragment.

float a, b, c ; int s ;

s = a \* b \* c / 100 + 32 / 4 - 3 \* 1.1 ;

Here, in the assignment statement, some operands are **int**s whereas others are **float**s. As we know, during evaluation of the expression, the **int**s would be promoted to **float**s and the result of the expression would be a **float**. But when this **float** value is assigned to **s** it is again demoted to an **int** and then stored in **s**.

Observe the results of the arithmetic statements shown in Figure 2.2. It has been assumed that **k** is an integer variable and **a** is a real variable.

### Arithmetic Instruction Result Arithmetic Instruction Result

k = 2 / 9 k = 2.0 / 9 k = 2 / 9.0 k = 2.0 / 9.0 k = 9 / 2 k = 9.0 / 2 k = 9 / 2.0 k = 9.0 / 2.0

0 0 0 0 4 4 4 4

a = 2 / 9 a = 2.0 / 9 a = 2 / 9.0 a = 2.0 / 9.0 a = 9 / 2 a = 9.0 / 2 a = 9 / 2.0 a = 9.0 / 2.0

0.0 0.222222 0.222222 0.222222 4.0 4.5 4.5 4.5

Figure 2.2

Note that though the following statements give the same result, 0, the results are obtained differently.

k = 2 / 9 ; k = 2.0 / 9 ;

In the first statement, since both 2 and 9 are integers, the result is an integer, i.e. 0. This 0 is then assigned to **k**. In the second statement 9 is promoted to 9.0 and then the division is performed. Division yields 0.222222. However, this cannot be stored in **k**, **k** being an **int**. Hence it gets demoted to 0 and then stored in **k**.

**Hierarchy of Operations** While executing an arithmetic statement that has multiple operators, there might be some issues about their evaluation. For example, does the expression 2 \* x - 3 \* y correspond to (2x)-(3y) or to 2(x-3y)? Similarly, does A / B \* C correspond to A / (B \* C) or to (A / B) \* C? To answer these questions satisfactorily, one has to understand the ‘hierarchy’ of operations. The priority or precedence in which the

operations in an arithmetic statement are performed is called the hierarchy of operations. The hierarchy of commonly used operators is shown in Figure 2.3.

### Priority Operators Description

1st 2nd 3rd

\* / % + - =

Multiplication, Division, Modular division Addition, Subtraction Assignment

Figure 2.3

Now a few tips about usage of operators in general.

- Within parentheses the same hierarchy as mentioned in Figure 2.3 is operative. Also, if there are more than one set of parentheses, the operations within the innermost parentheses would be performed first, followed by the operations within the second innermost pair and so on.

- We must always remember to use pairs of parentheses. A careless imbalance of the right and left parentheses is a common error. Best way to avoid this error is to type ( ) and then type an expression inside it.

A few examples would clarify the issue further.

**Example 2.1:** Determine the hierarchy of operations and evaluate the following expression, assuming that **i** is an integer variable:

i = 2 \* 3 / 4 + 4 / 4 + 8 - 2 + 5 / 8

Stepwise evaluation of this expression is shown below:

i = 2 \* 3 / 4 + 4 / 4 + 8 - 2 + 5 / 8 i = 6 / 4 + 4 / 4 + 8 - 2 + 5 / 8 operation: \* i = 1 + 4 / 4 + 8 - 2 + 5 / 8 operation: / i = 1 + 1+ 8 - 2 + 5 / 8 operation: / i = 1 + 1 + 8 - 2 + 0 operation: / i = 2 + 8 - 2 + 0 operation: + i = 10 - 2 + 0 operation: + i = 8 + 0 operation : - i = 8 operation: +

Note that 6 / 4 gives 1 and not 1.5. This so happens because 6 and 4 both are integers and therefore 6 / 4 must evaluate to an integer. Similarly 5 / 8 evaluates to zero, since 5 and 8 are integers and hence 5 / 8 must return an integer value.

**Example 2.2:** Determine the hierarchy of operations and evaluate the following expression, assuming that **kk** is a float variable:

kk = 3 / 2 \* 4 + 3 / 8

Stepwise evaluation of this expression is shown below:

kk = 3 / 2 \* 4 + 3 / 8 kk = 1 \* 4 + 3 / 8 operation: / kk = 4 + 3 / 8 operation: \* kk = 4 + 0 operation: / kk = 4 operation: +

Note that 3 / 8 gives zero, again for the same reason mentioned in the previous example.

All operators in C are ranked according to their precedence. And mind you, there are as many as 45 odd operators in C, and these can affect the evaluation of an expression in subtle and unexpected ways if we aren't careful. Unfortunately, there are no simple rules that one can follow, such as “BODMAS” that tells algebra students in which order does an expression evaluate. We have not encountered many out of these 45 operators, so we won’t pursue the subject of precedence any further here. However, it can be realized at this stage that it would be almost impossible to remember the precedence of all these operators. So a full-fledged list of all operators and their precedence is given in Appendix A. This may sound daunting, but when its contents are absorbed in small bites, it becomes more palatable.

So far we have seen how arithmetic statements written in C are evaluated. But our knowledge would be incomplete unless we know how to convert a general algebraic expression to a C statement. C can handle any complex algebraic expressions with ease. Some examples of algebraic expressions and their equivalent C expressions are shown in Figure 2.4.

### Algebraic Expression C Expression

a x b - c x d ( m + n ) ( a + b ) 3x2 + 2x + 5

a \* b - c \* d ( m + n ) \* ( a + b ) 3 \* x \* x + 2 \* x + 5 ( a + b + c ) / ( d + e )

2 \* b \* y / ( d + 1 ) - x / 3 \* ( z + y ) _ed_

_cba_





 

  



 

 )(31

2

_yz_

_x_

_d_

_BY_

Figure 2.4

**Associativity of Operators** When an expression contains two operators of equal priority the tie between them is settled using the associativity of the operators. All operators in C have either Left to Right associativity or Right to Left associativity. Let us understand this with the help of a few examples.

Consider the expression a = 3 / 2 \* 5 ;

Here there is a tie between operators of same priority, that is between / and \*. This tie is settled using the associativity of / and \*. Both enjoy Left to Right associativity. Therefore firstly / operation is done followed by \*.

Consider one more expression.

a = b = 3 ;

Here both assignment operators have the same priority. So order of operations is decided using associativity of = operator. = associates from Right to Left. Therefore, second = is performed earlier than first =.

Consider yet another expression.

z = a \* b + c / d ;

Here **\*** and **/** enjoys same priority and same associativity (Left to Right). Compiler is free to perform **\*** or **/** operation as per its convenience, since no matter which is performed earlier, the result would be same.

Appendix B gives the associativity of all the operators available in C. Note that the precedence and associativity of all operators is predetermined and we cannot change it.

**Control Instructions** As the name suggests, the ‘Control Instructions’ enable us to specify the order in which the various instructions in a program are to be executed by the computer. In other words, the control instructions determine the ‘flow of control’ in a program. There are four types of control instructions in C. They are:

- Sequence Control Instruction

- Selection or Decision Control Instruction

- Repetition or Loop Control Instruction

- Case Control Instruction

The Sequence control instruction ensures that the instructions are executed in the same order in which they appear in the program. Decision and Case control instructions allow the computer to take a decision as to which instruction is to be executed next. The Loop control instruction helps computer to execute a group of statements repeatedly. In the following chapters we are going to discuss these instructions in detail.

### Summary

- Instructions in a program control the behavior/working of the program.

- A C program can contain three types of instructions—Type declaration instruction, Arithmetic instruction, Control instruction.

- An expression may contain any sequence of constants, variables and operators.

- An expression is evaluated based on the hierarchy or precedence of operators.

- Operators having equal precedence are evaluated using associativity of operators.

- Associativity of all operators is either left to right or right to left.

### Exercise

**\[A\]** Point out the errors, if any, in the following C statements:

- x = ( y + 3 ) ;

- cir = 2 \* 3.141593 \* r ;

- char = ‘3’ ;

- 4 / 3 \* 3.14 \* r \* r \* r = vol\_of\_sphere ;

- volume = a3 ;

- area = 1 / 2 \* base \* height ;

- si = p \* r \* n / 100 ;

- area of circle = 3.14 \* r \* r ;

- peri\_of\_tri = a + b + c ;

- slope = ( y2 – y1 ) ÷ ( x2 – x1 ) ;

- 3 = b = 4 = a ;

- count = count + 1 ;

(m) char ch = '25 Apr 12' ;

**\[B\]** Evaluate the following expressions and show their hierarchy.

- ans = 5 \* b \* b \* x - 3 \* a \* y \* y - 8 \* b \* b \* x + 10 \* a \* y ;

(a = 3, b = 2, x = 5, y = 4 assume **ans** to be an int)

- res = 4 \* a \* y / c - a \* y / c ;

(a = 4, y = 1, c = 3, assume **res** to be an int)

- s = c + a \* y \* y / b ;

(a = 2.2, b = 0.0, c = 4.1, y = 3.0, assume **s** to be an float)

- R = x \* x + 2 \* x + 1 / 2 \* x \* x + x + 1 ;

(x = 3.5, assume **R** to be an float) **\[C\]** Indicate the order in which the following expressions would be

evaluated:

- g = 10 / 5 /2 / 1 ;

- b = 3 / 2 + 5 \* 4 / 3 ;

- a = b = c = 3 + 4 ;

- x = 2 – 3 + 5 \* 2 / 8 % 3 ;

- z = 5 % 3 / 8 \* 3 + 4

- y = z = -3 % -8 / 2 + 7 ;

**\[D\]** Convert the following algebraic expressions into equivalent C statements:

(a)

(b)

(c)

(d)

**\[E\]** What will be the output of the following programs:

- # include <stdio.h> int main( ) { int i = 2, j = 3, k, l ; float a, b ; k = i / j \* j ; l = j / i \* i ; a = i / j \* j ; b = j / i \* i ; printf ( "%d %d %f %f\\n", k, l, a, b ) ; return 0 ; }

- # include <stdio.h> int main( ) { int a, b, c, d ; a = 2 % 5 ; b = -2 % 5 ; c = 2 % -5 ; d = -2 % -5 ; printf ( "a = %d b = %d c = %d d = %d\\n", a, b, c, d ) ;

) 5 y ( ) 4 y (

x) 3 x( Z

3



 

v g

) d c ( 6.22 2v R



 

7.7b ( xy + a ) / c - 0.8 + 2b A =

( x + a ) (1 / y )

_xx_

_x_

_x_

_x_

_x_

_x_

8

8

84

8

4

12 X

23



return 0 ; }

- # include <stdio.h> int main( ) { float a = 5, b = 2 ; int c, d ; c = a % b ; d = a / 2 ; printf ( "%d\\n", d ) ; return 0 ; }

- # include <stdio.h> int main( ) { printf ( "nn \\n\\n nn\\n" ) ; printf ( "nn /n/n nn/n" ) ; return 0 ; }

- # include <stdio.h> int main( ) { int a, b ; printf ( "Enter values of a and b" ) ; scanf ( " %d %d ", &a, &b ) ; printf ( "a = %d b = %d", a, b ) ; return 0 ; }

**\[F\]** State whether the following statements are True or False:

- \* or /, + or – represents the correct hierarchy of arithmetic operators in C.

- \[ \] and { } can be used in Arithmetic instructions.

- Hierarchy decides which operator is used first.

- In C, Arithmetic instruction cannot contain constants on left side of =.

- In C \*\* operator is used for exponentiation operation.

- % operator cannot be used with floats.

**\[G\]** Fill in the blanks:

- In y = 10 \* x / 2 + z ; operation will be performed first.

- If **a** is an integer variable, a = 11 / 2 ; will store in **a**.

- The expression, a = 22 / 7 \* 5 / 3 ; would evaluate to .

- The expression x = -7 % 2 - 8 would evaluate to .

- If **d** is a **float** the operation d = 2 / 7.0 would store in **d**.

**\[H\]** Attempt the following:

- If a five-digit number is input through the keyboard, write a program to calculate the sum of its digits. (Hint: Use the modulus operator ‘%’)

- If a five-digit number is input through the keyboard, write a program to reverse the number.

- If lengths of three sides of a triangle are input through the keyboard, write a program to find the area of the triangle.

- Write a program to receive Cartesian co-ordinates (x, y) of a point and convert them into polar co-ordinates (r, ).

Hint: r = sqrt ( x2 + y2 ) and tan-1 ( y / x )

- Write a program to receive values of latitude (L1, L2) and longitude (G1, G2), in degrees, of two places on the earth and output the distance (D) between them in nautical miles. The formula for distance in nautical miles is:

D = 3963 cos-1 ( sin L1 sin L2 + cos L1 cos L2 \* cos ( G2 – G1 ) )

- Wind chill factor is the felt air temperature on exposed skin due to wind. The wind chill temperature is always lower than the air temperature, and is calculated as per the following formula:

wcf = 35.74 + 0.6215t + ( 0.4275t - 35.75 ) \* v0.16

where t is the temperature and v is the wind velocity. Write a program to receive values of t and v and calculate wind chill factor (wcf).

- If value of an angle is input through the keyboard, write a program to print all its Trigonometric ratios.

- Two numbers are input through the keyboard into two locations C and D. Write a program to interchange the contents of C and D.

- Consider a currency system in which there are notes of seven denominations, namely, Re. 1, Rs. 2, Rs. 5, Rs. 10, Rs. 50, Rs. 100. If a sum of Rs. N is entered through the keyboard, write a program to compute the smallest number of notes that will combine to give Rs. N.

