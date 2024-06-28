# Nmap Scanning Options Cheat Sheet

## Target Specification
- [**10.10.10.0/24**](#): Target network range.
- [**-sn**](#): Disables port scanning.
- [**-Pn**](#): Disables ICMP Echo Requests.
- [**-n**](#): Disables DNS Resolution.
- [**-PE**](#): Performs a ping scan using ICMP Echo Requests.
- [**--packet-trace**](#): Shows all packets sent and received.
- [**--reason**](#): Displays the reason for a specific result.
- [**--disable-arpping**](#): Disables ARP Ping Requests.
- [**--top-ports=<num>**](#): Scans the specified top ports defined as most frequent.
- [**-p-**](#): Scan all ports.
- [**-p22-110**](#): Scan ports between 22 and 110.

## Network Enumeration with Nmap

### Basic Scan Types
- [**-p22,25**](#): Scans only ports 22 and 25.
- [**-F**](#): Scans top 100 ports.
- [**-sS**](#): Performs a TCP SYN-Scan.
- [**-sA**](#): Performs a TCP ACK-Scan.
- [**-sU**](#): Performs an UDP Scan.
- [**-sV**](#): Scans discovered services for their versions.
- [**-sC**](#): Performs a Script Scan with default scripts.
- [**--script <script>**](#): Performs a Script Scan using specified scripts.
- [**-O**](#): Performs an OS Detection Scan.
- [**-A**](#): Performs OS Detection, Service Detection, and traceroute.

### Advanced Options
- [**-D RND:5**](#): Sets number of random Decoys used in scan.
- [**-e**](#): Specifies the network interface for the scan.
- [**-S 10.10.10.200**](#): Specifies source IP address for the scan.
- [**-g**](#): Specifies source port for the scan.
- [**--dns-server <ns>**](#): Performs DNS resolution using specified name server.

## Output Options
- [**-oA filename**](#): Stores results in all available formats with filename.
- [**-oN filename**](#): Stores results in normal format with filename.
- [**-oG filename**](#): Stores results in "grepable" format with filename.
- [**-oX filename**](#): Stores results in XML format with filename.

## Performance Options
- [**--max-retries <num>**](#): Sets number of retries for specific port scans.
- [**--stats-every=5s**](#): Displays scan status every 5 seconds.
- [**-v/-vv**](#): Displays verbose output during scan.
- [**--initial-rtt-timeout 50ms**](#): Sets initial RTT timeout.
- [**--max-rtt-timeout 100ms**](#): Sets maximum RTT timeout.
- [**--min-rate 300**](#): Sets number of packets sent simultaneously.
- [**-T <0-5>**](#): Specifies specific timing template.
