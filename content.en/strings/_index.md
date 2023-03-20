---
title: 'Strings'
weight: 15
---

In the last chapter, you learnt how to define arrays of various sizes and dimensions, how to initialize arrays, how to pass arrays to a function,

etc. With this knowledge under your belt, you should be ready to handle strings, which are, simply put, a special kind of array. And strings, the ways to manipulate them, and how pointers are related to strings are going to be the topics of discussion in this chapter.

### What are Strings?

The way a group of integers can be stored in an integer array, similarly a group of characters can be stored in a character array. Character arrays are many a time also called strings. Many languages internally treat strings as character arrays, but somehow conceal this fact from the programmer. Character arrays or strings are used by programming languages to manipulate text, such as words and sentences.

A string constant is a one-dimensional array of characters terminated by a null ( ’\\0’ ). For example,

char name\[ \] = { 'H', 'A', 'E', 'S', 'L', 'E', 'R', '\\0' } ;

Each character in the array occupies 1 byte of memory and the last character is always ’\\0’. What character is this? It looks like two characters, but it is actually only one character, with the \\ indicating that what follows it is something special. ’\\0’ is called null character. Note that ’\\0’ and ’0’ are not same. ASCII value of ’\\0’ is 0, whereas ASCII value of ’0’ is 48. Figure 15.1 shows the way a character array is stored in memory. Note that the elements of the character array are stored in contiguous memory locations.

The terminating null (’\\0’) is important, because it is the only way the functions that work with a string can know where the string ends. In fact, a string not terminated by a ’\\0’ is not really a string, but merely a collection of characters.

65518 65519 65520 65521 65522 65523 65524 65525

H A E S L E R \\0

Figure 15.1

I

C concedes the fact that you would use strings very often and hence provides a shortcut for initializing strings. For example, the string used above can also be initialized as,

char name\[ \] = "HAESLER" ;

Note that, in this declaration ’\\0’ is not necessary. C inserts the null character automatically.

**More about Strings** In what way are character arrays different from numeric arrays? Can elements in a character array be accessed in the same way as the elements of a numeric array? Do I need to take any special care of ’\\0’? Why numeric arrays don’t end with a ’\\0’? Declaring strings is okay, but how do I manipulate them? Questions galore!! Well, let us settle some of these issues right away with the help of sample programs.

/\* Program to demonstrate printing of a string \*/ # include <stdio.h> int main( ) { char name\[ \] = "Klinsman" ; int i = 0 ; while ( i <= 7 ) { printf ( "%c", name\[ i \] ) ; i++ ; } printf ( "\\n" ) ; return 0 ; }

And here is the output...

Klinsman

No big deal. We have initialized a character array, and then printed out the elements of this array within a **while** loop. Can we write the **while** loop without using the final value 7? We can; because we know that each character array always ends with a ’\\0’. Following program illustrates this:

\# include <stdio.h> int main( ) { char name\[ \] = "Klinsman" ; int i = 0 ; while ( name\[ i \] != '\\0' ) { printf ( "%c", name\[ i \] ) ; i++ ; } printf ( "\\n" ) ; return 0 ; }

And here is the output...

Klinsman

This program doesn’t rely on the length of the string (number of characters in it) to print out its contents and hence is definitely more general than the earlier one. Here is another version of the same program; this one uses a pointer to access the array elements.

\# include <stdio.h> int main( ) { char name\[ \] = "Klinsman" ; char \*ptr ; ptr = name ; /\* store base address of string \*/ while ( \*ptr != '\\0' ) { printf ( "%c", \*ptr ) ; ptr++ ; } printf ( "\\n" ) ; return 0 ; }

As with the integer array, by mentioning the name of the array, we get the base address (address of the zeroth element) of the array. This base address is stored in the variable **ptr** using,

ptr = name ;

Once the base address is obtained in **ptr**, **\*ptr** would yield the value at this address, which gets printed promptly through,

printf ( "%c", \*ptr ) ;

Then, **ptr** is incremented to point to the next character in the string. This derives from two facts: array elements are stored in contiguous memory locations and on incrementing a pointer, it points to the immediately next location of its type. This process is carried out until **ptr** points to the last character in the string, that is, ’\\0’.

In fact, the character array elements can be accessed exactly in the same way as the elements of an integer array. Thus, all the following notations refer to the same element:

name\[ i \] \*( name + i ) \*( i + name ) i\[ name \]

Even though there are so many ways (as shown above) to refer to the elements of a character array, rarely is any one of them used. This is because **printf( )** function has got a sweet and simple way of doing it, as shown below. Note that **printf( )** doesn’t print the ’\\0’.

