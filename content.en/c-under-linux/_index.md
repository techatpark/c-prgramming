---
title: 'C Under Linux'
weight: 23
---

Today the programming world is divided into two major camps—the Windows world and the Linux world. Since its humble beginning

about two decades ago, Linux has steadily drawn the attention of programmers across the globe and has successfully created a community of its own. So as a C programmer you must know how to do C programming under Linux environment. Without any further discussions let us now set out on the Linux voyage. I hope you find the journey interesting and exciting.

**What is Linux?** Linux is a clone of the UNIX operating system. Its kernel was written from scratch by Linus Trovalds with assistance from a loosely-knit team of programmers across the world on the Internet. It has all the features you would expect in a modern OS. Moreover, unlike Windows or UNIX, Linux is available completely free of cost. The kernel of Linux is available in source code form. Anybody is free to change it to suit his/her requirement, with a precondition that the changed kernel can be distributed only in the source code form. Several programs, frameworks, utilities have been built around the Linux kernel. A common user may not want the headaches of downloading the kernel, going through the complicated compilation process, then downloading the frameworks, programs and utilities. Hence many organizations have come forward to make this job easy. They distribute the precompiled kernel, programs, utilities and frameworks on a common media. Moreover, they also provide installation scripts for easy installations of the Linux OS and applications. Some of the popular distributions are RedHat, SUSE, Caldera, Debian, Mandrake, Slackware, etc. Each of them contain the same kernel but may contain different application programs, libraries, frameworks, installation scripts, utilities, etc. Which one is better than the other is only a matter of taste.

Linux was first developed for x86-based PCs (386 or higher). These days it also runs on Compaq Alpha AXP, Sun SPARC, Motorola 68000 machines (like Atari ST and Amiga), MIPS, PowerPC, ARM, Intel Itanium, SuperH, etc. Thus Linux works on literally every conceivable microprocessor architecture.

Under Linux one is faced with simply too many choices of Linux distributions, graphical shells and managers, editors, compilers, linkers, debuggers, etc. For simplicity (in my opinion), I have chosen the following combination for the programs in this chapter:

### T

Linux Distribution – Ubuntu Linux 11.10 Development Environment – NetBeans 8.0.2 Ubuntu Linux can be downloaded from www.ubuntu.com and Netbeans can be downloaded from www.netbeans.org

**C Programming Under Linux** Is C under Linux any different than C under DOS or C under Windows? Well, it is same as well as different. It is same to the extent of using language elements like data types, control instructions and the overall syntax. The usage of standard library functions is also same even though the implementation of each might be different under different OS. For example, a **printf( )** would work under all OSs, but the way it is defined is likely to be different for different OSs. However, the programmer doesn’t suffer because of this, since, he/she can continue to call **printf( )** the same way, no matter how it is implemented.

But there the similarity ends. If we are to build programs that utilize the features offered by the OS then things are bound to be different across OSs. For example, if we are to write a C program that would create a Window and display a message “hello” at the point where the user clicks the left mouse button. The architecture of this program would be very closely tied with the OS under which it is being built. This is because the mechanisms for creating a window, reporting a mouse click, handling a mouse click, displaying the message, closing the window, etc., are very closely tied with the OS for which the program is being built. In short, the programming architecture (better known as programming model) for each OS is different. Hence, naturally, the program that achieves the same task under different OS would have to be different.

**The ‘Hello Linux’ Program** As with any new platform, we would begin our journey in the Linux world by creating a simple ‘hello world’ program. Here is the source code....

\# include <stdio.h> int main( ) { printf ( "Hello Linux\\n" ) ; return 0 ; }

The program is exactly same as compared to a console program under DOS/Windows. It begins with **main( )** and uses **printf( )** standard library function to produce its output. So what is the difference? The difference is in the way programs are typed, compiled and executed. For this you should ideally use NetBeans as it offers an integrated development environment. Alternately, you can type the program using editor like ‘vi’ or ‘vim’ and compile and link it using ‘gcc’.

If you are using NetBeans then create a new C/C++ project in it, type the above program, and build and execute it using F6.

If you are using vi – gcc combination then carry out the following steps:

- Type the program and save it under the name ‘hello.c’.

- At the command prompt switch to the directory containing ‘hello.c’ using the **cd** command.

- Now compile the program using the **gcc** compiler as shown below:

$ gcc hello.c

- On successful compilation, **gcc** produces a file named ‘a.out’. This file contains the machine code of the program which can now be executed.

- Execute the program using the following command:

$ ./a.out

- Now you should be able to see the output ‘Hello Linux’ on the screen.

Having created a Hello Linux program and gone through the edit- compile-execute cycle once, let us now turn our attention to Linux specific programming. We will begin with processes.

