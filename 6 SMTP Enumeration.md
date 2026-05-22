# SMTP Enumeration

# What is SMTP?

SMTP stands for:

```text id="x5m2q8"
Simple Mail Transfer Protocol
```

It is used for:

* Sending emails
* Relaying mail between servers
* Mail communication over networks

---

# Simple Real-Life Understanding

Think like this:

```text id="r8v1m4"
SMTP = Post office of the internet
```

It transfers emails from:

* Sender
* To recipient

through mail servers.

---

# Common Mail Protocols

| Protocol | Purpose          |
| -------- | ---------------- |
| SMTP     | Sending emails   |
| POP3     | Receiving emails |
| IMAP     | Managing emails  |

---

# Default SMTP Ports

| Port | Protocol | Purpose    |
| ---- | -------- | ---------- |
| 25   | TCP      | SMTP       |
| 465  | TCP      | SMTPS      |
| 587  | TCP      | Submission |

---

# Why Attackers Enumerate SMTP

SMTP servers may reveal:

* Valid usernames
* Email addresses
* Mail server information
* Internal users
* Delivery addresses

---

# SMTP Enumeration Workflow

```text id="m4q7v2"
Discover SMTP Service
        ↓
Connect to SMTP Server
        ↓
Use SMTP Commands
        ↓
Enumerate Valid Users
        ↓
Collect Email Information
```

---

# Important SMTP Commands

| Command   | Purpose              |
| --------- | -------------------- |
| VRFY      | Verify usernames     |
| EXPN      | Expand mailing lists |
| RCPT TO   | Validate recipients  |
| HELO/EHLO | Identify client      |

---

# SMTP VRFY Command

# Purpose

Checks whether a username exists on the server.

---

# Manual SMTP Enumeration

# Connect Using Telnet

```bash id="n7m2q5"
telnet <Target-IP> 25
```

---

# Example

```bash id="x3v8m1"
telnet 192.168.1.40 25
```

---

# SMTP Banner

Example:

```text id="q8m4v2"
220 mailserver ESMTP
```

Meaning:

```text id="r5n1m7"
SMTP service detected
```

---

# Introduce Client

```text id="w9m2q4"
HELO test
```

---

# Verify User

```text id="p6v1m8"
VRFY administrator
```

---

# Possible Responses

## Valid User

```text id="t4m7q2"
250 User exists
```

---

## Invalid User

```text id="k8v2m5"
550 User unknown
```

---

# SMTP EXPN Command

# Purpose

Expands mailing lists and aliases.

---

# Example

```text id="x1m9q4"
EXPN admin
```

---

# RCPT TO Command

# Purpose

Checks if recipient mailbox exists.

---

# Example

```text id="r7v3m1"
MAIL FROM:test@test.com
RCPT TO:admin
```

---

# Valid User Response

```text id="n2m8q5"
250 Recipient OK
```

---

# Invalid User Response

```text id="w5v1m7"
550 User unknown
```

---

# SMTP Enumeration Using Nmap

# Scan SMTP Ports

```bash id="m9q4v1"
nmap -p 25,465,587 <Target-IP>
```

---

# Expected Result

```text id="j7m2q8"
25/tcp open smtp
```

---

# SMTP Commands NSE Script

```bash id="q4v8m2"
nmap -p 25 --script=smtp-commands <Target-IP>
```

---

# Purpose

Lists:

* Supported SMTP commands
* Mail server capabilities

---

# SMTP Open Relay Check

```bash id="x6m1q9"
nmap -p 25 --script=smtp-open-relay <Target-IP>
```

---

# Purpose

Checks whether SMTP relay is misconfigured.

---

# SMTP User Enumeration

```bash id="r8v3m4"
nmap -p 25 --script=smtp-enum-users <Target-IP>
```

---

# Purpose

Enumerates:

* Valid SMTP users

---

# SMTP Enumeration Using Metasploit

# Start Metasploit

```bash id="k5m2q7"
msfconsole
```

---

# Use SMTP Enumeration Module

```bash id="v1q8m3"
use auxiliary/scanner/smtp/smtp_enum
```

---

# Show Options

```bash id="n6m4q2"
show options
```

---

# Set Target IP

```bash id="x9v1m5"
set RHOSTS <Target-IP>
```

---

# Run Enumeration

```bash id="p3m7q8"
run
```

---

# Purpose

Enumerates:

* SMTP users
* Valid accounts

using SMTP VRFY/EXPN/RCPT commands.

---

# smtp-user-enum Tool

# Basic Syntax

```bash id="w4q8m1"
smtp-user-enum -M VRFY -u admin -t <Target-IP>
```

---

# Purpose

Checks:

* Whether username exists

---

# Important smtp-user-enum Options

| Option | Purpose         |
| ------ | --------------- |
| `-M`   | SMTP method     |
| `-u`   | Single username |
| `-U`   | User list       |
| `-t`   | Target IP       |
| `-p`   | SMTP port       |
| `-v`   | Verbose         |

---

# Example Using User List

```bash id="m2v7q4"
smtp-user-enum -M VRFY -U users.txt -t 192.168.1.40
```

---

# Common SMTP Enumeration Tools

| Tool             | Purpose            |
| ---------------- | ------------------ |
| Telnet           | Manual enumeration |
| Nmap             | SMTP scanning      |
| Metasploit       | User enumeration   |
| smtp-user-enum   | Username discovery |
| NetScanTools Pro | GUI SMTP testing   |

---

# Important Security Risks

Misconfigured SMTP servers may allow:

* User enumeration
* Open mail relays
* Internal email discovery
* Information leakage

---

# Open Relay Risk

If SMTP relay is open:

```text id="g7m1q5"
Attackers can send spam emails through the server
```

---

# Attack Flow

```text id="y4m8q2"
Discover SMTP Service
        ↓
Connect to Mail Server
        ↓
Use VRFY/EXPN/RCPT Commands
        ↓
Enumerate Valid Users
        ↓
Collect Email Information
```
