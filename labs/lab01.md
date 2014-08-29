---
layout: default
course_number: CS420
title: "Lab 1: File Copy"
---

**Due Friday, Sept 12th by 11:59pm**

### About this Lab
------------------

This lab is a 'warm-up' lab. Through this lab I hope to get a good feeling for your ability to write progr  ams in **C** and your ability to make use of the **POSIX API** and system calls. For this lab, and the rest of the labs that follow this semester, you are required to develop in a **POSIX-compliant environment**. This includes Linux and UNIX systems. If you have your own Linux or UNIX based system feel free to develop in those environments.  Otherwise, you can use the lab compueters in KEC119.

You can use any code editor you wish, but you can only use C system calls for reading/writing to the terminal screen and/or to the disk when copying your file. You may find the list of C system calls located [here](http://codewiki.wikidot.com/system-calls) useful. Read about them and determine which of the system calls listed there are appropriate for your task as described below. 

Before starting this lab, you should read Section 2.3 of your text book.


<br>
### Your Task
--------------
Download the lab files [here]().

Write a C program that uses system calls to copy one file to another. Your program needs to accept two arguments, the first is the source file to be copied, the second is the name of the destination file. Your program should then copy the file, one (or more) character(s) at a time, from the source to the destination. 

 - You MUST use C system calls to read/write to the terminal and disk
 - A list of the functions you are allowed to use on this lab can be found [here](http://codewiki.wikidot.com/system-calls).
(**```close```**, **```dup```**, **```dup2```**, **```fstat```**, **```lseek```**, **```lstat```**, **```open```**, **```read```**, **```stat```**, **```write```**)
 - You **CANNOT** use **```fopen```**, **```fclose```**, **```printf```**, **```fprintf```**, **```scanf```**, etc.
 - You may use the **```strlen```** function if necessary
 - Be sure to include the appropriate error checking (e.g. source file does not exist)
 - You don't have to worry about handling filenames with special characters in them (e.g. spaces)
 - Your code **MUST** compile with supplied Makefile. Simply type **```make```** at the command line to compile your code
 - The supplied Makefile also includes a simple test, type **```make test```** to see if your code functions properly

An example of what your program should look like when run is below:

<pre>
$>
$> ./filecopy hello.txt hello_copy.txt
   Copying hello.txt to hello_copy.txt
   DONE
$>
</pre>



<br>
### Grading
------------
This lab will be graded on a 100 point scale. To receive full credit, your program must successfully compile and copy files. You may lose points for writing bad code (e.g. not checking error conditions, not closing files when you're done with them). See below for more details:

 - **10 points** : Successfully compiles
 - **20 points** : Correct use of system calls
 - **30 points** : Successfully copies files
 - **20 points** : Checks necessary error conditions
 - **10 points** : Properly closes files when done
 - **10 points** : Design/coding style



<br>
### Submission
---------------
When you are done, run the following command from your terminal in the source directory for the project:

	make submit

You will be prompted for your Marmoset username and password,
which you should have received by email.  Note that your password will
not appear on the screen.

**DO NOT MANUALLY ZIP YOUR PROJECT AND SUBMIT IT TO MARMOSET.  
YOU MUST USE THE ```make submit``` COMMAND**.

