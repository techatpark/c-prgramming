---
title: 'Operations On'
weight: 21
---

   

o far we have dealt with characters, integers, floats and their variations. The smallest element in memory on which we are able to

operate as yet is a byte; and we operated on it by making use of the data type **char**. However, we haven’t attempted to look within these data types to see how they are constructed out of individual bits, and how these bits can be manipulated. Being able to operate on a bit-level, can be very important in programming, especially when a program must interact directly with the hardware. This is because, the programming languages are byte-oriented, whereas hardware tends to be bit- oriented. Let us now delve inside the byte and see how it is constructed and how it can be manipulated effectively. So let us take apart the byte... bit-by-bit.

**Bit Numbering and Conversion** A bit (short for Binary Digit) is the most basic unit of information. It can take a value 0 or 1. 4 bits together form a nibble, 8 bits form a byte, 16 bits form a word and 32 bits form a double-word. Bits are numbered from zero onwards, increasing from right to left as shown in Figure 21.1.

0123456789101112131415

16-bit Integer

Character

01234567

Figure 21.1

Suppose we wish to store binary values 10110110 and 00111100 in 2 bytes. If we are required to do this through a C program we won't be able to use these bit patterns directly. This is because C language doesn’t understand binary numbering system. So we need to convert these binary numbers into decimal numbers. This conversion is shown in Figure 21.2.

### S

1 0 1 1 0 1 1 0

7 6 5 4 3 2 1 0

0 \* 20 + 1 \* 21 + 1 \* 22 + 0 \* 23 + 1 \* 24 + 1 \* 25 + 0 \* 26 + 1 \* 27

\= 2 + 4 + 16 + 32 + 128

\= 182

0 0 1 1 1 1 0 0

7 6 5 4 3 2 1 0

0 \* 20 + 0 \* 21 + 1 \* 22 + 1 \* 23 + 1 \* 24 + 1 \* 25 + 0 \* 26 + 0 \* 27

\= 4 + 8 + 16 + 32

\= 60

Figure 21.2

As you can see from Figure 21.2 the binary to decimal conversion process involves remembering powers of 2. This is alright if the binary number is a 8-bit number, but if it is a 16-bit number then remembering powers like 215, 214, 213, etc., is difficult. A much easier method is to convert binary numbers to hexadecimal numbers. As you might be aware, in hexadecimal numbering system each number is built using a combination of digits 0 to 9 and A to F. Digits A to F are symbols used to represent value 10 to 15. Each hexadecimal digit can be represented using a 4-bit nibble as shown in Figure 21.3.

### Hex Binary Hex Binary

0

1

2

3

4

5

6

7

0000

0001

0010

0011

0100

0101

0110

0111

8

9

A

B

C

D

E

F

1000

1001

1010

1011

1100

1101

1110

1111

Figure 21.3

Using Figure 21.3, it is very easy to convert binary values into their equivalent hexadecimal values. This is shown in Figure 21.4.

1 0 1 1 0 1 1 0

7 6 5 4 3 2 1 0

0 0 1 1 1 1 0 0

7 6 5 4 3 2 1 0

B 6

3 C

0xB6

0x3C

Figure 21.4

You would agree this is an easier way to represent the binary number than to find its decimal equivalent. In this method, neither multiplication nor addition is needed. In fact, since there are only 16 hex digits, it’s fairly easy to memorize the binary equivalent of each one. Quick now, what’s binary 1100 in hex? That’s right—C. You are already getting the

feel of it. With a little practice, it is easy to translate even long numbers into hex. Thus, 1100 0101 0011 1010 binary is C53A hex.

As it happens with many unfamiliar subjects, learning hexadecimal numbers requires a little practice. Try your hand at converting some binary numbers and vice versa. Soon you will be talking hexadecimal as if you had known it all your life.

**Bit Operations** Now that we have understood the bit numbering and the binary to hex conversion process it is time to access or manipulate bits. Here are some examples of operations that we may wish to perform on bits:

