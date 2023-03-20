---
title: 'Console'
weight: 18
---

   

s mentioned in the first chapter, Dennis Ritchie wanted C to remain compact. In keeping with this intention, he deliberately omitted

everything related with Input/Output (I/O) from his definition of the language. Thus, C simply has no provision for receiving data from any of the input devices (like say keyboard, disk, etc.), or for sending data to the output devices (like say monitor, disk, etc.). Then how do we manage I/O, and how is it that we were able to use **printf( )** and **scanf( )** if C has nothing to offer for I/O? This is what we intend to explore in this chapter.

**Types of I/O** Though C has no provision for I/O, it, of course, has to be dealt with at some point or the other. There is not much use of writing a program that spends all its time telling itself a secret. Each Operating System (OS) has its own facility for inputting and outputting data from and to the files and devices. It’s a simple matter for a system programmer to write a few small programs that would link the C Compiler for a particular operating system’s I/O facilities.

The developers of C Compilers do just that. They write several standard I/O functions and put them in libraries. These libraries are available with all C Compilers. Whichever C Compiler you are using, it’s almost certain that you have access to a library of I/O functions.

Do understand that the I/O facilities with different operating systems would be different. Thus, the way one OS displays output on screen may be different than the way another OS does it. For example, the standard library function **printf( )** for DOS-based C compiler has been written keeping in mind the way DOS outputs characters to screen. Similarly, the **printf( )** function for a UNIX-based compiler has been written keeping in mind the way UNIX outputs characters to screen. We, as programmers, do not have to bother about which **printf( )** has been written in what manner. We should just use **printf( )** and it would take care of the rest of the details that are OS dependent. Same is true about all other standard library functions available for I/O.

There are numerous library functions available for I/O. These can be classified into two broad categories:

- Console I/O functions - Functions to receive input from keyboard and write output to VDU.

- File I/O functions - Functions to perform I/O operations on a floppy disk or a hard disk.

A

In this chapter we would be discussing only Console I/O functions. File I/O functions would be discussed in Chapter 19.

**Console I/O Functions** The screen and keyboard together are called a console. Console I/O functions can be further classified into two categories—formatted and unformatted console I/O functions. The basic difference between them is that the formatted functions allow the input read from the keyboard or the output displayed on the VDU to be formatted as per our requirements. For example, if values of average marks and percentage marks are to be displayed on the screen, then the details like where this output would appear on the screen, how many spaces would be present between the two values, the number of places after the decimal points, etc., can be controlled using formatted functions. The functions available under each of these two categories are shown in Figure 18.1. Now let us discuss these console I/O functions in detail.

Console Input/Output functions

### Formatted functions Unformatted functions

### Type Input Output

char scanf( ) printf( )

int scanf( ) printf( )

float scanf( ) printf( )

string scanf( ) printf( )

### Type Input Output

char getch( ) fgetchar( )

putch( ) fputchar( )

int - -

float - -

string gets( ) puts( )

Figure 18.1

### Formatted Console I/O Functions

As can be seen from Figure 18.1, the functions **printf( ),** and **scanf( )** fall under the category of formatted console I/O functions. These functions allow us to supply the input in a fixed format and let us obtain the output in the specified form. Let us discuss these functions one-by-one.

We have talked a lot about **printf(** **)**, used it regularly, but without having introduced it formally. Well, better late than never. Its general form looks like this...

printf ( "format string", list of variables ) ;

The format string can contain:

- Characters that are simply printed as they are (b) Format specifications that begin with a % sign (c) Escape sequences that begin with a \\ sign

For example, look at the following program:

\# include <stdio.h> int main( ) { int avg = 346 ; float per = 69.2 ; printf ( "Average = %d\\nPercentage = %f\\n", avg, per ) ; return 0 ; }

The output of the program would be...

Average = 346 Percentage = 69.200000

