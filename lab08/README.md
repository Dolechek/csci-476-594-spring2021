# Lab 08: RSA Public-Key Encryption and Signature Lab
- **Logan Dolechek (n47f693)**
- **logand.msu@gmail.com**
- **CSCI 476**
- **04/18/2021**
- **Link to assignment:**[https://www.traviswpeters.com/cs476-2021-spring/labs/lab08]

---

## Task 1: Deriving the Private Key

**Summary**
_Let p, q, and e be three prime numbers. Let n = p * q. We will use (e,n) as the public key. Using the big number APIs, please calculate the private key d._

I modified the template code to assign the values p, q, and e. I also created a BIGNUM variable 1 that holds the value of decimal 1. Subtracting 1 from p and q then multiplying them together gives me phi of n. Taking the mod inverse of e and phi n provides the private key. Running this code shown outputs the private key seen below. 

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab08/task1codesnippet.png>
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab08/task1privatekey.png>

---

## Task 2: Encrypting a Message

**Summary**
_Let (e,n) be the public key. Please encrypt the message m provided below. After you encyrpt the message, you should decrypt it - we provide you with the private key, d to verify that you can recover the message._

First I initialized m, e, n, and d as given in the task. Calculating m^e mod n outputs the encoded message as seen below. This can be decoded by taking that output to the power of d then modding by n. 

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab08/task2codesnippet.png>
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab08/task2output.png>

To verify that the encoding and decoding processes were correct I put the decoded message through the python command to confirm that I got the correct message back. 

---

## Task 3: Decrypting a Message

**Summary**
_The public/private keys used in this task are the same as the ones used in Task 2. Please decrypt the following ciphertext C, and convert it back to a plain ASCII string._

I reused n and d from the previous task as they are the same public and private keys used here. I modified my code from task 2 to only perform the decoding step for task 3. This involves taking C^d mod n to retrieve the message. I then used the same python command from task 2 this time with the hex value output by my code, to confirm that I decrypted the correct message.

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab08/task3codesnippet.png>
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab08/task3output.png> 

---
