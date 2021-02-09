# Lab 01: Environment Variables & Set-UID Programs
- **Logan Dolechek (n47f693)**
- **logand.msu@gmail.com**
- **CSCI 476**
- **02/07/2021**
- **Link to assignment:**[https://www.traviswpeters.com/cs476-2021-spring/labs/lab01]
---

## Task 1: Manipulating Environment Variables
**Task 1 Summary**
_In this task, we study the commands that can be used to set and unset environment variables. We are using Bash in the seed account._ 
**Task 1.1 Screenshots**

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task1_1p1.PNG" width="500" height="300"> 

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task1_1p2.PNG" width="500" height="">

**Task 1.2 Screenshot**

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task1_2.PNG" width="500" height="">  

---
## Task 2: Passing Environment Variables (Parent -> Child)  
**Task 2 Summary**  
_In this task, we study how a child process gets its environment variables from its parent. In Unix, fork() creates a new process by duplicating the calling process. The new process, referred to as the child, is an exact duplicate of the calling process, referred to as the parent; however, several things are not inherited by the child. In this task, we would like to know whether the parent’s environment variables are inherited by the child process or not._

**Task 2.1**  
_I ran vimdiff to show the output of myenv1 and the temp file I created to show the difference between the two files. The temp file contains the output printenv command and the myenv1 contains the output of the myprintenv.c program you asked us to run for Task 2. Within the comparison we can see that the underlined variables in temp were usr/bin/printenv and after running the .c file it changed the underscored variable to /.myprintenv_  
<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task2.PNG">  
**Task 2.2**  
myenv2 looks about the same as myenv1. Nothing appears to jump out at me on first glance.   
**Task 2.3**  
After running vimdiff myenv2 myenv1 the difference showed know differences at all. They are infact the same. Which should mean that child is inheriting from parent.   
---
## Task 3: Environment Variables and execve()  
**Task 3 Summary**  
_In this task, we study how environment variables are affected when a new program is executed via execve(). The function execve() calls a system call to load a new command and execute it; this function never returns. No new process is created; instead, the calling process’s text, data, bss, and stack are overwritten by that of the program loaded. Essentially, execve() runs the new program inside the calling process. We are interested in what happens to the environment variables; are they automatically inherited by the new program?_   
**Task 3.1**  
I compiled and ran the file as asked for this step and nothing was shown as expected.  
<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task3_1.PNG" width="500" height="300">  
**Task 3.2**  
After changing the code I recompiled the file and then ran it. This time it showed me all the environment variables.   
**Task 3.3**  
I believe that the main take away from this from a security stand point is that there will be certain times that I don't want the environment variables to be shown. Which is where NULL comes in handy. If I do want to see the environment variables I can pass environ as a perameter to execve.   
---
## Task 4: Environment Variables and system()  
**Task 4 Summary**  
_In this task, we study how environment variables are affected when a new program is executed via system(). This function is used to execute a command, but unlike execve(), which directly executes a command, system() actually executes /bin/sh -c command, i.e., it executes /bin/sh, and asks the shell to execute command.
If you look at the implementation of the system() function, you will see that it uses execl() to execute /bin/sh; execl() calls execve(), passing to it the environment variables array. Therefore, using system(), the environment variables of the calling process are passed to the new program /bin/sh. Please compile and run the following program to verify this._  
**Task 4**  
My observations is that by calling system() it basically made a subshell with new environment variables.   
---
## Task 5: Environment Variables and Set-UID Programs  
**Task 5 Summary**  
_Set-UID is an important security mechanism in Unix operating systems. When a Set-UID program runs, it assumes the owner’s privileges. For example, if the program’s owner is root, when anyone runs this program, the program gains root’s privileges during its execution. Set-UID allows us to do many interesting things, but since it escalates the user’s privilege, it is quite risky. Although the behavior of Set-UID programs is decided by their program logic, not by users, users can indeed affect the behavior via environment variables. To understand how Set-UID programs can be affected, let us first figure out whether environment variables are inherited by a Set-UID program’s process from the user’s process._  
**Task 5.1**  
I can confirm that running this correctly prints the environment variables   
<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task5_1.PNG">  
**Task 5.2** 
<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task5_2.PNG">  
**Task 5.3**
After setting exports and running the SET-UID program again. I noticed that TASK5 and my PATH showed up properly in my environment variables. LD_LIBRARY_PATH did not because that is used and dumped upon program call.  
<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task5_3p1.PNG">  
<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task5_3p2.PNG">  
---
## Task 6: PATH and Set-UID Programs  
**Task 6 Summary**  
_blahblah_  
<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task6_p1.PNG">  
<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task6_p2.PNG">  

After changing the permissions of ls_vuln to root and then trying to run the file again. It continued to only run the base ls command. I believe the reason behind this is that since system starts at the base shell and will point to dash. Dash has that countermessure mentioned to prevent itself being used as a Set-UID. It will revert it back to the process's real user ID which would cancel any permissions given before. 

---
## Task 7: LD_PRELOAD and Set-UID Programs  
**Task 7 Summary**  
_blahblahblah_  
**Task 7.1**

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task7_1.PNG">

**Task 7.2**

- Make myprog a regular program, and run it as a normal user

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task7_2p1.png">

- Make myprog a Set-UID root program, and run it as a normal user.

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task7_2p2.png">

- Make myprog a Set-UID root program, export the LD_PRELOAD environment variable again in the root account and run it.

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task7_2p3.png"> 

- Make myprog a Set-UID user1 program export the LD_PRELOAD enviornment variable again in a different user's account and run it.

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task7_2p4.png">  

**Task 7.3**  
I need to write a summary of 7.2 from my observations here. 

## Task 8: system() versus execve()

**Task 8.1**
Yes I was able to compromise the integrity of the system as "Bob". I was able to invoke two different calls within the same command line. Which allowed me to write/remove the file that I shouldn't have been able to access. There is a security breach within the arguments of catall.c that allows me to access permissions if I call within the same line.
<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task8_1.png"> 

**Task 8.2**
No I was not able to make the same attack as before. With execve it reads the entire quotations at once vs at seperate times. 
<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task8_2.png">

## Task 9: Capability Leaking
**Task 9 Summary**
_blahblahblah_

Yes this was able to be edited, due to leaked privileges from the Set-UID executable. 
<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task9.png"> 
