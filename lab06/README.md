# Lab 06: Secret-Key Encryption Lab
- **Logan Dolechek (n47f693)**
- **logand.msu@gmail.com**
- **CSCI 476**
- **04/03/2021**
- **Link to assignment:**[https://www.traviswpeters.com/cs476-2021-spring/labs/lab06]
---

## Task 1: Encryption Ciphers and Modes

**Summary**

_This task is meant to have us experiment with various encryption algorithms and modes._

I did the three encryptions and produced the following output within these screenshots.

<img src =https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task1-1.PNG width="" height="">
<img src =https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task1-2.PNG width="" height="">

---

## Task 2: Comparing Encryption Modes

**Summary**

_We want to use the provided .bmp file to encrypt it, so that anyone without the encryption key is unable to know what the file contains._

### Task 2.1

<img src =https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task2-1.PNG width="" height="">

After encrypting with the above commands, I attempted to open the encrypted output pictures. As expected, they did not open, due to the messed up header data. 

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task2.1-1.png width="" height="">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task2.1-2.png width="" height="">

In order to open these encrypted pictures I followed the in-lab steps to place the header of the original picture with the body of both encrypted pictures.

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task2-2.png width="" height="">

By doing the above commands, the encrypted pictures were then viewable. Below, I have put the original picture, the cbc encoded picture, and the ebc encoded picture.

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task2-2-3.png width="500" height="500">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task2-2-2.png width="500" height="500">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task2-2-1.png width="500" height="500">

With the ECB encrypted picture a red circle and some color of a visible square can be seen. However, in the CBC version, no data can be made out at all. The entire picture is a jumble of "static".

### Task 2.2

I created an image within ms paint and then ran the same steps as before and received similar results. Here are the steps that I took. First, I encrypted this picture using both ECB and CBC. After that, I used head, tail, and cat to place the original images header data with the encrypted images bodies. After that I opened them in the image viewer. 

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task2-2.2-6.png width="" height="">

The following images were produced from my own image that I created. The original picture has been included first. Just like before, details can be made out within the ECB version though text is ore difficult to make out than shapes themselves. Again, absolutely no details can be made out within the CBC version of encryption.

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task2-2.2-5.png width="500" height="500">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task2-2.2-4.png width="500" height="500">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task2-2.2-3.png width="500" height="500">

---

## Task 3: Padding

**Summary**

_This task is to show us how padding works for block ciphers._

### Task 3.1

First I created the following files with 5, 10, and 16 bytes.

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task3.1-5.png width="" height="">

Then I encoded the using CBC with the same key and iv. 

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task3.1-2.png width="" height="">

All of the encrypted files have a size that is a multiple of 16. The files that were 5 and 10 bytes were encoded to be 16 bytes and the file that was 16 bytes was encrypted to 32 bytes.

Then I decrypted the output of each of those commands, and viewed them in a hex editor. 

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task3.1-3.png width="" height="">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task3.1-4.png width="" height="">

The file with 5 bytes was padded with 11 bytes of the value 0b, the file with 10 bytes was padded with 6 bytes of the value 6, lastly the file with 16 bytes was padded with an additional 16 bytes of the value 10.

### Task 3.2

First I encoded f1, f2, and f3 text files from the previous step, using all the methods of ECB, CFB, and OFB.

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task3.2-1.png width="" height="">

Below the output of the files can be seen.

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task3.2-2.png width="" height="">

The sizes of the CFB files do not have padding, i.e, the encrypted files are the same size as the input files. The sizes of the ECB files do have padding. The file with 5 bytes was padded with 11 bytes, the file with 10 bytes was padded with 6 bytes, lastly the file with 16 bytes was padded with 16 additional bytes. The sizes of the OFB files do not have padding, they have just as many bytes that the original files have.

After this I decrypted all of the encrypted files and viewed their contents.

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task3.2-3.png height="" width="">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task3.2-4.png height="" width="">

Above is the output of the files starting with DEC, as previously mentioned the values are still the same for the size of this file and it's encrypted version.

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task3.2-5.png height="" width="">

The decrypted CFB files do not use padding. Padding is not used because padding is not requred on the last block. Since we are operating on files that fit within one block, that is treated as the last block and no padding occurs.

The decrypted ECB files do use padding. The file with 5 bytes received an additional 11 bytes of the value 0b. The file with 10 bytes received an additional 6 bytes of the value 06. The file with 16 bytes received an additional 16 bytes of the value 10. 

The decrypted OFB files do not use padding. Padding is not used because this is a stream cipher. Adding the padding information to the stream is redundant and a waste of bytes.

---

## Task 4: Error Propagation & corrupted Ciphertext

**Summary**

_The purpose of this task is for us to understand error propogation properties of various encryption modes. We will create a ciphertext using different encryption modes, intentionally corrupt that ciphertext, decrypt it, and then examine what the end result is._

### Task 4.1: Predictions

ECB: I expect the entire block to be corrupted, whereever that single corruption exists.

CBC: I think one corrupted block will impact only this block and the next block. Since blocks may have an effect on one another.

CFB: I think only the corrupt single byte but not the entire block where the byte is corrupted.

OFB: I think this will act like ECB and only one block will be corrupted.

### Task 4.2: ECB & Data Corruption

First I encrypted using ECB, edited the 55th byte (value 39 to value 3F) then decrypted and viewed in hexdump. Only a single block was corrupted where the corruption was, it seems that my prediction was correct. 

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task4.2-4.png height="" width="">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task4.2-1.png height="" width="">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task4.2-2.png height="" width="">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task4.2-3.png height="" width="">

### Task 4.3: CBC & Data Corruption

I did the same thing as the previous task but using CBC this time. I changed the 55th byte from (value AB to AF) I got the same result, only the one block was corrupted. My prediction was wrong.

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task4.3-4.png height="" width="">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task4.3-1.png height="" width="">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task4.3-2.png height="" width="">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task4.3-3.png height="" width="">

### Task 4.4: CFB & Data Corruption

Again I followed the same steps as above but with CFB this time. I changed the 55th byte from (value 74 to 78). Only one block was corrupted, making my prediction wrong. 

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task4.4-4.png height="" width="">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task4.4-1.png height="" width="">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task4.4-2.png height="" width="">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task4.4-3.png height="" width="">

### Task 4.5: OFB & Data Corruption

Repeated the steps again... this time for OFB. I changed the 55th byte (value from B8 to B6). There was no corrupted block or byte. My prediction was wrong.

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task4.5-4.png height="" width="">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task4.5-1.png height="" width="">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task4.5-2.png height="" width="">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task4.5-3.png height="" width="">

The output was long so I snapped a picture of the top half where the corruption should have taken place. I hope that this is suffecient.

---

## Task 5: Common Mistakes with IVs

**Summary**

_The overall goal of this task is to show us that if we are not careful with our Initialization Vectors we may not actually encrypt the data making it not secure at all._

### Task 5.1: Uniqueness of the IV

I made a simple text file and named it t1.txt, I encrypted it three times. The same key was used everytime, and one of the encryptions uses a different Initialization Vector. The encryptions with the same IV are the exact same. The encryption with the different IV is totally different from others. This shows that the IV needs to be unique so that the same encryptio is not remade when reusing the same key. All can be seen below.

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task5.1-1.png height="" width="">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task5.1-2.png height="" width="">