How does **printf( )** function interpret the contents of the format string? For this, it examines the format string from left to right. So long as it doesn’t come across either a **%** or a \\, it continues to dump the characters that it encounters, on to the screen. In this example, **Average** **\=** is dumped on the screen. The moment it comes across a format specification in the format string, it picks up the first variable in the list of variables and prints its value in the specified format. In this example, the moment **%d** is met, the variable **avg** is picked up and its value is printed. Similarly, when an escape sequence is met, it takes the appropriate action. In this example, the moment **\\n** is met, it places the cursor at the beginning of the next line. This process continues till the end of format string is reached.

### Format Specifications

The **%d** and **%f** used in the **printf( )** are called format specifiers. They tell **printf( )** to print the value of **avg** as a decimal integer and the value of

**per** as a float. Following is the list of format specifiers that can be used with the **printf( )** function.

### Data type Format specifier

Integer short signed

short unsigned

long singed

long unsigned

unsigned hexadecimal

unsigned octal

Real float

double

long double

Character signed character

unsigned character

String

%d or %I

%u

%ld

%lu

%x

%o

%f

%lf

%Lf

%c

%c

%s

Figure 18.2

We can provide optional specifiers shown in Figure 18.3 in the format specifications.

### Specifier Description

w

.

p

\-

Digits specifying field width

Decimal point separating field width from precision

(precision means number of places after the decimal point)

Digits specifying precision

Minus sign for left justifying the output in the specified field

width

Figure 18.3

Now a short explanation about these optional format specifiers. The field-width specifier tells **printf( )** how many columns on screen should

be used while printing a value. For example, **%10d** says, “print the variable as a decimal integer in a field of 10 columns”. If the value to be printed happens not to fill up the entire field, the value is right justified and is padded with blanks on the left. If we include the minus sign in format specifier (as in **%-10d**), this means left justification is desired and the value will be padded with blanks on the right. If the field-width used turns out to be less than what is required to print the number, the field- width is ignored and the complete number is printed. Here is an example that illustrates all these features.

\# include <stdio.h> int main( ) { int weight = 63 ; printf ( "weight is %d kg\\n", weight ) ; printf ( "weight is %2d kg\\n", weight ) ; printf ( "weight is %4d kg\\n", weight ) ; printf ( "weight is %6d kg\\n", weight ) ; printf ( "weight is %-6d kg\\n", weight ) ; printf ( "weight is %1d kg\\n", weight ) ; return 0 ; }

The output of the program would look like this ...

Columns 0123456789012345678901234567890 weight is 63 kg weight is 63 kg weight is 63 kg weight is 63 kg weight is 63 kg weight is 63 kg

Specifying the field width can be useful in creating tables of numeric values, as the following program demonstrates:

\# include <stdio.h> int main( ) { printf ( "%f %f %f\\n", 5.0, 13.5, 133.9 ) ; printf ( "%f %f %f\\n", 305.0, 1200.9, 3005.3 ) ; return 0 ;

}

And here is the output...

5.000000 13.500000 133.900000 305.000000 1200.900000 3005.300000

Even though the numbers have been printed, the numbers have not been lined up properly and hence are hard to read. A better way would be something like this...

\# include <stdio.h> int main( ) { printf ( "%10.1f %10.1f %10.1f\\n", 5.0, 13.5, 133.9 ) ; printf ( "%10.1f %10.1f %10.1f\\n", 305.0, 1200.9, 3005.3 ); return 0 ; }

This results into a much better output...

01234567890123456789012345678901 5.0 13.5 133.9 305.0 1200.9 3005.3

Note that the specifier **%10.1f** specifies that a float be printed left- aligned within 10 columns with only one place beyond the decimal point.

The format specifiers can be used even while displaying a string of characters. The following program would clarify this point:

\# include <stdio.h> int main( ) { char firstname1\[ \] = "Sandy" ; char surname1\[ \] = "Malya" ; char firstname2\[ \] = "AjayKumar" ; char surname2\[ \] = "Gurubaxani" ; printf ( "%20s%20s\\n", firstname1, surname1 ) ; printf ( "%20s%20s\\n", firstname2, surname2 ) ; return 0 ; }

