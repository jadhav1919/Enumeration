# IPsec Enumeration

# What is IPsec?

IPsec stands for:

```text id="x5m2q8"
Internet Protocol Security
```

It is used to:

* Secure network communication
* Create VPN tunnels
* Encrypt traffic between systems

---

# Simple Real-Life Understanding

Think like this:

```text id="m7q4v1"
IPsec = Secure encrypted tunnel between networks
```

Used in:

* Site-to-site VPNs
* Remote access VPNs
* Enterprise secure communication

---

# Main IPsec Components

| Component | Purpose                         |
| --------- | ------------------------------- |
| AH        | Authentication Header           |
| ESP       | Encapsulating Security Payload  |
| IKE       | Internet Key Exchange           |
| ISAKMP    | Security Association management |

---

# What is IKE?

IKE stands for:

```text id="r8v1m4"
Internet Key Exchange
```

Used to:

* Exchange encryption keys
* Negotiate VPN settings
* Establish secure tunnels

---

# What is ISAKMP?

ISAKMP stands for:

```text id="w2m6q9"
Internet Security Association and Key Management Protocol
```

Used for:

* Creating Security Associations (SA)
* Managing VPN negotiations

---

# Important IPsec Ports

| Port | Protocol | Purpose       |
| ---- | -------- | ------------- |
| 500  | UDP      | ISAKMP / IKE  |
| 4500 | UDP      | NAT Traversal |

---

# Why Attackers Enumerate IPsec

IPsec enumeration may reveal:

* VPN gateways
* Encryption algorithms
* Hashing algorithms
* Authentication methods
* VPN device information
* VPN usernames
* Security Association lifetime

---

# IPsec Enumeration Workflow

```text id="k3m8q2"
Discover UDP Port 500
        ↓
Identify ISAKMP Service
        ↓
Fingerprint VPN Gateway
        ↓
Enumerate IKE Transforms
        ↓
Collect VPN Information
```

---

# Nmap IPsec Enumeration

# Scan UDP Port 500

```bash id="m1q7v4"
nmap -sU -p 500 <Target-IP>
```

---

# Example

```bash id="x8m3q5"
nmap -sU -p 500 192.168.1.40
```

---

# Expected Result

```text id="v5q2m8"
500/udp open isakmp
```

Meaning:

```text id="p4m8q1"
VPN gateway detected
```

---

# What Nmap Reveals

Possible information:

* ISAKMP availability
* VPN presence
* Open UDP 500 service

---

# ike-scan Tool

# What is ike-scan?

Tool used to:

* Discover IKE hosts
* Fingerprint VPN gateways
* Enumerate VPN configurations

---

# Basic Syntax

```bash id="r7v3m1"
ike-scan -M <Target-IP>
```

---

# Example

```bash id="n2m6q5"
ike-scan -M 192.168.1.40
```

---

# Purpose

Discovers:

* IKE-enabled devices
* VPN gateways

---

# Example Output

```text id="w9m4q2"
HDR=(CKY-R=xxxx)
```

Meaning:

```text id="x1v7m3"
Target responds to IKE requests
```

---

# ike-scan Enumeration Capabilities

| Capability            | Purpose                     |
| --------------------- | --------------------------- |
| Discovery             | Detect VPN gateways         |
| Fingerprinting        | Identify VPN implementation |
| Transform Enumeration | Identify algorithms         |
| User Enumeration      | Discover usernames          |
| PSK Cracking Support  | Assist password attacks     |

---

# Fingerprinting

# Purpose

Identifies:

* VPN vendor
* Device type
* Software version

---

# Example Information Revealed

Possible findings:

* Cisco VPN
* SonicWall
* Fortinet
* Check Point
* Palo Alto

---

# Transform Enumeration

# Purpose

Retrieves supported:

* Encryption algorithms
* Hash algorithms
* Authentication methods

---

# Common Algorithms Found

| Type           | Example        |
| -------------- | -------------- |
| Encryption     | AES, 3DES      |
| Hashing        | SHA1, MD5      |
| Authentication | Pre-shared key |

---

# User Enumeration

Some VPN systems may reveal:

* Valid usernames
* Group names

through IKE responses.

---

# Pre-Shared Key (PSK) Cracking

If weak PSK authentication exists:

```text id="q8m2v6"
Offline dictionary attacks may be possible
```

---

# Important Security Risks

Misconfigured VPN gateways may allow:

* VPN fingerprinting
* Username enumeration
* Weak encryption discovery
* PSK cracking attacks

---

# Attack Flow

```text id="m6q1v8"
Discover UDP 500
        ↓
Identify ISAKMP/IKE
        ↓
Fingerprint VPN Device
        ↓
Enumerate Transforms
        ↓
Attempt Authentication Attacks
```

---

# Additional Useful Commands

# Aggressive Mode Scan

```bash id="t4m9q2"
ike-scan -A <Target-IP>
```

---

# Fingerprint VPN Vendor

```bash id="y7v3m1"
ike-scan -M --showbackoff <Target-IP>
```

---

# Save Hashes For Cracking

```bash id="k2m8q4"
ike-scan -A -P hashes.txt <Target-IP>
```

---

# Common IPsec Enumeration Tools

| Tool       | Purpose               |
| ---------- | --------------------- |
| Nmap       | Port scanning         |
| ike-scan   | IKE enumeration       |
| Wireshark  | Packet analysis       |
| Metasploit | VPN auxiliary modules |

---
