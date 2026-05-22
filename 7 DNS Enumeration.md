# DNS Enumeration

# What is DNS?

DNS stands for:

```text id="x5m2q8"
Domain Name System
```

DNS converts:

```text id="m7q4v1"
Domain Names → IP Addresses
```

Example:

```text id="r8v1m4"
google.com → 142.250.x.x
```



# Simple Real-Life Understanding

Think like this:

```text id="w2m6q9"
DNS = Phonebook of the Internet
```

Instead of remembering IP addresses, users use domain names.



# Default DNS Port

| Port | Protocol |
| ---- | -------- |
| 53   | TCP/UDP  |


# Why Attackers Enumerate DNS

DNS may reveal:

* Subdomains
* Internal IP addresses
* Mail servers
* Name servers
* Network structure
* Hidden hosts


# DNS Enumeration Workflow

```text id="k3m8q2"
Discover DNS Server
        ↓
Query DNS Records
        ↓
Enumerate Subdomains
        ↓
Attempt Zone Transfer
        ↓
Collect Network Information
```



# Important DNS Records

| Record | Purpose            |
| ------ | ------------------ |
| A      | Domain → IPv4      |
| AAAA   | Domain → IPv6      |
| MX     | Mail server        |
| NS     | Name server        |
| TXT    | Text information   |
| CNAME  | Alias              |
| PTR    | Reverse lookup     |
| SOA    | Start of authority |



# What Attackers Can Enumerate

Using DNS enumeration attackers may collect:

* Subdomains
* Hostnames
* Mail servers
* Internal IPs
* DNS servers
* Network architecture


# Basic DNS Enumeration Using dig

# Query DNS Information

```bash id="m1q7v4"
dig <Target-Domain>
```


# Example

```bash id="x8m3q5"
dig google.com
```


# Purpose

Retrieves:

* DNS records
* IP addresses
* Name servers



# DNS Zone Transfer

# What is Zone Transfer?

DNS zone transfer copies DNS records from:

```text id="v5q2m8"
Primary DNS Server → Secondary DNS Server
```


# Security Risk

If misconfigured:

```text id="p4m8q1"
Attackers may retrieve all DNS records
```

# Zone Transfer Workflow

```text id="r7v3m1"
Find Name Servers
        ↓
Attempt AXFR Request
        ↓
Retrieve DNS Records
```


# Step 1 — Find Name Servers

```bash id="n2m6q5"
dig ns <Target-Domain>
```



# Example

```bash id="w9m4q2"
dig ns example.com
```



# Step 2 — Attempt Zone Transfer

```bash id="x1v7m3"
dig @<Name-Server> <Target-Domain> axfr
```


# Example

```bash id="q8m2v6"
dig @ns1.example.com example.com axfr
```



# Successful Zone Transfer May Reveal

* Subdomains
* Hostnames
* Internal systems
* Mail servers
* IP addresses



# nslookup Enumeration

# Start nslookup

```bash id="m6q1v8"
nslookup
```


# Query SOA Record

```text id="t4m9q2"
set querytype=soa
example.com
```



# Purpose

Retrieves:

* Primary DNS server
* Administrative information



# Attempt Zone Transfer

```text id="y7v3m1"
ls -d example.com
```


# DNSRecon Tool

# Zone Transfer Enumeration

```bash id="k2m8q4"
dnsrecon -t axfr -d <Target-Domain>
```


# Example

```bash id="p5v1m7"
dnsrecon -t axfr -d example.com
```



# Purpose

Checks:

* Zone transfer vulnerability



# DNS Cache Snooping

# What is DNS Cache Snooping?

Technique used to determine:

```text id="v8m4q1"
Whether a DNS record exists in cache
```


# Non-Recursive Method

```bash id="x4q9m2"
dig @<DNS-IP> <Target-Domain> A +norecurse
```

# Purpose

Checks:

* Cached DNS records


# Recursive Method

```bash id="r1m7v5"
dig @<DNS-IP> <Target-Domain> A +recurse
```


# TTL Analysis

TTL values help determine:

* Cached records
* Recently visited domains


# DNSSEC Zone Walking

# What is DNSSEC?

DNSSEC stands for:

```text id="m3q8v2"
Domain Name System Security Extensions
```

Adds:

* Authentication
* Integrity protection

to DNS.


# What is Zone Walking?

Technique to enumerate:

* DNS records
* Internal subdomains

through DNSSEC misconfiguration.


# DNSSEC Enumeration Tools

| Tool     | Purpose            |
| -------- | ------------------ |
| LDNS     | DNSSEC enumeration |
| DNSRecon | Zone walking       |
| Nmap NSE | DNSSEC enumeration |


# LDNS Enumeration

```bash id="w5m2q8"
ldns-walk @<DNS-IP> <Target-Domain>
```



# Example

```bash id="q7v1m4"
ldns-walk @8.8.8.8 nl.netlabs.nl
```


# DNSRecon Zone Walking

```bash id="r9m3q6"
dnsrecon -d <Target-Domain> -z
```



# OWASP Amass

# What is Amass?

OWASP Amass is used for:

* Subdomain enumeration
* Attack surface mapping
* DNS intelligence gathering


# Basic Enumeration

```bash id="k4m8q1"
amass enum -d <Target-Domain>
```


# Example

```bash id="v2q7m5"
amass enum -d example.com
```


# Passive Enumeration

```bash id="m8v1q3"
amass enum --passive -d <Target-Domain> -src
```

# Active Enumeration

```bash id="x6m2q9"
amass enum --active -d <Target-Domain> -brute
```

# Information Gathered By Amass

* Subdomains
* IP addresses
* SSL certificates
* APIs
* Network ranges


# DNS Enumeration Using Nmap

# DNS Service Discovery

```bash id="n5m1q8"
nmap --script=broadcast-dns-service-discovery
```


# DNS Brute Force

```bash id="w3q7m2"
nmap -p 53 --script dns-brute <Target-Domain>
```

# Purpose

Enumerates:

* Subdomains
* Associated IP addresses


# DNS Recursion Check

```bash id="r6m9q1"
nmap -Pn -sU -p 53 --script=dns-recursion <Target-IP>
```

# DNSSEC Enumeration

```bash id="p2v8m4"
nmap -sU -p 53 --script dns-nsec-enum <Target-IP>
```


# Additional DNS Enumeration Tools

| Tool        | Purpose                |
| ----------- | ---------------------- |
| DNSRecon    | DNS enumeration        |
| Amass       | Attack surface mapping |
| Knock       | Subdomain enumeration  |
| Subfinder   | Passive enumeration    |
| Turbolist3r | Subdomain discovery    |
| Nmap        | DNS scanning           |

# Common DNS Attack Flow

```text id="g7m1q5"
Discover DNS Server
        ↓
Query DNS Records
        ↓
Find Name Servers
        ↓
Attempt Zone Transfer
        ↓
Enumerate Subdomains
        ↓
Map Target Network
```

# Important Security Risks

Misconfigured DNS may allow:

* Zone transfer attacks
* Internal network disclosure
* Subdomain enumeration
* DNS cache snooping
* DNSSEC zone walking

---
