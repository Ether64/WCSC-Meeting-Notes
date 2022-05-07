# Introduction to Redteaming (Pentesting)

Kali Linux + Metasploitable 2 Booted

- The general objective with pentesting is to go as far into a machine as possible; usually entails getting a root shell where you are of the highest privilege on a system.

**Pentesting Step 1: Reconnaissance**

- The first step in the pentester's methodology is scanning. We can run an nmap scan: `sudo nmap -sn 192.168.133.1/24`

- This is a ping scan that will reveal hosts within a subnet and see if they are available.

- Lets add options to an nmap scan of our metasploitable2 machine:

`sudo nmap 192.168.133.128 -v`


- This will print out a list of the services running on ports on the machine we are scanning, and aiming to exploit.

- `sudo nmap 192.168.133.128 -sC -sV -v`

-  The `sV` switch will query the version of the services on a machine (if no port is specified, it will query pretty much all the ports).

- The `sC` switch checks a port; once it confirms the nature of the port, it will essentially try to run simple scripts to exploit common vulnerabilities within that port service (say FTP).

- `CVE:....` signifies a common vulnerability which are centrally recognized by MITRE corp.

- We can use google to lookup common vulnerabilities (CVE's) to services that are running as an outdated (which usually means exploitable) version.

Ultimately, for the scanning phase, we generally want to:
   1. Conduct a ping scan to see all machines in a subnet.
   2. Conduct nmap scan to query top 1000 service versions
   3. Perform deeper scans as needed...

**Step 2: Exploiting( vsftpd vulnerability)**

- Type `ftp 192.168.169.129` (your ip address)

- ![[Pasted image 20220406180003.png]]

- oops, looks like this is gonna fail, lets exit out of the ftp prompt.

Why did we do this?

- We are trying to gain access to exploit `ftp` and look at the version, which we see is *vsFTPd 2.3.4*.

- Above, we wereusing the Smiley Face exploit against vsftpd ![[Pasted image 20220406180047.png]]

- Basically this exploit would create a bind shell on port 6200 if the user typed a smiley face after the username upon an ftp connection. Like this `ethan:)`
- Look at this: just typing `vsftpd exploit` into our browser brings us to this exploit hosted on ExploitDB:
- ![[Pasted image 20220406180204.png]]

- Lets download this by clicking the arrow next to 'Exploit'

- We download and run that script using `python3 49757.py -h <ipaddresstoexploit>`

![[Pasted image 20220406181801.png]]
look, we got root just running this script on the target ip.

- Let's try an anonymous login by doing `ftp <ipaddresstoexploit>`  and then entering 'anonymous' for the username and password for the ftp connection

- We are exploiting vulnerable ftp server 2.3.4


- Exploit-db is a reputable website to get exploits from as opposed to the dark web or github with no explanation....

- Don't just run random hex exploits on your computer.

- Can filter results from exploitdb based on typing the service in the 'Search' field.

Ex results from 'openssh' ![[Pasted image 20220406181003.png]]

**Bruteforcing ssh using hydra**

What is hydra?

Hydra is **a pre-installed tool in Kali Linux used to brute-force username and password to different services such as ftp, ssh, telnet, MS-SQL**

`hydra -h` to pull up options for the hydra tool.

- We are going to assume that the ssh service we are trying to bruteforce has `RootLogon`  enabled.

	`hydra -l root -P`  will try to logon with user `root` pulling passwords from a password list `rockyou.txt` which we first must unzip as it is gunzipped.

Unzip: `sudo gunzip -d /usr/share/wordlists/rockyou.txt.gz`

`hydra -l root -P /usr/share/wordlists/rockyou.txt 192.168.169.129 ssh -V` 

The above command is the full command to run a password list (which we compiled in the rockyou.txt file) attack on the target IP's ssh service)

- You will see this takes a while to process all of the inputted passwords from the list, looking for a match.

- Once we set a password on the rooted machine in our  shell (using `passwd`), we can run the password list attack until we find shorty, and we will see we have then cracked the password of the machine.

- Note: We logged in as root using the vsFTPd vulnerability and changed the root accounts password to *shorty* so the hydra scan goes smoother, and we can find credentials quicker. This was just to simulate how hydra works.

![[Pasted image 20220406182210.png]]

- Now that we have the password, lets login with ssh:

`ssh root@<ipaddressoftarget>`

![[Pasted image 20220406182516.png]]

Woah. Look at that. We have just ssh-ed into the machine using the password `shorty` and username `root` we cracked using a password list from before.

**Step 3: Infiltration and Enumeration/Exfiltration 
- Now we have free reign over this machine, and want to look to exfiltrate data or gain information about the processes running on a machine.

![[Pasted image 20220406182733.png]]

- We can now run commands such as `id` , `whoami` , and `ls -la` to be able to gather all this information and data located on the machine.

- Telnet is basically an insecure version of ssh.

- We can often connect to Telnet because of this.

`telnet 192.168.169.129 23` 

![[Pasted image 20220406183256.png]]

**More Exploitation Methods....**

**Privilege Escalation**

Two types of privesc:

- Lateral- moving to other users/machines within a network (horizontally)

- Vertical- using commands such as `sudo` to move to higher privileges on a machine (root)

`sudo su root` allows us to move into the root user once we are on the Metasploitable machine; in this way, we have elevated our privileges.

`sudo su user` we are now deescalating our privileges.

- Lets navigate to our `/user/` directory to look for interesting stuff:

- we see .bash history, which we can see previously ran commands by the user we are currently logged in as.

![[Pasted image 20220406183823.png]]

- Lets go into the `.ssh` folder and try to login as a user using their  key that we saw the user move into the /authorized_keys directory.

first `cd .ssh`

then

`cat id_dsa`

![[Pasted image 20220406185204.png]]

This will allow us to see the key data, and copy it over to our machine that will be ssh-ing to the vulnerable machine.

Once we have the key data copied, we want to store the data to a file on our exploit machine `nano key_file_data`
![[Pasted image 20220406185227.png]]

Then we can start the ssh process using this data with the `-i` switch:

`ssh -i user_private_key msfadmin@192.168.169.129`

This is attempting to connect to the vulnerable machine at that ipaddress with the keydata we have scraped from the vulnerable machine.

![[Pasted image 20220406184607.png]]

Now look here. When that key is loaded and validated as a valid ssh key, we are able to get an ssh connection to the vulnerable machine after typing the password, which we knew was *msfadmin*.

But wait. This was all pretty pointless, cause we still had to end up entering the password. The whole reason we are trying to login using this key, is so that we don't need to enter/know a password when ssh-ing to the machine we are looking to exploit.

In order to do what we really wanted to do, we needed to convert the key to use RSA, which won't really be explained here.

Anyways, you now get the gist of pentesting!

## Summary

- Start with nmap scan

  - Start with services/ports that you can easily get into `ftp`, 
 `telnet` anything that can give you details about versions of services

- Lookup exploits based on the version numbers and vulnerabilities you suspect will be relevant.

- Exploit and follow methodology of the exploit that you looked up.

- Once you have ssh-ed or established a shell on the machine, enumerate details/information using `ls -la`, `whoami`, `id`... etc.

- Of course, an attacker would then look to exfiltrate the information stealthily, or leave malware without you being a traceable entity. But remember, we are pentesters.... not hackers here!





