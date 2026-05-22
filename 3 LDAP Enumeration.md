# LDAP Enumeration

# What is LDAP?

LDAP stands for:

```text id="v4l9m2"
Lightweight Directory Access Protocol
```

LDAP is used to:

* Access directory services
* Query Active Directory information
* Manage users and systems in a network


# Simple Real-Life Understanding

Think like this:

```text id="m8q1t7"
LDAP = Phonebook of the organization
```

It stores:

* Usernames
* Password policies
* Departments
* Email addresses
* Computers
* Servers
* Groups

# Where LDAP is Commonly Used

LDAP is mainly used in:

* Active Directory (AD)
* Enterprise networks
* Windows domains


# Default LDAP Ports

| Port | Protocol | Purpose             |
| ---- | -------- | ------------------- |
| 389  | TCP      | LDAP                |
| 636  | TCP      | Secure LDAP (LDAPS) |


# Why Attackers Enumerate LDAP

If LDAP allows anonymous access or weak authentication:

```text id="f2x8r5"
Attackers can collect sensitive directory information
```

Possible information:

* Domain names
* User accounts
* Group names
* Organizational units
* Email addresses
* Server names
* Password policies


# LDAP Components

| Component   | Purpose                    |
| ----------- | -------------------------- |
| LDAP Client | Sends queries              |
| LDAP Server | Stores directory data      |
| DSA         | Directory System Agent     |
| DIT         | Directory Information Tree |


# Important LDAP Concepts

# DIT

```text id="q3k7m1"
Directory Information Tree
```

Hierarchical structure of directory data.


# DN

```text id="y9w4c2"
Distinguished Name
```

Unique path of an object.

Example:

```text id="u7v1n6"
CN=Administrator,CN=Users,DC=company,DC=local
```


# DC

```text id="x5r2m8"
Domain Component
```

Example:

```text id="d4p9q7"
DC=company,DC=local
```


# CN

```text id="r8m1t4"
Common Name
```

Represents object name.


# LDAP Enumeration Workflow

```text id="z6n2w5"
Discover LDAP Service
        ↓
Identify LDAP Port
        ↓
Connect to LDAP Server
        ↓
Query Naming Contexts
        ↓
Enumerate Users and Objects
        ↓
Collect Domain Information
```


# What Attackers Can Enumerate

Using LDAP enumeration attackers may collect:

* Domain information
* Usernames
* Departments
* Organizational structure
* Group memberships
* Server details
* Naming contexts
* Password policies

# Manual LDAP Enumeration

# Step 1 — Scan LDAP Ports

Using Nmap:

```bash id="m7q5r2"
nmap -p 389,636 <Target-IP>
```


# Purpose

Checks:

* LDAP service
* Secure LDAP service

# Expected Result

```text id="k2v8m1"
389/tcp open ldap
636/tcp open ldaps
```


# Step 2 — Install ldap3 Library

```bash id="p4w7x9"
pip3 install ldap3
```



# Step 3 — Start Python

```bash id="j6m2r8"
python3
```

# Step 4 — Import ldap3

```python id="z8n5t1"
import ldap3
```


# Step 5 — Create LDAP Server Object

```python id="x1v4m7"
server = ldap3.Server('Target-IP', get_info=ldap3.ALL, port=389)
```


# Purpose

Connects to:

* LDAP server
* Port 389
* Retrieves server information



# Step 6 — Create Connection

```python id="u5q2n9"
connection = ldap3.Connection(server)
```


# Step 7 — Bind Connection

```python id="r3m8x4"
connection.bind()
```

Expected:

```text id="d7v1k5"
True
```

Meaning:

```text id="n4w9m2"
Connection successful
```

# Step 8 — Retrieve Server Information

```python id="y2t7q8"
server.info
```

# Information Gathered

Possible output:

* Domain name
* Naming contexts
* LDAP versions
* Supported controls
* Directory structure

# Step 9 — Enumerate Directory Objects

```python id="m9r4x1"
connection.search(search_base='DC=DOMAIN,DC=LOCAL',
                  search_filter='(objectClass=*)',
                  search_scope='SUBTREE',
                  attributes='*')
```


# Purpose

Retrieves:

* All LDAP objects
* Entire directory tree


# Step 10 — Dump LDAP Entries

```python id="w6n1v3"
connection.entries
```

# Information Retrieved

May include:

* Users
* Groups
* Computers
* Organizational units
* Policies

# LDAP Enumeration Using ldapsearch

# Basic Naming Context Enumeration

```bash id="q8m2r6"
ldapsearch -h <Target-IP> -x -s base namingcontexts
```

# Meaning of Command

| Option           | Meaning                  |
| ---------------- | ------------------------ |
| `-h`             | Target IP                |
| `-x`             | Simple authentication    |
| `-s base`        | Base search              |
| `namingcontexts` | Retrieve naming contexts |

# Example Output

```text id="t4v9n1"
DC=company,DC=local
```

# Enumerate All Objects

```bash id="k7w3m5"
ldapsearch -x -h <Target-IP> -b "DC=company,DC=local" "(objectclass=*)"
```

# Purpose

Retrieves:

* Users
* Groups
* Directory objects

# Enumerate Users

```bash id="c1m8q4"
ldapsearch -x -h <Target-IP> -b "DC=company,DC=local" "(objectClass=user)"
```

# LDAP Enumeration Using Nmap

# LDAP NSE Script

```bash id="v5q7r1"
nmap -p 389 --script ldap-brute <Target-IP>
```

# Purpose

Attempts:

* LDAP authentication enumeration
* Valid credential discovery

# Common LDAP Enumeration Tools

| Tool                        | Purpose                 |
| --------------------------- | ----------------------- |
| ldapsearch                  | LDAP queries            |
| ldap3                       | Python LDAP enumeration |
| Nmap NSE                    | LDAP scanning           |
| Softerra LDAP Administrator | GUI LDAP browser        |

# Important Security Risk

If anonymous LDAP access is enabled:

```text id="n2x5v8"
Attackers can gather Active Directory information without credentials
```
# Attack Flow

```text id="g4m7q1"
Discover LDAP Service
        ↓
Enumerate Naming Contexts
        ↓
Enumerate Users and Groups
        ↓
Collect Domain Information
        ↓
Use Information For Further Attacks
```
