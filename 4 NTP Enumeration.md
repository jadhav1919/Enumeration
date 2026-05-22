# NTP Enumeration

# What is NTP?

NTP stands for:

```text id="x7m2q4"
Network Time Protocol
```

It is used to:

* Synchronize system clocks
* Maintain accurate network time
* Keep servers and clients using same time

---

# Simple Real-Life Understanding

Think like this:

```text id="r5v8m1"
NTP = Central clock server for the network
```

All systems ask the NTP server:

```text id="w2n6q9"
"What is the correct current time?"
```

---

# Default NTP Port

| Port | Protocol |
| ---- | -------- |
| 123  | UDP      |

---

# Why Attackers Enumerate NTP

Improperly configured NTP servers may reveal:

* Connected hosts
* Internal IP addresses
* Hostnames
* Network topology
* Time synchronization sources

---

# NTP Enumeration Workflow

```text id="m8q3v1"
Discover UDP 123
        ↓
Identify NTP Service
        ↓
Query NTP Server
        ↓
Collect Time and Peer Information
        ↓
Map Internal Network
```

---

# What Attackers Can Enumerate

Using NTP enumeration attackers may collect:

* Connected clients
* Internal IP addresses
* NTP peers
* Hostnames
* Operating systems
* Synchronization sources

---

# Important NTP Tools

| Tool     | Purpose                        |
| -------- | ------------------------------ |
| ntpdate  | Query NTP server               |
| ntptrace | Trace NTP hierarchy            |
| ntpdc    | Query ntpd daemon              |
| ntpq     | Query NTP peers and statistics |
| nmap     | NTP service discovery          |

---

# Nmap NTP Enumeration

# Scan UDP Port 123

```bash id="k3m8q1"
nmap -sU -p 123 <Target-IP>
```

---

# Expected Result

```text id="v7n2m5"
123/udp open ntp
```

Meaning:

```text id="r4m9q2"
NTP service detected
```

---

# Nmap NTP NSE Script

```bash id="x5q1m8"
nmap -sU -p 123 --script ntp-info <Target-IP>
```

---

# Purpose

Retrieves:

* NTP version
* System time
* Synchronization information

---

# ntpdate Command

# Basic Syntax

```bash id="n6v2m4"
ntpdate <Target-IP>
```

---

# Example

```bash id="p1m8q7"
ntpdate 192.168.1.40
```

---

# Purpose

Queries the NTP server and retrieves:

* Time information
* Offset
* Delay
* Synchronization details

---

# Important ntpdate Options

| Option | Purpose           |
| ------ | ----------------- |
| `-d`   | Debug mode        |
| `-q`   | Query only        |
| `-p`   | Number of samples |
| `-t`   | Timeout           |
| `-v`   | Verbose output    |

---

# Query Only Mode

```bash id="y4m7q2"
ntpdate -q <Target-IP>
```

---

# Purpose

Queries server without changing system time.

---

# Debug Mode

```bash id="j8v1m5"
ntpdate -d <Target-IP>
```

---

# Purpose

Shows detailed debugging information.

---

# ntptrace Command

# Basic Syntax

```bash id="w2q6m8"
ntptrace <Target-IP>
```

---

# Purpose

Traces:

* NTP synchronization chain
* Primary time source

---

# Example Output

```text id="g5m2v9"
localhost: stratum 4
10.10.1.1: stratum 1
```

Meaning:

```text id="t7q4m1"
Target synchronizes time from another NTP source
```

---

# Important ntptrace Options

| Option | Purpose             |
| ------ | ------------------- |
| `-n`   | Numeric IP output   |
| `-m`   | Maximum trace depth |

---

# ntpdc Command

# Basic Syntax

```bash id="v3m8q5"
ntpdc <Target-IP>
```

---

# Purpose

Queries the:

```text id="m1q7v4"
ntpd daemon
```

and retrieves:

* Peer information
* Statistics
* Server state

---

# Useful ntpdc Commands

| Command  | Purpose            |
| -------- | ------------------ |
| peers    | Show peers         |
| sysstats | System statistics  |
| version  | NTP version        |
| help     | Available commands |

---

# ntpq Command

# Basic Syntax

```bash id="x9m4q1"
ntpq <Target-IP>
```

---

# Purpose

Monitors:

* NTP daemon operations
* Performance
* Peers
* Associations

---

# Useful ntpq Commands

| Command      | Purpose      |
| ------------ | ------------ |
| peers        | Show peers   |
| associations | Associations |
| version      | Version      |
| host         | Current host |
| sysstats     | Statistics   |

---

# Example

```bash id="r6v2m7"
ntpq -p <Target-IP>
```

---

# Purpose

Displays:

* NTP peers
* Delay
* Offset
* Synchronization status

---

# Important NTP Security Risks

Misconfigured NTP servers may allow:

* Internal network disclosure
* Reflection/amplification attacks
* Host discovery
* Information leakage

---

# NTP Reflection Attack

Attackers may abuse NTP for:

```text id="z8m3q6"
DDoS amplification attacks
```

because NTP responses can be much larger than requests.

---

# Attack Flow

```text id="y1q7m4"
Discover UDP 123
        ↓
Identify NTP Service
        ↓
Query NTP Information
        ↓
Enumerate Peers and Clients
        ↓
Collect Internal Network Data
```

---

# Common NTP Enumeration Tools

| Tool      | Purpose             |
| --------- | ------------------- |
| ntpdate   | Query time server   |
| ntptrace  | Trace NTP hierarchy |
| ntpq      | Peer enumeration    |
| ntpdc     | Daemon statistics   |
| Wireshark | Packet analysis     |
| Nmap      | Service detection   |