\# include <stdio.h> int main( ) { char name\[ \] = "Klinsman" ; printf ( "%s", name ) ; }

The **%s** used in **printf( )** is a format specification for printing out a string. The same specification can be used to receive a string from the keyboard, as shown below.

\# include <stdio.h> int main( ) { char name\[ 25 \] ;

printf ( "Enter your name " ) ; scanf ( "%s", name ) ; printf ( "Hello %s!\\n", name ) ; return 0 ; }

And here is a sample run of the program...

Enter your name Debashish Hello Debashish!

Note that the declaration **char** **name\[ 25 \]** sets aside 25 bytes under the array **name\[ \]**, whereas the **scanf( )** function fills in the characters typed at keyboard into this array until the Enter key is hit. Once enter is hit, **scanf( )** places a ’\\0’ in the array. Naturally, we should pass the base address of the array to the **scanf( )** function.

While entering the string using **scanf( )**, we must be cautious about two things:

- The length of the string should not exceed the dimension of the character array. This is because the C compiler doesn’t perform bounds checking on character arrays. Hence, if you carelessly exceed the bounds, there is always a danger of overwriting something important, and in that event, you would have nobody to blame but yourselves.

- **scanf( )** is not capable of receiving multi-word strings. Therefore, names such as ‘Debashish Roy’ would be unacceptable. The way to get around this limitation is by using the function **gets( )**. The usage of functions **gets( )** and its counterpart **puts( )** is shown below.

\# include <stdio.h> int main( ) { char name\[ 25 \] ; printf ( "Enter your full name: " ) ; gets ( name ) ; puts ( "Hello!" ) ; puts ( name ) ; return 0 ; }

And here is the output...

Enter your full name: Debashish Roy Hello! Debashish Roy

The program and the output are self-explanatory except for the fact that, **puts( )** can display only one string at a time (hence the use of two **puts( )** in the program above). Also, on displaying a string, unlike **printf( )**, **puts( )** places the cursor on the next line. Though **gets( )** is capable of receiving only one string at a time, the plus point with **gets( )** is that it can receive a multi-word string.

If we are prepared to take the trouble, we can make **scanf( )** accept multi-word strings by writing it in this manner:

char name\[ 25 \] ; printf ( "Enter your full name " ) ; scanf ( "%\[ ^\\n \]s", name ) ;

Here, **\[^\\n\]** indicates that **scanf( )** will keep receiving characters into **name\[ \]** until \\n is encountered. Though workable, this is not the best of the ways to call a function, you would agree.

**Pointers and Strings** Suppose we wish to store “Hello”. We may either store it in a string or we may ask the C compiler to store it at some location in memory and assign the address of the string in a **char** pointer. This is shown below.

char str\[ \] = "Hello" ; char \*p = "Hello" ;

There is a subtle difference in usage of these two forms. For example, we cannot assign a string to another, whereas, we can assign a **char** pointer to another **char** pointer. This is shown in the following program:

int main( ) { char str1\[ \] = "Hello" ; char str2\[ 10 \] ; char \*s = "Good Morning" ; char \*q ; str2 = str1 ; /\* error \*/

q = s ; /\* works \*/ return 0 ; }

Also, once a string has been defined, it cannot be initialized to another set of characters. Unlike strings, such an operation is perfectly valid with **char** pointers.

int main( ) { char str1\[ \] = "Hello" ; char \*p = "Hello" ; str1 = "Bye" ; /\* error \*/ p = "Bye" ; /\* works \*/ }

**Standard Library String Functions** With every C compiler, a large set of useful string handling library functions are provided. Figure 15.2 lists the more commonly used functions along with their purpose.

### Function Use

strlen

strlwr

strupr

strcat

strncat

strcpy

strncpy

strcmp

strncmp

strcmpi

stricmp

strnicmp

strdup

strchr

strrchr

strstr

strset

strnset

strrev

Finds length of a string

Converts a string to lowercase

Converts a string to uppercase

Appends one string at the end of another

Appends first n characters of a string at the end of another

Copies a string into another

Copies first n characters of one string into another

Compares two strings

Compares first n characters of two strings

Compares two strings by ignoring the case

Compares two strings without regard to case (identical to strcmpi)

Compares first n characters of two strings without regard to case

Duplicates a string

Finds first occurrence of a given character in a string

Finds last occurrence of a given character in a string

Finds first occurrence of a given string in another string

Sets all characters of string to a given character

Sets first n characters of a string to a given character

Reverses string

Figure 15.2

