### Overview 

### Introduction to PowerShell

- PowerShell is exceptionally good at automating certain redundant tasks that you may see in common system hardening practices.

- Think of it as an advancement of the Windows command prompt, providing more complex built-in utilities.

- We can view all files/directories by doing `cd System32` and then `ls`

- **Aliases** are a shortcut for a command, `ls` is basically equivalent to `dir`

- Running the `alias` command will printout out commonly-used PowerShell commands and functionalities.

### Enumerating Details of 'Computer Management' in Powershell

- `Get-LocalUser` lists all users and a short description of their account credentials.

- Piping: `Get-LocalUser | Select *` This will give some more details about the users; password specifications will be printed out, last logon time, SID, and more.

- You can scroll down to see the details of various users: if they have a  password set, password expiration date, and all of the above stuff.

- Let's use another `Get` functionality: `Get-LocalGroup` will printout the local group policy information that we previously navigated to in the Windows 'Computer Management' GUI.

- `Get-LocalGroup | Select *` to pipe all the attributes of local groups to the terminal.

- `Get-Service` gives us the same information that you would find in 'Services' at the Task Manager on Windows.

- `Get-Service | findstr -i `Stopped pipes out all of the information about what services have been stopped.
   - Using this, we can see whether a firewall has been turned off, or an AntiVirus has stopped running
   - Quick and easy way to scan important services that should be up and running on Windows.

- `Get-Service | findstr -i Running` Does the opposite of the previous command, provides and locates information of all running processes on the current Windows machine.

- `Get-ComputerInfo` tells you your current windows version and hardware stats.
  - With this, we are easily able to tell if our windows version is out of date, AKA vulnerable.

- Lets customize the appearance of our console output:
- `Get-LocalUser | Select * | ConvertTo-Html | Out-File users.html` this shows us the html makeup of a specific page, and prints it out to a file 'users.html'

- Pay attention to where you are running commands in Powershell, with `ls` and `pwd`

- MAKE SURE YOU ARE RUNNING POWERSHELL ADMINSTRATOR

- We can not open the html file to see the commands output in this file.

- We can use `ConvertTo-` with many other files types, such as .csv with excel.


### BlueTeam Networking

- Powershell can be used to perform networking tasks on your local windows machine

- `Get-NetTCPConnection` will show us all established TCP connections on our windows machine.

 - `Get-NetTCPConnection -State Established` Using the above command with a -state specifier *Listen* will show us the connections that are currently established on the machine.

- Tabs and programs will appear under this scope of established TCP connections.

- `Get-NetTCPConnection -State Listen` will display currently listening TCP connections,
and will allow us to see whether a machine is currently looking to be exploited or connected to by an adversary.


- `Invoke-WebRequest -UseBasicParsing google.com` this command basically does what you do by navigating and opening a basic webpage such as 'google.com'.
- describes the content on the page, and the HTTP request that was sent to the website.

- ```Get-WinEvent -FilterHashTable @{
LogName = "Security"
ID = 4625}```

- Between those lines, we use Shift+Enter to make the command easier to read.

- The above command searches for incorrect logins to the system by searching the logs of windows in a hash table. Filters based on the log's name, and ID #.

- This is important, because by running the above command, we can get hints as to whether a RedTeam is trying to brute force passwords into our machine.

- Basically, the above command mimics the role of 'Event Viewer' that is part of the Windows 'Computer Management' GUI.

#### Windows wmic Tool

- run `wmic`

- This will put us in a shell that uses this tools functionalities.

- `product get name, version, vendor` Typing this into the created wmic shell will give us some information about the packages installed on the current windows machine (Microsoft Redistributables)

- This gives us insight as to whether or not the current machine is exploitable by way of outdated packages or versions.

- You can also use *wmic* to get all drives on the current machine.

- `partition get BlockSize, StartingOffset, Name, Index`

- Here we can see if any malicious or suspicious hard drives are connected to the machine by looking at connected disks and partitions.

- `Get-WmiObject -Class Win32_Product | select Name, Vendor, Version` does the same thing as the `product get name, version, vendor` command above, but without using the *wmic* tool.

