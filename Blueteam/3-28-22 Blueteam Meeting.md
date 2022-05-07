# Intro to Windows System Hardening
**TCP**

- uses for data transmission that requires an initial connection to be established before transfer (TCP handshake).
- Will check for errors in packets and request bad packets to be resent.
- protocols: HTTP, HTTPS, FTP
- Used for file download, web browsing - slow and reliable

**UDP**

- Does not require an established connection and no packet sequence
- Will drop errored packets.
- DNS, TFTP, VoIP
- Used for gaming, streaming - fast and unreliable

**Firewalls**

- Monitor and filter traffic for incoming and outgoing traffic
- Rules are defined from the user and applications.

**Types of Rules**

- Allow - Allows traffic
- Drop - Drops traffic and does not send response (connection timeouts)
- Reject - Traffic is denied

**Powershell with Firewall**

`Get-NetFirewallProfile` - Shows all profiles and their configs

`Set-NetFirewallProfile -Profile Domain, Public, Private -Enabled True` - Enables firewall profiles

`Get-NetFirewallProfile -Name Public | Get-NetFirewallRule` - Shows all rules for public profile.

`PS C:\> New-NetFirewallRule -DisplayName"Block Outbound Port 80" -Direction Outbound -LocalPort 80 -Protocol TCP -Action Block` - Blocks Outbound traffic on port 80.

- Games/applications will oftentimes generate their own firewall rules.

- `Get- NetTCPConnection` is basically the Powershell equivalent of netstat

- Can use GUI or Powershell to interact with firewalls.

- `Set-NetFirewallProfile -Porfile Public,Private,Domain Enable - True`
- enables firewalls of public, private, and domain categories.

- `Get-NetFirewallProfile -Name Public | Get-NetFirewallRule | findstr "Microsoft"`
- This will search the public profile and pull all the rules, in which it will look for a string dealing with Microsoft.

- `winver` to get Windows version on a machine. Can then look up this version number on exploit.db.

**Enabling Updates**

- `install-Module PSWindowsUpdate`
- `Get-WindowsUpdate`
- `Install-WindowsUpdate`
- `Get-WindowsUpdate -AcceptAll -Install -AutoReboot`