# Bash Scripting 

- Can create environment variables in our shell. A predominant example of this is `$PATH`
   - `$PATH` tells us where binaries are being looked for on our Linux system.

- We can then run `echo $PATH` to print out the value of the path variable in our terminal.

- Lets create a file test.sh to learn more about bash notation.

- `#!/bin/bash` at the start of the file specifies 'shebang' notation, which tells us that this file should run with the application after the !#, which in this case, is bash.

	- We can then put `echo enter the ip to ping` and then then `read IP` 

- If we run add to this file  `ping -c 2 $IP`, it can then be executed as a script to print out the ping results of an entered IP.

- ![[Pasted image 20220418173530.png]]

- We can alter the script like so...![[Pasted image 20220418173652.png]]
to ping all machines (1-254) within the .78 subnet.


**Traps in bash**

- **Traps** act as a listener in a program, that will call a subroutine based on a certain condition.

- Basically, using `trap` we can prototype (implement before instantiated) and declare a function (or a variable) at the same time.

- ![[Pasted image 20220418174240.png]]

- We can do the same program as above to redirect standard output to /dev/null, making our script for ping scanning our subnet, just a bit cleaner:
 
![[Pasted image 20220418174729.png]]

- This should only print to terminal the statement 
`"<ipaddress> is up"`

- If we are running a big scan, we can have a trap function as a cleanup routine to make sure our script exits properly.

**Netstat automation with bash**

- Lets make a new script 'network.sh'.

- ![[Pasted image 20220418175541.png]]

- First pulls color codes using `\e[31m;107`. In this case, the text will be red (\e31m), and the background color white (107).

- This script will read each line every line of the `netstat -tulpn` command, and will echo that read line.

![[Pasted image 20220418175832.png]]

**Using ps**:

-`ps` command is used to show running processes. 
- `ps -aux` will show all processes running on the machine.

- Lets create a process enumeration script:
![[Pasted image 20220418180910.png]]

- This will print out all processes running as root on our machine.

- the ''.bashrc' file can be edited to specify aliases to change how bash runs on our Linux system.