- Set bit 3 to 0 (b) Set bit 5 to 1 (c) Check whether bit 6 is 1 (on) or 0 (off)

As you can see, in the first two examples we are manipulating (writing) a bit, whereas, in the third example we are accessing (reading) a bit. To be able to access or manipulate individual bits C language provides a powerful set of bit manipulation operators. These are shown in Figure 21.5.

### Operator Meaning

~

\>>

<<

&

|

^

One’s complement

Right shift

Left shift

Bitwise AND

Bitwise OR

Bitwise XOR(Exclusive OR)

Figure 21.5

These operators can operate on **int**s and **char**s but not on **float**s and **double**s. Before we examine each of these operators, let me introduce you to a function called **showbits( )**. Throughout this discussion about bitwise operators, we are going to use this function, but we are not going to discuss the details of this function immediately. The task of **showbits( )** is to display the binary representation of any integer or

character value that it receives. Let us begin with a plain-jane example with **showbits( )** in action.

/\* Print binary equivalent of characters using showbits( ) function \*/ # include <stdio.h> void showbits ( unsigned char ) ; int main( ) { unsigned char num ; for ( num = 0 ; num <= 5 ; num++ ) { printf ( "\\nDecimal %d is same as binary ", num ) ; showbits ( num ) ; } return 0 ; } void showbits ( unsigned char n ) { int i ; unsigned char j, k, andmask ; for ( i = 7 ; i >= 0 ; i-- ) { j = i ; andmask = 1 << j ; k = n & andmask ; k == 0 ? printf ( "0" ) : printf ( "1" ) ; } }

On execution the program produces the following output...

Decimal 0 is same as binary 00000000 Decimal 1 is same as binary 00000001 Decimal 2 is same as binary 00000010 Decimal 3 is same as binary 00000011 Decimal 4 is same as binary 00000100 Decimal 5 is same as binary 00000101

Let us now explore the various bitwise operators one-by-one.

**One’s Complement Operator** On taking one’s complement of a number, all 1’s present in the number are changed to 0’s and all 0’s are changed to 1’s. For example, one’s complement of 1010 is 0101. Similarly, one’s complement of 1111 is 0000. Note that, here when we talk of a number, we are talking of binary equivalent of the number. Thus, one’s complement of 65 means one’s complement of 0100 0001, which is binary equivalent of 65. One’s complement of 65 therefore would be 1011 1110. One’s complement operator is represented by the symbol ~ (tilde). Following program shows one’s complement operator in action:

#include <stdio.h> int main( ) { unsigned char ch = 32 ; unsigned char dh ; dh = ~ch ; printf ( "~ch = %d\\n", dh ) ; printf ( "~ch = %x\\n", dh ) ; printf ( "~ch = %X\\n", dh ) ; return 0 ; }

On execution the program produces the following output:

~ch = 223 ~ch = df ~ch = DF

Here **ch** contains a value 32, whose binary equivalent is 00100000. On taking one's complement of it, we get 11011111, which in decimal is 223. As we learnt earlier, hexadecimal equivalent of 11011111 is DF. The hexadecimal equivalent gets printed in smallcase if we use **%x** and in capital if we use **%X**.

Let us try one more program that prints one's complement of different numbers in a loop. Once again to print the binary equivalent of a number we have used the **showbits( )** function.

\# include <stdio.h> void showbits ( unsigned char ) ; int main( ) { unsigned char num, k ; for ( num = 0 ; num <= 3 ; num++ ) { printf ( "\\nDecimal %d is same as binary ", num ) ; showbits ( num ) ; k = ~num ; printf ( "\\nOne's complement of %d is ", num ) ; showbits ( k ) ; } return 0 ; } void showbits ( unsigned char n ) { int i ; unsigned char j, k, andmask ; for ( i = 7 ; i >= 0 ; i-- ) { j = i ; andmask = 1 << j ; k = n & andmask ; k == 0 ? printf ( "0" ) : printf ( "1" ) ; } }

And here is the output of the above program...

