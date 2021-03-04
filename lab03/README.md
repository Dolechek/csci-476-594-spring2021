# Lab 02: Shellshock Attack Lab
- **Logan Dolechek (n47f693)**
- **logand.msu@gmail.com**
- **CSCI 476**
- **02/27/2021**
- **Link to assignment:**[https://www.traviswpeters.com/cs476-2021-spring/labs/lab03]
---

## Task 1: Getting Familiar with Shellcode

**Task 1 Summary**

**Task 1.1**

I was able to obtain a shell in both the 32 bit and 64 bit executables.

<img src = "" width="" height="">

**Task 1.2**

It's allocating a character buffer of size 500 and trys to copy the shellcode into that buffer. 

<img src = "" width="" height="">

## Task 2: Attacking a Vulnerable 32-bit Program (Level 1)

**Task Summary**
_summary_

**Task 2.1**

In the screenshot below, I used gdb to find the relevant address values and their differences within stack-L1-dbg.

<img src = "" width="" height="">

**Task 2.2**

Here I modified exploit.py, using the values from the previous task.

SCREENSHOT OF EXPLOIT.PY HERE <img src = "" width="" height="">
Afterwards, I executed exploit.py and ran stack-L1, confirming that I was able to acquire a root shell.

SCREENSHOT OF COMMAND LINE HERE (exploit.py --> stack-L1 --> which $0 --> whoami) <img src = "" width="" height="">

## Task 3: Attacking a Vulnerable 32-bit Program Without Knowing the Buffer Size (Level 2)

**Task Summary**

_Summary here_

This task tripped me up and I could not figure it out, so I moved on  

## Task 4: Defeating dash's Countermeasure

_Summary here_

**Task 4.1**

I was able to make the edits to the call_shellcode.c file and the image below will show my results. The only difference I saw was that the ./a32 gave me root access and the ./64 gave me seed permissions. 

<img src = "" width="" height="">

**Task 4.2**

I edited the exploit.py with the updated shellcode and re-ran the attack with the previous steps. Image below will show my outputs. 

<img src = "" width="" height="">

## Task 5: Defeated ASLR

_summary here_

**Task 5.1**

This attack did not work because with ASLR on, our attack is not garunteed to utilize the correct addresses. Refer to image below

<img src = "" width="" height="">

**Task 5.2**

Doing the brute force method it took my laptop roughly 5 minutes to attempt it. Below will be an image showing my output. 

<img src = "" width="" height="">

## Task 6: Experimenting with Other Countermeasures

_summary here_

**Task 6.1**

First I compiled the code with stackgaurd off and can confirm the attack worked. Afterwords I recompiled with stackgaurd on and the attack did not work.

<img src = "" width="" height="">

**Task 6.2**

I removed the -z execstack from the Makefile on both lines and then tried to compile the ./a32 and ./a64 both resulted with a Seg Fault which is to be expected. 

<img src = "" width="" height="">
