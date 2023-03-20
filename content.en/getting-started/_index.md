---
title: 'Getting Started'
weight: 1
---

{{< highlight c >}}
#include <stdio.h>
int main() {
   // printf() displays the string inside quotation
   printf("Hello, World!");
   return 0;
}
{{< / highlight >}}


Before we can begin to write serious programs in C, it would be interesting to find out what really is C, how it came into existence and how does it compare with other programming languages. In this chapter, we would briefly outline these issues.

Four important aspects of any language are the way it stores data, the way it operates upon this data, how it accomplishes input and output, and how it lets you control the sequence of execution of instructions in a program. We would discuss the first three of these building blocks in this chapter.

### What is C?

C is a programming language developed at AT & T’s Bell Laboratories of USA in 1972. It was designed and written by a man named Dennis Ritchie. In the late seventies C began to replace the more familiar languages of that time like PL/I, ALGOL, etc. No one pushed C. It wasn’t made the ‘official’ Bell Labs language. Thus, without any advertisement, C’s reputation spread and its pool of users grew. Ritchie seems to have been rather surprised that so many programmers preferred C to older languages like FORTRAN or PL/I, or the newer ones like Pascal and APL. But, that’s what happened.

Possibly why C seems so popular is because it is reliable, simple and easy to use. Moreover, in an industry where newer languages, tools and technologies emerge and vanish day in and day out, a language that has survived for more than three decades has to be _really_ good.

An opinion that is often heard today is—“C has been already superseded by languages like C++, C# and Java, so why bother to learn C today”. I seriously beg to differ with this opinion. There are several reasons for this. These are as follows:

- C++, C# or Java make use of a principle called Object Oriented Programming (OOP) to organize the program. This organizing principle has lots of advantages to offer. But even while using this organizing principle you would still need a good hold over the language elements of C and the basic programming skills. So it makes more sense to first learn C and then migrate to C++, C# and Java. Though this two-step learning process may take more time, but at the end of it you will definitely find it worth the trouble.

- Major parts of popular operating systems like Windows, UNIX, Linux and Android are written in C. This is because even today when it comes to performance (speed of execution) nothing beats C. Moreover, if one is to extend the operating system to work with new devices one needs to write device driver programs. These programs are exclusively written in C.

- Mobile devices like Smartphones and Tablets have become rage of today. Also, common consumer devices like microwave ovens, washing machines and digital cameras are getting smarter by the day. This smartness comes from a microprocessor, an operating system and a program embedded in these devices. These programs not only have to run fast but also have to work in limited amount of memory. No wonder that such programs are written in C. With these constraints on time and space, C is the language of choice while building such operating systems and programs.

- You must have seen several professional 3D computer games where the user navigates some object, like say a spaceship and fires bullets at the invaders. The essence of all such games is speed. Needless to say, such games won’t become popular if they take a long time to move the spaceship or to fire a bullet. To match the expectations of the player the game has to react fast to the user inputs. This is where C language scores over other languages. Many popular gaming frameworks (like DirectX) have been built using C language.

- At times one is required to very closely interact with the hardware devices. Since C provides several language elements that make this interaction feasible without compromising the performance, it is the preferred choice of the programmer.

I hope that these are very convincing reasons why you should adopt C as the first, and a very important step, in your quest for learning programming.

### Getting Started with C

Communicating with a computer involves speaking the language the computer understands, which immediately rules out English as the language of communication with computer. However, there is a close analogy between learning English language and learning C language. The classical method of learning English is to first learn the alphabets used in the language, then learn to combine these alphabets to form words, which, in turn, are combined to form sentences and sentences are combined to form paragraphs.

Learning C is similar and easier. Instead of straight-away learning how to write programs, we must first know what alphabets, numbers and special symbols are used in C, then how using them, constants, variables and keywords are constructed, and finally, how are these combined to form an instruction. A group of instructions would be combined later on to form a program. This is illustrated in the Figure 1.1.

{{< diagram "w-50 h-75 d-inline-block float-start" "Steps in learning English Language" >}}

```goat
┌─────────┐
│Alphabets│
└────┬────┘
  ┌──▽──┐  
  │Words│  
  └──┬──┘  
┌────▽────┐
│Sentences│
└────┬────┘
┌────▽────┐
│Paragraph│
└─────────┘

```
{{< /diagram >}}