Decimal 0 is same as binary 00000000 One’s complement of 0 is 11111111 Decimal 1 is same as binary 00000001 One’s complement of 1 is 11111110 Decimal 2 is same as binary 00000010 One’s complement of 2 is 11111101

Decimal 3 is same as binary 00000011 One’s complement of 3 is 11111100

**Right Shift Operator** The right shift operator is represented by >>. It needs two operands. It shifts each bit in its left operand to the right. The number of places the bits are shifted depends on the number following the operator (i.e., its right operand). Thus, **ch >> 3** would shift all bits in **ch** three places to the right. Similarly, **ch >> 5** would shift all bits 5 places to the right.

If the variable **ch** contains the bit pattern 11010111, then, **ch >> 1** would give 01101011 and **ch >> 2** would give 00110101.

Note that as the bits are shifted to the right, blanks are created on the left. These blanks must be filled somehow. They are always filled with zeros. The following program demonstrates the effect of right shift operator:

\# include <stdio.h> void showbits ( unsigned char ) ; int main( ) { unsigned char num = 225, i, k ; printf ( "\\nDecimal %d is same as binary ", i ) ; showbits ( i ) ; for ( i = 0 ; i <= 5 ; i++ ) { k = num >> i ; printf ( "\\n%d right shift %d gives ", num, i ) ; showbits ( k ) ; } return 0 ; } void showbits ( unsigned char n ) { int i ; unsigned char j, k, andmask ;

for ( i = 7 ; i >= 0 ; i-- ) { j = i ; andmask = 1 << j ; k = n & andmask ; k == 0 ? printf ( "0" ) : printf ( "1" ) ; } }

The output of the above program would be...

Decimal 225 is same as binary 11100001 5225 right shift 0 gives 11100001 5225 right shift 1 gives 01110000 5225 right shift 2 gives 00111000 5225 right shift 3 gives 00011100 5225 right shift 4 gives 00001110 5225 right shift 5 gives 00000111

Note that if the operand is a multiple of 2, then shifting the operand 1 bit to right is same as dividing it by 2 and ignoring the remainder. Thus,

64 >> 1 gives 32 64 >> 2 gives 16 128 >> 2 gives 32

but,

27 >> 1 is 13 49 >> 1 is 24 .

### A Word of Caution

In the expression **a >> b** if **b** is negative the result is unpredictable. If **a** is negative then its left most bit (sign bit) would be 1. On right shifting **a** it would result in extending the sign bit. For example, if **a** contains -1, its binary representation would be 11111111. If we right shift it by 4 then the result would still be 11111111. Similarly, if **a** contains -5, then its binary equivalent would be 11111011. On right shifting it by 1 we would get 11111101, which is equal to -3. Thus on right shifting 11111011 the right-most bit, i.e. 1, would be lost; other bits would be shifted one position to the right and the sign which was negative (1) will be

extended, i.e., it would be preserved as 1. The following program, would help you get a clear picture of this:

\# include <stdio.h> void showbits ( unsigned char ) ; int main( ) { char num = -5, j, k ; printf ( "\\nDecimal %d is same as binary ", num ) ; showbits ( num ) ; for ( j = 1 ; j <= 3 ; j++ ) { k = num >> j ; printf ( "\\n%d right shift %d gives ", num, j ) ; showbits ( k ) ; } return 0 ; } void showbits ( unsigned char n ) { int i ; unsigned char j, k, andmask ; for ( i = 7 ; i >= 0 ; i-- ) { j = i ; andmask = 1 << j ; k = n & andmask ; k == 0 ? printf ( "0" ) : printf ( "1" ) ; } }

The output of the above program would be...

Decimal -5 is same as binary 11111011 -5 right shift 1 gives 11111101 -5 right shift 2 gives 11111110 -5 right shift 3 gives 11111111

**Left Shift Operator** The left shift operator (<<) is similar to the right shift operator (>>), the only difference being that the bits are shifted to the left, and for each bit shifted, a 0 is added to the right of the number. The following program should clarify this point:

\# include <stdio.h> void showbits ( unsigned char ) ; int main( ) { unsigned char num = 225, j, k ; printf ( "\\nDecimal %d is same as binary ", num ) ; showbits ( num ) ; for ( j = 0 ; j <= 4 ; j++ ) { k = num << j ; printf ( "\\n%d left shift %d gives ", num, j ) ; showbits ( k ) ; } return 0 ; } void showbits ( unsigned char n ) { int i ; unsigned char j, k, andmask ; for ( i = 7 ; i >= 0 ; i-- ) { j = i ; andmask = 1 << j ; k = n & andmask ; k == 0 ? printf ( "0" ) : printf ( "1" ) ; } }

The output of the above program would be...

Decimal 225 is same as binary 11100001 225 left shift 0 gives 11100001 225 left shift 1 gives 11000010 225 left shift 2 gives 10000100 225 left shift 3 gives 00001000

### Utility of Left Shift Operator

The left shift operator is often used to create a number with a particular bit in it set to 1. For example, we can create a number with its 3rd bit set to 1. The following program shows how this can be achieved:

\# include <stdio.h> int main( ) { unsigned char a ; a = 1 << 3 ; printf ( "a = %02x", a ) ; return 0 ; }

Binary value of 1 is 00000001. On left-shifting this by 3 we get 00001000. Thus we are able to create a value with its 3rd bit set to 1. Such operations are required quite often while writing programs that interact with hardware or while building embedded systems. Hence it is often done using a macro as shown below.

\# define \_BV(x) ( 1 << x ) # include <stdio.h> int main( ) { unsigned char a ; a = \_BV(3) ; printf ( "a = %02x", a ) ; return 0 ; }

The **\_BV** macro stands for **Bit Value**. Its argument indicates which bit in the number would be set when this macro is used. As you must have guessed, during processing the macro **\_BV( 3 )** would get expanded to **1 << 3**.

Note the use of the format specifier **%02x** in the **printf( )** function. This ensures that the output is printed in 2 columns, with a leading 0, if required. Thus the output of both the programs would be 08.

**Bitwise AND Operator** This operator is represented as **&**. Remember it is different than **&&**, the logical AND operator. The **&** operator operates on two operands. While operating upon these two operands they are compared on a bit-by-bit basis. Hence both the operands must be of the same type (either **char** or **int**). The second operand is often called an AND mask. The **&** operator operates on a pair of bits to yield a resultant bit. The rules that decide the value of the resultant bit are shown in Figure 21.6.

### First bit Second bit First bit & Second bit

0

0

1

1

0

1

0

1

0

0

0

1

Figure 21.6

This can be represented in a more understandable form as a ‘Truth Table’ shown in Figure 21.7.

& 0 1

0

1

0 0

0 1

Figure 21.7

The example given in Figure 21.8 shows more clearly what happens while ANDing one operand with another. The rules given in the Figure 21.7 are applied to each pair of bits one-by-one.

This operand when ANDed bitwise

1 0 1 0 1 0 1 0

01234567

1 1 0 0 0 0 1 1

01234567

1 0 0 0 0 0 1 0

01234567

with this operand yields

this result

Figure 21.8

Work through the Truth Table and confirm that the result obtained is really correct.

Thus, it must be clear that the operation is being performed on individual bits, and the operation performed on one pair of bits is completely independent of the operation performed on the other pairs.

### Utility of AND Operator

AND operator is used in two situations:

- To check whether a particular bit of an operand is ON or OFF. (b) To turn OFF a particular bit.

Both these uses are discussed in the following example.

Suppose, from the bit pattern 10101101 (0xAD) of an operand, we want to check whether bit number 5 is ON (1) or OFF (0). Since we want to check the bit number 5, the second operand for the AND operation should be 00100000. This second operand if often known as AND mask. The ANDing operation is shown below.

10101101 Original bit pattern 00100000 AND mask -------------- 00100000 Resulting bit pattern

