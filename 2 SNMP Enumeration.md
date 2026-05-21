# SNMP Enumeration
## What is SNMP?
SNMP stands for: Simple Network Management Protocol
It is used by administrators to:
* Monitor network devices
* Manage routers/switches
* Check system status remotely
SNMP works mainly on: UDP Port 161

# Simple Real-Life Understanding

Think like this: SNMP = Remote Control + Information Center for network devices
Using SNMP, administrators can remotely see:

* Device name
* System information
* Running services
* Installed software
* Network interfaces
* Users
* RAM
* Routing tables
* Traffic statistics

# Why Attackers Like SNMP

Many devices use:

```text
public
private
```

as default community strings (passwords).

If administrators forget to change them:

* Attackers can collect sensitive information
* Sometimes attackers can modify configurations

# SNMP Components

## 1. SNMP Manager

The controlling system.

Example:

```text
Administrator machine
```

## 2. SNMP Agent

Runs on target device.

Example:

```text
Router
Windows Server
Switch
Printer
Linux Machine
```

# SNMP Community Strings

These are like passwords.

## Read Community String

Usually:

```text
public
```

Allows:

* Viewing information
* Enumeration

## Read/Write Community String

Usually:

```text
private
```

Allows:

* Changing configurations
* Editing values

Very dangerous if exposed.

# What Attackers Can Enumerate

Using SNMP attackers may collect:

* Hostname
* OS version
* Running processes
* Installed software
* User accounts
* Network interfaces
* Routing tables
* ARP tables
* Open ports
* System uptime
* RAM information

# Working of SNMP

## Step 1 Device Starts
SNMP agent starts on target device.
Usually listens on: UDP 161
## Step 2 Discovery
Manager searches for SNMP-enabled devices.
## Step 3 Information Exchange
Manager sends requests.
Agent replies with information.
# Important SNMP Requests

## Get Request

Gets one value.

Example: System name

## GetNext Request

Gets next available value in database.
Used for walking through information.

## Set Request
Changes values on device.
Dangerous if write access exists.

## Trap

Device automatically sends alerts.
Example:

* Device reboot
* Interface down

# MIB (Management Information Base)

## What is MIB?

MIB is: Database of SNMP information
Contains all manageable objects.

# OID (Object Identifier)

Every SNMP value has unique ID.
Example: 1.3.6.1.2.1
This is called OID.

# Important Enumeration Tools
## 1. SnmpWalk
Most common SNMP enumeration tool.

## Basic Command

```bash id="zxyvtm"
snmpwalk -v1 -c public <Target-IP>
```

### Meaning

| Part          | Meaning          |
| ------------- | ---------------- |
| `-v1`         | SNMP Version 1   |
| `-c public`   | Community string |
| `<Target-IP>` | Victim machine   |

---

# What SnmpWalk Does

It walks through the MIB database and retrieves information.

Can reveal:

* OS details
* Users
* Processes
* Interfaces
* Services
* RAM
* Hostname

---

# Useful SnmpWalk Commands

## SNMPv2 Enumeration

```bash id="pq6t95"
snmpwalk -v2c -c public <Target-IP>
```

---

## Installed Software

```bash id="qlpccm"
snmpwalk -v2c -c public <Target-IP> hrSWInstalledName
```

---

## RAM Information

```bash id="3a8mow"
snmpwalk -v2c -c public <Target-IP> hrMemorySize
```

---

# SNMP Enumeration Using Nmap

Nmap has NSE scripts for SNMP.

---

## Running Processes

```bash id="u4tn4r"
nmap -sU -p 161 --script=snmp-processes <Target-IP>
```

Gets:

* Running processes
* Process paths

## System Information

```bash id="tmr8fr"
nmap -sU -p 161 --script=snmp-sysdescr <Target-IP>
```

Gets:

* OS details
* Device information


## Installed Applications

```bash id="d88q64"
nmap -sU -p 161 --script=snmp-win32-software <Target-IP>
```

Gets:

* Installed software list


# snmp-check Tool

Very powerful enumeration tool.

## Command

```bash id="c9b9fd"
snmp-check <Target-IP>
```

# Information Gathered

* Hostname
* OS version
* Users
* Network interfaces
* TCP connections
* Routing information
* Uptime
* Processes

# SoftPerfect Network Scanner

GUI-based network scanner.

Can:

* Scan devices
* Discover shares
* Detect SNMP services
* Gather network information

# Common SNMP Ports

| Port | Protocol | Purpose      |
| ---- | -------- | ------------ |
| 161  | UDP      | SNMP Queries |
| 162  | UDP      | SNMP Traps   |


# Important Exam/Interview Points

## SNMP Uses UDP

```text
UDP 161
```


## Default Community Strings

```text
public
private
```


## SNMP Enumeration Goal

Collect:

* Users
* Processes
* Device information
* Network details

# Simple Flow of SNMP Enumeration

```text
Attacker
   ↓
Checks UDP 161
   ↓
Tries community string
   ↓
Queries SNMP agent
   ↓
Retrieves system/network information
```

# Very Important Security Point

If: public/private
community strings remain enabled,
attackers may gain huge information about the network.
Sometimes configuration modification also becomes possible.
