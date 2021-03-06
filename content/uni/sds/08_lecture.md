+++
title = "Security of Distributed Software - Lecture 08"
author = ["eo shiru"]
date = 2019-05-20
lastmod = 2019-07-04T12:20:09+02:00
tags = ["uni", "security-ds"]
draft = false
+++

## Internet Firewalls (Chapter 6) {#internet-firewalls--chapter-6}

Definition: Firewalls are hard- or software components, which control the interconnection point between two network areas and implement security strategies by restricting packet forwarding.

Fundamentals:

-   Packet filter
    -   entity, which selectively processes flowing packets according to predefined rules, in particular, preventing packet forwarding
-   Proxy approaches
    -   representative of a client process
-   Network Address Translation (NAT)
    -   address translation, public and private addresses are distinguished
-   Bastion Host
    -   computer with particularly high protection requirements; vulnerability mainly results from the computer's exposed location
-   Dual-Homed Host
    -   computer with at least two network interfaces for two different subnets

These approaches are now covered in more detail.


### Packet Filter {#packet-filter}

{{< figure src="/knowledge-database/images/packet-filter.png" >}}

Then there are also router filter rules for example `deny icmp 129.12.0.0 0.0.255.255 any` in Linux environments this can be done via iptables, ipchains, ipfilter, ...<br />
There are also dynamic packet filters:<br />
![](/knowledge-database/images/dynamic-packet-filter.png)

Filter Table Guidelines

-   "default deny" &rarr; prohibit everything, which is not explicitly allowed
-   order &rarr; filter table is usually processed sequentially, analysis is terminated after all the rules have been applied
    -   correct order should be maintained
-   prevent spoofing attacks
    -   packets coming from 'outside' with 'inside' addresses are rejected; the same holds true in the other direction if the source address is not an 'inside' address
-   static filters: UDP blocking
-   controlled handling of ICMP
-   prevent source-routing
-   efficiency: unneccessary filtering rules have to be removed


### Proxy Firewall {#proxy-firewall}

{{< figure src="/knowledge-database/images/proxy-firewall.png" >}}

-   typically at transport layer or as an application proxy
-   transport layer: requires client code modification
-   application proxy: can perform service-specific controls


### Network Address Translation {#network-address-translation}

NAT is a proxy concept at the network layer. Initially it was intended as a measure to preserve the IPv4 address space while today it is used to conceal internal network structures.

-   doing NAT in practice gives up the end-to-end principle as it leads to numerous diffuclties (eg ftp)

{{< figure src="/knowledge-database/images/NAT.png" >}}


### Architectures {#architectures}

Let's look at different architectures utilizing different kinds of firewalls:<br />
![](/knowledge-database/images/architectures-1.png)
![](/knowledge-database/images/architectures-2.png)
![](/knowledge-database/images/architectures-3.png)

One traditional conception in network design has been that of the "perimeter" which means that there's an "inside" and "outside" to our network. However this is not applicable to the modern situation because of eg

-   mobile devices
-   peer-to-peer systems
-   ubiquitous computing
-   ad-hoc networks
-   sensor networks
-   ...

So there is no clearly defined "perimeter network" available anymore.


### IT-Security Management Aspects {#it-security-management-aspects}

-   determination of the required security level
-   firewall placement and coordination
    -   clear transition between 'internal' and 'external'?
    -   select entrance architecture (dual homed, screened, subnet,..)
    -   should the subnets be protected from one another?
    -   do devices require 'personal firewalls'?
    -   how can the three stages (entrace, subnet, end-system) be kept consistent and checked for errors?
-   Analysis of open communication channels
    -   dependencies on the first point
    -   administration concept: who gets to issue which rules?
-   firewall management requires security policy support


## Intrusion Detection Systems (Chapter 7) {#intrusion-detection-systems--chapter-7}

Motivation:

-   computer has been compromized and is used for (illegal) data distribution
-   network operator performs IP accounting and finds out that a computer, which has previously generated next to no load, is suddenly generating a high amount of it
-   Goal: attack detection and intrusion detection alarm

Intrusion Detection Systems

-   find and report suspicious activity in systems and networks
-   intrusion prevention: initiation of control measures
    -   intrusion response


### Classification of Intrusion Detection Systems {#classification-of-intrusion-detection-systems}

Location:

-   Host-based
    -   system breach and misuse detection
    -   examination of log files
    -   integrity checks by checksums
    -   inspection of "privilege escalation"
-   Network-based
    -   monitoring and verification of network traffic, which can take place at various network locations
-   Hybrid

Detection:

-   signature-based
-   anomaly-based


#### Signature-based Detection {#signature-based-detection}

-   break-in (attempt) detection based on known procedures
    -   eg buffer overflow attack
    -   eg implies _default.ida_ within a URL in an HTTP packet together with a certain pattern in the URL Argument Name Field is a Code Red attack
-   signatures must (same holds true for virus scanners) be kept up-to-date
-   challenges:
    -   register the attacks
    -   describe the attacks
    -   errors of type 1 and 2 (classification problem)


#### Anomaly-based Detection {#anomaly-based-detection}

-   detection of "normal" user behaviour deviations
-   normal behaviour has to be statically describable
-   classification problem
-   normal behaviour should be determined through learning
-   very effective attacks which are not deviating much from normal user behaviour might remain undetected

-    Example: Securing Gateways

    {{< figure src="/knowledge-database/images/gateways.png" >}}


### Intrusion Detection System - Honeypots {#intrusion-detection-system-honeypots}

Approach:

-   place unsecured server/service ("honeypot") in the network
-   monitor honeypots
-   analyse attacks and compromises
    -   identify tools, tactics and intruder motives

Typical objectives:

-   detect botnet attacks
    -   botnet = network of compromized computers that can be remotely orchestrated by the attacker
-   detect phishing attacks


### IDS in IT-Security Management {#ids-in-it-security-management}

-   Intrusion Detection is a reactive IT-security approach
    -   complements preventive measures, such as firewalls
-   data protection legal requirements must be met
-   intrusion prevention (response): given automatic reactions, one has to make sure they cannot be used as an attack themselves (such as Denial of Service)
-   integration with network management is appropriate and necessary


## Incident Management (Chapter 8) {#incident-management--chapter-8}


### History of CERTs / CSIRTs {#history-of-certs-csirts}

-   CERT = Computer Emergency Response Team
-   CIRT = Computer Security Indicent Response Team

-   trigger: internet worm 1988
-   need of an IT-security 'fire brigage' became evident
-   CERT/CC (Coordination Center) was founded by DARPA located at CMU

Today:

-   not just 'response', but generally incident handling
-   many CERTs and CSIRTs in the world eg DFN-CERT, CERT-Bund
-   in Germany: CERT-network
-   international network: FIRST (Forum of Incident Response and Security Teams)


### CSIRTs Tasks {#csirts-tasks}

Reactive Services

-   alerts and warnings
-   incident handling
    -   incident analysis
    -   incident response on site
    -   incident response support
    -   incident response coordination
-   vulnerability handling
    -   vulnerability analysis
    -   vulnerability response
    -   vulnerability response coordination
-   artifact handling
    -   artifact analysis
    -   artifact response
    -   artifact response coordination

Proactive Services

-   announcements
-   technology watch
-   security audit or assessments
-   configuration & maintenance of security tools, applications & infrastructures
-   development of security tools
-   intrusion detection services
-   security related information dissemination

Security Quality Management Services

-   risk analysis
-   business continuity & disaster recovery planning
-   security consulting
-   awareness building
-   education/training
-   product evaluation or certification

-    Incident Handling

    {{< figure src="/knowledge-database/images/incident-handling.png" >}}

-    Coordination: Early Warning System

    {{< figure src="/knowledge-database/images/early-warning.png" >}}


#### Naming of Vulnerabilities {#naming-of-vulnerabilities}

Naming requires standardization

-   otherwise cooperation & coordination become complex

Standard: common vulnerabilities and exposures

-   managed by The Mitre Corporation

Example:

Name: CVE-2004-0309<br />
Description: Stack-based buffer overflow in the SMTP service support in vsmon.exe in Zone Labs ZoneAlarm before 4.5.538.001, ZoneLabs Integrity client 4.0 before 4.0.146.046, and 4.5 before 4.5.085, allows remote attackers to execute arbitrary code via a long RCPT TO argument.<br />
Status: Entry<br />
Reference: BUGTRAQ:20040219 EEYE: ZoneLabs SMTP Processing Buffer Overflow<br />
Reference: CERT-VN:VU#619982