From the list given in Figure 15.2, we shall discuss functions **strlen( )**, **strcpy( )**, **strcat( )** and **strcmp( )**, since these are the most commonly used. This will also illustrate how the library functions in general handle strings. Let us study these functions one-by-one.

### strlen( )

This function counts the number of characters present in a string. Its usage is illustrated in the following program:

\# include <stdio.h> # include <string.h> int main( ) {

char arr\[ \] = "Bamboozled" ; int len1, len2 ; len1 = strlen ( arr ) ; len2 = strlen ( "Humpty Dumpty" ) ; printf ( "string = %s length = %d\\n", arr, len1 ) ; printf ( "string = %s length = %d\\n", "Humpty Dumpty", len2 ) ; return 0 ; }

The output would be...

string = Bamboozled length = 10 string = Humpty Dumpty length = 13

Note that, in the first call to the function **strlen( )**, we are passing the base address of the string, and the function, in turn, returns the length of the string. While calculating the length, it doesn’t count ’\\0’. Even in the second call,

len2 = strlen ( "Humpty Dumpty" ) ;

what gets passed to **strlen( )** is the address of the string and not the string itself. Can we not write a function **xstrlen( )**, which imitates the standard library function **strlen( )**? Let us give it a try...

/\* A look-alike of the function strlen( ) \*/ # include <stdio.h> int xstrlen ( char \* ) ; int main( ) { char arr\[ \] = "Bamboozled" ; int len1, len2 ; len1 = xstrlen ( arr ) ; len2 = xstrlen ( "Humpty Dumpty" ) ; printf ( "string = %s length = %d\\n", arr, len1 ) ; printf ( "string = %s length = %d\\n", "Humpty Dumpty", len2 ) ; return 0 ; } int xstrlen ( char \*s )

{ int length = 0 ; while ( \*s != '\\0' ) { length++ ; s++ ; } return ( length ) ; }

The output would be...

string = Bamboozled length = 10 string = Humpty Dumpty length = 13

The function **xstrlen( )** is fairly simple. All that it does is to keep counting the characters till the end of string is met. Or in other words, keep counting characters till the pointer **s** points to ’\\0’.

### strcpy( )

This function copies the contents of one string into another. The base addresses of the source and target strings should be supplied to this function. Here is an example of **strcpy( )** in action...

\# include <stdio.h> # include <string.h> int main( ) { char source\[ \] = "Sayonara" ; char target\[ 20 \] ; strcpy ( target, source ) ; printf ( "source string = %s\\n", source ) ; printf ( "target string = %s\\n", target ) ; return 0 ; }

And here is the output...

source string = Sayonara target string = Sayonara

On supplying the base addresses, **strcpy( )** goes on copying the characters in source string into the target string till it encounters the end of source string (’\\0’). It is our responsibility to see to it that the target string’s dimension is big enough to hold the string being copied into it. Thus, a string gets copied into another, piece-meal, character-by- character. There is no short-cut for this. Let us now attempt to mimic **strcpy( )**, via our own string copy function, which we will call **xstrcpy( )**.

\# include <stdio.h> void xstrcpy ( char \*, char \* ) ; int main( ) { char source\[ \] = "Sayonara" ; char target\[ 20 \] ; xstrcpy ( target, source ) ; printf ( "source string = %s\\n", source ) ; printf ( "target string = %s\\n", target ) ; return 0 ; } void xstrcpy ( char \*t, char \*s ) { while ( \*s != '\\0' ) { \*t = \*s ; s++ ; t++ ; } \*t = '\\0' ; }

The output of the program would be...

source string = Sayonara target string = Sayonara

Note that having copied the entire source string into the target string, it is necessary to place a ’\\0’ into the target string, to mark its end.

If you look at the prototype of **strcpy( )** standard library function, it looks like this…

strcpy ( char \*t, const char \*s ) ;

We didn’t use the keyword const in our version of **xstrcpy( )** and still our function worked correctly. So what is the need of the **const** qualifier?

What would happen if we add the following lines beyond the last statement of **xstrcpy( )**?

s = s - 8 ; \*s = 'K' ;

This would change the source string to “Kayonara”. Can we not ensure that the source string doesn’t change even accidentally in **xstrcpy( )**? We can, by changing the definition as follows:

void xstrcpy ( char \*t, const char \*s ) { while ( \*s != '\\0' ) { \*t = \*s ; s++ ; t++ ; } \*t = '\\0' ; }

By declaring **char \*s** as **const**, we are declaring that the source string should remain constant (should not change). Thus the **const** qualifier ensures that your program does not inadvertently alter a variable that you intended to be a constant. It also reminds anybody reading the program listing that the variable is not intended to change.