{{< diagram "w-50 vh-50" "Steps in learning C Language" >}}
```goat
  ┌─────────────────┐ 
  │Alphabets,Digits,│ 
  │Special symbols  │ 
  └────────┬────────┘ 
┌──────────▽─────────┐
│Constants,Variables,│
│Keywords            │
└──────────┬─────────┘
    ┌──────▽─────┐    
    │Instructions│    
    └──────┬─────┘    
       ┌───▽───┐      
       │Program│      
       └───────┘      

```
{{< /diagram >}}

### The C Character Set

A character denotes any alphabet, digit or special symbol used to represent information. 
| Character | Range |
| ----------- | ----------- |
| Alphabets          | A, B, ….., Y, Z a, b, ….., y, z |
| Digits             | 0, 1, 2, 3, 4, 5, 6, 7, 8, 9    |
| Special symbols    | ~ ‘ ! @ # % ^ & \* ( ) \_ - + = | \\ { } \[ \] : ; " ' < > , . ? / $ |

### Constants, Variables and Keywords

The alphabets, digits and special symbols when properly combined form constants, variables and keywords. Let us now understand the meaning of each of them. A constant is an entity that doesn’t change, whereas, a variable is an entity that may change. A keyword is a word that carries special meaning.

In any C program we typically do lots of calculations. The results of these calculations are stored in computer’s memory. Like human memory, the computer’s memory also consists of millions of cells. The calculated values are stored in these memory cells. To make the retrieval and usage of these values easy, these memory cells (also called memory locations) are given names. Since the value stored in each location may change, the names given to these locations are called variable names. Let us understand this with the help of an example.

Consider the memory locations shown in Figure 1.3. Here 3 is stored in a memory location and a name **x** is given to it. Then we have assigned a new value 5 to the same memory location **x**. This would overwrite the earlier value 3, since a memory location can hold only one value at a time.

3 5x x

Figure 1.3

Since the location whose name is **x** can hold different values at different times **x** is known as a variable (or a variable name). As against this, 3 or 5 do not change, hence are known as constants.

In programming languages, constants are often called literals, whereas, variables are called identifiers.

Now that we understand the constants and the variables, let us see what different types of constants and variables exist in C.

### Types of C Constants

C constants can be divided into two major categories:

```goat
                                          +-------------+                                                          
                             +----------- |  Constants  |-------------+                                            
                             |            +-------------+             |                                            
                             |                                        |                                            
                      +-------------+                          +-------------+                                     
                      |  Primary    |                          |  Secondary  |                                     
                      +-------------+                          +-------------+           
                             |                                        |
                             |                                        |                                            
                             |                                        |                                            
                             |                                        |                                            
                      +-------------+                           +-------------+                                    
                      |  Integer    |                           | Array       |                                    
                      |  Charactor  |                           | Pointer     |                                    
                      |  Real       |                           | Structure   |                                    
                      +-------------+                           | Union,      |                                    
                                                                | Enum etc    |                                    
                                                                +-------------+                                   -
                                                                                    
```

At this stage, we would restrict our discussion to only Primary constants, namely, Integer, Real and Character constants. Let us see the details of each of these constants. For constructing these different types of constants, certain rules have been laid down. These rules are as under:

### Rules for Constructing Integer Constants

- An integer constant must have at least one digit.

- It must not have a decimal point.

- It can be either positive or negative.

- If no sign precedes an integer constant, it is assumed to be positive.

- No commas or blanks are allowed within an integer constant.

- The allowable range for integer constants is -2147483648 to +2147483647.

Truly speaking, the range of an Integer constant depends upon the compiler. For compilers like Visual Studio, gcc, it is -2147483648 to +214748364, whereas for compilers like Turbo C or Turbo C++ the range is -32768 to +32767.

Ex.: 426 +782 -8000 -7605

### Rules for Constructing Real Constants

Real constants are often called Floating Point constants. The real constants could be written in two forms—Fractional form and Exponential form.

Following rules must be observed while constructing real constants expressed in fractional form:

- A real constant must have at least one digit.

- It must have a decimal point.

- It could be either positive or negative.

- Default sign is positive.

- No commas or blanks are allowed within a real constant.

Ex.: +325.34 426.0 -32.76 -48.5792

The exponential form is usually used if the value of the constant is either too small or too large. It, however, doesn’t restrict us in any way from using exponential form for other real constants.

