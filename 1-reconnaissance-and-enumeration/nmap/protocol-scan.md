# Protocol Scan

### 🔐 Authentication & Identity

#### LDAP (389, 636)

```bash
nmap -p 389,636 --script=ldap* <target>
nmap --script "(ldap*) and not brute" -p 389 <target>
nmap -p 636 --script=ldap-search,ldap-rootdse <target>
```

#### Kerberos (88)

```bash
nmap -p 88 --script=krb5-enum-users --script-args="krb5-enum-users.realm='DOMAIN.LOCAL'" <target>
nmap -p 88 --script=krb5-info <target>
```

#### SMB (139, 445)

```bash
nmap -p 139,445 --script=smb-enum-shares,smb-enum-users,smb-os-discovery,smb-security-mode,smb2-capabilities,smb2-security-mode <target>
nmap --script smb-vuln* -p 445 <target>
nmap -p 445 --script=smb-null-session <target>
```

#### RDP (3389)

```bash
nmap -p 3389 --script=rdp-enum-encryption <target>
nmap -p 3389 --script=rdp-vuln-ms12-020 <target>
nmap -p 3389 --script=rdp-ntlm-info <target>
```

#### WinRM (5985, 5986)

```bash
nmap -p 5985,5986 --script=http-windows-enum <target>
nmap -p 5985,5986 --script=winrm-enum-users <target>
```

### 📱 Network Services

#### FTP (21)

```bash
nmap -p 21 --script=ftp-anon,ftp-bounce,ftp-syst,ftp-vsftpd-backdoor,ftp-proftpd-backdoor,ftp-libopie <target>
```

#### SSH (22)

```bash
nmap -p 22 --script=ssh-hostkey,ssh-auth-methods,sshv1,ssh2-enum-algos,ssh-brute <target>
```

#### Telnet (23)

```bash
nmap -p 23 --script=telnet-encryption,telnet-ntlm-info <target>
```

#### SMTP (25, 465, 587)

```bash
nmap -p 25,465,587 --script=smtp-commands,smtp-enum-users,smtp-open-relay,smtp-ntlm-info <target>
```

#### DNS (53)

```bash
nmap -p 53 --script=dns-zone-transfer,dns-nsid,dns-service-discovery,dns-recursion,dns-cache-snoop,dns-random-srcport <target>
```

#### TFTP (69)

```bash
nmap -sU -p 69 --script=tftp-enum <target>
```

#### POP3 (110, 995)

```bash
nmap -p 110,995 --script=pop3-capabilities,pop3-brute <target>
```

#### IMAP (143, 993)

```bash
nmap -p 143,993 --script=imap-capabilities,imap-brute <target>
```

#### SNMP (161, 162)

```bash
nmap -sU -p 161,162 --script=snmp-info,snmp-interfaces,snmp-processes,snmp-win32-services,snmp-brute,snmp-sysdescr <target>
```

#### R-Services (512, 513, 514)

```bash
nmap -p 512,513,514 --script=rpcinfo <target>
```

#### IPMI (623)

```bash
nmap -p 623 --script=ipmi-version,ipmi-cipher-zero <target>
```

#### RSync (873)

```bash
nmap -p 873 --script=rsync-list-modules <target>
```

#### MSSQL (1433, 1434, 2433)

```bash
nmap -p 1433,1434,2433 --script=ms-sql-info,ms-sql-empty-password,ms-sql-dump-hashes,ms-sql-brute,ms-sql-config <target>
```

#### Oracle TNS (1521)

```bash
nmap -p 1521 --script=oracle-tns-version,oracle-sid-brute <target>
```

#### NFS (2049)

```bash
nmap -p 2049 --script=nfs-ls,nfs-statfs,nfs-showmount,nfs-acls <target>
```

#### MySQL (3306)

```bash
nmap -p 3306 --script=mysql-info,mysql-users,mysql-databases,mysql-empty-password,mysql-query,mysql-brute,mysql-dump-hashes <target>
```

#### PostgreSQL (5432)

```bash
nmap -p 5432 --script=pgsql-brute,pgsql-databases,pgsql-users <target>
nmap -p 5432 --script=pgsql-enum <target>
```

#### PostgreSQL Secure (5433)

```bash
nmap -p 5433 --script=pgsql-info <target>
```

#### NetBIOS (137, 138)

```bash
nmap -p 137,138 --script=nbstat,smb-os-discovery,smb-enum-shares,smb-enum-users <target>
```

#### VNC (5900)