Let us understand the difference between the following two statements:

char str\[ \] = "Quest" ; char \*p = "Quest" ;

Here **str** acts as a constant pointer to a string, whereas, **p** acts as a pointer to a constant string. As a result, observe which operations are permitted, and which are not:

str++ ; /\* error, constant pointer cannot change \*/ \*str = 'Z' ; /\* works, because string is not constant \*/ p++ ; /\* works, because pointer is not constant \*/ \*p = 'M' ; /\* error, because string is constant \*/

The keyword **const** can also be used in context of ordinary variables like **int**, **float**, etc. The following program shows how this can be done:

\# include <stdio.h> int main( ) { float r, a ; const float pi = 3.14 ; printf ( "Enter radius of circle " ) ; scanf ( "%f", &r ) ; a = pi \* r \* r ; printf ( "Area of circle = %f\\n", a ) ; return 0 ; }

### strcat( )

This function concatenates the source string at the end of the target string. For example, “Bombay” and “Nagpur” on concatenation would result into a string “BombayNagpur”. Here is an example of **strcat( )** at work.

\# include <stdio.h> # include <string.h> int main( ) { char source\[ \] = "Folks!" ; char target\[ 30 \] = "Hello" ; strcat ( target, source ) ; printf ( "source string = %s\\n", source ) ; printf ( "target string = %s\\n", target ) ; return 0 ; }

And here is the output...

source string = Folks! target string = HelloFolks!

Note that the target string has been made big enough to hold the final string. I leave it to you to develop your own **xstrcat( )** on lines of **xstrlen( )** and **xstrcpy( )**.

### strcmp( )

This is a function which compares two strings to find out whether they are same or different. The two strings are compared character-by- character until there is a mismatch or end of one of the strings is reached, whichever occurs first. If the two strings are identical, **strcmp( )** returns a value zero. If they’re not, it returns the numeric difference between the ASCII values of the first non-matching pair of characters. Here is a program which puts **strcmp( )** in action.

\# include <stdio.h> # include <string.h> int main( ) { char string1\[ \] = "Jerry" ; char string2\[ \] = "Ferry" ; int i, j, k ; i = strcmp ( string1, "Jerry" ) ; j = strcmp ( string1, string2 ) ; k = strcmp ( string1, "Jerry boy" ) ; printf ( "%d %d %d\\n", i, j, k ) ; return 0 ; }

And here is the output...

0 4 -32

In the first call to **strcmp( )**, the two strings are identical—“Jerry” and “Jerry”—and the value returned by **strcmp( )** is zero. In the second call, the first character of “Jerry” doesn't match with the first character of “Ferry” and the result is 4, which is the numeric difference between ASCII value of ’J’ and ASCII value of ’F’. In the third call to **strcmp( )**, “Jerry” doesn’t match with “Jerry boy”, because the null character at the end of “Jerry” doesn’t match the blank in “Jerry boy”. The value returned is -32, which is the value of null character minus the ASCII value of space, i.e., ’\\0’ minus ’ ’, which is equal to -32.

The exact value of mismatch rarely concerns us. All that we usually want to know is whether or not the first string is alphabetically before the second string. If it is, a negative value is returned; if it isn’t, a positive value is returned. Try to implement this logic in a user-defined function **xstrcmp( )**.

### Summary

- A string is nothing but an array of characters terminated by ’\\0’.

- Being an array, all the characters of a string are stored in contiguous memory locations.

- Though **scanf( )** can be used to receive multi-word strings, **gets( )** can do the same job in a cleaner way.

- Both **printf( )** and **puts( )** can handle multi-word strings.

- Strings can be operated upon using several standard library functions like **strlen( )**, **strcpy( )**, **strcat( )** and **strcmp( )** which can manipulate strings.

### Exercise

**\[A\]** What will be the output of the following programs:

- # include <stdio.h> int main( ) { char c\[ 2 \] = "A" ; printf ( "%c\\n", c\[ 0 \] ) ; printf ( "%s\\n", c ) ; return 0 ; }

- # include <stdio.h> int main( ) { char s\[ \] = "Get organised! learn C!!" ; printf ( "%s\\n", &s\[ 2 \] ) ; printf ( "%s\\n", s ) ; printf ( "%s\\n", &s ) ; printf ( "%c\\n", s\[ 2 \] ) ; return 0 ; }

- # include <stdio.h> int main( ) { char s\[ \] = "No two viruses work similarly" ;

int i = 0 ; while ( s\[ i \] != 0 ) { printf ( "%c %c\\n", s\[ i \], \*( s + i ) ) ; printf ( "%c %c\\n", i\[ s \], \*( i + s ) ) ; i++ ; } return 0 ; }

