
### What is Brute Forcing?

A trial-and-error method used to crack passwords, login credentials, or encryption keys by systematically trying every possible combination of characters.

### Factors Influencing Brute Force Attacks

- Complexity of the password or key
- Computational power available to the attacker
- Security measures in place

### How Brute Forcing Works

1. **Start**: The attacker initiates the brute force process.
2. **Generate Possible Combination**: The software generates a potential password or key combination.
3. **Apply Combination**: The generated combination is attempted against the target system.
4. **Check if Successful**: The system evaluates the attempted combination.
5. **Access Granted (if successful)**: The attacker gains unauthorized access.
6. **End (if unsuccessful)**: The process repeats until the correct combination is found or the attacker gives up.

### Types of Brute Forcing

|Attack Type|Description|Best Used When|
|---|---|---|
|Simple Brute Force|Tries every possible character combination in a set.|No prior information about the password.|
|Dictionary Attack|Uses a pre-compiled list of common passwords.|The password is likely weak or common.|
|Hybrid Attack|Combines brute force and dictionary attacks.|Target uses modified common passwords.|
|Credential Stuffing|Uses leaked credentials from other breaches.|Target may reuse passwords.|
|Password Spraying|Attempts common passwords across many accounts.|Account lockout policies are in place.|
|Rainbow Table Attack|Uses precomputed tables of password hashes.|Cracking a large number of password hashes.|
|Reverse Brute Force|Targets a known password against multiple usernames.|Password reuse is suspected.|
|Distributed Brute Force|Distributes attempts across multiple machines.|Password is complex, and one machine isn't enough.|

### Default Credentials

|Device|Username|Password|
|---|---|---|
|Linksys Router|admin|admin|
|Netgear Router|admin|password|
|TP-Link Router|admin|admin|
|Cisco Router|cisco|cisco|
|Ubiquiti UniFi AP|ubnt|ubnt|

### Brute-Forcing Tools

#### Hydra

- Fast network login cracker.
- Supports numerous protocols.
- Uses parallel connections for speed.
- Flexible and adaptable.

```bash
hydra [-l LOGIN|-L FILE] [-p PASS|-P FILE] [-C FILE] -m MODULE [service://server[:PORT][/OPT]]
```

**Examples:**

```bash
hydra -l admin -P /path/to/password_list.txt ftp://192.168.1.100
hydra -l root -P /path/to/password_list.txt ssh://192.168.1.100
hydra -l admin -P /path/to/password_list.txt 127.0.0.1 http-post-form "/login.php:user=^USER^&pass=^PASS^:F=incorrect"
```

#### Medusa

- Fast, massively parallel, modular login brute-forcer.
- Supports a wide array of services.

```bash
medusa [-h host|-H file] [-u username|-U file] [-p password|-P file] [-C file] -M module [OPT]
```

**Examples:**

```bash
medusa -h 192.168.1.100 -u admin -P passwords.txt -M ssh
medusa -h 192.168.1.100 -U users.txt -P passwords.txt -M ftp -t 5
medusa -h 192.168.1.100 -u admin -P passwords.txt -M rdp
```

### Custom Wordlists

#### Username Anarchy

```bash
username-anarchy Jane Smith
username-anarchy -i names.txt
username-anarchy -a --country us
username-anarchy -l
username-anarchy -f format1,format2
username-anarchy -@ example.com
username-anarchy --case-insensitive
```

#### CUPP (Common User Passwords Profiler)

```bash
cupp -i
cupp -w profiles.txt
cupp -l
```

### Password Policy Filtering

|Policy Requirement|Grep Regex Pattern|Explanation|
|---|---|---|
|Minimum Length (8 characters)|grep -E '^.{8,}$' wordlist.txt|At least 8 characters long.|
|At Least One Uppercase Letter|grep -E '[A-Z]' wordlist.txt|Contains uppercase letters.|
|At Least One Lowercase Letter|grep -E '[a-z]' wordlist.txt|Contains lowercase letters.|
|At Least One Digit|grep -E '[0-9]' wordlist.txt|Contains digits.|
|At Least One Special Character|grep -E '[!@#$%^&*()_+-=[]{};':",.<>/?]' wordlist.txt|Contains special characters.|
|No Consecutive Repeated Characters|grep -E '(.)\1' wordlist.txt|Avoids repeated characters.|
|Exclude Common Patterns|grep -v -i 'password' wordlist.txt|Excludes common patterns.|
|Exclude Dictionary Words|grep -v -f dictionary.txt wordlist.txt|Excludes dictionary words.|
|Combination of Requirements|grep -E '^.{8,}$' wordlist.txt|grep -E '[A-Z]'|
