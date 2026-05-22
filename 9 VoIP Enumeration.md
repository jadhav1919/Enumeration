# VoIP Enumeration

# What is VoIP?

VoIP stands for:

```text id="x5m2q8"
Voice over Internet Protocol
```

VoIP allows:

* Voice calls over IP networks
* Video calls
* Internet telephony communication

instead of traditional telephone systems.

---

# Simple Real-Life Understanding

Think like this:

```text id="m7q4v1"
VoIP = Phone calls through the Internet
```

Instead of normal phone lines:

```text id="r8v1m4"
Calls travel through computer networks
```

---

# Important VoIP Protocol

# SIP

SIP stands for:

```text id="w2m6q9"
Session Initiation Protocol
```

Used for:

* Starting calls
* Managing calls
* Ending calls

---

# Default VoIP/SIP Ports

| Port | Protocol | Purpose    |
| ---- | -------- | ---------- |
| 5060 | UDP/TCP  | SIP        |
| 5061 | TCP      | Secure SIP |
| 2000 | TCP      | SCCP       |
| 2001 | TCP      | SCCP       |

---

# Why Attackers Enumerate VoIP

VoIP enumeration may reveal:

* SIP devices
* VoIP gateways
* PBX systems
* SIP usernames/extensions
* User-Agent information
* VoIP software versions

---

# VoIP Enumeration Workflow

```text id="k3m8q2"
Discover SIP Service
        ↓
Identify VoIP Devices
        ↓
Enumerate Extensions
        ↓
Fingerprint SIP Software
        ↓
Collect VoIP Information
```

---

# What Attackers Can Enumerate

Using VoIP enumeration attackers may collect:

* SIP phones
* PBX servers
* Extensions
* User-Agent details
* VoIP software versions
* Internal communication systems

---

# Important VoIP Enumeration Tools

| Tool       | Purpose              |
| ---------- | -------------------- |
| Svmap      | SIP scanning         |
| Metasploit | SIP enumeration      |
| Nmap       | SIP port scanning    |
| Wireshark  | VoIP packet analysis |

---

# Svmap Tool

# What is Svmap?

Svmap is an open-source SIP scanner used to:

* Identify SIP devices
* Detect PBX servers
* Scan SIP services

---

# Basic Syntax

```bash id="m1q7v4"
svmap <Target-IP>
```

---

# Example

```bash id="x8m3q5"
svmap 192.168.1.0/24
```

---

# Purpose

Scans:

* SIP devices
* VoIP systems
* PBX servers

---

# Example Output

```text id="v5q2m8"
151.50.106.225:5060
DLink VoIP Stack
```

Meaning:

```text id="p4m8q1"
SIP service detected
```

---

# What Svmap Can Do

| Feature          | Purpose               |
| ---------------- | --------------------- |
| SIP discovery    | Find SIP devices      |
| PBX detection    | Identify VoIP servers |
| Port scanning    | Scan SIP ports        |
| Network scanning | Scan large ranges     |

---

# SIP User Enumeration Using Metasploit

# Start Metasploit

```bash id="r7v3m1"
msfconsole
```

---

# Use SIP Enumerator Module

```bash id="n2m6q5"
use auxiliary/scanner/sip/enumerator
```

---

# Show Options

```bash id="w9m4q2"
show options
```

---

# Set Target

```bash id="x1v7m3"
set RHOSTS <Target-IP>
```

---

# Example

```bash id="q8m2v6"
set RHOSTS 192.168.1.0/24
```

---

# Run Enumeration

```bash id="m6q1v8"
run
```

---

# Purpose

Enumerates:

* SIP usernames
* SIP extensions
* VoIP devices

---

# Example Output

```text id="t4m9q2"
SIP/2.0 200 OK
User-Agent: Grandstream
```

Meaning:

```text id="y7v3m1"
Valid SIP device detected
```

---

# VoIP Fingerprinting

# Purpose

Identifies:

* VoIP vendor
* SIP software
* Phone model
* PBX implementation

---

# Possible Vendors

* Cisco
* Grandstream
* Asterisk
* Avaya
* D-Link

---

# Nmap SIP Enumeration

# Scan SIP Ports

```bash id="k2m8q4"
nmap -sU -p 5060 <Target-IP>
```

---

# SIP NSE Script

```bash id="p5v1m7"
nmap --script=sip-methods -sU -p 5060 <Target-IP>
```

---

# Purpose

Retrieves:

* Supported SIP methods

---

# Supported SIP Methods May Include

| Method   | Purpose         |
| -------- | --------------- |
| INVITE   | Start call      |
| ACK      | Acknowledge     |
| BYE      | End call        |
| OPTIONS  | Capabilities    |
| REGISTER | Register client |

---

# Important VoIP Security Risks

Misconfigured VoIP systems may allow:

* Extension enumeration
* Call hijacking
* Caller ID spoofing
* Eavesdropping
* VoIP phishing (Vishing)
* SPIT attacks

---

# What is SPIT?

SPIT stands for:

```text id="r9m3q6"
Spam over Internet Telephony
```

Similar to:

```text id="k4m8q1"
Spam calls in VoIP systems
```

---

# Common VoIP Attacks

| Attack             | Description          |
| ------------------ | -------------------- |
| DoS                | Service disruption   |
| Call Hijacking     | Stealing sessions    |
| Eavesdropping      | Listening to calls   |
| Caller ID Spoofing | Fake caller identity |
| Vishing            | Voice phishing       |

---

# Attack Flow

```text id="v2q7m5"
Discover SIP Service
        ↓
Identify VoIP Devices
        ↓
Enumerate Extensions
        ↓
Fingerprint SIP Software
        ↓
Launch VoIP Attacks
```

---

