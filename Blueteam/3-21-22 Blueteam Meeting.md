# Linux Hardening

In today's Blueteam meeting we went over common practices to ensure the security of a Linux machine.

- Detection of misconfigurations is important to see whether a system is vulnerable to exploitation, or if it is possibly being prepped as a target.

- In Linux, everything can be thought of as a 'file'. Files can represent hardware devices, file descriptors, and regular files.

- /.ssh directory stores ssh keys for validating. Private keys are used with ssh for password validation; a key pair is used for further security measures.
   - Key validation is an important part of how ssh works in terms of connecting to remote computers.

- `ssh_config` contains client-based details. 

- In the `ssh` directory, you may see a file ssh_config.d. 

- `sshd_config`  is perhaps the most important ssh configuration file on Linux machines.
    - This file is responsible for controlling ssh default ports, key authentication, root login (turn PermitRootLogin to 'no').

- do `sudo !!` to run previous command with sudo priv

- When creating a listener, you have to have `p` as the last variable for port. 

Ex: `nc -nvlp 4000{portnumber}`

use `kill {PIDnumber}` to kill a process
 - You can verify this worked using `sudo netstat -tulpn`
     - Remove `-l` to show only Established connections using netstat.

- `sudo ufw status` outputs the status of the Linux firewall system.

- use `sudo ufw default deny incoming` to configure firewalls to deny incoming traffic such as an external request to our machine.  Anything coming to us, will be blocked.

- Lets add another default rule: `sudo ufw default allow outgoing`

- If we set `sudo ufw deny 22` we will see that we deny all incoming ssh connections to the host machine. This can be checked by trying to connect to your ubuntu instance on your windows host machine using `ssh {username}@{ipaddressofhostmachine}`

- ubuntu comes with python3  by default, use `python3` to access the interpreter.

- lets use the python server module: `python3 -m http.server` to start a python-based web server.
    - Can now use `netstat -tulpn` to see python running.


- You can ban a specific IP address through ufw as well.
   - `sudo ufw allow from 203.0.113.4` this would allow everything from a specific address such as a USF addreess.
### Takeaways
`sudo ufw default deny incoming`

`sudo ufw default allow outgoing`

When working on machine remotely make sure ot enable:..

`sudo ufw ssh enable`


- Those two rules are really important for setting up a hardened linux machine. 

`sudo apt install htop` basically a task manager for linux. 

