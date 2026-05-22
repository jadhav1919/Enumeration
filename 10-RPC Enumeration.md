# RPC Enumeration

# What is RPC?

RPC stands for:

```text id="x5m2q8"
Remote Procedure Call
```

RPC allows:

* Clients and servers to communicate
* Remote services to execute functions
* Distributed systems to exchange data

---

# Simple Real-Life Understanding

Think like this:

```text id="m7q4v1"
RPC = Asking another computer to perform a task remotely
```

Example:

* Client sends request
* Remote server processes it
* Result is returned

---

# RPC Components

| Component       | Purpose                 |
| --------------- | ----------------------- |
| Client          | Sends request           |
| Server          | Processes request       |
| Stub            | Communication interface |
| Endpoint Mapper | Maps services to ports  |

---

# Important RPC Service

# Portmapper

Portmapper helps clients:

* Discover RPC services
* Find service ports

---

# Default RPC Ports

| Port    | Protocol | Purpose              |
| ------- | -------- | -------------------- |
| 111     | TCP/UDP  | Portmapper / rpcbind |
| Dynamic | TCP/UDP  | RPC services         |

---

# Why Attackers Enumerate RPC

RPC enumeration may reveal:

* Running services
* Network services
* Open ports
* Vulnerable RPC endpoints
* Windows services
* NFS services

---

# RPC Enumeration Workflow

```text id="k3m8q2"
Discover RPC Port 111
        ↓
Identify RPC Services
        ↓
Enumerate RPC Endpoints
        ↓
Identify Running Services
        ↓
Search For Vulnerabilities
```

---

# What Attackers Can Enumerate

Using RPC enumeration attackers may collect:

* RPC services
* Port mappings
* Windows services
* NFS-related services
* Domain information
* Service versions

---

# Nmap RPC Enumeration

# RPC Scan

```bash id="m1q7v4"
nmap -sR <Target-IP>
```

---

# Example

```bash id="x8m3q5"
nmap -sR 192.168.1.40
```

---

# Purpose

Enumerates:

* RPC services
* Registered RPC programs

---

# Aggressive Scan

```bash id="v5q2m8"
nmap -T4 -A <Target-IP>
```

---

# Purpose

Performs:

* Service detection
* Version detection
* OS detection
* RPC identification

---

# Expected RPC Indicators

Possible output:

```text id="p4m8q1"
111/tcp open rpcbind
```

or

```text id="r7v3m1"
rpcinfo service detected
```

---

# RPC Endpoint Enumeration

# Purpose

Retrieves:

* RPC endpoints
* Registered services
* Service mappings

---

# rpcinfo Command

# Basic Syntax

```bash id="n2m6q5"
rpcinfo -p <Target-IP>
```

---

# Example

```bash id="w9m4q2"
rpcinfo -p 192.168.1.40
```

---

# Purpose

Displays:

* RPC programs
* Program versions
* Protocols
* Ports

---

# Example Output

```text id="x1v7m3"
100000  2  tcp 111 portmapper
100003  3  tcp 2049 nfs
```

Meaning:

```text id="q8m2v6"
RPC and NFS services detected
```

---

# NetScanTools Pro RPC Enumeration

# Purpose

GUI-based RPC enumeration tool.

Can identify:

* RPC services
* Open RPC ports
* Portmapper services

---

# Information Gathered

Possible information:

* RPC program numbers
* Service names
* Listening ports
* RPC versions

---

# RPC Services Commonly Found

| Service  | Purpose      |
| -------- | ------------ |
| rpcbind  | Port mapping |
| mountd   | NFS mounting |
| nlockmgr | File locking |
| status   | RPC status   |
| ypserv   | NIS service  |

---

# RPC Enumeration on Windows

RPC may reveal:

* Active Directory services
* SMB-related services
* Domain services
* Microsoft RPC endpoints

---

# RPC Enumeration on Linux

RPC commonly supports:

* NFS
* Network services
* Remote administration

---

# Important Security Risks

Misconfigured RPC services may allow:

* Information leakage
* Remote service discovery
* Attack surface mapping
* Vulnerability discovery

---

# Common RPC Attack Flow

```text id="m6q1v8"
Discover Port 111
        ↓
Identify RPC Services
        ↓
Enumerate Endpoints
        ↓
Map Open Services
        ↓
Search Vulnerabilities
```

---

# Common RPC Enumeration Tools

| Tool             | Purpose             |
| ---------------- | ------------------- |
| rpcinfo          | RPC service listing |
| Nmap             | RPC scanning        |
| NetScanTools Pro | GUI RPC enumeration |
| Wireshark        | RPC packet analysis |

---

# Additional Useful Commands

# UDP RPC Scan

```bash id="t4m9q2"
nmap -sU -p 111 <Target-IP>
```

---

# TCP RPC Scan

```bash id="y7v3m1"
nmap -sT -p 111 <Target-IP>
```

---

# RPC Service Detection

```bash id="k2m8q4"
nmap -sV <Target-IP>
```