In exponential form the real constant is represented in two parts. The part appearing before ‘e’ is called mantissa, whereas the part following ‘e’ is called exponent. Thus 0.000342 can be written in exponential form as 3.42e-4 (which in normal arithmetic means 3.42 x 10-4).

Following rules must be observed while constructing real constants expressed in exponential form:

- The mantissa part and the exponential part should be separated by a letter e or E.

- The mantissa part may have a positive or negative sign.

- Default sign of mantissa part is positive.

- The exponent must have at least one digit, which must be a positive or negative integer. Default sign is positive.

- Range of real constants expressed in exponential form is -3.4e38 to 3.4e38.

Ex.: +3.2e-5

4.1e8 -0.2E+3 -3.2e-5

### Rules for Constructing Character Constants

- A character constant is a _single_ alphabet, a single digit or a single special symbol enclosed within single inverted commas.

- Both the inverted commas should point to the left. For example, ’A’ is a valid character constant whereas ‘A’ is not.

Ex.: 'A' 'I' '5' '='

### Types of C Variables

A particular type of variable can hold only the same type of constant. For example, an integer variable can hold only an integer constant, a real variable can hold only a real constant and a character variable can hold only a character constant. The rules for constructing different types of constants are different. However, for constructing variable names of all types, the same set of rules applies. These rules are given below.

### Rules for Constructing Variable Names

- A variable name is any combination of 1 to 31 alphabets, digits or underscores. Some compilers allow variable names whose length could be up to 247 characters. Still, it would be safer to stick to the rule of 31 characters. Do not create unnecessarily long variable names as it adds to your typing effort.

- The first character in the variable name must be an alphabet or underscore ( \_ ).

- No commas or blanks are allowed within a variable name.

- No special symbol other than an underscore (as in **gross\_sal**) can be used in a variable name.

Ex.: si\_int m\_hra pop\_e\_89

Since, the maximum allowable length of a variable name is 31 characters, an enormous number of variable names can be constructed using the above-mentioned rules. It is a good practice to exploit this abundant choice in naming variables by using meaningful variable names.

Thus, if we want to calculate simple interest, it is always advisable to construct meaningful variable names like **prin**, **roi**, **noy** to represent Principle, Rate of interest and Number of years rather than using the variables **a**, **b**, **c**.

The rules for creating variable names remain same for all the types of primary and secondary variables. Naturally, the question follows... how is C able to differentiate between these variables? This is a rather simple matter. C compiler is able to distinguish between the variable names by making it compulsory for you to declare the type of any variable name that you wish to use in a program. This type declaration is done at the beginning of the program. Examples of type declaration statements are given below.

Ex.: int si, m\_hra ; float bassal ; char code ;

### C Keywords

Keywords are the words whose meaning has already been explained to the C compiler (or in a broad sense to the computer). There are only 32 keywords available in C. Figure 1.5 gives a list of these keywords for your ready reference. A detailed discussion of each of these keywords would be taken up in later chapters wherever their use is relevant.

auto double int struct break else long switch case enum register typedef char extern return union const float short unsigned continue for signed void default goto sizeof volatile do if static while

Figure 1.5

The keywords **cannot** be used as variable names because if we do so, we are trying to assign a new meaning to the keyword, which is not allowed. Some C compilers allow you to construct variable names that exactly resemble the keywords. However, it would be safer not to mix up the variable names and the keywords.

Note that compiler vendors (like Microsoft, Borland, etc.) provide their own keywords apart from the ones mentioned in Figure 1.5. These include extended keywords like **near**, **far**, **asm**, etc. Though it has been suggested by the ANSI committee that every such compiler-specific keyword should be preceded by two underscores (as in **\_\_asm** ), not every vendor follows this rule.

**The First C Program** Once armed with the knowledge of variables, constants & keywords, the next logical step would be to combine them to form instructions. However, instead of this, we would write our first C program now. Once we have done that we would see in detail the instructions that it made use of. The first program is very simple. It calculates simple interest for a set of values representing principal, number of years and rate of interest.

/\* Calculation of simple interest \*/ /\* Author: gekay Date: 25/06/2016 \*/ # include <stdio.h> int main( ) { int p, n ; float r, si ; p = 1000 ; n = 3 ; r = 8.5 ; /\* formula for simple interest \*/ si = p \* n \* r / 100 ; printf ( "%f\\n" , si ) ; return 0 ; }

