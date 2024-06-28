# INFORMATION GATHERING - WEB EDITION
## WHOIS

- **[export TARGET="domain.tld"]**: Assign target to an environment variable.
- **[whois $TARGET](https://linux.die.net/man/1/whois)**: WHOIS lookup for the target domain.

## DNS Enumeration

- **[nslookup $TARGET](https://linux.die.net/man/1/nslookup)**: Identify the A record for the target domain.
- **[nslookup -query=A $TARGET](https://linux.die.net/man/1/nslookup)**: Identify the A record for the target domain.
- **[dig $TARGET @<nameserver/IP>](https://linux.die.net/man/1/dig)**: Identify the A record for the target domain.
- **[dig a $TARGET @<nameserver/IP>](https://linux.die.net/man/1/dig)**: Identify the A record for the target domain.
- **[nslookup -query=PTR <IP>](https://linux.die.net/man/1/nslookup)**: Identify the PTR record for the target IP address.
- **[dig -x <IP> @<nameserver/IP>](https://linux.die.net/man/1/dig)**: Identify the PTR record for the target IP address.
- **[nslookup -query=ANY $TARGET](https://linux.die.net/man/1/nslookup)**: Identify ANY records for the target domain.
- **[dig any $TARGET @<nameserver/IP>](https://linux.die.net/man/1/dig)**: Identify ANY records for the target domain.

## INFORMATION GATHERING - WEB EDITION

- **[nslookup -query=TXT $TARGET](https://linux.die.net/man/1/nslookup)**: Identify the TXT records for the target domain.
- **[dig txt $TARGET @<nameserver/IP>](https://linux.die.net/man/1/dig)**: Identify the TXT records for the target domain.
- **[nslookup -query=MX $TARGET](https://linux.die.net/man/1/nslookup)**: Identify the MX records for the target domain.
- **[dig mx $TARGET @<nameserver/IP>](https://linux.die.net/man/1/dig)**: Identify the MX records for the target domain.

## Passive Subdomain Enumeration

- **[VirusTotal](https://www.virustotal.com/gui/home/url)**: Check subdomains for a given domain.
- **[Censys](https://censys.io/)**: Discover subdomains using Censys.
- **[Crt.sh](https://crt.sh/)**: Certificate transparency.
- **[curl -s https://sonar.omnisint.io/subdomains/{domain} \| jq -r '.[]' \| sort -u](https://sonar.omnisint.io/)**: All subdomains for a given domain.
- **[curl -s https://sonar.omnisint.io/tlds/{domain} \| jq -r '.[]' \| sort -u](https://sonar.omnisint.io/)**: All TLDs found for a given domain.
- **[curl -s https://sonar.omnisint.io/all/{domain} \| jq -r '.[]' \| sort -u](https://sonar.omnisint.io/)**: All results across all TLDs for a given domain.
- **[curl -s https://sonar.omnisint.io/reverse/{ip} \| jq -r '.[]' \| sort -u](https://sonar.omnisint.io/)**: Reverse DNS lookup on IP address.
- **[curl -s https://sonar.omnisint.io/reverse/{ip}/{mask} \| jq -r '.[]' \| sort -u](https://sonar.omnisint.io/)**: Reverse DNS lookup of a CIDR range.
- **[curl -s "https://crt.sh/?q=${TARGET}&output=json" \| jq -r '.[] | "\(.name_value)\n\(.common_name)"' \| sort -u](https://crt.sh/)**: Certificate Transparency.
- **[cat sources.txt \| while read source; do theHarvester -d "${TARGET}" -b $source -f "${source}-${TARGET}";done](https://github.com/laramies/theHarvester)**: Searching for subdomains and other information from various sources.

## Passive Infrastructure Identification

- **[Netcraft](https://www.netcraft.com/)**: Discover infrastructure information.
- **[WayBackMachine](http://web.archive.org/)**: Retrieve historical snapshots of websites.
- **[WayBackURLs](https://github.com/tomnomnom/waybackurls)**: Crawling URLs from a domain with timestamps.

## Active Infrastructure Identification

- **[curl -I "http://${TARGET}"](https://linux.die.net/man/1/curl)**: Display HTTP headers of the target webserver.
- **[whatweb -a https://www.facebook.com -v](https://github.com/urbanadventurer/WhatWeb)**: Technology identification.
- **[Wappalyzer](https://www.wappalyzer.com/)**: Identify technologies used on websites.
- **[wafw00f -v https://$TARGET](https://github.com/EnableSecurity/wafw00f)**: WAF fingerprinting.
- **[Aquatone](https://github.com/michenriksen/aquatone)**: Capture screenshots and gather information.

## Active Subdomain Enumeration

- **[HackerTarget](https://hackertarget.com/zone-transfer/)**: Perform zone transfer using Nslookup.
- **[SecLists](https://github.com/danielmiessler/SecLists)**: Use SecLists for subdomain brute-forcing.
- **[gobuster dns -q -r "${NS}" -d "${TARGET}" -w "${WORDLIST}" -p ./patterns.txt -o "gobuster_${TARGET}.txt"](https://github.com/OJ/gobuster)**: Bruteforce subdomains.
- **[curl -s http://192.168.10.10 -H "Host: randomtarget.com"](https://linux.die.net/man/1/curl)**: Changing the HOST HTTP header.
- **[cat ./vhosts.list \| while read vhost;do echo "\n********\nFUZZING: ${vhost}\n********";curl -s -I http://<IP address> -H "HOST: ${vhost}.target.domain" | grep "Content-Length: ";done](https://linux.die.net/man/1/curl)**: Bruteforce virtual hosts on the target domain.
- **[ffuf -w ./vhosts -u http://<IP address> -H "HOST: FUZZ.target.domain" -fs 612](https://github.com/ffuf/ffuf)**: Bruteforce virtual hosts using ffuf.

## Crawling Resources

- **[ZAP](https://www.zaproxy.org/)**: Web application security scanner.
- **[ffuf -recursion -recursion-depth 1 -u http://192.168.10.10/FUZZ -w /opt/useful/SecLists/Discovery/Web-Content/raft-small-directories-lowercase.txt](https://github.com/ffuf/ffuf)**: Discovering files and folders.
- **[ffuf -w ./folders.txt:FOLDERS,./wordlist.txt:WORDLIST,./extensions.txt:EXTENSIONS -u http://www.target.domain/FOLDERS/WORDLISTEXTENSIONS](https://github.com/ffuf/ffuf)**: Mutated bruteforcing against the target web server.