And here’s the output...

012345678901234567890123456789012345678901234567890 Sandy Malya AjayKumar Gurubaxani

The format specifier **%20s** reserves 20 columns for printing a string and then prints the string in these 20 columns with right justification. This helps lining up names of different lengths properly. Obviously, the format **%-20s** would have left-justified the string. Had we used **%20.10s** it would have meant left justify the string in 20 columns and print only first 10 characters of the string.

### Escape Sequences

We saw earlier how the newline character, **\\n**, when inserted in a **printf( )**’s format string, takes the cursor to the beginning of the next line. The newline character is an ‘escape sequence’, so called because the backslash symbol (\\) is considered as an ‘escape’ character—it causes an escape from the normal interpretation of a string, so that the next character is recognized as one having a special meaning.

The following example shows usage of **\\n** and a new escape sequence **\\t**, called ‘Tab’. A **\\t** moves the cursor to the next Tab stop. A 80-column screen usually has 10 Tab stops. In other words, the screen is divided into 10 zones of 8 columns each. Printing a Tab takes the cursor to the beginning of next printing zone. For example, if cursor is positioned in column 5, then printing a Tab takes it to column 8.

\# include <stdio.h> int main( ) { printf ( "You\\tmust\\tbe\\tcrazy\\nto\\thate\\tthis\\tbook\\n" ) ; return 0 ; }

And here’s the output...

01234567890123456789012345678901234567890 You must be crazy to hate this book

The **\\n** character causes a new line to begin following ‘crazy’. The Tab and newline are probably the most commonly used escape sequences,

but there are others as well. Figure 18.4 shows a complete list of these escape sequences.

### Escape Seq. Purpose

\\n

\\b

\\f

\\’

\\\\

New line

Backspace

Form feed

Single quote

Backslash

### Escape Seq. Purpose

\\t

\\r

\\a

\\”

Tab

Carriage return

Alert

Double quote

Figure 18.4

The first few of these escape sequences are more or less self- explanatory. **\\b** moves the cursor one position to the left of its current position. **\\r** takes the cursor to the beginning of the line in which it is currently placed. **\\a** alerts the user by sounding the speaker inside the computer. Form feed advances the computer stationery attached to the printer to the top of the next page. Characters that are ordinarily used as delimiters... the single quote, double quote, and the backslash can be printed by preceding them with the backslash. Thus, the statement,

printf ( "He said, \\"Let's do it!\\"" ) ;

will print...

He said, "Let's do it!"

So far we have been describing **printf( )’**s specification as if we are forced to use only **%d** for an integer, only **%c** for a char, only **%s** for a string and so on. This is not true at all. In fact, **printf( )** uses the specification that we mention and attempts to perform the specified conversion, and does its best to produce a proper result. Sometimes the result is nonsensical, as in case when we ask it to print a string using **%d**. Sometimes the result is useful, as in the case we ask **printf( )** to print ASCII value of a character using **%d**. Sometimes the result is disastrous and the entire program blows up.

The following program shows a few of these conversions, some sensible, some weird:

\# include <stdio.h> int main( ) { char ch = 'z' ; int i = 125 ; float a = 12.55 ; char s\[ \] = "hello there !" ; printf ( "%c %d %f\\n", ch, ch, ch ) ; printf ( "%s %d %f\\n", s, s, s ) ; printf ( "%c %d %f\\n",i ,i, i ) ; printf ( "%f %d\\n", a, a ) ; return 0 ; }

And here’s the output ...

z 122 -9362831782501783000000000000000000000000000.000000 hello there ! 3280 - 9362831782501783000000000000000000000000000.000000 } 125 -9362831782501783000000000000000000000000000.000000 12.550000 0

I would leave it to you to analyze the results by yourselves. Some of the conversions you would find are quite sensible.

