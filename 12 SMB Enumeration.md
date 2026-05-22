# SMB Enumeration

# What is SMB?

SMB stands for:

```text id="x5m2q8"
Server Message Block
```

SMB is used mainly in Windows systems for:

* File sharing
* Printer sharing
* Remote access
* Network communication

---

# Simple Real-Life Understanding

Think like this:

```text id="m7q4v1"
SMB = Windows network file-sharing service
```

Example:

* Accessing shared folders on another computer
* Sharing printers in a network

---

# Default SMB Ports

| Port | Protocol | Purpose                  |
| ---- | -------- | ------------------------ |
| 445  | TCP      | SMB over TCP             |
| 139  | TCP      | NetBIOS Session Service  |
| 137  | UDP      | NetBIOS Name Service     |
| 138  | UDP      | NetBIOS Datagram Service |

---

# Why Attackers Enumerate SMB

SMB enumeration may reveal:

* Shared folders
* User accounts
* Operating system details
* SMB versions
* Domain information
* NetBIOS names
* File shares

---

# SMB Enumeration Workflow

```text id="r8v1m4"
Discover SMB Ports
        ↓
Identify SMB Service
        ↓
Enumerate SMB Versions
        ↓
Gather Shares and Users
        ↓
Collect System Information
```

---

# What Attackers Can Enumerate

Using SMB enumeration attackers may collect:

* Shared directories
* Hostnames
* Usernames
* SMB protocol versions
* OS details
* Domain/workgroup names

---

# Important SMB Enumeration Tools

| Tool       | Purpose             |
| ---------- | ------------------- |
| Nmap       | SMB scanning        |
| enum4linux | SMB enumeration     |
| smbclient  | SMB interaction     |
| SMBMap     | Share enumeration   |
| smbmap     | Permission checking |
| Metasploit | SMB modules         |

---

# Nmap SMB Enumeration

# Scan SMB Port 445

```bash id="w2m6q9"
nmap -p 445 -A <Target-IP>
```

---

# Example

```bash id="k3m8q2"
nmap -p 445 -A 192.168.1.40
```

---

# Purpose

Retrieves:

* SMB service information
* OS details
* NetBIOS information
* SMB scripts output

---

# Expected Result

```text id="m1q7v4"
445/tcp open microsoft-ds
```

Meaning:

```text id="x8m3q5"
SMB service detected
```

---

# Example SMB Details

Possible information:

```text id="v5q2m8"
OS: Windows Server 2019
NetBIOS Name: SERVER2019
```

---

# SMB Protocol Enumeration

# Check SMB Protocols

```bash id="p4m8q1"
nmap -p 445 --script smb-protocols <Target-IP>
```

---

# NetBIOS Enumeration

```bash id="r7v3m1"
nmap -p 139 --script smb-protocols <Target-IP>
```

---

# Purpose

Retrieves:

* Supported SMB versions
* SMB protocol information

---

# Common SMB Versions

| Version | Description           |
| ------- | --------------------- |
| SMBv1   | Old and insecure      |
| SMBv2   | Improved version      |
| SMBv3   | Modern secure version |

---

# Why SMBv1 is Dangerous

SMBv1 is vulnerable to:

* EternalBlue
* Worm attacks
* Remote code execution

---

# enum4linux Tool

# What is enum4linux?

Linux tool used for:

* SMB enumeration
* User enumeration
* Share enumeration

---

# Basic Syntax

```bash id="n2m6q5"
enum4linux <Target-IP>
```

---

# Example

```bash id="w9m4q2"
enum4linux 192.168.1.40
```

---

# Information Gathered

Possible information:

* Users
* Shares
* Groups
* Password policies
* OS information

---

# smbclient Tool

# List Shares

```bash id="x1v7m3"
smbclient -L //<Target-IP>/ -N
```

---

# Example

```bash id="q8m2v6"
smbclient -L //192.168.1.40/ -N
```

---

# Purpose

Lists:

* Shared folders
* Available SMB resources

---

# Connect To Share

```bash id="m6q1v8"
smbclient //<Target-IP>/Shared
```

---

# SMBMap Tool

# Basic Syntax

```bash id="t4m9q2"
smbmap -H <Target-IP>
```

---

# Example

```bash id="y7v3m1"
smbmap -H 192.168.1.40
```

---

# Purpose

Displays:

* SMB shares
* Permissions
* Read/write access

---

# Common SMB NSE Scripts

| NSE Script       | Purpose           |
| ---------------- | ----------------- |
| smb-protocols    | SMB versions      |
| smb-os-discovery | OS information    |
| smb-enum-shares  | Share enumeration |
| smb-enum-users   | User enumeration  |

---

# SMB OS Discovery

```bash id="k2m8q4"
nmap --script smb-os-discovery -p 445 <Target-IP>
```

---

# SMB Share Enumeration

```bash id="p5v1m7"
nmap --script smb-enum-shares -p 445 <Target-IP>
```

---

# SMB User Enumeration

```bash id="r9m3q6"
nmap --script smb-enum-users -p 445 <Target-IP>
```

---

# Important Security Risks

Misconfigured SMB services may allow:

* Anonymous share access
* User enumeration
* SMB relay attacks
* Remote code execution
* Credential theft

---

# Common SMB Attacks

| Attack        | Description          |
| ------------- | -------------------- |
| SMB Relay     | Relay authentication |
| EternalBlue   | SMBv1 exploit        |
| Pass-the-Hash | NTLM hash abuse      |
| Null Session  | Anonymous access     |

---

# Null Session Enumeration

# What is Null Session?

Accessing SMB without credentials.

---

# Example

```bash id="k4m8q1"
smbclient -L //<Target-IP>/ -N
```

---

# Attack Flow

```text id="v2q7m5"
Discover SMB Ports
        ↓
Identify SMB Service
        ↓
Enumerate Shares and Users
        ↓
Identify SMB Version
        ↓
Search For Vulnerabilities
```

---