- # include <stdio.h> int main( ) { char s\[ \] = "Churchgate: no church no gate" ; char t\[ 25 \] ; char \*ss, \*tt ; ss = s ; while ( \*ss != '\\0' ) \*tt++ = \*ss++ ; printf ( "%s\\n", t ) ; return 0 ; }

- # include <stdio.h> int main( ) { char str1\[ \] = { ’H’, ’e’, ’l’, ’l’, ’o’, 0 } ; char str2\[ \] = "Hello" ; printf ( "%s\\n", str1 ) ; printf ( "%s\\n", str2 ) ; return 0 ; }

- # include <stdio.h> void main( ) { printf ( 5 + "Good Morning " ) ; return 0 ; }

- # include <stdio.h> int main( ) {

printf ( "%c\\n", "abcdefgh"\[ 4 \] ) ; return 0 ; }

- # include <stdio.h> int main( ) { printf ( "%d %d %d\\n", sizeof ( ’3’ ), sizeof ( "3" ), sizeof ( 3 ) ) ; return 0 ; }

**\[B\]** Point out the errors, if any, in the following programs:

- # include <stdio.h> # include <string.h> int main( ) { char \*str1 = "United" ; char \*str2 = "Front" ; char \*str3 ; str3 = strcat ( str1, str2 ) ; printf ( "%s\\n", str3 ) ; return 0 ; }

- # include <stdio.h> int main( ) { int arr\[ \] = { ’A’, ’B’, ’C’, ’D’ } ; int i ; for ( i = 0 ; i <= 3 ; i++ ) printf ( "%d", arr\[ i \] ) ; printf ( "\\n" ) ; return 0 ; }

- # include <stdio.h> int main( ) { char arr\[ 8 \] = "Rhombus" ; int i ; for ( i = 0 ; i <= 7 ; i++ ) printf ( "%d", \*arr ) ; arr++ ;

return 0 ; }

**\[C\]** Fill in the blanks:

- "A" is a \_\_\_\_\_\_\_\_\_\_\_ whereas ’A’ is a \_\_\_\_\_\_\_\_\_\_\_\_.

- A string is terminated by a \_\_\_\_\_\_ character, which is written as \_\_\_\_\_\_.

- The array **char name\[ 10 \]** can consist of a maximum of \_\_\_\_\_\_ characters.

- The array elements are always stored in \_\_\_\_\_\_\_\_\_ memory locations.

**\[D\]** Attempt the following:

- Which is more appropriate for reading in a multi-word string?

gets( ) printf( ) scanf( ) puts( )

- If the string "Alice in wonder land" is fed to the following **scanf( )** statement, what will be the contents of the arrays **str1**, **str2**, **str3** and **str4**?

scanf ( "%s%s%s%s", str1, str2, str3, str4 ) ;

- Write a program that extracts part of the given string from the specified position. For example, if the sting is "Working with strings is fun", then if from position 4, 4 characters are to be extracted then the program should return string as "king". If the number of characters to be extracted is 0 then the program should extract entire string from the specified position.

- Write a program that converts a string like "124" to an integer 124.

- Write a program that generates and prints the Fibonacci words of order 0 through 5. If f(0) = "a", f(1) = "b", f(2) = "ba", f(3) = "bab", f(4) = "babba", etc.

- To uniquely identify a book a 10-digit ISBN (International Standard Book Number) is used. The rightmost digit is a checksum digit. This digit is determined from the other 9 digits using the condition that d1 + 2d2 + 3d3 + ... + 10d10 must be a multiple of 11 (where di denotes the ith digit from the right). The checksum digit d1 can be any value from 0 to 10: the ISBN convention is to use the value X to denote 10. Write a program that receives a 10-digit integer,

computes the checksum, and reports whether the ISBN number is correct or not.

- A Credit Card number is usually a 16-digit number. A valid Credit Card number would satisfy a rule explained below with the help of a dummy Credit Card number—4567 1234 5678 9129. Start with the rightmost - 1 digit and multiply every other digit by 2.

4 5 6 7 1 2 3 4 5 6 7 8 9 1 2 9

8 12 2 6 10 14 18 4

Then subtract 9 from any number larger than 10. Thus we get:

8 3 2 6 1 5 9 4

Add them all up to get 38.

Add all the other digits to get 42.

Sum of 38 and 42 is 80. Since 80 is divisible by 10, the Credit Card number is valid.

Write a program that receives a Credit Card number and checks using the above rule whether the Credit Card number is valid.