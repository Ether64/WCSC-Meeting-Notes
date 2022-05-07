# Overview of First CTF Meeting

-   Using wildcards/printing out contents of hidden/non-human-readable files **./* or *./-*
- Using *find* with human readable files -- you can use *find* to search for files that using certain tags such as *-size* and *-executable*

- Ex: `find . -size 1033c -type f`
- Ex: `find / -size 33c -user bandit7 -group bandit6`

- /dev/null file is a file that is forever empty; used to write temporary stuff to
- 2 means standard error in Linux
- Ex: `2> /dev/null`\
- So this command gets all the standard errors and places them into the place after >, which is */dev/null*

- *>* is a redirect (overwrites)
- *>>* appends
- Ex: `cat file3 >> file2`
- In the above command, the file contents of file 3 are being appended to file2.

## Network Fundamentals
- Lateral movement and MITM attacks brought up.
- Talked about interconnected access points in local-area connection
- Wide-area-network(WAN) = the larger network of information around the world
- IP address - unique identifier for device on internet
- NAT (Network Address Translation) - way to solve the problem of over abundance of machines for IP addresses on the internet. A router designates private ips to each device connected to it.

- Private IP -> router (public IP) -> WAN
- Public, private IPs - private IPs are dynamically assigned

- A,B,C networks = different network types that can be identified by looking at an IP Adress' octet range

- IPV4 = most commonly used protocol for device identification. (looks like ###.###.###.###)\
- **DHCP** (dynamic host configuration protocol) = how the router assigns device an IP address.
- DHCP looks at MAC addresses to assign them IP addresses, and memorize previous connections.
- Went over finding IPs using NSLookup
- Ports are doorways for your IP addresses.