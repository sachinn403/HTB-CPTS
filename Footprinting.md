# FOOTPRINTING

## Infrastructure-based Enumeration

### Certificate Transparency

- **[curl -s https://crt.sh/\?q\=<targetdomain>\&output\=json | jq .](https://crt.sh/)**: Certificate transparency.

### FTP

- **[ftp \<FQDN/IP\>](https://linux.die.net/man/1/ftp)**: Interact with the FTP service on the target.
- **[nc -nv \<FQDN/IP\> 21](https://linux.die.net/man/1/nc)**: Interact with the FTP service on the target using Netcat.
- **[telnet \<FQDN/IP\> 21](https://linux.die.net/man/1/telnet)**: Interact with the FTP service on the target using Telnet.
- **[openssl s_client -connect \<FQDN/IP\>:21 -starttls ftp](https://www.openssl.org/docs/manmaster/man1/s_client.html)**: Interact with the FTP service on the target using an encrypted connection.
- **[wget -m --no-passive ftp://anonymous:anonymous@\<target\>](https://www.gnu.org/software/wget/manual/wget.html)**: Download all available files on the FTP server.

### SMB

- **[smbclient -N -L \\\<FQDN/IP\>](https://linux.die.net/man/1/smbclient)**: Null session authentication on SMB.
- **[smbclient \\\<FQDN/IP\>/\<share\>](https://linux.die.net/man/1/smbclient)**: Connect to a specific SMB share.
- **[rpcclient -U "" \<FQDN/IP\>](https://linux.die.net/man/1/rpcclient)**: Interaction with the target using RPC.
- **[samrdump.py \<FQDN/IP\>](https://github.com/SecureAuthCorp/impacket)**: Username enumeration using Impacket scripts.
- **[smbmap -H \<FQDN/IP\>](https://github.com/ShawnDEvans/smbmap)**: Enumerate SMB shares.
- **[crackmapexec smb \<FQDN/IP\> --shares -u '' -p ''](https://github.com/byt3bl33d3r/CrackMapExec)**: Enumerate SMB shares using null session authentication.
- **[enum4linux-ng.py \<FQDN/IP\> -A](https://github.com/cddmp/enum4linux-ng)**: SMB enumeration using enum4linux.

### NFS

- **[showmount -e \<FQDN/IP\>](https://linux.die.net/man/8/showmount)**: Show available NFS shares.
- **[mount -t nfs \<FQDN/IP\>:/\<share\> ./target-NFS/ -o nolock](https://linux.die.net/man/8/mount.nfs)**: Mount the specific NFS share.
- **[umount ./target-NFS](https://linux.die.net/man/8/umount)**: Unmount the specific NFS share.

### DNS

- **[dig ns \<domain.tld\> @\<nameserver\>](https://linux.die.net/man/1/dig)**: NS request to the specific nameserver.
- **[dig any \<domain.tld\> @\<nameserver\>](https://linux.die.net/man/1/dig)**: ANY request to the specific nameserver.
- **[dig axfr \<domain.tld\> @\<nameserver\>](https://linux.die.net/man/1/dig)**: AXFR request to the specific nameserver.

### SMTP

- **[telnet \<FQDN/IP\> 25](https://linux.die.net/man/1/telnet)**: Interact with the SMTP service on the target.

### IMAP/POP3

- **[curl -k 'imaps://\<FQDN/IP\>' --user \<user\>:\<password\>](https://linux.die.net/man/1/curl)**: Log in to the IMAPS service using cURL.
- **[openssl s_client -connect \<FQDN/IP\>:imaps](https://www.openssl.org/docs/manmaster/man1/s_client.html)**: Connect to the IMAPS service.
- **[openssl s_client -connect \<FQDN/IP\>:pop3s](https://www.openssl.org/docs/manmaster/man1/s_client.html)**: Connect to the POP3s service.

### SNMP

- **[snmpwalk -v2c -c \<community string\> \<FQDN/IP\>](https://linux.die.net/man/1/snmpwalk)**: Query OIDs using snmpwalk.
- **[onesixtyone -c community-strings.list \<FQDN/IP\>](https://tools.kali.org/information-gathering/onesixtyone)**: Bruteforce community strings of the SNMP service.
- **[braa \<community string\>@\<FQDN/IP\>:.1.\*](https://github.com/ajinabraham/brut3k1t)**: Bruteforce SNMP service OIDs.

### MySQL

- **[mysql -u \<user\> -p\<password\> -h \<FQDN/IP\>](https://dev.mysql.com/doc/refman/8.0/en/mysql.html)**: Log in to the MySQL server.

### MSSQL

- **[mssqlclient.py \<user\>@\<FQDN/IP\> -windows-auth](https://github.com/SecureAuthCorp/impacket)**: Log in to the MSSQL server using Windows authentication.

### IPMI

- **[msf6 auxiliary(scanner/ipmi/ipmi_version)](https://github.com/rapid7/metasploit-framework)**: IPMI version detection.
- **[msf6 auxiliary(scanner/ipmi/ipmi_dumphashes)](https://github.com/rapid7/metasploit-framework)**: Dump IPMI hashes.

### Linux Remote Management

- **[ssh-audit.py \<FQDN/IP\>](https://github.com/arthepsy/ssh-audit)**: Remote security audit against the SSH service.
- **[ssh \<user\>@\<FQDN/IP\>](https://linux.die.net/man/1/ssh)**: Log in to the SSH server using the SSH client.
- **[ssh -i private.key \<user\>@\<FQDN/IP\>](https://linux.die.net/man/1/ssh)**: Log in to the SSH server using a private key.
- **[ssh \<user\>@\<FQDN/IP\> -o PreferredAuthentications=password](https://linux.die.net/man/5/ssh_config)**: Enforce password-based authentication.

### Windows Remote Management

- **[rdp-sec-check.pl \<FQDN/IP\>](https://github.com/portcullislabs/rdp-sec-check)**: Check the security settings of the RDP service.
- **[xfreerdp /u:\<user\> /p:"\<password\>" /v:\<FQDN/IP\>](https://linux.die.net/man/1/xfreerdp)**: Log in to the RDP server from Linux.
- **[evil-winrm -i \<FQDN/IP\> -u \<user\> -p \<password\>](https://github.com/Hackplayers/evil-winrm)**: Log in to the WinRM server.
- **[wmiexec.py \<user\>:"\<password\>"@\<FQDN/IP\> "\<system command\>"](https://github.com/SecureAuthCorp/impacket)**: Execute command using the WMI service.

### Oracle TNS

- **[./odat.py all -s \<FQDN/IP\>](https://github.com/quentinhardy/odat)**: Perform scans to gather information about Oracle database services.
- **[sqlplus \<user\>/\<pass\>@\<FQDN/IP\>/\<db\>](https://docs.oracle.com/cd/E11882_01/server.112/e16604/start.htm#SQPUG008)**: Log in to the Oracle database.
- **[./odat.py utlfile -s \<FQDN/IP\> -d \<db\> -U \<user\> -P \<pass\> --sysdba --putFile C:\\insert\\path file.txt ./file.txt](https://github.com/quentinhardy/odat)**: Upload a file with Oracle RDBMS.
