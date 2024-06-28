# Command Reference

## Basic Tools

### General

- [**sudo openvpn user.ovpn**](#): **Connect to VPN**
- [**ifconfig/ip a**](#): **Show our IP address**
- [**netstat -rn**](#): **Show networks accessible via the VPN**
- [**ssh user@10.10.10.10**](#): **SSH to a remote server**
- [**ftp 10.129.42.253**](#): **FTP to a remote server**

### tmux

- [**tmux**](#): **Start tmux**
- [**ctrl+b**](#): **tmux: default prefix**
- [**prefix c**](#): **tmux: new window**
- [**prefix 1**](#): **tmux: switch to window (1)**
- [**prefix shift+%**](#): **tmux: split pane vertically**
- [**prefix shift+"**](#): **tmux: split pane horizontally**

### Vim

- [**vim file**](#): **vim: open file with vim**
- [**esc+i**](#): **vim: enter insert mode**
- [**esc**](#): **vim: back to normal mode**
- [**x**](#): **vim: Cut character**
- [**dw**](#): **vim: Cut word**
- [**dd**](#): **vim: Cut full line**
- [**yw**](#): **vim: Copy word**
- [**yy**](#): **vim: Copy full line**
- [**p**](#): **vim: Paste**
- [**:1**](#): **vim: Go to line number 1.**
- [**:w**](#): **vim: Write the file 'i.e. save'**
- [**:q**](#): **vim: Quit**
- [**:q!**](#): **vim: Quit without saving**
- [**:wq**](#): **vim: Write and quit**

### Pentesting

#### Service Scanning

- [**nmap 10.129.42.253**](#): **Run nmap on an IP**
- [**nmap -sV -sC -p- 10.129.42.253**](#): **Run an nmap script scan on an IP**
- [**locate scripts/citrix**](#): **List various available nmap scripts**
- [**nmap --script smb-os-discovery.nse -p445 10.10.10.40**](#): **Run an nmap script on an IP**
- [**netcat 10.10.10.10 22**](#): **Grab banner of an open port**

#### Click to Copy

To enable clickable commands for copying, you can add a bit of JavaScript or use markdown extensions that support clickable text to copy. If you're using markdown in GitHub, you might need to use raw HTML and JavaScript for this functionality.