**Processes** Gone are the days when only one processor in the PC/Laptop executed only one job (task) in memory at any time. Today, the modern OSs like Windows and Linux exploit the capabilities of Dual-core and Quad-core processors and execute several tasks simultaneously. In Linux each running task is known as a ‘process’.

The scheduling of different processes on multiple processors is done by a program called ‘Scheduler’ which is a vital component of the Linux OS.

The Kernel (core) of the OS assigns each process running in memory a unique ID to distinguish it from other running processes. This ID is often known as Process ID or simply PID. It is very simple to print the PID of a running process programmatically. Here is the program that achieves this…

\# include <stdio.h> # include <sys/types.h> int main( ) { printf ( "Process ID = %d", getpid( ) ) ; return 0 ; }

Here **getpid( )** is a library function which returns the process ID of the calling process. When the execution of the program comes to an end, the process stands terminated. Every time we run the program a new process is created. Hence the kernel assigns a new ID to the process each time. This can be verified by executing the program several times— each time it would produce a different output.

**Parent and Child Processes** As we know, our running program is a process. From this process we can create another process. There is a parent-child relationship between the two processes. The way to achieve this is by using a library function called **fork( )**. This function splits the running process into two processes, the existing one is known as parent and the new process is known as child. Here is a program that demonstrates this…

\# include <stdio.h> # include <unistd.h> /\* for prototype of fork( ) \*/ int main( ) { printf ( "Before Forking\\n" ) ; fork( ) ; printf ( "After Forking\\n" ) ; return 0 ; }

Here is the output of the program…

Before Forking

After Forking After Forking

Watch the output of the program. You can notice that all the statements after the **fork( )** are executed twice—once by the parent process and second time by the child process. In other words **fork( )** has managed to split our process into two.

But why on earth would we like to do this? At times, we want our program to perform two jobs simultaneously. Since these jobs may be inter-related, we may not want to create two different programs to perform them. Let me give you an example. Suppose we want to perform two jobs—copy contents of source file to target file and display an animated GIF file indicating that the file copy is in progress. The GIF file should continue to play till file copy is taking place. Once the copying is over the playing of the GIF file should be stopped. Since both these jobs are inter-related, they cannot be performed in two different programs. Also, they cannot be performed one after another. Both jobs should be performed simultaneously.

At such times, we would want to use **fork( )** to create a child process and then write the program in such a manner that file copy is done by the parent and displaying of animated GIF file is done by the child process. The following program shows how this can be achieved. Note that, the issue here is to show how to perform two different but inter-related jobs simultaneously. Hence I have skipped the actual code for file copying and playing the animated GIF file.

\# include <stdio.h> # include <sys/types.h> # include <unistd.h> int main( ) { int pid ; pid = fork( ) ; if ( pid == 0 ) { printf ( "In child process\\n" ) ; /\* code to play animated GIF file \*/ } else {

printf ( "In parent process\\n" ) ; /\* code to copy file \*/ } return 0 ; }

As we know, **fork( )** creates a child process and duplicates the code of the parent process in the child process. There onwards, the execution of the **fork( )** function continues in both the processes. Thus, the duplication code inside **fork( )** is executed once, whereas, the remaining code inside it is executed in both the parent as well as the child process. Hence, control would come back from **fork( )** twice, even though it is actually called only once. When control returns from **fork( )** of the parent process, it returns the PID of the child process. As against this, when control returns from **fork( )** of the child process, it always returns a 0. This can be exploited by our program to segregate the code that we want to execute in the parent process, from the code that we want to execute in the child process. We have done this in our program using an **if** statement. In the parent process the ‘else block’ would get executed, whereas, in the child process the ‘if block’ would get executed.

Let us now write one more program. This program would use the **fork( )** call to create a child process. In the child process we would print the PID of child and its parent, whereas, in the parent process we would print the PID of the parent and its child. Here is the program…

\# include <stdio.h> # include <sys/types.h> # include <unistd.h> int main( ) { int pid ; pid = fork( ) ; if ( pid == 0 ) { printf ( "Child : Hello I am the child process\\n" ) ; printf ( "Child : Child’s PID: %d\\n", getpid( ) ) ; printf ( "Child : Parent’s PID: %d\\n”, getppid( ) ) ; } else {

