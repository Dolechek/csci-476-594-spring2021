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