The resulting value we get in this case is 32 (or 0x20), i.e., the value of the second operand. The result turned out to be 32 (or 0x20) since the fifth bit of the first operand was ON. Had it been OFF, the bit number 5 in the resulting bit pattern would have evaluated to 0 and the complete bit pattern would have been 00000000.

Thus, depending upon the bit number to be checked in the first operand, we decide the second operand, and on ANDing these two operands the result decides whether the bit was ON or OFF. If the bit is ON (1), the resulting value turns out to be a non-zero value, which is equal to the value of second operand. If the bit is OFF (0), the result is zero, as seen above.

Let us now turn our attention to the second use of the AND operator. As you can see, in the bit pattern 10101101 (0xAD), 3rd bit is ON. To put it off, we need to AND the 3rd bit with 0. While doing so the values of other bits in the pattern should not get disturbed. For this we need to AND the other bits with 1. This operation is shown below.

10101101 Original bit pattern 11110111 AND mask -------------- 10100101 Resulting bit pattern

The following program puts this logic into action:

\# include <stdio.h> void showbits ( unsigned char ) ; int main( ) { unsigned char num = 0xAD, j ; printf ( "\\nValue of num = " ) ; showbits ( num ) ; j = num & 0x20 ; if ( j == 0 ) printf ( "\\nIts fifth bit is off" ) ; else printf ( "\\nIts fifth bit is on" ) ;

j = num & 0x08 ; if ( j == 0 ) printf ( "\\nIts third bit is off" ) ; else { printf ( "\\nIts third bit is on" ) ; num = num & 0xF7 ; printf ( "\\nNew value of num = " ) ; showbits ( num ) ; j = num & 0x08 ; if ( j == 0 ) printf ( "\\nNow its third bit is turned off" ) ; } return 0 ; } void showbits ( unsigned char n ) { int i ; unsigned char j, k, andmask ; for ( i = 7 ; i >= 0 ; i-- ) { j = i ; andmask = 1 << j ; k = n & andmask ; k == 0 ? printf ( "0" ) : printf ( "1" ) ; } }

And here is the output...

Value of num = 10101101 Its fifth bit is on Its third bit is on New value of num = 10100101 Now its third bit is turned off

Note the use of **&** operator in the statements:

j = num & 0x20 ; j = num & 0x08 ; num = num & 0xF7 ;

A quick glance at these statements does not indicate what operation is being carried out through them. Hence a better idea is to use the macro **\_BV** as shown below.

\# define \_BV(x) ( 1 << x ) j = num & \_BV( 5 ) ; j = num & \_BV( 3 ) ; num = num & ~ \_BV( 3 ) ;

In the last statement **\_BV( 3 )** would yield 00001000 and one's complement of this number would fetch 11110111.

**Bitwise OR Operator** Another important bitwise operator is the OR operator which is represented as **|**. The rules that govern the value of the resulting bit obtained after ORing of two bits is shown in the Truth Table shown in Figure 21.9.

| 0 1

0

1

0 1

1 1

Figure 21.9

Using the Truth Table confirm the result obtained on ORing the two operands as shown below.

11010000 Original bit pattern 00000111 OR mask -------------

11010111 Resulting bit pattern

Bitwise OR operator is usually used to put ON a particular bit in a number.

Let us consider the bit pattern 11000011. If we want to put ON bit number 3, then the OR mask to be used would be 00001000. Note that all the other bits in the mask are set to 0 and only the bit, which we want to set ON in the resulting value is set to 1. The code snippet which will achieve this is given below.

\# define \_BV(x) ( 1 << x ) unsigned char num = 0xC3 ; num = num | \_BV( 3 ) ;

**Bitwise XOR Operator** The XOR operator is represented as **^** and is also called an Exclusive OR Operator. The OR operator returns 1, when any one of the two bits or both the bits are 1, whereas XOR returns 1 only if one of the two bits is 1. The Truth Table for the XOR operator is shown in Figure 21.10.

^ 0 1

0

1

0 1

1 0

Figure 21.10