printf ( "Parent : Hello I am the parent process\\n" ) ; printf ( "Parent : Parent’s PID: %d\\n”, getpid( ) ) ; printf ( "Parent : Child’s PID: %d\\n", pid ) ; } return 0 ; }

Given below is the output of the program.

Child : Hello I am the child process Child : Child's PID: 4706 Child : Parent's PID: 4705 Parent : Hello I am the Parent process Parent : Parent's PID: 4705 Parent : Child's PID: 4706

In addition to **getpid( )**, there is another related function that we have used in this program—**getppid( )**. As the name suggests, this function returns the PID of the parent of the calling process.

You can tally the PIDs from the output and convince yourself that you have understood the **fork( )** function well. A lot of things that follow use the **fork( )** function. So make sure that you understand it thoroughly.

Note that, even Linux internally uses **fork( )** to create new child processes. Thus, there is a inverted tree-like structure of all the processes running in memory. The father of all these processes is a process called **init**. If we want to get a list of all the running processes in memory we can do so using the **ps** command as shown below.

$ ps –A

Here the switch **–A** indicates that we want to list all the running processes. We can get the **$** prompt by starting a Terminal Window in Ubuntu Linux from Applications | Accessories menu.

**More Processes** Suppose we want to execute a program on the disk as part of a child process. For this, first we should create a child process using **fork( )** and then from within the child process we should call an **exec** function to execute the program on the disk as part of a child process. Note that, there is a family of **exec** library functions, each basically does the same job, but with a minor variation. For example, **execl( )** function permits us

to pass a list of command-line arguments to the program to be executed. **execv( )** also does the same job as **execl( )** except that the command-line arguments can be passed to it in the form of an array of pointers to strings. There also exist other variations like **execle( )** and **execvp( )**.

Let us now see a program that uses **execl( )** to run a new program in the child process.

\# include <stdio.h> # include <unistd.h> int main( ) { int pid ; pid = fork( ) ; if ( pid == 0 ) { execl ( "/bin/ls","-al", "/etc", NULL ) ; printf ( "Child: After exec( )\\n") ; } else printf ( "Parent process\\n" ) ; return 0 ; }

After forking a child process, we have called the **execl( )** function. This function accepts variable number of arguments. The first parameter to **execl( )** is the absolute path of the program to be executed. The remaining parameters describe the command-line arguments for the program to be executed. The last parameter is an end of argument marker which must always be **NULL**. Thus, in our case we have called upon the **execl( )** function to execute the **ls** program as shown below.

$ ls -al /etc

As a result, all the contents of the **/etc** directory are listed on the screen. Note that the **printf( )** below the call to **execl( )** function is not executed. This is because, the **exec** family functions overwrite the image of the calling process with the code and data of the program that is to be executed. In our case, the child process’s memory was overwritten by the code and data of the **ls** program. Hence, the call to **printf( )** did not materialize.

It would make little sense in calling **execl( )** before **fork( )**. This is because, a child would not get created and **execl( )** would simply overwrite the main process itself. As a result, no statement beyond the call to **execl( )** would ever get executed. Hence **fork( )** and **execl( )** usually go hand in hand.

**Zombies and Orphans** We know that the **ps –A** command lists all the running processes. But from where does the **ps** program get this information? Well, Linux maintains a table containing information about all the processes. This table is called ‘Process Table’. Apart from other information, the process table contains an entry of ‘exit code’ of the process. This integer value indicates the reason why the process was terminated. Even though the process comes to an end, its entry would remain in the process table until such time that the parent of the terminated process queries the exit code. This act of querying deletes the entry of the terminated process from the process table and returns the exit code to the parent that raised the query.

When we fork a new child process and the parent and the child continue to execute there are two possibilities—either the child process ends first or the parent process ends first. Let us discuss both these possibilities.

- Child terminates earlier than the parent

In this case, till the time parent does not query the exit code of the terminated child the entry of the child process would continue to exist. Such a process in Linux terminology is known as a ‘Zombie’ process. Zombie means ghost, or in plain simple Hindi a ‘Bhoot’. Moral is, a parent process should query the process table immediately after the child process has terminated. This would prevent a Zombie.

What if the parent terminates without querying. In such a case, the Zombie child process is treated as an ‘Orphan’ process. Immediately, the father of all processes—**init**—adopts the Orphaned process. Next, as a responsible parent, **init** queries the process table, as a result of which, the child process entry is eliminated from the process table.

- Parent terminates earlier than the child

Since every parent process is launched from the Linux shell, the parent of the parent is the **shell** process. When our parent process terminates, the **shell** queries the process table. Thus a proper cleanup happens for

the parent process. However, the child process which is still running is left Orphaned. Immediately, the **init** process would adopt it and when its execution is over **init** would query the process table to clean up the entry for the child process. Note that in this case the child process does not become a Zombie.

Thus, when a Zombie or an Orphan gets created the OS takes over and ensures that a proper cleanup of the relevant process table entry happens. However, as a good programming practice our program should get the exit code of the terminated process and thereby ensure a proper cleanup. Note that, here cleanup is important (it happens anyway). Why is it important to get the exit code of the terminated process? It is because, it is the exit code that would give indication about whether the job assigned to the process was completed successfully or not. The following program shows how this can be done.

\# include <stdio.h> # include <unistd.h> # include <sys/wait.h> /\* for waitpid( ) and WIFEXITED \*/ int main( ) { unsigned int i = 0 ; int pid, status ; pid = fork( ) ; if ( pid == 0 ) { while ( i < 4294967295u ) i++ ; printf ( "The child is now terminating\\n" ) ; } else { waitpid ( pid, &status, 0 ) ; if ( WIFEXITED ( status ) ) printf ( "Parent: Child terminated normally\\n" ) ; else printf ( "Parent: Child terminated abnormally\\n" ) ; } return 0 ; }

In this program we have applied a big loop in the child process. This loop ensures that the child does not terminate immediately. From within the parent process we have made a call to the **waitpid( )** function. This function makes the parent process wait till the time the execution of the child process does not come to an end. This ensures that the child process never becomes Orphaned. Once the child process terminates, the **waitpid( )** function queries its exit code and returns back to the parent. As a result of querying, the child process does not become a Zombie.

The first parameter of **waitpid( )** function is the pid of the child process for which the wait has to be performed. The second parameter is the address of an integer variable which is set up with the exit status code of the child process. The third parameter is used to specify some options to control the behavior of the wait operation. We have not used this parameter and hence we have passed a **0**. Next, we have made use of the **WIFEXITED( )** macro to test if the child process exited normally or not. This macro takes the status value as a parameter and returns a non- zero value if the process terminated normally. Using this macro the parent suitably prints a message to report the termination status (normal / abnormal) of its child process.

**One Interesting Fact** When we use **fork( )** to create a child process the child process does not contain the entire data and code of the parent process. Then does it mean that the child process contains the data and code below the **fork( )** call. Even this is not so. In actuality, the code never gets duplicated. Linux internally manages to intelligently share it. As against this, some data is shared, some is not. Till the time both the processes do not change the value of the variables they keep getting shared. However, if any of the processes (either child or parent) attempt to change the value of a variable it is no longer shared. Instead a new copy of the variable is made for the process that is attempting to change it. This not only ensures data integrity but also saves precious memory.

**Communication using Signals** Communication is the essence of all progress. This is true in real life as well as in programming. In today’s world a program that runs in isolation is of little use. A worthwhile program has to communicate with the outside world in general and with the OS in particular. Let us explore how this communication happens under Linux.

We have already seen how to use **fork( )** and **exec( )** functions to create a child process and to execute a new program, respectively. These library functions got the job done by communicating with the Linux OS. Thus, the direction of communication was from the program to the OS. The reverse communication—from the OS to the program—is achieved using a mechanism called ‘Signal’. Let us now write a simple program that would help you experience the signal mechanism.

\# include <stdio.h> int main( ) { while ( 1 ) printf ( "Program Running\\n" ) ; return 0 ; }

The program is fairly straightforward. All that we have done here is, we have used an infinite **while** loop to print the message "Program Running" on the screen. When the program is running, we can terminate it by pressing the Ctrl+C. When we press Ctrl+C, the keyboard device driver informs the Linux kernel about pressing of this special key combination. The kernel reacts to this by sending a signal to our program. Since we have done nothing to handle this signal, the default signal handler gets called. In this default signal handler there is code to terminate the program. Hence on pressing Ctrl+C the program gets terminated.

But how on earth would the default signal handler get called. Well, it is simple. There are several signals that can be sent to a program. A unique number is associated with each signal. To avoid remembering these numbers, they have been defined as macros like **SIGINT**, **SIGKILL**, **SIGCONT**, etc., in the file ‘signal.h’. Every process contains several ‘signal ID - function pointer’ pairs indicating for which signal which function should be called. If we do not decide to handle a signal then against that signal ID the address of the default signal handler function is present. It is precisely this default signal handler for **SIGINT** that got called when we pressed Ctrl+C when the above program was executed. INT in **SIGINT** stands for interrupt.

Let us now see how we can prevent the termination of our program even after hitting Ctrl+C. This is shown in the following program:

\# include <stdio.h>

\# include <signal.h> void sighandler ( int signum ) { printf ( "SIGINT received. Inside sighandler\\n" ) ; } int main( ) { signal ( SIGINT, sighandler ) ; while ( 1 ) printf ( "Program Running\\n" ) ; return 0 ; }

In this program we have registered a signal handler for the SIGINT signal by using the **signal( )** library function. The first parameter of this function specifies the ID of the signal that we wish to register. The second parameter is the address of a function that should get called whenever the signal is received by our program. The signal handler function must always receive an **int** and return a **void**.

Now when we press Ctrl+C, the registered handler, namely, **sighandler( )** would get called. This function would display the message ‘**SIGINT received. Inside sighandler**’ and return the control back to **main( )**. Note that, unlike the default handler, our handler does not terminate the execution of our program. So only way to terminate it is to kill the running process from a different terminal. For this we need to open the terminal window. Next, do a **ps** **–a** to obtain the list of processes running at all the command prompts that we have launched. Note down the process id of our application. Finally kill our application process by saying,

$ kill 23312

In my case the process id turned out to be **23312**. In your case the the process id might be a different number.

If we wish, we can abort the execution of the program in the signal handler itself by using the **exit ( 0 )** beyond the **printf( )**.

Note that signals work asynchronously. That is, when a signal is received no matter what our program is doing, the signal handler would

immediately get called. Once the execution of the signal handler is over, the execution of the program is resumed from the point where it left off when the signal was received.

**Handling Multiple Signals** Now that we know how to handle one signal, let us try to handle multiple signals. Here is the program to do this…

\# include <stdio.h> # include <signal.h> void inthandler ( int signum ) { printf ( "SIGINT Received\\n" ) ; } void termhandler ( int signum ) { printf ( "SIGTERM Received\\n" ) ; } int main( ) { signal ( SIGINT, inthandler ) ; signal ( SIGTERM, termhandler ) ; while ( 1 ) printf ( "Program Running\\n" ) ; return 0 ; }

In this program, apart from **SIGINT**, we have additionally registered a new signal, **SIGTERM**. The **signal( )** function is called twice to register a different handler for the two signals. After registering the signals, we enter an infinite **while** loop to print the ‘**Program Running**’ message on the screen.

As in the previous program, here too, when we press Ctrl+C the handler for the **SIGINT**, i.e., **inthandler( )** is called. However, when we try to kill the program from the second terminal using the **kill** command, the program does not terminate. This is because, when the **kill** command is

used, it sends the running program a **SIGTERM** signal. The default handler for the message terminates the program. Since we have handled this signal ourselves, the handler for **SIGTERM**, i.e., **termhandler( )** gets called. As a result, the **printf( )** statement in the **termhandler( )** function gets executed and the message ‘SIGTERM Received’ gets displayed on the screen. Once the execution of **termhandler( )** function is over, the program resumes its execution and continues to print ‘Program Running’. Then how are we supposed to terminate the program? Simple. Use the following command from the another terminal window:

$ kill –SIGKILL 23312

As the command indicates, we are trying to send a **SIGKILL** signal to our program. A **SIGKILL** signal terminates the program.

Most signals may be caught by the process, but there are a few signals that the process cannot catch, and they cause the process to terminate. Such signals are often known as uncatchable signals. The **SIGKILL** signal is an uncatchable signal that forcibly terminates the execution of a process.

Note that, even if a process attempts to handle the **SIGKILL** signal by registering a handler for it, still the control would always land in the default **SIGKILL** handler, which would terminate the program.

The **SIGKILL** signal is to be used as a last resort to terminate a program that gets out of control. One such process that makes uses of this signal is a system shutdown process. It first sends a **SIGTERM** signal to all processes, waits for a while, thus giving a ‘grace period’ to all the running processes. However, after the grace period is over, it forcibly terminates all the remaining processes using the **SIGKILL** signal.

Note that it is also possible to handle multiple signals using a common signal handler. For this, all that we need to do is register the same function for multiple signals which calling the **signal( )** function. This is shown in the following code snippet:

signal ( SIGINT, sighandler ) ; signal ( SIGTERM, sighandler ) ; signal ( SIGCONT, sighandler ) ;

Here, during each call to the **signal( )** function we have specified the address of a common signal handler named **sighandler( )**. Thus, the

same signal handler function would get called when one of the three signals are received. This does not lead to a problem since inside the **sighandler( )** we can figure out the signal ID using the **signum** parameter of the function.

Note that, we can easily afford to mix the two methods of registering signals in a program. That is, we can register separate signal handlers for some of the signals and a common handler for some other signals. Registering a common handler makes sense if we want to react to different signals in exactly the same way.

**Blocking Signals** Sometimes, we may want that flow of execution of a critical/time-critical portion of the program should not be hampered by the occurrence of one or more signals. In such a case, we may decide to block the signal. Once we are through with the critical/time-critical code, we can unblock the signals(s). Note that, if a signal arrives when it is blocked, it is simply queued into a signal queue. When the signals are unblocked, the process immediately receives all the pending signals one after another. Thus blocking of signals defers the delivery of signals to a process till the execution of some critical/time-critical code is over. Instead of completely ignoring the signals or letting the signals interrupt the execution, it is preferable to block the signals for the moment and deliver them some time later. Let us now write a program to understand signal blocking. Here is the program…

\# include <stdio.h> # include <signal.h> void sighandler ( int signum ) { switch ( signum ) { case SIGTERM : printf ( "SIGTERM Received\\n" ) ; break ; case SIGINT : printf ( "SIGINT Received\\n" ) ; break ; case SIGCONT : printf ( "SIGCONT Received\\n" ) ; break ;

} } int main( ) { char buffer \[ 80 \] = "\\0" ; sigset\_t block ; signal ( SIGTERM, sighandler ) ; signal ( SIGINT, sighandler ) ; signal ( SIGCONT, sighandler ) ; sigemptyset ( &block ) ; sigaddset ( &block, SIGTERM ) ; sigaddset ( &block, SIGINT ) ; sigprocmask ( SIG\_BLOCK, &block, NULL ) ; while ( strcmp ( buffer, "n" ) != 0 ) { printf ( "Enter a String: " ) ; gets ( buffer ) ; puts ( buffer ) ; } sigprocmask ( SIG\_UNBLOCK, &block, NULL ) ; while ( 1 ) printf ( "Program Running\\n" ) ; return 0 ; }

