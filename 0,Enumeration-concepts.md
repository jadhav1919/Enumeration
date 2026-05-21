
# Enumeration
## 1. What is Enumeration? 

**Enumeration** is the process of **actively connecting** to a target computer or network and **asking specific questions** to get useful information.

> **Think of it like this:**  
> If footprinting is "watching a house from across the street"
>  scanning is "walking around the house to see open windows,"
> enumeration is **knocking on the door and asking who lives there**.

## 2. Why Do Attackers Enumerate?

Attackers enumerate to find:

- **Weak spots** in the system
- **Usernames and passwords** (or places to guess them)
- **Shared folders** they can access
- **Network devices** (routers, printers, servers)

Once they have this information, they can plan their attack.

## 3. Is Enumeration Legal?

- **Without permission:** Usually **illegal**
- **With permission:** Legal for ethical hackers and penetration testers

>  **Always get written authorization before performing enumeration.**

## 4. What Information Can Be Enumerated?

| Category | Specific Information |
|----------|----------------------|
| **Users & Groups** | Usernames, group memberships |
| **Network Resources** | Shared folders, printers, drives |
| **System Details** | Machine names, operating systems, banners |
| **Network Configuration** | Routing tables, audit settings, service settings |
| **Other Details** | SNMP community strings, FQDN names |

## 5. Techniques Used for Enumeration

Here are the **main techniques** explained simply:

### Technique 1: Extract Usernames from Email IDs
- **How:** An email like `john@company.com` suggests a username `john`
- **Why it works:** Many companies use the same format for login names

### Technique 2: Use Default Passwords
- **How:** Check online databases for default passwords on routers, cameras, etc.
- **Why it works:** Many users never change the default password

### Technique 3: Brute Force Active Directory (AD)
- **How:** Try different usernames and watch for different error messages
- **Why it works:** Microsoft Active Directory gives different errors for valid vs invalid users

### Technique 4: DNS Zone Transfer
- **How:** Use commands like `nslookup` or `dig` to copy the DNS server's address book
- **Why it works:** Some DNS servers are **misconfigured** and allow anyone to copy data

### Technique 5: Extract Windows User Groups
- **How:** If the attacker already has a normal user account, they can list group members
- **Why it works:** Regular users can often see group information

### Technique 6: Extract Usernames Using SNMP
- **How:** Guess common SNMP community strings like `public` or `private`
- **Why it works:** Many devices still use default SNMP settings

## 6. Important Ports and Services to Know

> **Quick Reminder:**  
> - **TCP** = Reliable, connection-based (like a phone call)  
> - **UDP** = Faster, no connection (like sending a letter)

### Port 53 - DNS (Domain Name System)
| Detail | Information |
|--------|-------------|
| **Protocol** | TCP & UDP |
| **Service** | DNS Zone Transfer |
| **What it does** | Translates domain names to IP addresses |
| **What attackers do** | Copy the entire DNS database if misconfigured |
| **Tool example** | `nslookup`, `dig` |

### Port 135 - Microsoft RPC
| Detail | Information |
|--------|-------------|
| **Protocol** | TCP & UDP |
| **Service** | RPC Endpoint Mapper |
| **What it does** | Helps programs find each other on Windows |
| **What attackers do** | Send bad messages to cause a crash (DoS attack) |

### Port 137 - NetBIOS Name Service
| Detail | Information |
|--------|-------------|
| **Protocol** | UDP (mostly) |
| **Service** | NBNS / WINS |
| **What it does** | Matches computer names to IP addresses |
| **What attackers do** | First port they attack to map the network |

### Port 139 & 445 - SMB (File Sharing)
| Detail | Information |
|--------|-------------|
| **Protocol** | TCP 139, TCP/UDP 445 |
| **Service** | SMB (Windows file and printer sharing) |
| **What it does** | Allows file sharing between Windows computers |
| **What attackers do** | Create "null sessions" to access files without a password |
| **Risk** | **Very high** - misconfiguration can expose entire file system |

### Port 161 & 162 - SNMP (Network Management)
| Detail | Information |
|--------|-------------|
| **Protocol** | UDP 161 (queries), UDP 162 (traps) |
| **Service** | Simple Network Management Protocol |
| **What it does** | Monitors network devices (routers, printers, servers) |
| **What attackers do** | Guess community strings like `public` to read device info |
| **Information found** | Users, network topology, device configurations |

### Port 389 & 3268 - LDAP (Directory Services)
| Detail | Information |
|--------|-------------|
| **Protocol** | TCP & UDP |
| **Service** | Lightweight Directory Access Protocol |
| **What it does** | Accesses company directories (like Active Directory) |
| **What attackers do** | Query for all users, groups, and computers |
| **Extra** | Port 3268 = Global Catalog (searches entire company) |

### Port 2049 - NFS (Network File System - Linux/Unix)
| Detail | Information |
|--------|-------------|
| **Protocol** | TCP |
| **Service** | Network File System |
| **What it does** | Shares files on Linux/Unix systems |
| **What attackers do** | Mount remote folders if misconfigured |
| **Risk** | Privilege escalation, backdoor injection |

### Port 25 - SMTP (Email)
| Detail | Information |
|--------|-------------|
| **Protocol** | TCP |
| **Service** | Simple Mail Transfer Protocol |
| **What it does** | Sends email across networks |
| **Attackers use these commands** | `VRFY` (verify username), `EXPN` (expand mailing list) |
| **Example** | `VRFY john` - tells if "john" is a valid user |

### Port 22 - SSH/SFTP (Secure Access)
| Detail | Information |
|--------|-------------|
| **Protocol** | TCP |
| **Service** | Secure Shell / Secure FTP |
| **What it does** | Secure remote login and file transfer |
| **What attackers do** | Brute force passwords, enumerate user accounts |

### Port 5060/5061 - SIP (VoIP Phones)
| Detail | Information |
|--------|-------------|
| **Protocol** | TCP & UDP |
| **Service** | Session Initiation Protocol |
| **What it does** | Makes voice and video calls over Internet |
| **What attackers do** | Enumerate phone extensions and user accounts |

### Port 500 - ISAKMP/IKE (VPNs)
| Detail | Information |
|--------|-------------|
| **Protocol** | UDP |
| **Service** | IPsec VPN setup |
| **What it does** | Creates secure VPN connections |
| **What attackers do** | Gather VPN configuration details |

### Other Important Ports
| Port | Protocol | Service | Simple Explanation |
|------|----------|---------|---------------------|
| 20/21 | TCP | FTP | File transfer - attackers grab banners and brute force |
| 23 | TCP | Telnet | Old remote access - sends passwords in clear text! |
| 69 | UDP | TFTP | Simple file transfer - no authentication, attackers upload malware |
| 179 | TCP | BGP | Internet routing - misconfiguration can hijack traffic |


---
