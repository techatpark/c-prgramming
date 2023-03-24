---
title: 'The C Preprocessor'
weight: 7
---

   

he C preprocessor is exactly what its name implies. It is a program that processes our source program before it is passed to the

compiler. Preprocessor commands (often known as directives) form what can almost be considered a language within C language. We can certainly write C programs without knowing anything about the preprocessor or its facilities. But preprocessor is such a great convenience that virtually all C programmers rely on it. This chapter explores the preprocessor directives, and discusses the pros and cons of using them in programs.

**Features of C Preprocessor** There are several steps involved from the stage of writing a C program to the stage of getting it executed. The combination of these steps is known as the ‘Build Process’. The detailed build process is discussed in the last section of this chapter. At this stage it would be sufficient to note that before a C program is compiled it is passed through another program called ‘Preprocessor’. The C program is often known as ‘Source Code’. The Preprocessor works on the source code and creates ‘Expanded Source Code’. If the source code is stored in a file PR1.C, then the expanded source code gets stored in a file PR1.I. It is this expanded source code that is sent to the compiler for compilation.

The preprocessor offers several features called preprocessor directives. Each of these preprocessor directives begins with a # symbol. The directives can be placed anywhere in a program but are most often placed at the beginning of a program, before the first function definition. We would learn the following preprocessor directives here:

- Macro expansion (b) File inclusion (c) Conditional compilation (d) Miscellaneous directives

Let us understand these features of preprocessor one-by-one.

**Macro Expansion** Have a look at the following program:

\# include <stdio.h> # define UPPER 25 int main( ) { int i ;

T

for ( i = 1 ; i <= UPPER ; i++ ) printf ( "%d\\n", i ) ;

return 0 ; }

In this program, instead of writing 25 in the **for** loop we are writing it in the form of UPPER, which has already been defined before **main( )** through the statement,

\# define UPPER 25

This statement is called ‘macro definition’ or more commonly, just a ‘macro’. What purpose does it serve? During preprocessing, the preprocessor replaces every occurrence of UPPER in the program with 25. Here is another example of macro definition.

\# include <stdio.h> # define PI 3.1415 int main( ) { float r = 6.25 ; float area ; area = PI \* r \* r ; printf ( "Area of circle = %f\\n", area ) ;

return 0 ; }

UPPER and PI in the above programs are often called ‘macro templates’, whereas, 25 and 3.1415 are called their corresponding ‘macro expansions’.

When we compile the program, before the source code passes to the compiler, it is examined by the C preprocessor for any macro definitions. When it sees the **#define** directive, it goes through the entire program in search of the macro templates; wherever it finds one, it replaces the macro template with the appropriate macro expansion. Only after this procedure has been completed, is the program handed over to the compiler.

In C programming, it is customary to use capital letters for macro template. This makes it easy for programmers to pick out all the macro templates when reading through the program.

Note that a macro template and its macro expansion are separated by blanks or tabs. A space between **#** and **define** is optional. Remember that a macro definition is never to be terminated by a semicolon.

And now a million dollar question... why use **#define** in the above programs? What have we gained by substituting PI for 3.1415 in our program? Probably, we have made the program easier to read.

There is perhaps a more important reason for using macro definition than mere readability. Suppose a constant like 3.1415 appears many times in your program. This value may have to be changed some day to 3.141592. Ordinarily, you would need to go through the program and manually change each occurrence of the constant. However, if you have defined PI in a **#define** directive, you only need to make one change, in the **#define** directive itself:

\# define PI 3.141592

Beyond this, the change will be made automatically to all occurrences of PI before the beginning of compilation.

In short, it is nice to know that you would be able to change values of a constant at all the places in the program by just making a change in the **#define** directive. This convenience may not matter for small programs shown above, but with large programs, macro definitions are almost indispensable.

But the same purpose could have been served had we used a variable **pi** instead of a macro template **PI**. A variable could also have provided a meaningful name for a constant and permitted one change to affect many occurrences of the constant. It’s true that a variable can be used in this way. Then, why not use it? For three reasons it’s a bad idea.