In this program we have registered a common handler for the **SIGINT**, **SIGTERM** and **SIGCONT** signals. Next, we want to repeatedly accept strings in a buffer and display them on the screen till the time the user does not enter an “**n**” from the keyboard. Additionally, we want that this activity of receiving input should not be interrupted by the **SIGINT** or the **SIGTERM** signals. However, a **SIGCONT** should be permitted. So before we proceed with the loop, we must block the **SIGINT** and **SIGTERM** signals. Once we are through with the loop, we must unblock these

signals. This blocking and unblocking of signals can be achieved using the **sigprocmask( )** library function.

Before we turn our attention to this function, let us answer one question—when does a process receive the **SIGCONT** signal? Well, a process under Linux can be suspended using the Ctrl+Z command. The process is stopped but is not terminated, i.e., it is, suspended. This gives rise to the uncatchable **SIGSTOP** signal. To resume the execution of the suspended process, we can make use of the **fg** (foreground) command. As a result of which, the suspended program resumes its execution and receives the **SIGCONT** signal (CONT means continue execution).

Let us now understand the **sigprocmask( )** function. The first parameter of the **sigprocmask( )** function specifies whether we want to block/unblock a set of signals. The next parameter is the address of a structure (**typedef**ed as **sigset\_t**) that describes a set of signals that we want to block/unblock. The last parameter can be either NULL or the address of **sigset\_t** type variable which would be set up with the existing set of signals before blocking/unblocking signals.

