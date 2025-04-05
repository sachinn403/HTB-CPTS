*To check which shell is present in the system* 
```shell
cat /etc/shells
```

bash
```shell
/bin/bash -i
```

sh
```shell
/bin/sh -i
```

python 
```shell
python -c 'import pty; pty.spwan("/bin/bash")'
```

Perl
```shell
perl -e 'exec "bin/bash";'
```

Ruby
```shell
ruby: exe "bin/bash"
```

Perl
```shell
perl: exec "bin/bash";
```

Lua
```shell
lua: os.execute('/bin/sh')
```

awk
```sh
awk 'BEGIN{system("/bin/sh")}'
```

Find
```sh
find / -name {name of file} -exec /bin/awk 'BEGIN{system("/bin/sh")}'
```

### using Exec to launch the shell

```sh
find . -exec /bin/sh \; -quit
```

### vim
``
```sh
vim -c ';!/bin/sh'
```

Vim Escape

```sh
vim
:set shell=/bin/sh
:shell
```

permission
```shell
ls -la <path/to/file or binary>
```

# Stabilize Shell 


Steps to Stabilize Your Shell

1. Upgrade to an Interactive Shell
```shell
python3 -c 'import pty;pty.spawn("/bin/bash")'
````
If `python3` is unavailable, try:
```shell
python -c 'import pty;pty.spawn("/bin/bash")'
```
This gives you job control and allows using built-in commands like `su`.

2. Set Terminal Type
```shell
export TERM=xterm
```
This ensures compatibility with commands like `clear` and `vim`.

3. Background the Shell Press:
```sh
Ctrl + Z
```
This suspends the session and returns control to your local shell.

4. Modify Terminal Settings on Your Local Machine
```shell
stty raw -echo; fg
```
- `stty raw -echo` disables local echo and allows features like **Tab autocompletion, arrow keys, and Ctrl + C**.
- `fg` brings the background shell back to the foreground.

5. Adjust Terminal Size (Optional)
```shell
stty rows 38 columns 116
```
This ensures proper formatting for commands like `vim` or `less`.
Bonus: Enable a Full TTY Shell If the above steps aren’t enough, try:
```shell
script /dev/null -c bash
```

or

```shell
reset
```
This may further improve terminal capabilities.