Firstly, it is inefficient, since the compiler can generate faster and more compact code for constants than it can for variables. Secondly, using a variable for what is really a constant encourages sloppy thinking and makes the program more difficult to understand: if something never changes, it is hard to imagine it as a variable. And thirdly, there is always a danger that the variable may inadvertently get altered somewhere in the program. So it’s no longer a constant that you think it is.

Thus, using **#define** can produce more efficient and more easily understandable programs. This directive is used extensively by C programmers, as you will see in many programs in this book.

Following three examples show places where a **#define** directive is popularly used by C programmers.

A **#define** directive is many a time used to define operators as shown below.

\# include <stdio.h> # define AND && # define OR || int main( ) { int f = 1, x = 4, y = 90 ; if ( ( f < 5 ) AND ( x <= 20 OR y <= 45 ) ) printf ( "Your PC will always work fine...\\n" ) ; else printf ( "In front of the maintenance man\\n" ) ;

return 0 ; }

A **#define** directive could be used even to replace a condition, as shown below.

\# include <stdio.h> # define AND && # define ARANGE ( a > 25 AND a < 50 ) int main( ) { int a = 30 ; if ( ARANGE ) printf ( "within range\\n" ) ; else printf ( "out of range\\n" ) ;

return 0 ; }

A **#define** directive could be used to replace even an entire C statement. This is shown below.

\# include <stdio.h> # define FOUND printf ( "The Yankee Doodle Virus\\n" ) ;

int main( ) { char signature ; if ( signature == 'Y' ) FOUND else printf ( "Safe... as yet !\\n" ) ;

return 0 ; }

### Macros with Arguments

The macros that we have used so far are called simple macros. Macros can have arguments, just as functions can. Here is an example that illustrates this fact.

\# include <stdio.h> # define AREA(x) ( 3.14 \* x \* x ) int main( ) { float r1 = 6.25, r2 = 2.5, a ; a = AREA ( r1 ) ; printf ( "Area of circle = %f\\n", a ) ; a = AREA ( r2 ) ; printf ( "Area of circle = %f\\n", a ) ;

return 0 ; }

Here’s the output of the program...

Area of circle = 122.656250 Area of circle = 19.625000

In this program, wherever the preprocessor finds the phrase **AREA(x)** it expands it into the statement **( 3.14 \* x \* x )**. However, that’s not all that it does. The **x** in the macro template **AREA(x)** is an argument that matches the **x** in the macro expansion **( 3.14 \* x \* x )**. The statement **AREA(r1)** in the program causes the variable **r1** to be substituted for **x**. Thus the statement **AREA(r1)** is equivalent to:

( 3.14 \* r1 \* r1 )

After the above source code has passed through the preprocessor, what the compiler gets to work on will be this:

\# include <stdio.h> int main( ) { float r1 = 6.25, r2 = 2.5, a ; a = 3.14 \* r1 \*r1 ; printf ( "Area of circle = %f\\n", a ) ; a = 3.14 \*r2 \* r2 ; printf ( "Area of circle = %f\\n", a ) ;

return 0 ; }

Here is another example of macros with arguments:

\# include <stdio.h> # define ISDIGIT(y) ( y >= 48 && y <= 57 ) int main( ) { char ch ; printf ( "Enter any digit " ) ; scanf ( "%c", &ch ) ; if ( ISDIGIT ( ch ) ) printf ( "You entered a digit\\n" ) ; else printf ( "Illegal input\\n" ) ;

return 0 ; }

Here are some important points to remember while writing macros with arguments:

- Be careful not to leave a blank between the macro template and its argument while defining the macro. For example, there should be

no blank between **AREA** and **(x)** in the definition, #define AREA(x) ( 3.14 \* x \* x )

If we were to write **AREA (x)** instead of **AREA(x)**, the **(x)** would become a part of macro expansion, which we certainly don’t want. What would happen is, the template would be expanded to

( r1 ) ( 3.14 \* r1 \* r1 )

which won’t run. Not at all what we wanted.

- The entire macro expansion should be enclosed within parentheses. Here is an example of what would happen if we fail to enclose the macro expansion within parentheses.

\# include <stdio.h> # define SQUARE(n) n \* n int main( ) { int j ; j = 64 / SQUARE ( 4 ) ; printf ( "j = %d\\n", j ) ; return 0 ; }

The output of the above program would be:

j = 64

