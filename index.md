---
layout: default
---

<style>
body {
  max-width: 900px;
  margin: 40px auto;
  padding: 0 20px;
  font-family: -apple-system, sans-serif;
  line-height: 1.6;
  color: #333;
  background: #fff;
}

h1 {
  border-bottom: 3px solid #000;
  padding-bottom: 10px;
}

details {
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 10px;
  margin: 15px 0;
}

summary {
  font-weight: bold;
  cursor: pointer;
  padding: 10px;
  font-size: 1.2em;
}

summary:hover {
  background: #f5f5f5;
}

pre {
  background: #f5f5f5;
  padding: 15px;
  border-left: 3px solid #000;
  overflow-x: auto;
}

code {
  font-family: monospace;
  font-size: 0.9em;
}
</style>

# Pentesting Notes

<details>
<summary>Reconnaissance</summary>
```bash
nmap -sn 192.168.1.0/24
nmap -sV -sC -p- <target>
```

</details>

<details>
<summary>Web Application Testing</summary>
```bash
# SQL Injection
sqlmap -u "http://target.com/page?id=1" --dbs

# XSS (escaped)
<script>alert(1)</script>
<img src=x onerror=alert(1)>
```

</details>

<details>
<summary>Privilege Escalation</summary>
```bash
# Linux SUID
find / -perm -u=s -type f 2>/dev/null

# Sudo
sudo -l
```

</details>