Let us now understand this program in detail.

### Form of a C Program

Form of a C program indicates how it has to be written/typed. There are certain rules about the form of a C program that are applicable to all C programs. These are as under:

- Each instruction in a C program is written as a separate statement.

- The statements in a program must appear in the same order in which we wish them to be executed.

- Blank spaces may be inserted between two words to improve the readability of the statement.

- All statements should be in lower case letters.

- C has no specific rules for the position at which a statement is to be written in a given line. That’s why it is often called a free-form language.

- Every C statement must end with a semicolon ( **; )**. Thus **;** acts as a statement terminator.

### Comments in a C Program

Comments are used in a C program to clarify either the purpose of the program or the purpose of some statement in the program. It is a good practice to begin a program with a comment indicating the purpose of the program, its author and the date on which the program was written.

Here are a few things that you must remember while writing comments in a C program:

- Comment about the program should be enclosed within /\* \*/. Thus, the first two statements in our program are comments.

- Sometimes it is not very obvious as to what a particular statement in a program accomplishes. At such times it is worthwhile mentioning the purpose of the statement (or a set of statements) using a comment. For example:

/\* formula for simple interest \*/ si = p \* n \* r / 100 ;

- Any number of comments can be written at any place in the program. For example, a comment can be written before the

statement, after the statement or within the statement as shown below.

/\* formula \*/ si = p \* n \* r / 100 ; si = p \* n \* r / 100 ; /\* formula \*/ si = p \* n \* r / /\* formula \*/ 100 ;

- The normal language rules do not apply to text written within **/\* .. \*/**. Thus we can type this text in small case, capital or a combination. This is because the comments are solely given for the understanding of the programmer or the fellow programmers and are completely ignored by the compiler.

- Comments cannot be nested. This means one comment cannot be written inside another comment. For example,

/\* Cal of SI /\* Author: gekay date: 25/06/2016 \*/ \*/

is invalid.

- A comment can be split over more than one line, as in,

/\* This comment has three lines in it \*/

Such a comment is often called a multi-line comment.

- ANSI C permits comments to be written in the following way:

// Calculation of simple interest // Formula

### What is _main( )_?

**main( )** forms a crucial part of any C program. Let us understand its purpose as well as its intricacies.

- **main( )** is a function. A function is nothing but a container for a set of statements. In a C program there can be multiple functions. To begin with, we would concentrate only on those programs which have only one function. The name of this function has to be **main( )**, it cannot be anything else. All statements that belong to **main( )** are enclosed within a pair of braces { } as shown below.

int main( ) { statement 1 ; statement 2 ; statement 3 ; }

- The way functions in a calculator return a value, similarly, functions in C also return a value. **main( )** function always returns an integer value, hence there is an **int** before **main( )**. The integer value that we are returning is 0. 0 indicates success. If for any reason the statements in **main( )** fail to do their intended work we can return a non-zero number from **main( )**. This would indicate failure.

- Some compilers like Turbo C/C++ even permit us to return nothing from **main( )**. In such a case we should precede it with the keyword **void**. But this is non-standard way of writing the **main( )** function. We would discuss functions and their working in great detail in Chapter 8.

### Variables and their Usage

We have learnt constants and variables in isolation. Let us understand their significance with reference to our first C program.

- Any variable used in the program must be declared before using it. For example,

int p, n ; /\* declaration \*/ float r, si ; /\* declaration \*/ si = p \* n \* r / 100 ; /\* usage \*/

- In the statement,

si = p \* n \* r / 100 ;

**\*** and **/** are the arithmetic operators. The arithmetic operators available in C are **+**, **\-**, **\*** and **/**. C is very rich in operators. There are as many as 45 operators available in C.

Surprisingly there is no operator for exponentiation... a slip, which can be forgiven considering the fact that C has been developed by an individual, not by a committee.

### _printf( )_ and its Purpose

C does not contain any instruction to display output on the screen. All output to screen is achieved using readymade library functions. One such function is **printf(** **)**. Let us understand this function with respect to our program.

- Once the value of **si** is calculated it needs to be displayed on the screen. We have used **printf( )** to do so.