XOR operator is used to toggle (change) a bit ON or OFF. A number XORed with another number twice gives the original number. This is shown in the following program:

\# include <stdio.h> int main( ) { unsigned char b = 0x32 ; /\* Binary 00110010 \*/

b = b ^ 0x0C ; printf ( "\\n%02x", b ) ; /\* this will print 0x3E \*/ b = b ^ 0x0C ; printf ( "\\n%02x", b ) ; /\* this will print 0x32 \*/ return 0 ; }

**The _showbits( )_ Function** We have used this function quite often in this chapter. Now we have sufficient knowledge of bitwise operators and hence are in a position to understand it. The function is given below followed by brief explanation.

void showbits ( unsigned char n ) { unsigned char i, k, andmask ; for ( i = 7 ; i >= 0 ; i-- ) { andmask = 1 << i ; k = n & andmask ; k == 0 ? printf ( "0" ) : printf ( "1" ) ; } }

All that is being done in this function is, using an AND operator and a variable **andmask**, we are checking the status of individual bits of **n**. If the bit is OFF we print a 0, otherwise we print a 1.

First time through the loop, the variable **andmask** will contain the value 10000000, which is obtained by left-shifting 1, seven places. If the variable **n’**s most significant bit (leftmost bit) is 0, then **k** would contain a value 0, otherwise it would contain a non-zero value. If **k** contains 0, then **printf( )** will print out 0, otherwise it will print out 1.

In the second go-around of the loop, the value of **i** is decremented and hence the value of **andmask** changes, which will now be 01000000. This checks whether the next most significant bit is 1 or 0, and prints it out accordingly. The same operation is repeated for all bits in the number.

**Bitwise Compound Assignment Operators** Consider the following bitwise operations:

unsigned char a = 0xFA, b = 0xA7, c = 0xFF, d = 0xA3, e = 0x43 ; a = a << 1 ; b = b >> 2 ; c = c | 0x2A ; d = d & 0x4A ; e = e ^ 0x21 ;

These operations can be written more elegantly and in a compact fashion as shown below.

unsigned char a = 0xFA, b = 0xA7, c = 0xFF, d = 0xA3, e = 0x43 ; a <<= 1 ; b >>= 2 ; c |= 0x2A ; d &= 0x4A ; e ^= 0x21 ;

The operators **<<=**, **\>>=**, **|=**, **&=** and **^=** are called bitwise compound assignment operators. Note that there does not exist an operator **~=**. This is because ~ is a unary operator and needs only one operand.

### Summary

- To help manipulate hardware oriented data—individual bits rather than bytes a set of bitwise operators are used.

- It is convenient to convert binary numbers into their hexadecimal equivalents than converting them to their decimal equivalents.

- The bitwise operators include operators like one’s complement, right-shift, left-shift, bitwise AND, OR, and XOR.

- The one’s complement converts all 0s in its operand to 1s and all 1s to 0s.

- The right-shift and left-shift operators are useful in eliminating bits from a number—either from the left or from the right.

- The bitwise AND operators is useful in testing whether a bit is on/off and in putting off a particular bit.

- The bitwise OR operator is used to turn on a particular bit.

- The XOR operator works almost same as the OR operator except one minor variation.

### Exercise

**\[A\]** Answer the following:

- The information about colors is to be stored in bits of a **char** variable called **color**. The bit number 0 to 6, each represent 7 colors of a rainbow, i.e., bit 0 represents violet, 1 represents indigo, and so on. Write a program that asks the user to enter a number and based on this number it reports which colors in the rainbow do the number represents.

- A company planning to launch a new newspaper in market conducts a survey. The various parameters considered in the survey were, the economic status (upper, middle, and lower class) the languages readers prefer (English, Hindi, Regional language) and category of paper (daily, supplement, tabloid). Write a program, which reads data of 10 respondents through keyboard, and stores the information in an array of integers. The bit-wise information to be stored in an integer is given below:

Bit Number Information

0 Upper class 1 Middle class 2 Lower class 3 English 4 Hindi 5 Regional Language 6 Daily 7 Supplement 8 Tabloid