Let us now turn our attention to **scanf( )**. The **scanf( )** function allows us to enter data from keyboard that will be formatted in a certain way.

The general form of **scanf( )** statement is as follows:

scanf ( "format string", list of addresses of variables ) ;

For example:

scanf ( "%d %f %c", &c, &a, &ch ) ;

Note that we are sending addresses of variables (addresses are obtained by using ‘**&’** the ‘address of’ operator) to **scanf( )** function. This is necessary because the values received from keyboard must be dropped into variables corresponding to these addresses. The values that are supplied through the keyboard must be separated by either blank(s),

Tab(s), or newline(s). Do not include these escape sequences in the format string.

All the format specifications that we learnt in **printf( )** function are applicable to **scanf( )** function as well.

### _sprintf( )_ and _sscanf( )_ Functions

The **sprintf( )** function works similar to the **printf( )** function except for one small difference. Instead of sending the output to the screen as **printf( )** does, this function writes the output to an array of characters. The following program illustrates this:

\# include <stdio.h> int main( ) { int i = 10 ; char ch = 'A' ; float a = 3.14 ; char str\[ 20 \] ; printf ( "%d %c %f\\n", i, ch, a ) ; sprintf ( str, "%d %c %f", i, ch, a ) ; printf ( "%s\\n", str ) ; return 0 ; }

In this program, the **printf( )** prints out the values of **i**, **ch** and **a** on the screen, whereas **sprintf( )** stores these values in the character array **str**. Since the string **str** is present in memory, what is written into **str** using **sprintf( )** doesn’t get displayed on the screen. Once **str** has been built, its contents can be displayed on the screen. In our program this was achieved by the second **printf( )** statement.

The counterpart of **sprintf( )** is the **sscanf( )** function. It allows us to read characters from a string and to convert and store them in C variables according to specified formats. The **sscanf( )** function comes in handy for in-memory conversion of characters to values. You may find it convenient to read in strings from a file and then extract values from a string by using **sscanf( )**. The usage of **sscanf( )** is same as **scanf( )**, except that the first argument is the string from which reading is to take place.

### Unformatted Console I/O Functions

There are several standard library functions available under this category—those that can deal with a single character and those that can deal with a string of characters. For openers, let us look at those which handle one character at a time.

So far, for input we have consistently used the **scanf( )** function. However, for some situations, the **scanf( )** function has one glaring weakness... you need to hit the Enter key before the function can digest what you have typed. However, we often want a function that will read a single character the instant it is typed without waiting for the Enter key to be hit. **getch( )** and **getche( )** are two functions which serve this purpose. These functions return the character that has been most recently typed. The ‘**e**’ in **getche( )** function means it echoes (displays) the character that you typed to the screen. As against this, **getch( )** just returns the character that you typed without echoing it on the screen. **getchar( )** works similarly and echoes the character that you typed on the screen, but unfortunately requires Enter key to be typed following the character that you typed. The difference between **getchar( )** and **fgetchar( )** is that the former is a macro whereas the latter is a function.

The prototypes of **getch( )** and **getche( )** are present in the header file **conio.h**. The macro **getchar( )** and the prototype of **fgetchar( )** are present in **stdio.h**. Here is a sample program that illustrates the use of these functions and macro.

\# include <stdio.h> # include <conio.h> int main( ) { char ch ; printf ( "Press any key to continue" ) ; getch( ) ; /\* will not echo the character \*/ printf ( "\\nType any character" ) ; ch = getche( ) ; /\* will echo the character typed \*/ printf ( "\\nType any character" ) ; getchar( ) ; /\* will echo character, must be followed by enter key \*/ printf ( "\\nContinue Y/N" ) ; fgetchar( ) ; /\* will echo character, must be followed by enter key \*/

return 0 ; }

And here is a sample run of this program...

Press any key to continue Type any character B Type any character W Continue Y/N Y

