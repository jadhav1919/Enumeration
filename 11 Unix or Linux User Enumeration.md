# Unix/Linux User Enumeration

# What is Unix/Linux User Enumeration?

Unix/Linux user enumeration is the process of collecting:

* Logged-in users
* User account information
* Session details
* Login activity

from Unix/Linux systems.

---

# Simple Real-Life Understanding

Think like this:

```text id="x5m2q8"
Checking who is currently using the Linux system
```

or

```text id="m7q4v1"
Viewing all active users and sessions
```

---

# Why Attackers Enumerate Users

User enumeration may reveal:

* Valid usernames
* Active sessions
* Login times
* Hostnames
* User activity

These usernames can later be used for:

* Password attacks
* SSH attacks
* Privilege escalation
* Social engineering

---

# Unix/Linux User Enumeration Workflow

```text id="r8v1m4"
Identify Logged-In Users
        ↓
Collect Session Information
        ↓
Gather User Details
        ↓
Identify Active Accounts
        ↓
Use Information For Further Attacks
```

---

# Important User Enumeration Commands

| Command | Purpose                      |
| ------- | ---------------------------- |
| rusers  | Remote logged-in users       |
| rwho    | Users on local network       |
| finger  | Detailed user information    |
| who     | Current logged-in users      |
| w       | Active sessions and activity |

---

# rusers Command

# What is rusers?

Displays:

* Logged-in users
* Remote machine users
* Local network sessions

---

# Basic Syntax

```bash id="w2m6q9"
/usr/bin/rusers [options] [Host]
```

---

# Simple Usage

```bash id="k3m8q2"
rusers
```

---

# Purpose

Shows:

* Logged-in users
* Host systems
* Active sessions

---

# Important rusers Options

| Option | Purpose                 |
| ------ | ----------------------- |
| `-a`   | Show all users          |
| `-h`   | Sort by host            |
| `-l`   | Long listing            |
| `-u`   | Sort by number of users |
| `-i`   | Sort by idle time       |

---

# Example

```bash id="m1q7v4"
rusers -l
```

---

# Purpose

Displays detailed user session information.

---

# rwho Command

# What is rwho?

Displays:

* Users logged into systems
* Active sessions on local network

---

# Basic Syntax

```bash id="x8m3q5"
rwho
```

---

# Purpose

Shows:

* Username
* Hostname
* Login time
* Session details

---

# Important rwho Option

| Option | Purpose                                |
| ------ | -------------------------------------- |
| `-a`   | Show all users including idle sessions |

---

# Example

```bash id="v5q2m8"
rwho -a
```

---

# finger Command

# What is finger?

Displays detailed information about users.

---

# Information Revealed

Possible information:

* Username
* Real name
* Home directory
* Shell
* Login time
* Idle time
* Office location
* Phone number

---

# Basic Syntax

```bash id="p4m8q1"
finger [user]
```

---

# Example

```bash id="r7v3m1"
finger ubuntu
```

---

# Example Output

```text id="n2m6q5"
Login: ubuntu
Directory: /home/ubuntu
Shell: /bin/bash
```

Meaning:

```text id="w9m4q2"
Detailed user information discovered
```

---

# Important finger Options

| Option | Purpose                 |
| ------ | ----------------------- |
| `-l`   | Long detailed output    |
| `-s`   | Short output            |
| `-p`   | Hide .plan files        |
| `-m`   | Exact username matching |

---

# Long Format Example

```bash id="x1v7m3"
finger -l ubuntu
```

---

# Short Format Example

```bash id="q8m2v6"
finger -s ubuntu
```

---

# Additional Useful Commands

# who Command

```bash id="m6q1v8"
who
```

---

# Purpose

Shows:

* Currently logged-in users

---

# w Command

```bash id="t4m9q2"
w
```

---

# Purpose

Displays:

* Active users
* Running processes
* Login sessions
* System load

---

# Example Output

```text id="y7v3m1"
USER   TTY   FROM   LOGIN@
ubuntu pts/0 192.168.1.14
```

---

# Important Security Risks

User enumeration may help attackers:

* Discover valid usernames
* Identify active users
* Plan password attacks
* Target administrators

---

# Common Attack Flow

```text id="k2m8q4"
Enumerate Logged-In Users
        ↓
Collect User Details
        ↓
Identify Valid Accounts
        ↓
Target Accounts For Attacks
```

---

# Common User Enumeration Tools

| Tool   | Purpose                   |
| ------ | ------------------------- |
| rusers | Remote user listing       |
| rwho   | Network user sessions     |
| finger | Detailed user info        |
| who    | Logged-in users           |
| w      | Active session monitoring |

---
