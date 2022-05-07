# Overview

- Today saw us visited by Ben Weber, a current professional that works as part of Raymond James BlueTeam.

- His credentials as a Lead Engineer include CISSP, Sec+, OSCP, GCIH, GCWN, GCUX, GPYC, GPEN, GWAPT, GSEC, GCIA, GXPN, GCCC, GDSA, GCPM and many more

- We were also joined by Jack Zimmer a Cyber Threat Analyst who won a recent CTF at Raymond James. He will be talking more next week.

**Discussions Topics**

  - What is Blue teaming? Red teaming? Purple Teaming?
  - Introduction to the Cyber Threat Center
  - How we respond to threats - Pyramid of Pain and MITRE ATT&CK formats

## Teams

- A **BlueTeam** consists of a team that is designated with the role to protect an organization's critical assets against any kind of threat.

- BlueTeamers help to strengthen the metaphorical 'castle walls' so no intruder can compromise corporate infrastructure.

- One of the biggest and most common motivators for cyber attacks is money. Raymond James, being a banking company, has to work especially closely with security experts to optimize blueteam security strategy.

- Blueteam operations will most likely be for protecting a company's infrastructure, personnel, PII, and intellectual property.

- Blueteaming and Redteaming work in tandem, and get exponentially better at similar rates, most of the time.
   - Ex: a new pentesting tool gets pushed to GitHub, then blueteam has to react quickly towards countering usage of that tool.

- Weber notes that they use tools to 'fool' a bad guy, such as **honeypots**, which will allow the blueteam to gather intel on what kind of exploits attackers are looking to run.

**Redteam**:

- A group of people authorized and organized to emulate a potential adversary's attack or exploitation capabilities against an enterprise's security posture.

- A **redteam's** main objective is to improve enterprise cybersecurity by demonstrating what can happen after successful cyberattacks, while also demonstrating what defenders can do to mitigate them in an operational environment.

**Purpleteam**:

- A security methodology where blue and red teams work closely together to maximize cyber capabilities through continuous feedback and knowledge transfer between both blue and red team groups.

### The Cyber Threat Center

- Personnel comprised of 
   - Incident Response
   - Cyber Intelligence
   - HUNT
   - Vulnerability Management
   - Cyber Crime
   - Special Projects
   - SIEM Operations

- Raymond James is mainly a **purpleteam**-focused organization.

- **Threat Hunting** is focused on discovering how we can find a threat actor once they compromise enterprise systems/tools.

- Weber notes that one of the tools that use is a **SIEM**; at Raymond James, they hold 1.5 trillion bytes of log data.

- The Cyber Threat Center is premised on 5 main operations:

   - A **Configuration Management Database** (46 Thousand Nodes) 
   - **Log and Event Management** (about 2.33 trillion events)
   - **Incident Response Handbook
   - **Incident Documentation** (105,151 incidents)
   - **Security, Orchestration, Automation & Response (153 Billion Automated Blocks)**

- We want to make attacker's efforts as cumbersome and expensive as possible, and if possible make them reveal data on themselves in the process due to simple complacency.

### Mitre ATT&CK Matrix

- Gives list of common tactics with many different techniques

Ex: **Reconnaissance**
Techniques:
  - Active Scanning
  - Gather Victim Host Information
  - Gather Victim Network Information
  - Phishing for Information
  - Search Open Technical Databases...

- MITRE framework also provides information on different APT groups which can give insight as to what kind of attack we can attribute to different regional aptitudes.

- Ex: if you are trying to protect against a threat group such as APT 28, MITRE will provide and highlight specific techniques you would want to work to instill countermeasures towards.

- Threat groups of certain country's often have very similar endgoals (Russia to make the U.S. look bad). On the other hand, Chinese threat actors often try to steal private information of software groups in order to make cheaper imitation of software to sell to other countries.

- They want to replicate a product at a cheaper price for easy profitability without the need for investment in innovation.

- Weber emphasizes to setup a homelab, even if most of the tools you use emulate expensive versions of a server/lab.

- YouTube channels (Malware Engineering)
  Malware for Hedgehogs
  OALabs
  Colin Hardy

## Demo of Open-Source Tool Employment in a Mock Phishing Attempt

- Starts with phishing email and html attachment.
- Comes from Gmail domain.

- Proceed to an automated analysis using **Cuckoo Malware Sandbox**

- Provides summary of the analysis and hashes of the attacked html document. Assigns a malicious behavior score to the file.

- Automated analysis like this is a firsthand go-to in the presence of possible phishing attempts.

- Another tool: **VirusTotal**

- Used on a regular basis within Raymond James.

- **BurpSuite**
- **Censys** - OSINT
helps provide details by scouring the internet, on an adversary by following ip addresses and routing information.



