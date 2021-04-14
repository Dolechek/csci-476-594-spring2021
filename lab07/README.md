# Lab 07: MD5 Collision Attack Lab
- **Logan Dolechek (n47f693)**
- **logand.msu@gmail.com**
- **CSCI 476**
- **04/10/2021**
- **Link to assignment:**[https://www.traviswpeters.com/cs476-2021-spring/labs/lab07]
---

## Task 1: Generating Two Different Files with the Same MD5 Hash

**Summary**
_We will generate two different files with the same MD5 hash values. The beginning parts of these two files will have the same prefix. We can achieve this using the md5collgen program, which allows us to provide a prefix file with arbitrary content._

### Task 1.1: 

As you can see in the screenshots provided below. The hash values are the same, however, the hex values are different when we view it within a hex editor. 

### Task 1.2:

Using the same prefix from the previous task, which isn't a multiple of 64, it is padded until it becomes a multiple of 64. See screenshot below and the offset value for reference. 

### Task 1.3:

Looking at the screenshots provided below, we can see that when the file is filled to 64 bytes, there is no need for padding. I believe that this is the main take away of this step.

### Task 1.4:

First I directed output of those files to temporary files and then ran diff on those two to see the diffrences and the simularities. Below will be a screenshot of what I will discuss here. On the first line of the left and right files you can see that the 4th byte of line 50 does not match, the second line of the left and right files you can see that the 14th byte doesn't match and then the 12th byte of third line you can see doesn't match. The fourth line of the left and right file you can see that the 4th byte doesn't match. The fifth line of the left and right the 14th byte doesn't match. The sixth line you can see that the 12th byte doesn't match.

---

## Task 2: Understanding MD5's "Suffix Extension" Property

**Summary**

__

Seen in the screenshot below. I used md5collgen to produce M and N with the same prefix, and they have the same md5 hash. Then I created the T (suffix) and concatenated them to M and N separately. The MD5 hash was the same for these new files were the same. 

---

## Task 3: Generating Two Executable Files with the Same MD5 Hash.

**Summary**

__

I compiled print_array.c and opened it in bless. Bless showed that the first array value is at offset 3020 which is 12320 in decimal. The next value divisible by 64 is 12352, so I used the first 12352 bytes to create the prefix. I used this prefix in md5collgen to make two different files with the same hash. I then grabbed the rest of the program from byte 12353 to the end, using it as a suffix. I concatenated this suffix to the two files from md5collgen to make a complete program from the md5collgen files. The md5 hashes of these programs are the same, but running them shows that some values in the arrays are different. Everything done can be seen below within the three screenshots.

---

## Task 4: Making the Two Programs Behave Differently

**Summary**

__

Just like in Task 3 I compiled benign_evil.c and opened it with bless. The array started at offest 0x3020 (12320) so again the next closest multiple of 64 is 12352. So I created the prefix with the first 12352 bytes. I then used md5collgen to make the two different files (prefix-P and prefix-Q) with the same hash. To get P on it's own I took the last 128 bytes from prefix-P and created the file P128. To find the middle to the end of the program where Array X ends and Array Y starts up to where P is located. I took the last 12481 bytes of the program. The first 288 bytes of this part represent the end of Array X up to Array Y where P needs to be. I took these bytes and created the file mid. The suffix is byte 12897 to the end, found by adding 288 (size of mid) and 128 (size of P) to the size of suffix-P. One more byte must be added because of where suffix-P ends. 

From these files I concatenate prefix-P mid P128 and suffix to make version 1. Then I concatenate Prefix-Q mid P128 and suffix to make version 2. The md5sum of these versions match one another, yet you can see that version 1 is executing the benign code and version 2 is executing the malicious code.