- For us to be able to use the **printf( )** function, it is necessary to use **#include <stdio.h>** at the beginning of the program. **#include** is a preprocessor directive. Its purpose will be clarified in Chapter 8. For now, use it whenever you use **printf( )**.

- The general form of **printf( )** function is,

printf ( "<format string>", <list of variables> ) ;

<format string> can contain,

**%f** for printing real values **%d** for printing integer values **%c** for printing character values

In addition to format specifiers like **%f**, **%d** and **%c**, the format string may also contain any other characters. These characters are printed as they are when **printf( )** is executed.

- Given below are some more examples of usage of **printf( )** function:

printf ( "%f", si ) ; printf ( "%d %d %f %f", p, n, r, si ) ; printf ( "Simple interest = Rs. %f", si ) ; printf ( "Principal = %d \\nRate = %f", p, r ) ;

The output of the last statement would look like this...

Principal = 1000 Rate = 8.500000

What is ‘\\n’ doing in this statement? It is called newline and it takes the cursor to the next line. Therefore, you get the output split over two lines. ‘\\n’ is one of the several Escape Sequences available in C. These are discussed in detail in Chapter 18. Right now, all that we

can say is ‘\\n’ comes in handy when we want to format the output properly on separate lines.

- **printf(** **)** can not only print values of variables, it can also print the result of an expression. An expression is nothing but a valid combination of constants, variables and operators. Thus, 3, 3 + 2, c and a + b \* c – d all are valid expressions. The results of these expressions can be printed as shown below.

printf ( "%d %d %d %d", 3, 3 + 2, c, a + b \* c – d ) ;

Note that **3** and **c** also represent valid expressions.

### Compilation and Execution

Once you have written the program you need to type it and instruct the machine to execute it. To type your C program you need another program called Editor. Once the program has been typed it needs to be converted to machine language instructions before the machine can execute it. To carry out this conversion we need another program called Compiler. Compiler vendors provide an Integrated Development Environment (IDE) which consists of an Editor as well as the Compiler.

There are several IDEs available in the market targeted towards different operating systems and microprocessors. Details of which IDE to use, how to procure, install and use it are given in Appendix A. Please go through this appendix and install the right IDE on your machine before you try rest of the programs in this book.

**Receiving Input** In the program discussed above we assumed the values of **p**, **n** and **r** to be 1000, 3 and 8.5. Every time we run the program we would get the same value for simple interest. If we want to calculate simple interest for some other set of values then we are required to make the relevant changes in the program, and again compile and execute it. Thus the program is not general enough to calculate simple interest for any set of values without being required to make a change in the program. Moreover, if you distribute the EXE file of this program to somebody he would not even be able to make changes in the program. Hence it is a good practice to create a program that is general enough to work for any set of values.

To make the program general, the program itself should ask the user to supply the values of **p**, **n** and **r** through the keyboard during execution. This can be achieved using a function called **scanf( )**. This function is a counter-part of the **printf( )** function. **printf( )** outputs the values to the screen whereas **scanf( )** receives them from the keyboard. This is illustrated in the program given below.

/\* Calculation of simple interest \*/ /\* Author gekay Date 25/06/2016 \*/ # include <stdio.h> int main( ) { int p, n ; float r, si ; printf ( "Enter values of p, n, r" ) ; scanf ( "%d %d %f", &p, &n, &r ) ; si = p \* n \* r / 100 ; printf ( "%f\\n" , si ) ; return 0 ; }

The first **printf(** **)** outputs the message ‘Enter values of p, n, r’ on the screen. Here we have not used any expression in **printf( )** which means that using expressions in **printf( )** is optional.

Note the use of ampersand (**&**) before the variables in the **scanf(** **)** function is a must. **&** is an ‘Address of’ operator. It gives the location number (address) used by the variable in memory. When we say **&a**, we are telling **scanf( )** at which memory location should it store the value supplied by the user from the keyboard. The detailed working of the **&** operator would be taken up in Chapter 6.

Note that a blank, a tab or a new line must separate the values supplied to **scanf( )**. A blank is created using a spacebar, tab using the Tab key and new line using the Enter key. This is shown below.

Ex.: The three values separated by blank:

1000 5 15.5

Ex.: The three values separated by tab:

1000 5 15.5

Ex.: The three values separated by newline:

1000 5 15.5

So much for the tips. How about writing another program to give you a feel of things. Here it is...