whereas, what we expected was j = 4.

What went wrong? The macro was expanded into

j = 64 / 4 \* 4 ;

which yielded 64.

- Macros can be split into multiple lines, with a ‘\\’ (backslash) present at the end of each line. Following program shows how we can define and use multiple line macros.

\# include <stdio.h>

#include <windows.h> void gotoxy ( short int col, short int row ) ; # define HLINE for ( i = 0 ; i < 79 ; i++ ) \\ printf ( "%c", 196 ) ; # define VLINE( X, Y ) { \\ gotoxy ( X, Y ) ; \\ printf ( "%c", 179 ) ; \\ } int main( ) { int i, y ; /\* system( ) will work in Visual Studio. In Turbo C / C++ use clrscr( ) \*/ system ( "cls" ) ; /\* position cursor in row x and column y. Use this function in Visual Studio. If you are using Turbo C / C++ use standard library function gotoxy( ) declared in file conio.h \*/ gotoxy ( 1, 12 ) ; HLINE for ( y = 1 ; y < 25 ; y++ ) VLINE ( 39, y ) ; return 0 ; } void gotoxy ( short int col, short int row ) { HANDLE hStdout = GetStdHandle ( STD\_OUTPUT\_HANDLE ) ; COORD position = { col, row } ; SetConsoleCursorPosition ( hStdout, position ) ; }

This program draws a vertical and a horizontal line in the center of the screen.

- If for any reason, you are unable to debug a macro, then you should view the expanded code of the program to see how the macros are getting expanded. If your source code is present in the file PR1.C then the expanded source code would be stored in PR1.I. You need to generate this file at the command prompt by saying:

cpp pr1.c

Here CPP stands for C PreProcessor. It generates the expanded source code and stores it in a file called PR1.I. You can now open this file and see the expanded source code. Note that the file PR1.I gets generated in C:\\TC\\BIN directory. The procedure for generating expanded source code for compilers other than Turbo C/C++ might be a little different.

### Macros versus Functions

In the above example, a macro was used to calculate the area of the circle. As we know, even a function can be written to calculate the area of the circle. Though macro calls are ‘like’ function calls, they are not really the same things. Then what is the difference between the two?

In a macro call, the preprocessor replaces the macro template with its macro expansion, in a stupid, unthinking, literal way. As against this, in a function call the control is passed to a function along with certain arguments, some calculations are performed in the function and a useful value is returned back from the function.

This brings us to a question: when is it best to use macros with arguments and when is it better to use a function? Usually macros make the program run faster but increase the program size, whereas functions make the program smaller and compact.

If we use a macro hundred times in a program, the macro expansion goes into our source code at hundred different places, thus increasing the program size. On the other hand, if a function is used, then even if it is called from hundred different places in the program, it would take the same amount of space in the program.

But passing arguments to a function and getting back the returned value does take time and would therefore slow down the program. This gets avoided with macros since they have already been expanded and placed in the source code before compilation. Thus the trade-off is between memory space and time.

Moral of the story is—if the macro is simple and sweet like in our examples, it makes nice shorthand and avoids the overheads associated with function calls. On the other hand, if we have a fairly large macro and it is used fairly often, perhaps we ought to replace it with a function.

If memory space in the machine in which the program is being executed is less (like a mobile phone or a tablet), then it may make sense to use functions instead of macros. By doing so, the program may run slower, but will need less memory space.

**File Inclusion** The second preprocessor directive we’ll explore in this chapter is file inclusion. This directive causes one file to be included in another. The preprocessor command for file inclusion looks like this:

\# include "filename"

and it simply causes the entire contents of **filename** to be inserted into the source code at that point in the program. Of course, this presumes that the file being included exists. When and why this feature is used? It can be used in two cases:

- If we have a very large program, the code is best divided into several different files, each containing a set of related functions. It is a good programming practice to keep different sections of a large program separate. These files are **#included** at the beginning of main program file.

- There are some functions and some macro definitions that we need almost in all programs that we write. These commonly needed functions and macro definitions can be stored in a file, and that file can be included in every program we write, which would add all the statements in this file to our program as if we have typed them in.

