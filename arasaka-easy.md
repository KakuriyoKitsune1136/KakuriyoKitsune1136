---
description: >-
  An easy Cyberpunk themed machine on Hack Smarter labs that I did during a CTF,
  a more thorough explanation will come later on, when I buy the lab for this.
---

# Arasaka (easy)

## Scenario <a href="#user-content-scenario" id="user-content-scenario"></a>

author of the machine/lab: Henry Lever.

#### Starting Credentials <a href="#user-content-starting-credentials" id="user-content-starting-credentials"></a>

faraday:hacksmarter123

#### Objective and Scope <a href="#user-content-objective-and-scope" id="user-content-objective-and-scope"></a>

You are a member of the Hack Smarter Red Team. This penetration test will operate under an assumed breach scenario, starting with valid credentials for a standard domain user, `faraday`.

The primary goal is to simulate a realistic attack, identifying and exploiting vulnerabilities to escalate privileges from a standard user to a Domain Administrator.



A quick CTF with my notes:&#x20;

### Enumeration

nxc ldap hacksmarter.local -u faraday -p hacksmarter123

<figure><img src="https://app.notion.com/p/Arasaka-Easy-1-373fe83a0848800b887cfc3c316d8b08?source=copy_link#373fe83a0848803eab70c70187009bfa" alt=""><figcaption></figcaption></figure>

bloodhound --zip -c All -d hacksmarter.local -u faraday -p 'hacksmarter123' -dc DC01.hacksmarter.local -ns ip addr

<figure><img src=".gitbook/assets/bloodhoumd.webp" alt=""><figcaption></figcaption></figure>

upload time\~ (Meaning we take the information and turn it into a zip file so we can use it to find out more information, and find important users.

<figure><img src=".gitbook/assets/Bloodhound CE.webp" alt=""><figcaption></figcaption></figure>

alt.svc:babygirl1

<figure><img src=".gitbook/assets/BloodyAD.webp" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/BloodyAD Syntax.webp" alt=""><figcaption></figcaption></figure>

we can do remote admin! which means the faraday user is pwnable.

<figure><img src=".gitbook/assets/Faraday.webp" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/UserHash.webp" alt=""><figcaption></figcaption></figure>

yorinobu:newP@ssword2022

<figure><img src=".gitbook/assets/Domain User Password.webp" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/users.webp" alt=""><figcaption></figcaption></figure>

soulkiller.svc has shares!&#x20;

[soulkiller.py](http://soulkiller.py/)



#### Will Finish putting the photos of these at a later date:

local domain hash!

Hash for svc killer.

works.

Emperor Pwned NTDS.dit dumped:

Finished Arasaka.