There are library functions that help us to populate the **sigset\_t** structure. The **sigemptyset( )** empties a **sigset\_t** variable so that it does not refer to any signals. The only parameter that this function accepts is the address of the **sigset\_t** variable. We have used this function to quickly initialize the **sigset\_t** variable block to a known empty state. To block the **SIGINT** and **SIGTERM** we have to add the signals to the empty set of signals. This can be achieved using the **sigaddset( )** library function. The first parameter of **sigaddset( )** is the address of the **sigset\_t** variable and the second parameter is the ID of the signal that we wish to add to the existing set of signals.

After the loop, we have also used an infinite **while** loop to print the ‘**Program Running**’ message. This is done so that we can easily check that till the time the loop that receives input is not over the program cannot be terminated using Ctrl+C or **kill** command since the signals are blocked. Once the user enters “n” from the keyboard the control comes out of the **while** loop and unblocks the signals. As a result, pending signals, if any, are immediately delivered to the program. So if we press Ctrl+C or use the **kill** command when the execution of the loop that receives input is not over, these signals would be kept pending. Once we are through with the loop, the signal handlers would be called.

**Event Driven programming** Having understood the mechanism of signal processing let us now see how signaling is used by Linux-based libraries to create event driven GUI programs. As you know, in a GUI program events occur typically when we click on the window, type a character, close the window, repaint the window, etc. We have chosen the GTK library version 2.0 to create the GUI applications. Here, GTK stands for Gimp’s Tool Kit. Given below is the first program that uses this Tool Kit to create a window on the screen.

