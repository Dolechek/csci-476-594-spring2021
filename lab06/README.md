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

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task2-2-3.png width="" height="">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task2-2-2.png width="" height="">
<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task2-2-1.png width="" height="">

With the ECB encrypted picture a red circle and some color of a visible square can be seen. However, in the CBC version, no data can be made out at all. The entire picture is a jumble of "static".

### Task 2.2

I created an image within ms paint and then ran the same steps as before and received similar results. Here are the steps that I took. First, I encrypted this picture using both ECB and CBC. After that, I used head, tail, and cat to place the original images header data with the encrypted images bodies. After that I opened them in the image viewer. 

<img src=https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab06/task2-2.2-6.png width="" height="">

The following images were produced from my own image that I created. The original picture has been included first. Just like before, details can be made out within the ECB version though text is ore difficult to make out than shapes themselves. Again, absolutely no details can be made out within the CBC version of encryption.

# IF YOU ARE LOOKING AT THIS BEFORE 04/08/2021 @ 11:59 am. I AM NOT DONE MOVING EVERYTHING FROM MY DOCUMENT TO THIS README FILE. I STILL NEED TO FORMAT AND FINISH ADDING EVERYTHING. I CANNOT KEEP MY EYES OPEN.

<img src= width="" height="">
<img src= width="" height="">
<img src= width="" height="">

