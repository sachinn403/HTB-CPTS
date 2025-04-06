# Initial  Enumeration

## Scanning

#### NMAP TCP quick

```bash
sudo nmap -Pn -v -sS -sV -sC -oN tcp-quick.nmap IP
```

#### NMAP TCP Full

```bash
sudo nmap -Pn -sS --stats-every 3m --max-retries 1 --max-scan-delay 20 --defeat-rst-ratelimit -T4 -p1-65535 -oN tcp-full.nmap -sV IP 
```

#### NMAP TCP - Repeat if extra ports found

```bash
sudo nmap -Pn -v -sS -A -oN tcp-extra.nmap -p PORTS IP 
```

#### NMAP UDP quick

```bash
sudo nmap -Pn -v -sU -sV --top-ports=30 -oN udp-quick.nmap IP
```

#### NMAP UDP 1000

```bash
sudo nmap -Pn --top-ports 1000 -sU --stats-every 3m --max-retries 1 -T4 -oN udp-1000.nmap IP
```

#### NMAP UDP - Repeat if extra ports found

```bash
sudo nmap -Pn -sU -A -oN udp-extra.nmap -p PORTS IP 
```

#### ICMP Sweep

```bash
fping -a -g 10.10.10.0/24 2>/dev/null
```

#### ARP Scan (Local Network)

```bash
arp-scan -l
```

## Enumeration

#### FTP - Port 21

```bash
# Check for FTP version vulns
# Check for Anonymous login 
# Check for Read access
# Check for Web root or root directories of any other accessible service 
# Check for write access 
```

#### SSH - Port 22

```bash
# Check for SSH version vulns
# Check for User enumeration if necessary 
# Check if host key was seen somewhere else 
# Check if it prompts for a password - means password login is allowed for some users
nmap -sV --script=ssh-hostkey -p22 IP
# Bruteforce if necessary with CeWL, Hydra, Patator, Crowbar, MSF (if port gets filtered, there's defense mechanisms - fail2ban) 
```

#### Telnet - Port 23

```bash
# Connect and check for service running
```

#### SMTP - Port 25

```bash
# Check for SMTP vulns 
# Check version with HELO / HELLO <domain>  
```

#### POP - PORT 110

```bash
# Connect using telnet 
user <username> 
pass <pass> 
LIST - to list emails 
RETR <email numbr> - To retrieve emails 
```

#### DNS - Port 53

```bash
# Might indicate a domain controller on Windows 
# Check for zone transfer 
```

#### Kerberos - Port 88

## Indication that it's a DC

```bash
kerbrute userenum --dc IP -d DOMAIN users.txt
GetNPUsers.py domain.local/ -usersfile users.txt -no-pass
```

#### Netbios - Port 139

```bash
nmblookup -A IP
nbtscan IP 
# On older hosts, this port serves SMB / SAMBA, scan by adding 'client min protocol = LANMAN1' to GLOBAL setting in /etc/samba/smb.conf or by using --option='client min protocol'=LANMAN1 with smbclient
```

#### RPC - PORT 135

```bash
sudo nmap -sS -Pn -sV --script=rpcinfo.nse -p135 0 
rpcinfo IP
rpcclient -U "" -N [ip]
```

#### LDAP - Ports 389,636,3268,326

```bash
sudo nmap -sS -Pn -sV --script=ldap* -p389,636,3268,3269  
```

#### SNMP - Port 161

```bash
snmpwalk -v2c -c public IP
snmp-check IP
onesixtyone -c community.txt IP
sudo nmap -sU -sV -p 161 --script snmp* IP
snmpenum -t IP -c public
```

#### Oracle - Port 1521

```bash
tnscmd10g version -h IP
nmap -sV --script=oracle-tns-version -p1521 IP
odat tnscmd -s IP --ping
odat all -s IP -p 1521
odat sidguesser -s IP
```

#### MySQL - Port 3306

```bash
mysql -h IP -u root -p
nmap -sV --script=mysql* -p3306 IP
hydra -L users.txt -P passwords.txt mysql://IP
mysql -h IP -u root
```

#### WEB - PORT 80 / 443

NMAP Web

