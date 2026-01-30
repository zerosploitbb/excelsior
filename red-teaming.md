---
layout: default
title: Red Teaming Commands
---

# Red Teaming Command Reference

Essential commands red teamers should know by heart.

## Table of Contents
- [Reconnaissance](#reconnaissance)
- [Network Discovery](#network-discovery)
- [Exploitation](#exploitation)
- [Privilege Escalation](#privilege-escalation)
- [Lateral Movement](#lateral-movement)
- [Persistence](#persistence)

## Reconnaissance

### Network Discovery
```bash
nmap -sn 192.168.1.0/24              # Ping sweep
nmap -sV -sC -p- <target>            # Service/version detection, all ports
nmap -sU -p 161,162 <target>         # UDP scan
```

### DNS Enumeration
```bash
dig @<dns-server> <domain> ANY       # All DNS records
nslookup -type=mx <domain>           # Mail servers
host -t ns <domain>                  # Name servers
dnsenum <domain>                     # Automated DNS enumeration
```

### Web Enumeration
```bash
gobuster dir -u http://<target> -w /path/to/wordlist
dirb http://<target>
nikto -h http://<target>
```

[Continue with full red teaming content...]

---
[Back to Home](/)