**putch( )** and **putchar( )** form the other side of the coin. They print a character on the screen. As far as the working of **putch( )** **putchar( )** and **fputchar( )** is concerned, it’s exactly same. The following program illustrates this:

\# include <stdio.h> # include <conio.h> int main( ) { char ch = 'A' ; putch ( ch ) ; putchar ( ch ) ; fputchar ( ch ) ; putch ( 'Z' ) ; putchar ( 'Z' ) ; fputchar ( 'Z' ) ; return 0 ; }

And here is the output...

AAAZZZ

The limitation of **putch( ),** **putchar( )** and **fputchar( )** is that they can output only one character at a time.

### _gets( )_ and _puts( )_

**gets( )** receives a string from the keyboard. Why is it needed? Because **scanf( )** function has some limitations while receiving string of characters, as the following example illustrates:

\# include <stdio.h>

int main( ) { char name\[ 50 \] ; printf ( "Enter name " ) ; scanf ( "%s", name ) ; printf ( "%s\\n", name ) ; return 0 ; }

And here is the output...

Enter name Jonty Rhodes Jonty

Surprised? Where did “Rhodes” go? It never got stored in the array **name\[ \],** because the moment the blank was typed after “Jonty”, **scanf( )** assumed that the name being entered has ended. The result is that there is no way (at least not without a lot of trouble on the programmer’s part) to enter a multi-word string into a single variable (**name** in this case) using **scanf( ).** The solution to this problem is to use **gets( )** function. As said earlier, it gets a string from the keyboard. It is terminated when an Enter key is hit. Thus, spaces and tabs are perfectly acceptable as part of the input string. More exactly, **gets( )** function gets a newline (**\\n**) terminated string of characters from the keyboard and replaces the **\\n** with a **\\0**.

The **puts( )** function works exactly opposite to **gets( )** function. It outputs a string to the screen.

Here is a program which illustrates the usage of these functions.

\# include <stdio.h> int main( ) { char footballer\[ 40 \] ; puts ( "Enter name" ) ; gets ( footballer ) ; /\* sends base address of array \*/ puts ( "Happy footballing!" ) ; puts ( footballer ) ; return 0 ; }

Following is the sample output:

Enter name Jonty Rhodes Happy footballing! Jonty Rhodes

Why did we use two **puts( )** functions to print “Happy footballing!” and “Jonty Rhodes”? Because, unlike **printf( ),** **puts( )** can output only one string at a time. If we attempt to print two strings using **puts( ),** only the first one gets printed. Similarly, unlike **scanf( ),** **gets( )** can be used to read only one string at a time.

### Summary

- There is no keyword available in C for doing input/output.

- All I/O in C is done using standard library functions.

- Apart from **printf( )** and **scanf( )**, there are several functions available for performing console input/output.

- The formatted console I/O functions can force the user to receive the input in a fixed format and display the output in a fixed format.

- There are several format specifiers and escape sequences available to format input and output.

- Unformatted console I/O functions work faster since they do not have the overheads of formatting the input or output.

### Exercise

**\[A\]** What will be the output of the following programs:

- # include <stdio.h> # include <ctype.h> int main( ) { char ch ; ch = getchar( ) ; if ( islower ( ch ) ) putchar ( toupper ( ch ) ) ; else putchar ( tolower ( ch ) ) ;

return 0 ; }

- # include <stdio.h> int main( )

{ int i = 2 ; float f = 2.5367 ; char str\[ \] = "Life is like that" ; printf ( "%4d\\t%3.3f\\t%4s\\n", i, f, str ) ; return 0 ; }

- # include <stdio.h> int main( )

{ printf ( "More often than \\b\\b not \\rthe person who \\ wins is the one who thinks he can!\\n" ) ; return 0 ; }

- # include <conio.h> char p\[ \] = "The sixth sick sheikh's sixth ship is sick" ;

int main( ) { int i = 0 ; while ( p\[ i \] != '\\0' ) { putch ( p\[ i \] ) ; i++ ; } return 0 ; }

