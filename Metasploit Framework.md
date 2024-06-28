# USING THE METASPLOIT FRAMEWORK

## MSFconsole Commands

### General Commands

- **[show exploits](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#show-exploits)**: Show all exploits within the Framework.
- **[show payloads](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#show-payloads)**: Show all payloads within the Framework.
- **[show auxiliary](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#show-auxiliary)**: Show all auxiliary modules within the Framework.
- **[search <name>](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#search-name)**: Search for exploits or modules within the Framework.
- **[info](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#info)**: Load information about a specific exploit or module.

### Module and Exploit Loading

- **[use <name>](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#use-name)**: Load an exploit or module (e.g., `use windows/smb/psexec`).
- **use <number>**: Load an exploit by using the index number displayed after the search command.

### Setting Parameters

- **[set <function>](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#set-function)**: Set a specific value (e.g., LHOST or RHOST).
- **[setg <function>](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#setg-function)**: Set a specific value globally (e.g., LHOST or RHOST).

### Options and Configuration

- **[show options](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#show-options)**: Show the options available for a module or exploit.
- **[show targets](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#show-targets)**: Show the platforms supported by the exploit.
- **[set target <number>](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#set-target-number)**: Specify a specific target index if you know the OS and service pack.
- **[set payload <payload>](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#set-payload-payload)**: Specify the payload to use.
- **set payload <number>**: Specify the payload index number to use after the show payloads command.
- **[show advanced](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#show-advanced)**: Show advanced options.
- **[set autorunscript migrate -f](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#set-autorunscript)**: Automatically migrate to a separate process upon exploit completion.
- **[check](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#check)**: Determine whether a target is vulnerable to an attack.

### Exploitation and Execution

- **[exploit](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#exploit)**: Execute the module or exploit and attack the target.
- **[exploit -j](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#exploit-j)**: Run the exploit in the background.
- **[exploit -z](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#exploit-z)**: Do not interact with the session after successful exploitation.
- **[exploit -e <encoder>](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#exploit-e-encoder)**: Specify the payload encoder to use (e.g., `exploit -e shikata_ga_nai`).

### Session Handling

- **[sessions -l](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#sessions-l)**: List available sessions (used when handling multiple shells).
- **[sessions -l -v](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#sessions-l-v)**: List all available sessions and show verbose fields.
- **[sessions -s <script>](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#sessions-s-script)**: Run a specific Meterpreter script on all Meterpreter live sessions.
- **[sessions -K](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#sessions-k)**: Kill all live sessions.
- **[sessions -c <cmd>](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#sessions-c-cmd)**: Execute a command on all live Meterpreter sessions.
- **[sessions -u <sessionID>](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#sessions-u-sessionid)**: Upgrade a normal Win32 shell to a Meterpreter console.

### Database Operations

- **[db_create <name>](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#db_create-name)**: Create a database for database-driven attacks.
- **[db_connect <name>](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#db_connect-name)**: Create and connect to a database for database-driven attacks.
- **[db_nmap](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#db_nmap)**: Use Nmap and place results in a database.
- **[db_destroy](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfconsole#db_destroy)**: Delete the current database.

## Meterpreter Commands

### General Meterpreter Commands

- **[help](https://github.com/rapid7/metasploit-framework/wiki/Meterpreter-Basic-Usage)**: Open Meterpreter usage help.
- **[run <scriptname>](https://github.com/rapid7/metasploit-framework/wiki/Meterpreter-Basic-Usage#run-scriptname)**: Run Meterpreter-based scripts.

### System and File Operations

- **[sysinfo](https://github.com/rapid7/metasploit-framework/wiki/Meterpreter-Basic-Usage#sysinfo)**: Show system information on the compromised target.
- **[ls](https://github.com/rapid7/metasploit-framework/wiki/Meterpreter-Basic-Usage#ls)**: List the files and folders on the target.
- **[use priv](https://github.com/rapid7/metasploit-framework/wiki/Meterpreter-Basic-Usage#use-priv)**: Load the privilege extension for extended Meterpreter libraries.
- **[ps](https://github.com/rapid7/metasploit-framework/wiki/Meterpreter-Basic-Usage#ps)**: Show all running processes and associated accounts.
- **[migrate <proc. id>](https://github.com/rapid7/metasploit-framework/wiki/Meterpreter-Basic-Usage#migrate-proc-id)**: Migrate to a specific process ID (PID obtained from ps command).
- **[use incognito](https://github.com/rapid7/metasploit-framework/wiki/Meterpreter-Basic-Usage#use-incognito)**: Load incognito functions for token stealing and impersonation.
- **[list_tokens -u](https://github.com/rapid7/metasploit-framework/wiki/Meterpreter-Basic-Usage#list_tokens-u)**: List available tokens on the target by user.
- **[list_tokens -g](https://github.com/rapid7/metasploit-framework/wiki/Meterpreter-Basic-Usage#list_tokens-g)**: List available tokens on the target by group.
- **[impersonate_token <DOMAIN_NAME\\USERNAME>](https://github.com/rapid7/metasploit-framework/wiki/Meterpreter-Basic-Usage#impersonate_token-domain_nameusername)**: Impersonate a token available on the target.
- **[steal_token <proc. id>](https://github.com/rapid7/metasploit-framework/wiki/Meterpreter-Basic-Usage#steal_token-proc-id)**: Steal and impersonate tokens for a given process.
- **[drop_token](https://github.com/rapid7/metasploit-framework/wiki/Meterpreter-Basic-Usage#drop_token)**: Stop impersonating the current token.
- **[getsystem](https://github.com/rapid7/metasploit-framework/wiki/Meterpreter-Basic-Usage#getsystem)**: Attempt to elevate permissions to SYSTEM-level access.
- **[shell](https://github.com/rapid7/metasploit-framework/wiki/Meterpreter-Basic-Usage#shell)**: Drop into an interactive shell with all available tokens.
- **[execute -f <cmd.exe> -i](https://github.com/rapid7/metasploit-framework/wiki/Meterpreter-Basic-Usage#execute-f-cmdexe-i)**: Execute cmd.exe and interact with it.
- **[execute -f <cmd.exe> -i