At the end give the statistical data for number of persons who read English daily, number of Upper class people who read Tabloid and number of Regional Language readers.

- In an inter-college competition, various sports like cricket, basketball, football, hockey, lawn tennis, table tennis, carom and chess are played between different colleges. The information regarding the games won by a particular college is stored in bit numbers 0, 1, 2, 3, 4, 5, 6, 7 and 8, respectively of an integer

variable called **game**. The college that wins in 5 or more than 5 games is awarded the Champion of Champions trophy. If a number representing the bit pattern mentioned above is entered through the keyboard then write a program to find out whether the college won the Champion of the Champions trophy or not, along with the names of the games won by the college.

- An animal could be a canine (dog, wolf, fox, etc.), a feline (cat, lynx, jaguar, etc.), a cetacean (whale, narwhal, etc.) or a marsupial (koala, wombat, etc.). The information whether a particular animal is canine, feline, cetacean, or marsupial is stored in bit number 0, 1, 2 and 3, respectively of a integer variable called **type**. Bit number 4 of the variable **type** stores the information about whether the animal is Carnivore or Herbivore.

For the following animal, complete the program to determine whether the animal is a herbivore or a carnivore. Also determine whether the animal is a canine, feline, cetacean or a marsupial.

struct animal { char name\[ 30 \] ; int type ; } struct animal a = { "OCELOT", 18 } ;

- The time field in a structure is 2 bytes long. Distribution of different bits which account for hours, minutes and seconds is given in Figure 21.11. Write a function which would receive the 2-byte time and return to the calling function, the hours, minutes and seconds.

H H H H H M M M M M M S S S S S

0123456789101112131415

Figure 21.11

- In order to save disk space, information about student is stored in an integer variable. If bit number 0 is on then it indicates Ist year student, bit number 1 to 3 stores IInd year, IIIrd year and IVth year student, respectively. Bits 4 to 7 store the stream Mechanical, Chemical, Electronics and IT. Rest of the bits store room number. Based on the given data, write a program that asks for the room

number and displays the information about the student, if its data exists in the array. The contents of array are,

int data\[ \] = { 273, 548, 786, 1096 } ;

- What will be the output of the following program:

\# include <stdio.h> int main( ) { int i = 32, j = 65, k, l, m, n, o, p ; k = i | 35 ; l = ~k ; m = i & j ; n = j ^ 32 ; o = j << 2 ; p = i >> 5 ; printf ( "k = %d l = %d m = %d\\n", k, l, m ) ; printf ( "n = %d o = %d p = %d\\n", n, o, p ) ; return 0 ; }

**\[B\]** Answer the following:

- What is hexadecimal equivalent of the following binary numbers:

0101 1010 11000011 1010101001110101 1111000001011010

- Rewrite the following expressions using bitwise compound assignment operators:

a = a | 3 a = a & 0x48 b = b ^ 0x22 c = c << 2 d = d >> 4

- Consider an unsigned integer in which rightmost bit is numbered as 0. Write a function **checkbits ( x, p, n )** which returns true if all "n" bits starting from position "p" are turned on. For example, **checkbits ( x, 4, 3 )** will return true if bits 4, 3 and 2 are 1 in number x.

- Write a program to scan a 8-bit number into a variable and check whether its 3rd, 6th and 7th bit is on.

- Write a program to receive an unsigned 16-bit integer and then exchange the contents of its 2 bytes using bitwise operators.

- Write a program to receive a 8-bit number into a variable and then exchange its higher 4 bits with lower 4 bits.

- Write a program to receive a 8-bit number into a variable and then set its odd bits to 1.

- Write a program to receive a 8-bit number into a variable and then if its 3rd and 5th bit are on. If these bits are found to be on then put them off.

- Write a program to receive a 8-bit number into a variable and then if its 3rd and 5th bit are off. If these bits are found to be off then put them on.

- Rewrite the **showbits( )** function used in this chapter using the **\_BV** macro.

