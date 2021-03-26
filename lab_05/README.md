# Lab 05: Cross-Site Scripting (XSS) Attack Lab
- **Logan Dolechek (n47f693)**
- **logand.msu@gmail.com**
- **CSCI 476**
- **03/23/2021**
- **Link to assignment:**[https://www.traviswpeters.com/cs476-2021-spring/labs/lab05]
---

## Task 1: Post a Malicious Message to Display an Alert Window

**Task 1 Summary**

_The objective of this task is to embed JavaScript code in your Elgg profile, such that when another user views your profile, the JavaScript code will be executed and an alert window will be displayed._

I was able to get the notification to pop up by putting the <script> line into the short discription part of Alice's about me. When done I got this pop up menu that will be shown below. 

<img src =https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab_05/t_1.png  width="" height="">

## Task 2: Post a Malicious Message to Display Cookies.

**Task 2 Summary**

_The objective of this task is to embed JavaScript code in your Elgg profile, such that when another user views your profile, the user's cookies will be displayed in the alert window this window. This can be done by adding additional code to the JavaScript code from the previous task._

After embeding the JavaScript within the profile I was able to get this pop up screen that will be shown below. 

<img src =https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab_05/t_2.png width="" height="">

## Task 3: Steal Cookies from the Victim's Machine

**Task 3 Summary**

_The objective of this task is to get the JavaScript code to send the information of the cookies to the attacker and not notify the victim about it._

After embeding the <script> line within the victims profile I was able to get the info to pop up on the attackers side. Images below will show what I mean. 
  
<img src =https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab_05/t_3_1.png width="" height="">

<img src =https://github.com/Dolechek/csci-476-594-spring2021-private/blob/main/lab_05/t_3_2.png width="" height="">

#Task 4: Becoming the Victims Friend

**Task Summary**

_The objective of this task is to embed some malicious code on Samy's profile so that when any other user simply visits his page, they will automatically be added as a friend, even though they don't phsyically click "add friend"._

**Task 4.1**

I was able to find what I needed to add to the //FILL IN section of the JavaScript code by logging in as Alice and then visiting Samy's profile then addhing him as a friend. Using the built in HTTP reader on firefox I was able to find the ts + token + ts + token to use within that FILL IN section. Below will be the line I used.

var sendurl="http://xsslabelgg.com/action/friends/add?=59" + ts + token + ts + token;

**Task 4.2**

Yes, if you have the editor mode you can use the script HTML tag to embed the JavaScript code to force the attack. Done to a similar style done in Task 1. 

## Task 5: Modifying the Victim's Profile

**Task Summary**

_The objective of this task is to modify the victim's profile when the victim visit's Samy's page. We will write an XSS worm to complete the task. This worm does not self-propogate._

**Task 5.1**

The following variables were set to these values for the following attack:

Var sendurl =  "http://www.xsslabelgg.com/action/profile/edit" 

Var content= "__elgg_token="+elgg.security.token.__elgg_token+ts+name+"&description=edited by Samy&accesslevel[description]=2&briefdescription=&accesslevel[briefdescription]=2&location=&accesslevel[location]=2&interests=&accesslevel[interests]=2&skills=&accesslevel[skills]=2&contactemail=&accesslevel[contactemail]=2&phone=&accesslevel[phone]=2&mobile=&accesslevel[mobile]=2&website=&accesslevel[website]=2&twitter=&accesslevel[twitter]=2"+guid; 

Var samyGuid= 59;

After setting these variables, loggin in as Alice and Visiting Samy's profile. Alice's profile was edited to "edited by samy". 

**Task 5.2**

Without "line 1" the attack would run on Samy's page overriding the code and defeating it's purpose of spreading to the other profiles or defeat the purpose of targeting other profiles.

## Task 6: Writing a Self-Propogating XSS Worm

I honestly couldn't figure this step out. The assignment is already late so, may as well submit what I got so far. 