/\* Just for fun. Author: Bozo \*/ # include <stdio.h> int main( ) { int num ; printf ( "Enter a number" ) ; scanf ( "%d", &num ) ; printf ( "Now I am letting you on a secret...\\n" ) ; printf ( "You have just entered the number %d\\n", num ) ; return 0 ; }

**Summary** (a) Constant is an entity whose value remains fixed.

- Variable is an entity whose value can change during course of execution of the program.

- Keywords are special words whose meaning is known to the Compiler.

- There are certain rules that must be followed while building constants or variables.

- The three primary constants and variable types in C are integer, float and character.

- We should not use a keyword as a variable name.

- Comments should be used to indicate the purpose of the program or statements in a program.

- Comments can be single line or multi-line.

- Input/output in C can be achieved using scanf( ) and printf( ) functions.

### Exercise

**\[A\]** Which of the following are invalid C constants and why?

’3.15’ 35,550 3.25e2 2e-3 ‘eLearning’ "show" ‘Quest’ 23 4 6 5 2

**\[B\]** Which of the following are invalid variable names and why?

B’day int $hello #HASH dot. number totalArea \_main( ) temp\_in\_Deg total% 1st stack-queue variable name %name% salary

**\[C\]** State whether the following statements are True or False:

- C language has been developed by Dennis Ritchie.

- Operating systems like Windows, UNIX, Linux and Android are written in C.

- C language programs can easily interact with hardware of a PC / Laptop.

- A real constant in C can be expressed in both Fractional and Exponential forms.

- A character variable can at a time store only one character.

- The maximum value that an integer constant can have varies from one compiler to another.

- Usually all C statements are written in small case letters.

- Spaces may be inserted between two words in a C statement.

- Spaces cannot be present within a variable name.

- C programs are converted into machine language with the help of a program called Editor.

- Most development environments provide an Editor to type a C program and a Compiler to convert it into machine language.

- int, char, float, real, integer, character, char, main, printf and scanf all are keywords.

**\[D\]** Match the following:

- \\n Literal (b) 3.145 Statement terminator (c) -6513 Character constant (d) ’D’ Escape sequence (e) 4.25e-3 Input function (f) main( ) Function (g) %f, %d, %c Integer constant (h) ; Address of operator (i) Constant Output function (j) Variable Format specifier (k) & Exponential form (l) printf( ) Real constant (m) scanf( ) Identifier

**\[E\]** Point out the errors, if any, in the following programs:

- int main( ) { int a, float b, int c ; a = 25 ; b = 3.24 ; c = a + b \* b – 35 ; }

- /\* Calculation of average /\* Author: Sanjay \*/ /\* Place – Whispering Bytes \*/ \*/

#include <stdio.h> int main( ) { int a = 35 ; float b = 3.24 ; printf ( "%d %f %d", a, b + 1.5, 235 ) ; }

- #include <stdio.h> int main( ) { int a, b, c ; scanf ( "%d %d %d", a, b, c ) ; }

- #include <stdio.h>

int main( ) { int m1, m2, m3 printf ( "Enter values of marks in 3 subjects" ) scanf ( "%d %d %d", &m1, &m2, &m3 ) printf ( "You entered %d %d %d", m1, m2, m3 ) ; }

**\[F\]** Attempt the following:

- Ramesh’s basic salary is input through the keyboard. His dearness allowance is 40% of basic salary, and house rent allowance is 20% of basic salary. Write a program to calculate his gross salary.

- The distance between two cities (in km.) is input through the keyboard. Write a program to convert and print this distance in meters, feet, inches and centimeters.

- If the marks obtained by a student in five different subjects are input through the keyboard, write a program to find out the aggregate marks and percentage marks obtained by the student. Assume that the maximum marks that can be obtained by a student in each subject is 100.

- Temperature of a city in Fahrenheit degrees is input through the keyboard. Write a program to convert this temperature into Centigrade degrees.

- The length and breadth of a rectangle and radius of a circle are input through the keyboard. Write a program to calculate the area and perimeter of the rectangle, and the area and circumference of the circle.

- Paper of size A0 has dimensions 1189 mm x 841 mm. Each subsequent size A(n) is defined as A(n-1) cut in half parallel to its shorter sides. Thus paper of size A1 would have dimensions 841 mm x 594 mm. Write a program to calculate and print paper sizes A0, A1, A2, … A8.