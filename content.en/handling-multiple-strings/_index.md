---
title: 'Handling Multiple Strings'
weight: 16
---

In the last chapter, you learnt how to deal with individual strings. But often we are required to deal with a set of strings rather an isolated

string. This chapter discusses how such situations can be handled effectively.

**Two-Dimensional Array of Characters** In Chapter 14 we saw several examples of two-dimensional integer arrays. Let’s now look at a similar entity, but one dealing with characters. Our example program asks you to type your name. When you do so, it checks your name against a master list to see if you are worthy of entry to the palace. Here’s the program...

\# include <stdio.h> # include <string.h> # define FOUND 1 # define NOTFOUND 0 int main( ) { char masterlist\[ 6 \]\[ 10 \] = { "akshay", "parag", "raman", "srinivas", "gopal", "rajesh" } ; int i, flag, a ; char yourname\[ 10 \] ; printf ( "Enter your name " ) ; scanf ( "%s", yourname ) ; flag = NOTFOUND ; for ( i = 0 ; i <= 5 ; i++ ) { a = strcmp ( &masterlist\[ i \]\[ 0 \], yourname ) ; if ( a == 0 ) { printf ( "Welcome, you can enter the palace\\n" ) ; flag = FOUND ;

I

break ; } } if ( flag == NOTFOUND ) printf ( "Sorry, you are a trespasser\\n" ) ; return 0 ; }

And here is the output for two sample runs of this program...

Enter your name dinesh Sorry, you are a trespasser Enter your name raman Welcome, you can enter the palace

Notice how the two-dimensional character array has been initialized. The order of the subscripts in the array declaration is important. The first subscript gives the number of names in the array, while the second subscript gives the length of each item in the array.

Instead of initializing names, had these names been supplied from the keyboard, the program segment would have looked like this...

for ( i = 0 ; i <= 5 ; i++ ) scanf ( "%s", &masterlist\[ i \]\[ 0 \] ) ;

While comparing the strings through **strcmp( )**, note that the addresses of the strings are being passed to **strcmp( )**. As seen in the last section, if the two strings match, **strcmp( )** would return a value 0, otherwise it would return a non-zero value.

The variable **flag** is used to keep a record of whether the control did reach inside the if or not. To begin with, we set **flag** to NOTFOUND. Later through the loop, if the names match, **flag** is set to FOUND. When the control reaches beyond the **for** loop, if **flag** is still set to NOTFOUND, it means none of the names in the **masterlist\[ \]\[ \]** matched with the one supplied from the keyboard.

The names would be stored in the memory as shown in Figure 16.1. Note that each string ends with a ’\\0’. The arrangement, as you can appreciate, is similar to that of a two-dimensional numeric array.

a k s h a y \\0

p a r a g \\0

r a m a n \\0

s r i n i v a s \\0

g o p a l \\0

r a j e s h \\0

65454

65464

65474

65484

65494

65504 65513 (last location)

Figure 16.1

Here, 65454, 65464, 65474, etc., are the base addresses of successive names. As seen from the above pattern, some of the names do not occupy all the bytes reserved for them. For example, even though 10 bytes are reserved for storing the name “akshay”, it occupies only 7 bytes. Thus, 3 bytes go waste. Similarly, for each name, there is some amount of wastage. In fact, more the number of names, more would be the wastage. Can this not be avoided? Yes, it can be... by using what is called an ‘array of pointers’, which is our next topic of discussion.

**Array of Pointers to Strings** As we know, a pointer variable always contains an address. Therefore, if we construct an array of pointers, it would contain a number of addresses. Let us see how the names in the earlier example can be stored in the array of pointers.

char \*names\[ \] = { "akshay", "parag", "raman", "srinivas", "gopal", "rajesh" } ;

In this declaration, **names\[ \]** is an array of pointers. It contains base addresses of respective names. That is, base address of “akshay” is stored in **names\[ 0 \]**, base address of “parag” is stored in **names\[ 1 \]** and so on. This is depicted in Figure 16.2.

akshay\\0 raman\\0 srinivas\\0

gopal\\0 rajesh\\0 parag\\0

182 195 201

210 216 189

182 189 195 201 210 216

65514 65518 65522 65526 65530 65534

names\[ \]

Figure 16.2

In the two-dimensional array of characters, the strings occupied 60 bytes. As against this, in array of pointers, the strings occupy only 41 bytes—a net saving of 19 bytes. A substantial saving, you would agree. Thus, one reason for storing strings in an array of pointers is to make a more efficient use of available memory.