/\* mywindow.c \*/ # include <gtk/gtk.h> int main ( int argc, char \*argv\[ \] ) { GtkWidget \*p ; gtk\_init ( &argc, &argv ) ; p = gtk\_window\_new ( GTK\_WINDOW\_TOPLEVEL ) ; gtk\_window\_set\_title ( p , "Sample Window" ) ; g\_signal\_connect ( p, "destroy", gtk\_main\_quit, NULL ) ; gtk\_widget\_set\_size\_request ( p, 300, 300 ) ; gtk\_widget\_show ( p ) ; gtk\_main( ) ; return 0 ; }

We need to compile this program as follows:

$ gcc mywindow.c \`pkg-config gtk+-2.0 --cflags --libs\`

Here we are compiling the program ‘mywindow.c’ and then linking it with the necessary libraries from GTK. Note the quotes that we have used in the command. Here we are using the program “pkg-config”, which can be obtained from www.freedesktop.org. This program reads the .pc which comes with GTK to determine what compiler switches are needed to compile programs that use GTK. --cflags will output a list of include directories for the compiler to look in, and --libs will output the list of libraries for the compiler to link with and the directories to find them in.

Figure 23.1 shows the output of the program.

Figure 23.1

The GTK library provides a large number of functions that makes it very easy for us to create GUI programs. Every window under GTK is known as a widget. To create a simple window we have to carry out the following steps:

- Initialize the GTK library with a call to **gtk\_init( )** function. This function requires the addresses of the command-line arguments received in **main( )**.

- Next, call the **gtk\_window\_new( )** function to create a top- level window. The only parameter this function takes is the type of window to be created. A top-level window can be created by specifying the **GTK\_WINDOW\_TOPLEVEL** value. This call creates a window in memory and returns a pointer to the widget object. The widget object is a structure (**GtkWidget**) variable that stores lots of information including the attributes of window it represents. We have collected this pointer in a **GtkWidget** structure pointer called **p**.

- Set the title for the window by making a call to **gtk\_window\_set\_title( )** function. The first parameter of this function is a pointer to the **GtkWidget** structure representing the window for which the title has to be set. The second parameter is a string describing the text to be displayed in the title of the window.

- Register a signal handler for the destroy signal. The **destroy** signal is received whenever we try to close the window. The handler for the **destroy** signal should perform cleanup activities and then shut down the application. GTK provides a ready-made function called **gtk\_main\_quit( )** that does this job. We only need to associate this function with the destroy signal. This can be achieved using the **g\_signal\_connect( )** function. The first parameter of this function is the pointer to the widget for which destroy signal handler has to be registered. The second parameter is a string that specifies the name of the signal. The third parameter is the address of the signal handler routine. We have not used the fourth parameter.

- Resize the window to the desired size using the **gtk\_widget\_set\_size\_request( )** function. The second and the third parameters specify the height and the width of the window, respectively.

- Display the window on the screen using the function **gtk\_widget\_show( )**.

- Wait in a loop to receive events for the window. This can be accomplished using the **gtk\_main( )** function.

How about another program that draws a few shapes in the window? Here is the program…

/\* myshapes.c \*/ # include <gtk/gtk.h> int expose\_event ( GtkWidget \*widget, GdkEventExpose \*event ) { GdkGC \* p ; GdkPoint arr \[ 5\] = { 250, 150, 250, 300, 300, 350, 400, 300, 320, 190 } ; p = gdk\_gc\_new ( widget -> window ) ; gdk\_draw\_line ( widget -> window, p, 10, 10, 200, 10 ) ; gdk\_draw\_rectangle ( widget -> window, p, TRUE, 10, 20, 200, 100 ) ; gdk\_draw\_arc ( widget -> window, p, TRUE, 200, 10, 200, 200, 315 \* 64, 90 \* 64 ) ; gdk\_draw\_polygon ( widget -> window, p, TRUE , arr, 5 ) ; /\* True – fill \*/ gdk\_gc\_unref ( p ) ;

return TRUE ; } int main ( int argc, char \*argv\[ \] ) { GtkWidget \*p ; gtk\_init ( &argc, &argv ) ; p = gtk\_window\_new ( GTK\_WINDOW\_TOPLEVEL ) ; gtk\_window\_set\_title ( p, "Sample Window" ) ; g\_signal\_connect ( p, "destroy", gtk\_main\_quit, NULL ) ; g\_signal\_connect ( p , "expose\_event", expose\_event, NULL ) ; gtk\_widget\_set\_size\_request ( p, 500, 500 ) ; gtk\_widget\_show ( p ) ; gtk\_main( ) ; return 0 ; }

Figure 23.2 shows the output of the program.

Figure 23.2

This program is similar to the previous one. The only difference is that, in addition to the destroy signal, we have registered a signal handler for the **expose\_event** using the **g\_signal\_connect( )** function. This signal is sent to our process whenever the window needs to be redrawn. By writing the code for drawing shapes in the handler for this signal we are assured that the drawing would never vanish if the window is dragged outside the screen and then brought back in, or some other window uncovers a portion of our window which was previously overlapped, and so on. This is because a **expose\_event** signal would be sent to our application, which would immediately redraw the shapes in our window.

In order to draw in the window we need to obtain a graphics context for the window using the **gdk\_gc\_new( )** function. This function returns a pointer to the graphics context structure. This pointer must be passed to the drawing functions like **gdk\_draw\_line( )**, **gdk\_draw\_rectangle( )**, **gdk\_draw\_arc( )**, **gdk\_draw\_polygon( )**, etc. The arguments passed to most of these functions are self-explanatory. Note that, the last two arguments that are passed to **gdk\_draw\_arc( )** represent the starting

angle and the ending angle of the arc. These angles are always mentioned as multiple of 64 and the ending angle is measured relative to the starting angle. Once we are through with drawing, we should release the graphics context using the **gdk\_gc\_unref( )** function.

**Where do you go from here?** You have now understood signal processing, the heart of programming under Linux. With that knowledge under your belt you are now capable of exploring the vast world of Linux on your own. Complete Linux programming deserves a book on its own. Idea here was to raise the hood and show you what lies underneath it. I am sure that if you have taken a good look at it, you can try the rest yourselves. Good luck!

### Summary

- Linux is a free OS whose kernel was built by Linus Trovalds and friends.

- C programs under Linux can be compiled using the popular **gcc** compiler.

- **fork( )** library function can be used to create child processes.

- **execl( )** library function is used to execute another program from within a running program.

- **execl( )** function overwrites the image (code and data) of the calling process.

- **ps** command can be used to get a list of all processes.

- **kill** command can be used to terminate a process.

- A ‘Zombie’ is a child process that has terminated, but its parent is running and has not called a function to get the exit code of the child process.

- An ‘Orphan’ is a child process whose parent has terminated.

- Orphaned processes are adopted by **init** process automatically.

- A parent process can avoid creation of a Zombie and Orphan processes using **waitpid( )** function.

- Programs can communicate with the Linux OS using library functions.

(m) The Linux OS communicates with a program by means of signals.

(n) The interrupt signal (**SIGINT**) is sent by the kernel to our program when we press Ctrl+C.

(o) A terminate signal (**SIGTERM**) is sent to the program when we use the **kill** command.

(p) A process cannot handle an uncatchable signal.

(q) The **kill –SIGKILL** variation of the **kill** command generates an uncatchable **SIGKILL** signal that terminates a process.

(r) A process can block a signal or a set of signals using the **sigprocmask( )** function.

(s) Blocked signals are delivered to the process when the signals are unblocked.

(t) A **SIGSTOP** signal is generated when we press Ctrl+Z.

(u) A **SIGSTOP** signal is uncatchable signal.

(v) A suspended process can be resumed using the **fg** command.

(w) A process receives the **SIGCONT** signal when it resumes execution.

(x) In GTK, the **g\_signal\_connect( )** function can be used to connect a function with an event.

### Exercise

**\[A\]** State True or False:

- We can modify the kernel of Linux OS.

- All distributions of Linux contain the same collection of applications, libraries and installation scripts.

- Basic scheduling unit in Linux is a file.

- **execl( )** library function can be used to create a new child process.

- The scheduler process is the father of all processes.

- A family of **fork( )** and **exec( )** functions are available, each doing basically the same job but with minor variations.

- **fork( )** completely duplicates the code and data of the parent process into the child process.

- **fork( )** overwrites the image (code and data) of the calling process.

- **fork( )** is called twice but returns once.

- Every Zombie process is essentially an Orphan process.

- Every Orphan process is essentially a Zombie process.

- All registered signals must have a separate signal handler.

(m) Blocked signals are ignored by a process.

(n) Only one signal can be blocked at a time.

(o) Blocked signals are ignored once the signals are unblocked.

(p) If our signal handler gets called, the default signal handler still gets called.

(q) **gtk\_main( )** function makes uses of a loop to prevent the termination of the program.

(r) Multiple signals can be registered at a time using a single call to **signal( )** function.

(s) The **sigprocmask( )** function can block as well as unblock signals.

**\[B\]** Answer the following:

- If a program contains four calls to **fork( )** one after the other, how many total processes would get created?

- What is the difference between a Zombie process and an Orphan process?

- Write a program that prints the command-line arguments that it receives. What would be the output of the program if the command-line argument is \* ?

- What purpose do the functions **getpid( )** and **getppid( )** serve?

- Rewrite the program in the section ‘Zombies and Orphans’ in this chapter by replacing the **while** loop with a call to the **sleep( )** function. Do you observe any change in the output of the program?

- How does **waitpid( )** prevent creation of Zombie or Orphan processes?

- How does the Linux OS know if we have registered a signal or not?

- What happens when we register a handler for a signal?

- Write a program to verify whether **SIGSTOP** and **SIGKILL** signals are un-catchable signals.

- Write a program to handle the **SIGINT** and **SIGTERM** signals. From inside the handler for **SIGINT** signal write an infinite loop to print the message ‘Processing Signal’. Run the program and make use of Ctrl+C more than once. Run the program once again and press Ctrl+C once. Then use the **kill** command. What are your observations?

- Write a program that blocks the **SIGTERM** signal during execution of the **SIGINT** signal.