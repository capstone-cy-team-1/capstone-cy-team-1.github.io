# CY Capstone Project By Team 1

## Project 

This project is intended to apply the MITRE ATT&CK framework and tools to map a cyber incident and then use the Caldera tool to complete an emulation plan. Included into team's tasks is the deployment in the Cloud of a mock-up scenario that represents the system compromised in the cyberincident studied. 

As a result of the project, with the Adversary Emulation Plan is needed to elaborate Threat Report of the incident analized (including a STIX2.1 JSON representation). 

You can find the 
1. Presentation docs here: [Docs](https://github.com/capstone-cy-team-1/capstone-cy-team-1.github.io/tree/main/public)
2. Organization housing all the repositories: [Capstone-cy-team-1](https://github.com/capstone-cy-team-1/)
3. Scrum Board here: [Team-1 Scrum Board](https://github.com/orgs/capstone-cy-team-1/projects/1)

## Proposal 

Vulnerability: Supply Chain Attack(s)
Idea: Build an infrastructure for an organization that heavily relies on a JavaScript environment. This environment will be utilized for implementing the Dependency Confusion attack using custom scripts and the Caldera tool.

## Status

![](/public/chart.png)

Sprint-1 [3rd Feb - 15th Feb]:  Completed 

Sprint-2 [13th Feb - 20th March]:  Completed 

Sprint-3 [20th March - 30th March]:  Ongoing 

## Overview

The implementation is divided into two halves.
1. Organization Network + Employee Machine
2. Adversary’s Network

![](/public/file_1.drawio.png)

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
# 1 Linux Machine
RAM: 4GB or more
Storage: Min
```

The machine requires 

```
pip: v23.0.1
pyOpenSSL: v23.0.0

# The versions can change depending on the time of implementation
```
