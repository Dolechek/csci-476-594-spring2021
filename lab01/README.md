# Lab 01: Environment Variables & Set-UID Programs
- **Logan Dolechek (n47f693)**
- **logand.msu@gmail.com**
- **CSCI 476**
- **02/07/2021**
- **Link to assignment:**[https://www.traviswpeters.com/cs476-2021-spring/labs/lab01]
---

## Task 1: Manipulating Environment Variables

**Task 1 Summary**

_This task we are simply looking at commands that can be used to set and unset environment variables._

**Task 1.1 Screenshots**

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task1_1p1.PNG" width="500" height="300"> 

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task1_1p2.PNG" width="500" height="">

**Task 1.2 Screenshot**

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task1_2.PNG" width="500" height="">  

---

## Task 2: Passing Environment Variables (Parent -> Child)

**Task 2 Summary**

_This task is to demonstrate how a child process can get to a parent class._

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

_This task examins how execve() affects environment variables when a new program is executed._

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

_This task takes a look at how system() affects environment variables when executed._

**Task 4**

My observations is that by calling system() it basically made a subshell with new environment variables.

---

## Task 5: Environment Variables and Set-UID Programs

**Task 5 Summary**

_This task demonstrates how Set-UID is an important part of the security mechanism in Unix._

**Task 5.1**

I can confirm that running this correctly prints the environment variables 

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task5_1.PNG" width="700" height="400">

**Task 5.2**

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task5_2.PNG" width="700" height="400">

**Task 5.3**

After setting exports and running the SET-UID program again. I noticed that TASK5 and my PATH showed up properly in my environment variables. LD_LIBRARY_PATH did not because that is used and dumped upon program call.

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task5_3p1.PNG">

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task5_3p2.PNG">

---
## Task 6: PATH and Set-UID Programs

**Task 6 Summary**

_This task demonstrates how Set-UID programs deal with environment variables. Taking a look at PATH environment and its potential impact on Set-UID programs._ 

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task6_p1.PNG">

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task6_p2.PNG" width="" height="">

After changing the permissions of ls_vuln to root and then trying to run the file again. It continued to only run the base ls command. I believe the reason behind this is that since system starts at the base shell and will point to dash. Dash has that countermessure mentioned to prevent itself being used as a Set-UID. It will revert it back to the process's real user ID which would cancel any permissions given before. 

---

## Task 7: LD_PRELOAD and Set-UID Programs

**Task 7 Summary**

_This task is to show how Set-UID programs deal with environment variables specifically examining the LD_PRELOAD environment variable and its potential impact on Set-UID programs._

**Task 7.1**

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task7_1.PNG">

**Task 7.2**

- Make myprog a regular program, and run it as a normal user

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task7_2p1.png" width="" height="">

- Make myprog a Set-UID root program, and run it as a normal user.

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task7_2p2.png">

- Make myprog a Set-UID root program, export the LD_PRELOAD environment variable again in the root account and run it.

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task7_2p3.png"> 

- Make myprog a Set-UID user1 program export the LD_PRELOAD enviornment variable again in a different user's account and run it.

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task7_2p4.png">  

**Task 7.3**

For the first bullet point in task 7.2 we were able to see the print statement running the program as regular and as a normal user. For the second bullet point we were not able to see it when we set it to root permissions and tried to run it again as a normal user. This is because the file was only able to be executed by the root and not by a normal user outside of that group. For the third bullet point in task 7.2 this time we do see the print statement again. This time around we actually access root as the user and execute the file. This was expected since we set the UID to root and then ran it from root. For the last bullet point in task 7.2 we were actually able to see the print statment when trying to run the file as user1. This one surprised me a bit but I assume it has something to do with how the LD_LOADER handles those permissions within the environment. 

## Task 8: system() versus execve()

**Task 8 Summary**

_The overall point of this task is to try to attack/break in to a file and write/remove a file when in theory we shouldn't be able to._

**Task 8.1**

Yes I was able to compromise the integrity of the system as "Bob". I was able to invoke two different calls within the same command line. Which allowed me to write/remove the file that I shouldn't have been able to access. There is a security breach within the arguments of catall.c that allows me to access permissions if I call within the same line.

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task8_1.png"> 

**Task 8.2**

No I was not able to make the same attack as before. With execve it reads the entire quotations at once vs at seperate times. 

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task8_2.png">

## Task 9: Capability Leaking

**Task 9 Summary**

_This task is to demonstrate the Principle of Least Privelege, Set-UID programs should relingquish their root privileges as soon as such privileges no longer are needed. The program also needs to hand over its control to the user. When this happens root privileges must be revoked._

Yes this was able to be edited, due to leaked privileges from the Set-UID executable.

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab01/task9.png"> 