```bash
nmap -p 5900 --script=vnc-info,vnc-title,vnc-brute <target>
```

#### Redis (6379)

```bash
nmap -p 6379 --script=redis-info,redis-brute <target>
```

#### Elasticsearch (9200)

```bash
nmap -p 9200 --script=http-elasticsearch-head,http-title,http-methods,http-headers <target>
```

#### Memcached (11211)

```bash
nmap -p 11211 --script=memcached-info <target>
```

#### RPCBind (111)

```bash
nmap -sU -sT -p 111 --script=rpcinfo <target>
```

#### SIP (5060)

```bash
nmap -sU -p 5060 --script=sip-methods,sip-enum-users <target>
```

#### MQTT (1883)

```bash
nmap -p 1883 --script=mqtt-subscribe,mqtt-connect <target>
```

#### RMI (1099)

```bash
nmap -p 1099 --script=rmi-dumpregistry,rmi-vuln-classloader <target>
```

#### NTP (123)

```bash
nmap -sU -p 123 --script=ntp-info,ntp-monlist <target>
```

#### Docker (2375)

```bash
nmap -p 2375 --script=docker-version <target>
```

#### RabbitMQ (5672)

```bash
nmap -p 5672 --script=rabbitmq-info <target>
```

#### Jenkins (8080)

```bash
nmap -p 8080 --script=http-jenkins-info,http-headers,http-title <target>
# Common Vulnerabilities: Anonymous Access, Script Console Exposure
```

#### AJP (Apache JServ Protocol - 8009)

```bash
nmap -p 8009 --script=ajp-methods,ajp-headers,ajp-auth <target>
# Common Exploit: Ghostcat CVE-2020-1938 (File Inclusion via AJP)
```

#### Kubernetes API Server (6443)

```bash
nmap -p 6443 --script=http-kubernetes-info,http-headers,http-title <target>
# Check for: Unauthorized access, misconfigured kubelet, exposed dashboard
```

#### CouchDB (5984)

```bash
nmap -p 5984 --script=http-couchdb-info,http-title,http-headers <target>
# Common Exploits: CVE-2017-12635 & CVE-2017-12636 (Remote Code Execution)
```

#### VMware (902, 903, 443)

```bash
nmap -p 902,903,443 --script=vmware-version <target>
```

#### TeamViewer (5938)

```bash
nmap -p 5938 --script=teamviewer-info <target>
```

#### Bacula (9101)

```bash
nmap -p 9101 --script=bacula-info <target>
```

#### X11 (6000)

```bash
nmap -p 6000 --script=x11-access <target>
```

#### Web Services (80, 443, 8080, 8443)

```bash
nmap -p 80,443,8080,8443 --script=http-title,http-methods,http-enum,http-headers,http-server-header,http-auth-finder,http-vuln* <target>
```

#### WebDAV (80, 443, 8080)

```bash
nmap -p 80,443,8080 --script=http-webdav-scan <target>
```

#### Apache Hadoop (50070)

```bash
nmap -p 50070 --script=http-hadoop-info <target>
```

#### Tomcat (8080, 8443)

```bash
nmap -p 8080,8443 --script=http-tomcat-manager,http-tomcat-users <target>
```

#### Zookeeper (2181)

```bash
nmap -p 2181 --script=zookeeper-info <target>
```

#### Kafka (9092)

```bash
nmap -p 9092 --script=kafka-info <target>
```

#### Varnish (6081)

```bash
nmap -p 6081 --script=http-headers,http-title <target>
```

### 🧰 Other Useful Nmap Scripts

#### Common Nmap Automation & Misc Scripts

```bash
nmap --script=default,safe <target>
nmap -p- --min-rate=10000 -T4 <target>  # Fast full port scan
nmap -sV --version-all -p <port> <target>  # Aggressive service detection
nmap -sC -sV <target>  # Default scripts and version detection
nmap -Pn -n -sS -p- -T4 <target>  # Stealth SYN scan without DNS resolution
```

#### Brute Force

```bash
nmap -p 21,22,23,25,80,110,143,443,3306,5432,6379,8080 --script brute <target>
```

#### Vulnerability Detection

```bash
nmap --script vuln <target>
nmap -p 80,443 --script=http-vuln* <target>
nmap -p 445 --script=smb-vuln* <target>
```

#### Web Technologies & Frameworks

```bash
nmap -p 80,443 --script=http-headers,http-title,http-methods,http-enum,http-php-version,http-aspnet-debug,http-wordpress-enum,http-drupal-enum <target>
```