Another reason to use an array of pointers to store strings is to obtain greater ease in manipulation of the strings. This is shown by the following programs. The first one uses a two-dimensional array of characters to store the names, whereas the second uses an array of pointers to strings. The purpose of both the programs is very simple. We want to exchange the position of the names “raman” and “srinivas”.

/\* Exchange names using 2-D array of characters \*/ # include <stdio.h> int main( ) { char names\[ \]\[ 10 \] = { "akshay", "parag", "raman", "srinivas", "gopal", "rajesh" } ; int i ; char t ;

printf ( "Original: %s %s\\n", &names\[ 2 \]\[ 0 \], &names\[ 3 \]\[ 0 \] ) ; for ( i = 0 ; i <= 9 ; i++ ) { t = names\[ 2 \]\[ i \] ; names\[ 2 \]\[ i \] = names\[ 3 \]\[ i \] ; names\[ 3 \]\[ i \] = t ; } printf ( "New: %s %s\\n", &names\[ 2 \]\[ 0 \], &names\[ 3 \]\[ 0 \] ) ; return 0 ; }

And here is the output...

Original: raman srinivas New: srinivas raman

Note that in this program to exchange the names, we are required to exchange corresponding characters of the two names. In effect, 10 exchanges are needed to interchange two names.

Let us see, if the number of exchanges can be reduced by using an array of pointers to strings. Here is the program...

\# include <stdio.h> int main( ) { char \*names\[ \] = { "akshay", "parag", "raman", "srinivas", "gopal", "rajesh" } ; char \*temp ; printf ( "Original: %s %s\\n", names\[ 2 \], names\[ 3 \] ) ; temp = names\[ 2 \] ; names\[ 2 \] = names\[ 3 \] ; names\[ 3 \] = temp ; printf ( "New: %s %s\\n", names\[ 2 \], names\[ 3 \] ) ; return 0 ;

}

And here is the output...

Original: raman srinivas New: srinivas raman

The output is same as the earlier program. In this program, all that we are required to do is to exchange the addresses (of the names) stored in the array of pointers, rather than the names themselves. Thus, by effecting just one exchange, we are able to interchange names. This makes handling strings very convenient.

Thus, from the point of view of efficient memory usage and ease of programming, an array of pointers to strings definitely scores over a two-dimensional character array. That is why, even though, in principle, strings can be stored and handled through a two-dimensional array of characters, in actual practice, it is the array of pointers to strings, which is more commonly used.

**Limitation of Array of Pointers to Strings** When we are using a two-dimensional array of characters, we are at liberty to either initialize the strings where we are declaring the array, or receive the strings using **scanf( )** function. However, when we are using an array of pointers to strings, we can initialize the strings at the place where we are declaring the array, but we cannot receive the strings from keyboard using **scanf( )**. Thus, the following program would never work out:

\# include <stdio.h> int main( ) { char \*names\[ 6 \] ; int i ; for ( i = 0 ; i <= 5 ; i++ ) { printf ( "Enter name " ) ; scanf ( "%s", names\[ i \] ) ; } return 0 ; }

The program doesn’t work because; when we are declaring the array, it is containing garbage values. And it would be definitely wrong to send these garbage values to **scanf( )** as the addresses where it should keep the strings received from the keyboard.

**Solution** If we are bent upon receiving the strings from keyboard using **scanf( )** function and then storing their addresses in an array of pointers to strings, we can do it in a slightly roundabout manner as shown below.

\# include <stdio.h> # include <stdlib.h> # include <string.h> int main( ) { char \*names\[ 6 \] ; char n\[ 50 \] ; int len, i ; char \*p ; for ( i = 0 ; i <= 5 ; i++ ) { printf ( "Enter name " ) ; scanf ( "%s", n ) ; len = strlen ( n ) ; p = ( char \* ) malloc ( len + 1 ) ; /\* +1 for accommodating \\0 \*/ strcpy ( p, n ) ; names\[ i \] = p ; } for ( i = 0 ; i <= 5 ; i++ ) printf ( "%s\\n", names\[ i \] ) ; return 0 ; }

Here we have first received a name using **scanf( )** in a string **n\[ \]**. Then we have found out its length using **strlen( )** and allocated space for making a copy of this name. This memory allocation has been done using a standard library function called **malloc( )**. This function requires the number of bytes to be allocated and returns the base address of the chunk of memory that it allocates. The address returned by this function is always of the type **void \***. This is because **malloc( )** doesn’t know what for did we allocate the memory. A **void \*** means a pointer which is a