- When creating our own library of functions which we wish to distribute to others. In this situation the functions are defined in a ".c" file and their corresponding prototype declarations and macros are declared in a ".h" file. While distributing the definitions are compiled into a library file (in machine language) and then the library file and the ".h" file. This way the function definitions in the ".c" file remain with you and are not exposed to users of these functions.

It is common for the files that are to be included to have a .h extension. This extension stands for ‘header file’, because it contains statements which when included go to the head of your program. The prototypes of all the library functions are grouped into different categories and then stored in different header files. For example, prototypes of all mathematics related functions are stored in the header file ‘math.h’, prototypes of console input/output functions are stored in the header file ‘conio.h’, and so on.

Actually there exist two ways to write **#include** statement. These are:

\# include "filename" # include <filename>

The meaning of each of these forms is given below.

\# include "mylib.h" This command would look for the file **mylib.h** in the current directory as well as the specified list of directories as mentioned in the include search path that might have been set up.

\# include <mylib.h> This command would look for the file **mylib.h** in the specified list of directories only.

The include search path is nothing but a list of directories that would be searched for the file being included. Different C compilers let you set the search path in different manners. If you are using Turbo C/C++ compiler, then the search path can be set up by selecting ‘Directories’ from the ‘Options’ menu. On doing this, a dialog box appears. In this dialog box against ‘Include Directories’, we can specify the search path. We can also specify multiple include paths separated by ‘;’ (semicolon) as shown below.

c:\\tc\\lib ; c:\\mylib ; d:\\libfiles

The path can contain maximum of 127 characters. Both relative and absolute paths are valid. For example, ‘..\\dir\\incfiles’ is a valid path.

In Visual Studio the search path for a project can be set by right-clicking the project name in Solution Explorer and selecting "Properties" from the menu that pops up. This brings up a dialog box. You can now set up the search path by going to "Include Directories" in "Configuration Properties" tab.

**Conditional Compilation** We can, if we want, have the compiler skip over part of a source code by inserting the preprocessing commands **#ifdef** and **#endif**, which have the general form given below.

\# ifdef macroname statement 1 ; statement 2 ; statement 3 ; # endif

If **macroname** has been **#define**d, the block of code will be processed as usual; otherwise not.

Where would **#ifdef** be useful? When would you like to compile only a part of your program? In three cases:

- To “comment out” obsolete lines of code. It often happens that a program is changed at the last minute to satisfy a client. This involves rewriting some part of source code to the client’s satisfaction and deleting the old code. But veteran programmers are familiar with the clients who change their mind and want the old code back again just the way it was. Now you would definitely not like to retype the deleted code again.

One solution in such a situation is to put the old code within a pair of /\* - - - \*/ combination. But we might have already written a comment in the code that we are about to “comment out”. This would mean we end up with nested comments. Obviously, this solution won’t work since we can’t nest comments in C.

Therefore, the solution is to use conditional compilation as shown below.

int main( ) { # ifdef OKAY statement 1 ; statement 2 ; /\* detects virus \*/ statement 3 ; statement 4 ; /\* specific to stone virus \*/ # endif

statement 5 ; statement 6 ; statement 7 ; }

Here, statements 1, 2, 3 and 4 would get compiled only if the macro OKAY has been defined, and we have purposefully omitted the definition of the macro OKAY. At a later date, if we want that these statements should also get compiled, all that we are required to do is to delete the **#ifdef** and **#endif** statements.

- A more sophisticated use of **#ifdef** has to do with making the programs portable, i.e., to make them work on two totally different computers. Suppose an organization has two different types of computers and you are expected to write a program that works on both the machines. You can do so by isolating the lines of code that must be different for each machine by marking them off with **#ifdef**. For example:

int main( ) { # ifdef INTEL code suitable for an Intel PC # else code suitable for a Motorola PC # endif code common to both the computers }

When you compile this program, it would compile only the code suitable for Mototola PC and the common code. This is because the macro INTEL has not been defined. Note that, the working of **#ifdef - #else - #endif** is similar to the ordinary **if - else** control instruction of C.

If you want to run your program on a Intel PC, just add a statement at the top saying,

\# define INTEL

Sometimes, instead of **#ifdef**, the **#ifndef** directive is used. The **#ifndef** (which means ‘if not defined’) works exactly opposite to

**#ifdef**. The above example, if written using **#ifndef**, would look like this:

int main( ) { # ifndef INTEL code suitable for a Motorola PC # else code suitable for a Intel PC # endif code common to both the computers }

- Suppose a function **myfunc( )** is defined in a file ‘myfile.h’ which is **#include**d in a file ‘myfile1.h’. Now in your program file, if you **#include** both ‘myfile.h’ and ‘myfile1.h’, the compiler flashes an error ‘Multiple declaration for **myfunc’**. This is because the same file ‘myfile.h’ gets included twice. To avoid this, we can write following code in the ‘myfile.h’ header file:

/\* myfile.h \*/ # ifndef \_\_myfile\_h # define \_\_myfile\_h myfunc( ) { /\* some code \*/ }

\# endif

First time the file ‘myfile.h’ gets included, the preprocessor checks whether a macro called **\_\_myfile\_h** has been defined or not. If it has not been, then it gets defined and the rest of the code gets included. Next time we attempt to include the same file, the inclusion is prevented since **\_\_myfile\_h** already stands defined. Note that there is nothing special about **\_\_myfile\_h**. In its place, we can use any other macro as well.

**_#if_ and _#elif_ Directives** The **#if** directive can be used to test whether an expression evaluates to a non-zero value or not. If the result of the expression is non-zero, then subsequent lines upto a **#else**, **#elif** or **#endif** are compiled, otherwise they are skipped.

A simple example of **#if** directive is shown below:

int main( ) { # if TEST <= 5 statement 1 ; statement 2 ; statement 3 ; # else statement 4 ; statement 5 ; statement 6 ; # endif }

If the expression, **TEST <= 5** evaluates to true, then statements 1, 2 and 3 are compiled, otherwise statements 4, 5 and 6 are compiled. In place of the expression **TEST <= 5**, other expressions like **( LEVEL == HIGH || LEVEL == LOW )** or **ADAPTER == VGA** can also be used.

If we so desire, we can have nested conditional compilation directives. An example that uses such directives is shown below.

\# if ADAPTER == VGA code for video graphics array # else # if ADAPTER == SVGA code for super video graphics array # else code for extended graphics adapter # endif # endif

The above program segment can be made more compact by using another conditional compilation directive called **#elif**. The same program using this directive can be rewritten as shown below. Observe

that by using the **#elif** directives, the number of #**endif**s used in the program get reduced.

\# if ADAPTER == VGA code for video graphics array # elif ADAPTER == SVGA code for super video graphics array # else code for extended graphics adapter # endif

**Miscellaneous Directives** There are two more preprocessor directives available, though they are not very commonly used. They are:

- #undef (b) #pragma

### _#undef_ Directive

On some occasions, it may be desirable to cause a defined name to become ‘undefined’. This can be accomplished by means of the **#undef** directive. In order to undefine a macro that has been earlier **#define**d, the directive,

\# undef macro template

can be used. Thus the statement,

\# undef PENTIUM

would cause the definition of PENTIUM to be removed from the system. All subsequent **#ifdef PENTIUM** statements would evaluate to false. In practice, seldom are you required to undefine a macro, but for some reason if you are required to, then you know that there is something to fall back upon.

### _#pragma_ Directive

This directive is another special-purpose directive that you can use to turn on or off certain features. Pragmas vary from one compiler to another. There are certain pragmas available with Microsoft C compiler that deal with formatting source listings and placing comments in the object file generated by the compiler. Turbo C/C++ compiler has got a

pragma that allows you to suppress warnings generated by the compiler. Some of these pragmas are discussed below.

- **#pragma startup** and **#pragma exit**: These directives allow us to specify functions that are called upon program startup (before **main( )**) or program exit (just before the program terminates). Their usage is as follows:

\# include <stdio.h> void fun1( ) ; void fun2( ) ; # pragma startup fun1 # pragma exit fun2 int main( ) { printf ( "Inside main\\n" ) ; return 0 ; } void fun1( ) { printf ( "Inside fun1\\n" ) ; } void fun2( ) { printf ( "Inside fun2\\n" ) ; }

And here is the output of the program.

Inside fun1 Inside main Inside fun2

Note that the functions **fun1( )** and **fun2( )** should neither receive nor return any value. If we want two functions to get executed at startup then their pragmas should be defined in the reverse order in which you want to get them called.

- **#pragma warn**: On compilation the compiler reports Errors and Warnings in the program, if any. Errors provide the programmer with no options, apart from correcting them. Warnings, on the other hand, offer the programmer a hint or suggestion that something may be _wrong_ with a particular piece of code. Two most common situations when warnings are displayed are as under:

- If you have written code that the compiler's designers (or the ANSI-C specification) consider bad C programming practice. For example, if a function does not return a value then it should be declared as **void**.

- If you have written code that might cause run-time errors, such as assigning a value to an uninitialized pointer.

The **#pragma warn** directive tells the compiler whether or not we want to suppress a specific warning. Usage of this pragma is shown below.

\# include <stdio.h> # pragma warn –rvl /\* return value \*/ # pragma warn –par /\* parameter not used \*/ # pragma warn –rch /\* unreachable code \*/ int f1( ) { int a = 5 ; } void f2 ( int x ) { printf ( "Inside f2" ) ; } int f3( ) { int x = 6 ; return x ; x++ ; } int main( ) {

f1( ) ; f2 ( 7 ) ; f3( ) ; return 0 ; }

If you go through the program, you can notice three problems immediately. These are:

- Though promised, **f1( )** doesn’t return a value.

- The parameter **x** that is passed to **f2( )** is not being used anywhere in **f2( )**.

- The control can never reach **x++** in **f3( )**.

If we compile the program, we should expect warnings indicating the above problems. However, this does not happen since we have suppressed the warnings using the **#pragma** directives. If we replace the ‘–’ sign with a ‘+’, then these warnings would be flashed on compilation. Though it is a bad practice to suppress warnings, at times, it becomes useful to suppress them. For example, if you have written a huge program and are trying to compile it, then to begin with, you are more interested in locating the errors, rather than the warnings. At such times, you may suppress the warnings. Once you have located all errors, then you may turn on the warnings and sort them out.

**The Build Process** There are many steps involved in converting a C program into an executable form. Figure 12.1 shows these different steps along with the files created during each stage.

Many software development tools, like TC++ and Visual Studio, hide many of the steps shown in Figure 12.1 from us. However, it is important to understand these steps for two reasons:

- It would help you understand the process much better, than just believing that, some kind of ‘magic’ generates the executable code.

- If you are to alter any of these steps, then you would know how to do it.

Let us now understand the steps mentioned in Figure 12.1 in detail.

C Source code (PR1.C)

Expanded source code (PR1.I)

Assembly code (PR1.ASM)

Relocatable Object code Object code of Library Functions

Executable code (PR1.EXE)

Preprocessor

Compiler

Assembler

Linker

Figure 12.1

### Preprocessing

During this step, the C source code is expanded based on the preprocessor directives like **#define**, **#include**, **#ifdef**, etc. The expanded source code is stored in an intermediate file with **.i** extension. Thus, if our source code is stored in PR1.C then the expanded source code is stored in PR1.I. The expanded source code is also in C language. Note that the ‘.I’ extension may vary from one compiler to another.

### Compilation

The expanded source code is then passed to the compiler, which identifies the syntax errors in the expanded source code. These errors are displayed along with warnings, if any. As we saw in the last section, using the **#pragma** directive we can control which warnings are to be displayed / hidden.

If the expanded source code is error-free, then the compiler translates the expanded source code in C, into an equivalent assembly language program. Different processors (CPUs) support different set of assembly instructions, using which they can be programmed. Hence, the compiler

targeted for Intel Itanium platform would generate the assembly code using the instructions understood by Intel Itanium. Likewise, the same C program, when compiled using a compiler targeted for Intel Pentium V, is likely to generate a different assembly language code. The assembly code is typically stored in .ASM file. Thus, for PR1.I the assembly code would be stored in PR1.ASM.

### Assembling

The job of the Assembler is to translate .ASM program into Relocatable Object code. Thus, if the assembly language instructions are present in PR1.ASM then the relocatable object code gets stored in PR1.OBJ.

Here the word ‘Relocatable’ means that the program is complete except for one thing—no specific memory addresses have yet been assigned to the code and data sections in the relocatable code. All the addresses are relative offsets.

The .OBJ file that gets created is a specially formatted binary file. The object file contains a header and several sections. The header describes the sections that follow it. These sections are:

- Text section – This section contains machine language code equivalent to the expanded source code.

- Data Section – This section contains global variables and their initial values.

- Bss (Block Started by Symbol) section – This section contains uninitialized global variables.

- Symbol Table – This section contains information about symbols found during assembling of the program. Typical information present in the symbol table includes:

\- Names, types and sizes of global variables. - Names and addresses of functions defined in source code. - Names of external functions like **printf( )** and **scanf( )**.

Although there are machine language instructions in the .OBJ file it cannot be executed directly. This is because of following reasons:

- The external functions like **printf( )** are not present in the .OBJ file.

- The .OBJ file may use some global variables defined in another .OBJ file. For example, PR1.OBJ may use a global variable **count2** which is defined in the file PR2.OBJ.

- The .OBJ file may use a function defined in another .OBJ file. For example, PR2.OBJ may use a function **display( )** defined in the file PR1.OBJ.

Note that parts of the symbol table may be incomplete because all the variables and functions may not be defined in the same file. The references to such variables and functions (symbols) that are defined in other source files are later on resolved by the linker.

### Linking

Linking is the final stage in creating an executable program. It has to do the following important things:

- Find definition of all external functions—those which are defined in other .OBJ files, and those which are defined in Libraries (like **printf( )**).

- Find definition of all global variables—those which are defined in other .OBJ files, and those which are defined in Libraries (like **errno** which is a commonly used global variable that is defined in Standard C Library).

- Combine Data Sections of different .OBJ files into a single Data Section.

- Combine Code Sections of different .OBJ files into a single Code Section.

While combining different .OBJ files the linker has to address one problem. Addresses of all variables and functions in the Symbol Table of the .OBJ file are Relative addresses. This means that address of a Symbol (variable or function), is in fact only an offset from start of the Section (Data or Code Section) to which it belongs. For example, if there are two 4-byte wide global integer variables **count1** and **index1** in PR1.OBJ, then the Symbol Table will have addresses 0 and 4 for them. Similarly, if PR2.OBJ has two similar variables **count2** and **index2** then Symbol Table in PR2.OBJ will have addresses 0 and 4 for these variables. Same addressing scheme is used with functions present in each .OBJ file.

When linker combines the two .OBJ files, it has to re-adjust the addresses of global variables and functions. Thus, the variables **count1**, **index1**, **count2** and **index2** will now enjoy addresses 0, 4, 8 and 12, respectively. Similar re-adjustment of addresses will be done for functions. Even after re-adjustment the addresses of variables and functions are still ‘relative’ in the combined Data and Code sections of the .EXE file.

In the .EXE file machine language code from all of the input object files will be in the Text section. Similarly, all initialized and uninitialized variables will reside in the new Data and Bss sections, respectively.

During linking if the linker detects errors such as mis-spelling the name of a library function in the source code, or using the incorrect number or type of parameters for a function, it stops the linking process and doesn’t create the binary executable file.

### Loading

Once the .EXE file is created and stored on the disk, it is ready for execution. When we execute it, it is first brought from the disk into the memory (RAM) by an Operating System component called Program Loader. Program Loader can place the .EXE anywhere in memory depending on its availability. Since all the addresses in the .EXE file are ‘relative’ addresses, exact ‘position’ where .EXE is loaded in memory doesn’t matter. No further adjustment of addresses is necessary. Thus, the Code and Data in .EXE file are ‘Position Independent’. Once the loading process is completed, the execution begins from the first instruction in Code section of the file loaded in memory.

Modern Operating Systems like Windows and Linux permit loading and execution of multiple programs in memory. One final word before we end this topic. Like a .OBJ file, a .EXE file is also a formatted binary file. The format of these binary file differs from one Operating System to another. For example, Windows Operating System uses Portable Executable (PE) file format, whereas, Linux uses Executable and Linking Format (ELF). Hence an .OBJ or .EXE file created for Windows cannot be used on Linux and vice-versa.

Figure 12.2 summarizes the role played by each processor program during the build process.

### Processor Input Output

Editor

Preprocessor

Compiler

Assembler

Linker

Loader

Program typed from keyboard

C source code file

Expanded Source code file

Assembly language code

Object code of our program and object code of library functions

Executable file

C source code containing program and preprocessor commands

Expanded Source code file created after processing preprocessor commands

Assemby language code

Relocatable Object code in machine language

Executable code in machine language

\-

Figure 12.2

### Summary

- The preprocessor directives enable the programmer to write programs that are easy to develop, read, modify and transport to a different computer system.

- We can make use of various preprocessor directives, such as **#define**, **#include**, **#ifdef** \- **#else** \- **#endif**, **#if** and **#elif** in our program.

- The directives like **#undef** and **#pragma** are also useful although they are seldom used.

- A good understanding of entire build process is important as it gives a good insight into the conversion of source code to executable code.

### Exercise

**\[A\]** Answer the following:

- A preprocessor directive is:

1\. A message from compiler to the programmer 2. A message from compiler to the linker

3\. A message from programmer to the preprocessor 4. A message from programmer to the microprocessor

- Which of the following are correctly formed **#define** statements:

#define INCH PER FEET 12 #define SQR (X) ( X \* X ) #define SQR(X) X \* X #define SQR(X) ( X \* X )

- State True or False:

1\. A macro must always be written in capital letters. 2. A macro should always be accommodated in a single line. 3. After preprocessing when the program is sent for compilation

the macros are removed from the expanded source code. 4. Macros with arguments are not allowed. 5. Nested macros are allowed. 6. In a macro call the control is passed to the macro.

- How many **#include** directives can be there in a given program file?

- What is the difference between the following two **#include** directives:

#include "conio.h" #include <conio.h>

- A header file is:

1\. A file that contains standard library functions 2. A file that contains definitions and macros 3. A file that contains user-defined functions 4. A file that is present in current working directory

- Which of the following is not a preprocessor directive

1\. #if 2. #elseif 3. #undef 4. #pragma

- All macro substitutions in a program are done:

1\. Before compilation of the program

2\. After compilation 3. During execution 4. None of the above

- In a program the statement:

#include "filename"

- is replaced by the contents of the file “filename”:

1\. Before compilation 2. After Compilation 3. During execution 4. None of the above

**\[B\]** What will be the output of the following programs:

- # include <stdio.h> int main( ) { int i = 2 ; # ifdef DEF i \*= i ; # else printf ( "%d\\n", i ) ; # endif return 0 ; }

- # include <stdio.h> # define PRODUCT(x) ( x \* x ) int main( ) { int i = 3, j, k, l ; j = PRODUCT( i + 1 ) ; k = PRODUCT( i++ ) ; l = PRODUCT ( ++i ) ; printf ( "%d %d %d %d\\n", i, j, k, l ) ; return 0 ; }

- # include <stdio.h> # define PI 3.14 # define AREA( x, y, z ) ( PI \* x \* x + y \* z ) ;

int main( ) { float a = AREA ( 1, 5, 8 ) ; float b = AREA ( AREA ( 1, 5, 8 ), 4, 5 ) ; printf ( " a = %f\\n", a ) ; printf ( " b = %f\\n", b ) ; return 0 ; }

**\[C\]** Attempt the following:

- If a macro is not getting expanded as per your expectation, how will you find out how is it being expanded by the preprocessor.

- Write down macro definitions for the following:

1\. To test whether a character is a small case letter or not. 2. To test whether a character is a upper case letter or not. 3. To test whether a character is an alphabet or not. Make use of

the macros you defined in 1 and 2 above. 4. To obtain the bigger of two numbers.

- Write macro definitions with arguments for calculation of area and perimeter of a triangle, a square and a circle. Store these macro definitions in a file called “areaperi.h”. Include this file in your program, and call the macro definitions for calculating area and perimeter for different squares, triangles and circles.

- Write down macro definitions for the following:

1\. To find arithmetic mean of two numbers. 2. To find absolute value of a number. 3. To convert a upper case alphabet to lower case. 4. To obtain the bigger of two numbers.

- Write macro definitions with arguments for calculation of Simple Interest and Amount. Store these macro definitions in a file called “interest.h”. Include this file in your program, and use the macro definitions for calculating simple interest and amount.