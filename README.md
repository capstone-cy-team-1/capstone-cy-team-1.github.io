# CY Capstone Project By Team 1

## Project 

This project is intended to develop an application and apply tools to map a cyber incident and then use the Caldera tool to complete an emulation plan. Included into team's tasks is the deployment in the Cloud of a mock-up scenario that represents the system compromised in the cyberincident studied. 

As a result of the project, with the Adversary Emulation Plan is needed to elaborate Threat Report of the incident analized (including a STIX2.1 JSON representation). 

You can find the 
1. Presentation docs here: [Docs](https://github.com/capstone-cy-team-1/capstone-cy-team-1.github.io/tree/main/public)
2. Organization housing all the repositories: [Capstone-cy-team-1](https://github.com/capstone-cy-team-1/)
3. Scrum Board here: [Team-1 Scrum Board](https://github.com/orgs/capstone-cy-team-1/projects/1)

> As a team we understood, the flaws within our system, as it had to be made this way for the project.  However, for the purposes of the assignment we were tasked with performing a security analysis of our own systems. [Find the detialed report here](https://github.com/capstone-cy-team-1/capstone-cy-team-1.github.io/blob/main/public/Submitted-docs/Security%20Analysis%20.pdf)

> You can also find a [threat model report for the project here](https://github.com/capstone-cy-team-1/capstone-cy-team-1.github.io/blob/main/public/Submitted-docs/Threat%20Modeling%20Report.pdf)

## Proposal 

Vulnerability: Supply Chain Attack(s)
Idea: Build an infrastructure for an organization that heavily relies on a JavaScript environment. This environment will be utilized for implementing the Dependency Confusion attack using custom scripts and the Caldera tool. [You can read the doc here](https://github.com/capstone-cy-team-1/capstone-cy-team-1.github.io/blob/main/public/Submitted-docs/Project%20Proposal.pdf)

## Status

Sprint-1 [3rd Feb - 15th Feb]:  Completed 

Sprint-2 [13th Feb - 20th March]:  Completed 

Sprint-3 [20th March - 30th March]:  Completed

Sprint-4 [30th March - 3rd April]: Completed

## Overview

The implementation is divided into two halves.
1. Organization Network + Employee Machine
2. Adversary’s Network

![](/public/file_1.drawio.png)

**Network Overview Diagram**

![](/public/network_overview.png)

**Organization Network**

This segment is a virtual network deployed in GCP with three servers (Linux) with NodeJS and NPM installed. The servers, namely the Production, Deployment/Staging, and Repository, are the only components in the organization environment.

Production and Deployment servers will run the vulnerable web application we will be building. The web application will have vulnerabilities 
“None” algorithm attack:  This will allow us to do account takeovers and leak the private package that the admin has stored in their account.
Dependency Confusion: This is another supply chain attack that we will use to allow code injections and execute the malicious payload in the “development servers.”

The production server would be allowed to have DNS lookups, whereas the Development server will have outbound HTTP(s) and DNS lookup capabilities.

As shown in the diagram, we also have an employee machine, which can be outside or inside the organization's network. The idea is to compromise this machine, provided it tries to download the private package.


**Adversary’s Network**

This segment is a virtual network deployed in GCP with two servers (Linux). The servers, namely the Attacker’s DNS and Caldera servers, are the only components in the adversary’s environment.

The attacker’s DNS Server will run a Bind9 service with our custom domain name `0xparthhackerone.me`. This is where the callbacks will be made whenever the victim machine does a DNS lookup on our domain.

Caldera Server will be running on a Linux-based machine which will help us demonstrate the execution of the agent script.

## Organization Network

Machine requirements:

```bash
# 3 Linux Machines
RAM: 4GB or more
Storage: Min
```

The 3 machines require 

```
Node: v18.11.0
npm: v8.19.2
pm2: 5.2.2

# The versions can change depending on the time of implementation
```

## Adversary’s Network

Machine requirements:

```bash
# Web Server
RAM: 4GB or more
Storage: Min

# Dev Server
RAM: 4GB or more
Storage: Min

# Verdaccio Server
RAM: 4GB or more
Storage: Min
```

The machine requires 

```
# Caldera Server
pip: v23.0.1
pyOpenSSL: v23.0.0

# The versions can change depending on the time of implementation

# DNS server
Custom Domain: 0xparthhackerone.me ( Hosting: Namecheap.me)
Service for capturing DNS log: Bind9

```

## Conclusion
Final report includes the executive summary of the attack and a presentation of the attack performed. The attack will also include mapping the whole attack to MITRE’s framework.

END
