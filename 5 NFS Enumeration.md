# NFS Enumeration

# What is NFS?

NFS stands for:

```text id="q7m2v4"
Network File System
```

It is a file-sharing protocol used mainly in:

* Linux
* Unix systems

NFS allows systems to:

* Access remote files
* Read shared directories
* Write files remotely

---

# Simple Real-Life Understanding

Think like this:

```text id="m4v8q1"
NFS = Shared network folder for Linux systems
```

Example:

* One Ubuntu machine shares a folder
* Another Linux machine accesses it remotely

---

# How NFS Works

NFS works using:

```text id="x2n6m9"
Remote Procedure Call (RPC)
```

The NFS server exports directories.

Clients then:

```text id="r5m1q7"
mount
```

those shared directories remotely.

---

# Important File in NFS

```text id="v9q3m2"
/etc/exports
```

Contains:

* Shared directories
* Allowed client IP addresses
* Permissions

---

# Default NFS Ports

| Port | Protocol | Purpose |
| ---- | -------- | ------- |
| 111  | TCP/UDP  | RPCBind |
| 2049 | TCP/UDP  | NFS     |

---

# Why Attackers Enumerate NFS

If NFS is misconfigured:

```text id="p8m4q6"
Attackers may access sensitive shared files remotely
```

Possible risks:

* Sensitive data exposure
* Writable shares
* File theft
* Unauthorized access
* Privilege escalation

---

# NFS Enumeration Workflow

```text id="k1v7m3"
Discover RPC Services
        ↓
Identify NFS Port 2049
        ↓
Enumerate Shared Directories
        ↓
Mount NFS Share
        ↓
Access Shared Files
```

---

# What Attackers Can Enumerate

Using NFS enumeration attackers may collect:

* Shared directories
* User files
* Backup files
* Configuration files
* Writable shares
* Internal network information

---

# Important Enumeration Tools

| Tool      | Purpose                |
| --------- | ---------------------- |
| rpcinfo   | Enumerate RPC services |
| showmount | List NFS shares        |
| nmap      | Scan NFS ports         |
| RPCScan   | RPC enumeration        |
| SuperEnum | Automated enumeration  |

---

# rpcinfo Command

# Basic Syntax

```bash id="t4m8q2"
rpcinfo -p <Target-IP>
```

---

# Example

```bash id="w7n1m5"
rpcinfo -p 192.168.1.40
```

---

# Purpose

Lists:

* RPC services
* Port mappings
* NFS services

---

# Example Output

```text id="j3m9q6"
2049/tcp open nfs
```

Meaning:

```text id="n6v2m8"
NFS service detected
```

---

# showmount Command

# Basic Syntax

```bash id="x5m2q9"
showmount -e <Target-IP>
```

---

# Example

```bash id="q8v4m1"
showmount -e 192.168.1.40
```

---

# Purpose

Displays:

* Exported NFS shares
* Shared directories

---

# Example Output

```text id="r2m7q4"
/home/shared
```

Meaning:

```text id="y4v8m2"
Remote shared directory discovered
```

---

# Mounting NFS Share

# Create Mount Directory

```bash id="m1q5v7"
sudo mkdir /mnt/nfs
```

---

# Mount Remote Share

```bash id="p6m2q8"
sudo mount -t nfs 192.168.1.40:/home/shared /mnt/nfs
```

---

# Purpose

Mounts remote NFS share locally.

---

# Access Shared Files

```bash id="v3q9m1"
cd /mnt/nfs
ls -la
```

---

# Nmap NFS Enumeration

# Scan NFS Ports

```bash id="k7m1q5"
nmap -p 111,2049 <Target-IP>
```

---

# Purpose

Checks:

* RPCBind
* NFS service

---

# Expected Result

```text id="x8v4m2"
111/tcp open rpcbind
2049/tcp open nfs
```

---

# Nmap NSE Script

```bash id="j9m3q7"
nmap --script=nfs-showmount <Target-IP>
```

---

# Purpose

Retrieves:

* NFS exported shares

---

# Additional NSE Scripts

| NSE Script    | Purpose                |
| ------------- | ---------------------- |
| nfs-showmount | List shares            |
| nfs-ls        | List files             |
| nfs-statfs    | File system statistics |

---

# RPCScan Tool

# Command

```bash id="w5q2m9"
python3 rpc-scan.py <Target-IP> --rpc
```

---

# Purpose

Enumerates:

* RPC services
* NFS-related services
* Misconfigurations

---

# SuperEnum Tool

# Run Tool

```bash id="r8m4q1"
./superenum
```

---

# Purpose

Automated enumeration of:

* Open ports
* NFS services
* Shares

---

# Important Security Risks

Misconfigured NFS may allow:

* Anonymous access
* Writable remote shares
* Sensitive file disclosure
* Remote privilege escalation

---

# Common NFS Attack Flow

```text id="g2m8q5"
Discover RPCBind
        ↓
Identify NFS Service
        ↓
Enumerate Shares
        ↓
Mount Remote Share
        ↓
Access Sensitive Files
```
