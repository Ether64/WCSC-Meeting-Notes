### CTF Meeting Overview

- Today we used Metasploitable, a commonly used vulnerable virtual machine platform, and also learned about some fundamentals of web security.

- Content on a webpage:
  - HTML 
  - CSS
  - JS (javascript)
  - Many other technologies

- Javascript allows special embedded functionalities within a webpage (animations)

- Websites are loaded by an initial DNS request. This asks the server for a web page.

- Types of connections:
   - HTTP
   - HTTPS 

### Web verbs/methods, and headers

- GET
- POST

- These are web verbs

- GET request is the first part of a connection header.

- A full web **request** header will look something like this:

  - GET /index.html HTTP/1.1
	Host: 192.168.170.129:8081
	Connection: keep-alive
	User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)AppleWebKit...
	Accept:....
	Referrer:...
	Accept-Encoding:....
	Accept-Language:...

**Response Headers**

- Status codes:
  100-199: Information
  200-299: Successes
  300-399: Redirects
  400-499: Client Errors
  500-599: Server Errors

HTTP/1.1 200 OK         (see that 200 there? that is the status code.)
Accept-Ranges: bytes
Content-Length: 28
Content-Type: text/html; charset=utf8
Last-Modified: Wed, 12 Feb 2020 ...
Date: Thu, 27 Feb 2020 ...

- This is a **response header**, this is what the webpage sends back after getting a **request header** 

### Cookies

- These are small bits of data that are stored in your browser. Not edible

- These often help companies gain information about those who visit their webpages, and they can then profit off your data. Kind of cringe.

### Common Web Vulnerabilities

- LFI (Local File Inclusion)
- RFI (Remote File Inclusion)
- Authentication Bypass
- XSS (Cross-Site Scripting)
- SSRF(Server Side Request Forgery)
- SQLi (SQL Injection)
- Common Misconfiguration

- A recent example of a web vulnerability is Log4J. This was premised on the remote file inclusion(RFI) vulnerability by allowing java code to be run on a machine through the execution of a string on a Minecraft server.
   - This would now allow you to get shells on every single person's machine on the Minecraft server.

- We talked about a tool called *Evilginx2* which emulates a real google.com page, it sits in the middle of this webpage to intercept all of your login information by stealing the user's cookie once they are logged in to their google account (XSS tool).

- XSS is founded on the idea of using embedded javascript to execute javascript on unsanitized webpage fields.

- SQL injection occurs when the attacker enters SQL code into the login fields (username and password) of a webpage in order to have the SQL database running in the background do some unplanned-for action.

- Website exploitation so often includes injections or misconfigurations.

### Metasploitable

- first lets analyze our network topography once we connect to the Metasploitable environment `nmap -sn ip.address.of.metasploitable 1-255 -v`

- `nmap ip.addres -sV`

Gives you information on services up on the mapped address.

Copy Metasploitable IP address into browser to connect to DVWA.

- By running `ifconfig` on my Metasploitable instance, I can see my IP address

 https://i.imgur.com/ZhRWkeE.png


- Basically by using Nmap here, we are looking for a remote entry point into the Metasploitable machine, from our other Ubuntu virtual machine that is trying to connect to Metasploitable.

- We can connect to the Metasploitable instance by typing its IP address into a web browser.

- Here we can see many common exploitative tactics that we can dive into hands on, such as Brute Force Attacks, SQL Injections, Command Execution, XSS (Cross-Site Scripting)...

- CONTINUE PRACTICING on overthewire.org. 