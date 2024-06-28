# FOOTPRINTING

## Infrastructure-based Enumeration

### Certificate Transparency

- **curl -s https://crt.sh/\?q\=<targetdomain>\&output\=json | jq .**: Certificate transparency.

### FTP

- **ftp \<FQDN/IP\>**: Interact with the FTP service on the target.
- **nc -nv \<FQDN/IP\> 21**: Interact with the FTP service on the target using Netcat.
- **telnet \<FQDN/IP\> 21**: Interact with the FTP service on the target using Telnet.
- **openssl s_client -connect \<FQDN/IP\>:21 -starttls ftp**: Interact with the FTP service on the target using an encrypted connection.
- **wget -m --no-passive ftp://anonymous:anonymous@\<target\>**: Download all available files on the FTP server.

### SMB

- **smbclient -N -L \\\<FQDN/IP\>**: Null session authentication on SMB.
- **smbclient \\\<FQDN/IP\>/\<share\>**: Connect to a specific SMB share.
- **rpcclient -U "" \<FQDN/IP\>**: Interaction with the target using RPC.
- **samrdump.py \<FQDN/IP\>**: Username enumeration using Impacket scripts.
- **smbmap -H \<FQDN/IP\>**: Enumerate SMB shares.
- **crackmapexec smb \<FQDN/IP\> --shares -u '' -p ''**: Enumerate SMB shares using null session authentication.
- **enum4linux-ng.py \<FQDN/IP\> -A**: SMB enumeration using enum4linux.

### NFS

- **showmount -e \<FQDN/IP\>**: Show available NFS shares.
- **mount -t nfs \<FQDN/IP\>:/\<share\> ./target-NFS/ -o nolock**: Mount the specific NFS share.
- **umount ./target-NFS**: Unmount the specific NFS share.

### DNS

- **dig ns \<domain.tld\> @\<nameserver\>**: NS request to the specific nameserver.
- **dig any \<domain.tld\> @\<nameserver\>**: ANY request to the specific nameserver.
- **dig axfr \<domain.tld\> @\<nameserver\>**: AXFR request to the specific nameserver.

### SMTP

- **telnet \<FQDN/IP\> 25**: Interact with the SMTP service on the target.

### IMAP/POP3

- **curl -k 'imaps://\<FQDN/IP\>' --user \<user\>:\<password\>**: Log in to the IMAPS service using cURL.
- **openssl s_client -connect \<FQDN/IP\>:imaps**: Connect to the IMAPS service.
- **openssl s_client -connect \<FQDN/IP\>:pop3s**: Connect to the POP3s service.

### SNMP

- **snmpwalk -v2c -c \<community string\> \<FQDN/IP\>**: Query OIDs using snmpwalk.
- **onesixtyone -c community-strings.list \<FQDN/IP\>**: Bruteforce community strings of the SNMP service.
- **braa \<community string\>@\<FQDN/IP\>:.1.\***: Bruteforce SNMP service OIDs.

### MySQL

- **mysql -u \<user\> -p\<password\> -h \<FQDN/IP\>**: Log in to the MySQL server.

### MSSQL

- **mssqlclient.py \<user\>@\<FQDN/IP\> -windows-auth**: Log in to the MSSQL server using Windows authentication.

### IPMI

- **msf6 auxiliary(scanner/ipmi/ipmi_version)**: IPMI version detection.
- **msf6 auxiliary(scanner/ipmi/ipmi_dumphashes)**: Dump IPMI hashes.

### Linux Remote Management

- **ssh-audit.py \<FQDN/IP\>**: Remote security audit against the SSH service.
- **ssh \<user\>@\<FQDN/IP\>**: Log in to the SSH server using the SSH client.
- **ssh -i private.key \<user\>@\<FQDN/IP\>**: Log in to the SSH server using a private key.
- **ssh \<user\>@\<FQDN/IP\> -o PreferredAuthentications=password**: Enforce password-based authentication.

### Windows Remote Management

- **rdp-sec-check.pl \<FQDN/IP\>**: Check the security settings of the RDP service.
- **xfreerdp /u:\<user\> /p:"\<password\>" /v:\<FQDN/IP\>**: Log in to the RDP server from Linux.
- **evil-winrm -i \<FQDN/IP\> -u \<user\> -p \<password\>**: Log in to the WinRM server.
- **wmiexec.py \<user\>:"\<password\>"@\<FQDN/IP\> "\<system command\>"**: Execute command using the WMI service.

### Oracle TNS

- **./odat.py all -s \<FQDN/IP\>**: Perform scans to gather information about Oracle database services.
- **sqlplus \<user\>/\<pass\>@\<FQDN/IP\>/\<db\>**: Log in to the Oracle database.
- **./odat.py utlfile -s \<FQDN/IP\> -d \<db\> -U \<user\> -P \<pass\> --sysdba --putFile C:\\insert\\path file.txt ./file.txt**: Upload a file with Oracle RDBMS.