**\[B\]** Point out the errors, if any, in the following programs:

- # include <stdio.h> int main( )

{ int i ; char a\[ \] = "Hello" ; while ( a != '\\0' ) {

printf ( "%c", \*a ) ; a++ ; } return 0 ; }

- # include <stdio.h> int main( )

{ double dval ; scanf ( "%f", &dval ) ; printf ( "Double Value = %lf\\n", dval ) ; return 0 ; }

- # include <stdio.h> int main( )

{ int ival ; scanf ( "%d\\n", &n ) ; printf ( "Integer Value = %d\\n", ival ) ; return 0 ; }

- # include <stdio.h> int main( )

{ char \*mess\[ 5 \] ; int i ; for ( i = 0 ; i < 5 ; i++ ) scanf ( "%s", mess\[ i \] ) ; return 0 ; }

- # include <stdio.h> int main( )

{ int dd, mm, yy ; printf ( "Enter day, month and year\\n" ) ; scanf ( "%d%\*c%d%\*c%d", &dd, &mm, &yy ) ; printf ( "The date is: %d - %d - %d\\n", dd, mm, yy ) ; return 0 ; }

- # include <stdio.h> int main( )

{ char text ; sprintf ( text, "%4d\\t%2.2f\\n%s", 12, 3.452, "Merry Go Round" ) ; printf ( "%s\\n", text ) ; return 0 ; }

- # include <stdio.h> int main( )

{ char buffer\[ 50 \] ; int no = 97; double val = 2.34174 ; char name\[ 10 \] = "Shweta" ; sprintf ( buffer, "%d %lf %s", no, val, name ) ; printf ( "%s\\n", buffer ) ; sscanf ( buffer, "%4d %2.2lf %s", &no, &val, name ) ; printf ( "%s\\n", buffer ) ; printf ( "%d %lf %s\\n", no, val, name ) ; return 0 ; }

**\[C\]** Answer the following:

- To receive the string "We have got the guts, you get the glory!!" in an array **char str\[ 100 \]** which of the following functions would you use?

1\. scanf ( "%s", str ) ; 2. gets ( str ) ; 3. getche ( str ) ; 4. fgetchar ( str ) ;

- Which function would you use if a single key were to be received through the keyboard?

1\. scanf( ) 2. gets( ) 3. getche( ) 4. getchar( )

- If an integer is to be entered through the keyboard, which function would you use?

1\. scanf( ) 2. gets( ) 3. getche( ) 4. getchar( )

- What is the difference between **getchar( )**, **fgetchar( )**, **getch(** **)** and **getche( )**?

- Which of the following can a format string of a **printf( )** function contain:

1\. Characters, format specifications and escape sequences 2. Character, integers and floats 3. Strings, integers and escape sequences 4. Inverted commas, percentage sign and backslash character

- The purpose of the field-width specifier in a **printf( )** function is to:

1\. Control the margins of the program listing 2. Specify the maximum value of a number 3. Control the size of font used to print numbers 4. Specify how many columns would be used to print the number

**\[D\]** Answer the following:

- Define two functions **xgets( )** and **xputs( )** which work similar to the standard library functions **gets( )** and **puts( )**.

- Define a function **getint( )**, which would receive a numeric string from the keyboard, convert it to an integer number and return the integer to the calling function. A sample usage of **getint( )** is shown below.

\# include <stdio.h> int main( ) { int a ; a = getint( ) ; printf ( "you entered %d\\n", a ) ; return 0 ; }

- Define a function **getfloat( )**, which would receive a numeric string from the keyboard, convert it to a float value and return the float to the calling function.

- If we are to display the following output properly aligned which format specifiers would you use?

Discovery of India Jawaharlal Nehru 425.50 My Experiments with Truth Mahatma Gandhi 375.50 Sunny Days Sunil Gavaskar 95.50 One More Over Erapalli Prasanna 85.00