legal address but it is not address of a **char**, or address of an **int**, or address of any other datatype. Hence it has been converted into **char \*** using a C language feature called typecasting. Typecasting will be discussed in detail in Chapter 22. The prototype of this function has been declared in the header file ‘stdlib.h’. Hence we have **#include**d this file.

But why did we not use array to allocate memory? This is because, with arrays, we have to commit to the size of the array at the time of writing the program. Moreover, there is no way to increase or decrease the array size during execution of the program. In other words, when we use arrays, static memory allocation takes place. Unlike this, using **malloc( )**, we can allocate memory dynamically, during execution. The argument that we pass to **malloc( )** can be a variable whose value can change during execution.

Once we have allocated the memory using **malloc( )**, we have copied the name received through the keyboard into this allocated space and finally stored the address of the allocated chunk in the appropriate element of **names\[ \]**, the array of pointers to strings.

This solution suffers in performance because we need to allocate memory and then do the copying of string for each name received through the keyboard.

### Summary

- Though in principle a 2-D array can be used to handle several strings, in practice an array of pointers to strings is preferred since it takes less space and is efficient in processing strings.

- **malloc( )** function can be used to allocate space in memory on the fly during execution of the program.

### Exercise

**\[A\]** Answer the following:

- How many bytes in memory would be occupied by the following array of pointers to strings? How many bytes would be required to store the same strings, if they are stored in a two-dimensional character array?

char \*mess\[ \] = { "Hammer and tongs", "Tooth and nail", "Spit and polish", "You and C" } ;

- Can an array of pointers to strings be used to collect strings from the keyboard? If yes, how? If not, why not?

**\[B\]** Attempt the following:

- Write a program that uses an array of pointers to strings **str\[ \]**. Receive two strings **str1** and **str2** and check if **str1** is embedded in any of the strings in **str\[ \]**. If **str1** is found, then replace it with **str2**.

char \*str\[ \] = { "We will teach you how to...", "Move a mountain", "Level a building", "Erase the past", "Make a million", "...all through C!" } ;

For example if **str1** contains "mountain" and **str2** contains "car", then the second string in **str** should get changed to "Move a car".

- Write a program to sort a set of names stored in an array in alphabetical order.

- Write a program to reverse the strings stored in the following array of pointers to strings:

char \*s\[ \] = { "To err is human...", "But to really mess things up...", "One needs to know C!!" } ;

- Develop a program that receives the month and year from the keyboard as integers and prints the calendar in the following format.

April 2015

Mon Tue Wed Thu Fri Sat Sun

1 2 3 4 5

6 7 8 9 10 11 12

13 14 15 16 17 18 19

20 21 22 23 24 25 26

27 28 29 30

Note that according to the Gregorian calendar 01/01/01 was Monday. With this as the base, the calendar should be generated.

- A factory has 3 divisions and stocks 4 categories of products. An inventory table is updated for each division and for each product as they are received. There are three independent suppliers of products to the factory.

1\. Design a data format to represent each transaction. 2. Write a program to take a transaction and update the inventory. 3. If the cost per item is also given write a program to calculate the

total inventory values.

- Modify the above program suitably so that once the calendar for a particular month and year has been displayed on the screen, then using arrow keys the user must be able to change the calendar in the following manner:

Up arrow key : Next year, same month

Down arrow key : Previous year, same month

Right arrow key : Same year, next month

Left arrow key : Same year, previous month

If the Escape (Esc) key is hit then the procedure should stop.

Hint: Use the **getkey( )** function discussed in Chapter 14, problem number \[C\](d).

- Write a program to delete all vowels from a sentence. Assume that the sentence is not more than 80 characters long.

- Write a program that will read a line and delete from it all occurrences of the word ‘the’.

- Write a program that takes a set of names of individuals and abbreviates the first, middle and other names except the last name by their first letter.

- Write a program to count the number of occurrences of any two vowels in succession in a line of text. For example, in the following sentence:

“Please read this application and give me gratuity”

such occurrences are ea, ea, ui.

- Write a program that receives an integer (less than or equal to nine digits in length) and prints out the number in words. For example, if the number input is 12342, then the output should be Twelve Thousand Three Hundred Forty Two.

- Write a program that receives a 5-digit number and prints it out in large size as shown below.

\##### ##### # # ######

\# # ## # #

\# # # # #

\##### # # # # ######

\# ##### # # # ### #

\# # # # #

\# # # # #

\##### ##### ### # #### #