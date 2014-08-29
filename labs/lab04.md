---
layout: default
course_number: CS420
title: "Lab 3: Semaphore Fun"
---

**Due Friday, Nov 14th by 11:59pm**

### About this Lab
------------------

The goal of this lab is to get you working with semaphores/mutexes.
To get started download the lab files [here]().


<br>
### Your Task
---------------
Write a C program called threadTester that creates multiple processes (each of which will eventually creates multiple threads) that attempt to access, read, and write a common file. You program **MUST** take three command line arguments **EXACTLY** as shown below. The usage statement for your program, with an explanation of each of the command line arguments is below:

<pre>
USAGE : threadTester -p <num_procs> -t <num_threads> -f <filename>
    -p : the number of processes to create
    -t : the number of threads to create per process
    -f : the name of the shared file in which to write output
</pre>

I highly recommend reading about and using the **```getopt```** function that is included in the **```unistd.h```** C library to parse your command line options. The man page for the **```getopt```** function can be found [here](http://pubs.opengroup.org/onlinepubs/009696899/functions/getopt.html#tag_03_234) 

The provided Makefile contains a command that will run and test your code. Your program **MUST** run correctly when the following Makefile command is run:

<pre>
make runTest
</pre>

If your program does not run with the above Makefile command, I will not run your program and you will receive 0 credit for your submission. If you program runs and produces the correct output file, it will print out **```--SUCCESS--```**. The code to verify your output file and print this message is already written for you and is included in the **```threadTester.c```** file. **DO NOT MODIFY THE CODE THE TESTS YOUR OUTPUT FILE.** Modifying the test code will result in 0 credit for this lab assignment. 

When your program is run from the command line, your main process should create a new file and write the integer value '0' (without the quotes) into the first line of the file. It will be the only line in the file for now. At this point, the main process should close that file. It will be reopened again later. **NOTE:** a utility function called **```open_file```** is provided for you in the **```utils.c```** file. Use it.

Next, your main process will need to create a **named semaphore**. A named semaphore is maintained by the operating system and is very easy to share between unrelated processes. There is no need to manually created a shared memory space that would be required of other types of semaphores and mutexes (in other words, you're getting off easy here). You can read everything you need to know about semaphores and named semaphores [here](http://www.linuxdevcenter.com/pub/a/linux/2007/05/24/semaphores-in-linux.html?page=1). Please read ALL six pages of the linked semaphore documentation before proceeding. When you're ready to create your named semaphore, **use your YCP login name as the name for your semaphore**. 


Now the fun begins. Your main process should create **```P```** new child processes (number specified via the **```-p```** option on the command line) that **run concurrently** (i.e. fork off ALL processes before calling **```wait(NULL)```** and waiting for any to finish). **DO NOT WAIT FOR A PROCESS TO FINISH BEFORE FORKING THE NEXT PROCESS!** 

Each child process should replaces its process contents with a call to **```execlp```** and run the code in the **```fileWriter.c```** file. You will need to fill in the code in **```fileWriter.c```**. However, before proceeding with the code for **```fileWriter.c```**, you should simply have **```fileWriter.c```** print out a ```"Hello World"``` message. This will allow you to test that your **```threadTester.c```** is properly creating each of the required processes. 

Once you're confident that your **```threadTester```** can create the required processes and terminate properly you can move onto writing the **```fileWriter.c```**. Each child processes (i.e. each **```fileWriter```**) should first create **```T```** new threads (the number of threads is specified by the **```-t```** option on the command line). Each of those **```T```** threads **MUST** also run concurrently and attempt to read from and write to the same file that was originally created by the main process. Each thread should: 

 - Attempt to open the shared file
 - Read the **LAST** numeric value in the file (the first thread to access the file will read the 0 written by the main process)
 - Increment the value read from the file and append the newly incremented value to the file. Each newly appended value should be appended as its own line in the shared file

If you need a refresher on POSIX pthreads, check out a great resource [here](https://computing.llnl.gov/tutorials/pthreads/). 

Use semaphores/mutexes as you see necessary. When all of the threads complete and all of the processes terminate the shared file should contain the numeric values 0 through **```(P * T)```** . . . **IN ASCENDING ORDER**. If your values are not in ascending order, or if some of the values are repeated/missing then you should re-evaluate how you are using semaphores because you did something wrong.


After all of the sub-threads finish writing to the file, your main process must check the file to see if the contents of the file are correct. If the contents are correct, then the main process should print **```--SUCCESS--```** to the terminal. If the contents are incorrect, then the main process should print **```--FAIL--```** to the terminal. **This code has already been provided for you . . . DO NOT CHANGE IT.** Whatever code you write, must pass the test that has been provided. Any modifications to the provided code will result in a 0 for this assignment.


<br>
### Sample Output File
-----------------------
If your program is run with **```-p 5```** and **```-t 3```**, you should create a total of 5 processes, each with 3 threads. That's a total of 15 threads that are trying to access and write to the shared file. If successful, the contents of the shared file should look **EXACTLY** like the following when all 15 threads get done with it. The very first line of the file should contain the '0' written by the original processes, followed by each additional value on a newline.

<pre>
0
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
</pre>


<br>
### Grading
-------------
This lab will be graded on a 100 point scale as follows: 

 - **5 points** : correctly parse and error check command line arguments
 - **10 points** : main process successfully writes the initial '0' to the file
 - **5 points** : main process correctly creates a named semaphore
 - **10 points** : main process correctly forks off P new processe
 - **5 points** : main process correctly closes named semaphore
 - **10 points** : fileWriter process correctly receives arguments passed from main process
 - **5 points** : fileWriter process correctly attaches to named semaphore
 - **10 points** : fileWriter process correctly spawns T new threads
 - **10 points** : fileWriter threads correctly read from, and update the shared file
 - **30 points** : all data is written correctly to the shared data file

You may lose additional points for writing bad code (e.g. not checking error conditions, not closing files when you're done with them, etc.).


<br>
### Submission
---------------
Before submitting your assignment:
 1. run **```make clean```** from the terminal
 2. run **```make```** to compile your code from scratch
 3. **ADDRESS ANY AND ALL WARNINGS**
 4. goto #1 until no more warnings exist

There are NO acceptable warnings on this assignment or any other assigning in this course. All warnings are an indication that you've done something incorrectly.



When you are done, run the following command from your terminal in the source directory for the project:

	make submit

You will be prompted for your Marmoset username and password,
which you should have received by email.  Note that your password will
not appear on the screen.

**DO NOT MANUALLY ZIP YOUR PROJECT AND SUBMIT IT TO MARMOSET.  
YOU MUST USE THE ```make submit``` COMMAND.**

