# Lab 03: Buffer Overflow Attack Lab
- **Logan Dolechek (n47f693)**
- **logand.msu@gmail.com**
- **CSCI 476**
- **02/27/2021**
- **Link to assignment:**[https://www.traviswpeters.com/cs476-2021-spring/labs/lab03]
---

## Task 1: Getting Familiar with Shellcode

**Task 1 Summary**

_Within this task we use look at different versions of shellcode. A 32-bit and 64-bit shellcode to be exact. Shellcode is used in most code-injected attacks. _

**Task 1.1**

I was able to obtain a shell in both the 32 bit and 64 bit executables.

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab03/T1_1.png" width="" height="">

**Task 1.2**

It's allocating a character buffer of size 500 and trys to copy the shellcode into that buffer. 

---

## Task 2: Attacking a Vulnerable 32-bit Program (Level 1)

**Task Summary**

_Within this task we will compile the vulnerable program into the 32-bit binary called stack-L1._

**Task 2.1**

In the screenshot below, I used gdb to find the relevant address values and their differences within stack-L1-dbg.

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab03/T2_1.png" width="" height="">

**Task 2.2**

Here I modified exploit.py, using the values from the previous task.

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab03/T_2_2_2.png" width="" height="">

Afterwards, I executed exploit.py and ran stack-L1, confirming that I was able to acquire a root shell.

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab03/T2_2_1.png" width="" height="">

---

## Task 3: Attacking a Vulnerable 32-bit Program Without Knowing the Buffer Size (Level 2)

**Task Summary**

_The task here is to get the vulnerable program to run your shellcode under a restraint that we don't know the buffer size._

This task tripped me up and I could not figure it out, so I moved on  

---

## Task 4: Defeating dash's Countermeasure

_We re-link dash to shell since before these steps we had shell linked to dash. This will allow us to get around dash's countermeasure of dropping any elevated privelege._

**Task 4.1**

I was able to make the edits to the call_shellcode.c file and the image below will show my results. The only difference I saw was that the ./a32 gave me root access and the ./64 gave me seed permissions. 

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab03/T4_1.png" width="" height="">

**Task 4.2**

I edited the exploit.py with the updated shellcode and re-ran the attack with the previous steps. Image below will show my outputs. 

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab03/T4_2.png" width="" height="">

---

## Task 5: Defeated ASLR

_Within this task we will brute force our way through ASLR._

**Task 5.1**

This attack did not work because with ASLR on, our attack is not garunteed to utilize the correct addresses. Refer to image below

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab03/T5_1.png" width="" height="">

**Task 5.2**

Doing the brute force method it took my laptop roughly 5 minutes to attempt it. Below will be an image showing my output. 

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab03/T5_2.png" width="" height="">

---

## Task 6: Experimenting with Other Countermeasures

_In this task we will explore some of the other countermeasures that exist to defend against buffer overflow attacks._

**Task 6.1**

First I compiled the code with stackgaurd off and can confirm the attack worked. Afterwords I recompiled with stackgaurd on and the attack did not work.

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab03/T6_1.png" width="" height="">

**Task 6.2**

I removed the -z execstack from the Makefile on both lines and then tried to compile the ./a32 and ./a64 both resulted with a Seg Fault which is to be expected. 

<img src = "https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab03/T6_2.png" width="" height="">