```bash
sudo nmap -Pn -sC -p80,443 
```

Checks

```bash
# Browse the webapp 
# Check for usernames, keywords 
# Check Web server vulns
# Check for Cgi's shellshock
# Check Certificates for hostname
# Check robots.txt
# Check sitemap.xml
# Check for known software - View source 
# Check for default credentials 
# Check for input validation - SQLi
# Check for OS Command execution
# Check for LFI / RFI 
```

Dirb

```bash
dirb IP
dirb with -X extensions based on web technology, .php,.asp,.txt,.jsp
dirb IP -a  'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/42.0.2311.135 Safari/537.36 Edge/12.246'
```

Gobuster

```bash
gobuster dir --url IP --wordlist /usr/share/seclists/Discovery/Web-Content/big.txt
gobuster dir --url IP --wordlist /usr/share/seclists/Discovery/Web-Content/big.txt -k -a 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/42.0.2311.135 Safari/537.36 Edge/12.246'
```

Nikto

```bash
nikto -host IP
```

whatweb / wappalyzer

```bash
whatweb http://IP
wappalyzer http://IP
```

wpscan (WordPress)

```bash
wpscan --url http://IP --enumerate u
```

#### SMB - Ports

NMAP vuln scripts

```bash
sudo nmap -Pn --script=smb-proto* -p139,445 
sudo nmap -Pn --script=smb-os-discovery.nse -p139,445
sudo nmap -Pn --script=smb-enum* -p139,445
sudo nmap -Pn --script=smb-vuln* -p139,445
nmap -p 445 -vv --script=smb-vuln-cve2009-3103.nse,smb-vuln-ms06-025.nse,smb-vuln-ms07-029.nse,smb-vuln-ms08-067.nse,smb-vuln-ms10-054.nse,smb-vuln-ms10-061.nse,smb-vuln-ms17-010.nse 
crackmapexec smb IP -u '' -p '' --shares
```

Check for Null logins

```bash
nmap --script smb-enum-shares -p 139,445 
smbclient -L \\ip\ -N 
smbclient -m=SMB2 -L \\Hostname\ -N
```

Connect to a share with Null session

```bash
smbclient \\IP\$Admin -N 
smbmap -H IP
smbmap -u DoesNotExists -H IP
enum4linux -a IP
```

Impacket Tools

```bash
impacket-smbclient -no-pass IP
impacket-lookupsid domain/username:password@ip
```

Check permissions on a connect share

```bash
smb: \> showacls # enable acl listing
smb: \> dir # list directories with acls
```

Mount share on local machine

```bash
sudo mount -t cifs //10.10.10.134/SHARENAME ~/path/to/mount_directory
```

List share with credentials

```bash
smbmap -u USERNAME -p PASSWORD -d DOMAIN.TLD -H <TARGET-IP>
```

Recursively list all files in share

```bash
smbmap -R -H <TARGET-IP>
smbmap -R Replication -H <TARGET-IP>
```

With smbclient (recurse downloads all files)

```bash
smbclient //<TARGET-IP>/Replication
smb: \> recurse ON
smb: \> prompt OFF
smb: \> mget *
```

Upload / Download specific files

```bash
smbmap -H <TARGET-IP> --download 'Replication\active.htb\ 
smbmap -H <TARGET-IP> --upload test.txt SHARENAME/test.txt 
```

#### NFS - Port 2049

```bash
showmount -e IP 
mount -t nfs -o vers=3 10.1.1.1:/home/ ~/home
mount -t nfs4 -o proto=tcp,port=2049 127.0.0.1:/srv/Share mountpoint
```

#### TFTPD - UDP 69

```bash
tftp client to connect
atftp is a better client 
Can be used to read system files, MSSQL password mdf file
```

## Automation Tools

#### AutoRecon

```bash
autorecon IP
```

#### NmapAutomator

```bash
./NmapAutomator.sh IP All
```

## Finding exploits

```bash
# Search on EDB and searchsploit
# Check each service on CVE details for RCE / LFI / RFI / SQLI issues 
# Google search the with the service banner 
searchsploit apache 2.4.49
searchsploit -x path/to/exploit
```
