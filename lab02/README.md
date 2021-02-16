# Lab 02: Shellshock Attack Lab
- **Logan Dolechek (n47f693)**
- **logand.msu@gmail.com**
- **CSCI 476**
- **02/13/2021**
- **Link to assignment:**[https://www.traviswpeters.com/cs476-2021-spring/labs/lab02]
---

## Task 1: Experimenting with Bash Functions

**Task 1 Summary**

_Summary here._

*Task 1**
Within this image you can see that the vulnerable version of bash inside of the container does indeed allow us to use the bash_shellshock command to attack the foo function. 
T1.png here

### Task 2: Passing Data to Bash via Environment Variables

**Task 2 Summary**
_Summary here._

**Task 2.1: Passing Data via the Browser**
As shown in the image below. The enironment variables are given their values based on the fields within the HTTP request itself.
T2.1.png

**Task 2.2.1: The -v option**
The -v option shows the http request and response that was recieved from this command. Additionally, environment variables are listed below which were provided by that CGI file. 
task2.2.1.png  here

**Task 2.2.2: the -A option**
The -A option set the user agent to "my data" instead of grabbing the default user-agent when just running curl without using -A.
T2.2.2.png here

**Task 2.2.3: the -e option**
The -e option set the referer to "my data" while running this command. 
T2.2.3.png here

**Task 2.2.4: the -H option**
The -H option gave us an extra header to include to the request when sending to the HTTP server. 
T2.2.4.png here

### Task 3: Launching the Shellshock Attack

**Task 3 Summary**
_Summary here._

**Task 3.1: Shellshock & Reading A File**
1. A summary of your approach, with relevant command inputs/outputs
I used the -A flag to set user-agent to the malicious string in my screenshot. This string creates a function that echos some fake variable, followed by echo commands to get the contents of /etc/passwT
2. The curl option you used
-A
3. The result (i.e., was your attack succesful? why or why not? other observations?)
Yes it was succesful because of the way I manipulated the environment variable user-agent to poke my way into getting a /etc/passwd read out. 

T3.1.png here

**Task 3.2: Shellshock & Process info**
1. A summary of your approach, with relevant command i/o.
I was able to use sort of the same approach as 3.1 by just changing the curl command to curl -e. I figured the attack would work the same if I just removed the /etc/passwd and changed /bin/cat to /bin/id. I was able to get the uid doing this method.
2. the curl option used
-e
3. the result.
After running the command it printed out the uid, gid, and the groups immediately. Below will show an image with the command and return. 
T3.2.png

**Task 3.3: Shellshock & Creating A File**
1. a summary of your approach, relevant command i/o.
I first tried a command $ curl -H "() {echo tmp;} echo Content_type; text/plain; echo; /usr/bin/touch /tmp/newFile.txt;" etc. It didn't work and shot back a 400 Bad request. I then adjust my curl to a curl -e and when I ran that command it didn't do anything so I figured I would run the same command again but with 'echo; bin/ls -l /tmp/newFile.txt'. When I did that it shot back that I did indeed succesfully create the tmp folder, as well as, a .txt file within that folder. 
2. the curl opt used
-e
3. result.
After a few trouble shooting situations I was able to succesfully get the tmp folder to create and a txt file within it. Image below will show that. 
T3.3.png

**Task 3.4: Shellshock & Deleting A File**
1. summary of your approach, relevant command i/o.
I followed the same line of attack as Task 3.3. I changed the line a bit to 'echo /bin/rm /tmp/newFile.txt' which removed the folder and file and then I ran the same command to list it to see if it was actually gone. Nothing appeared.
2. curl opt used
-e
3. result.
I was succesfully able to remove the folder and file and check to see if it was there or not. It was no longer there. 
T3.4.png

**Task 3.5: Shellshock & Reading A Priveleged File**
1. summary of approach, relevant command i/o.
With this task I decided to try out -H. Just as I thought from previous attempts on the last couple tasks the -H doesn't work. It always spits back a 400 Bad Request error. I then attempted to read out the /etc/shadow with a -e and -A curl but was unable to get anything to print. 
2. opt used
-H, -e, -A
3. result.
The ultimate result here is that no matter the curl option attack I was unable to read the /etc/shadow because it is a privileged file. The permissions that are set to that do not allow me to get into and see what is within that shadow file. 

### Task 4: Getting a Reverse Shell via Shellshock

**Task 4 Summary**

_Summary here._

The image below will show that I was able to get the reverse shell to connect and spit back information to my attacker side. 
T4.png

### Task 5: Using the Patched Bash

**Task Summary**

_Summary here._

After succesfully changing the command from /bin/bash_shellshock to only /bin/bash. I only attempted the first two sub-task commands from the entirety of Task 3. I did this because I knew that the rest of the commands wouldn't work as well. Since we removed that attack command no attack will work. Image below will show what I did. 

T5.png
