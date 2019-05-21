+++
title = "Security of Distributed Software - Lecture 03"
author = ["eo shiru"]
date = 2019-04-16
lastmod = 2019-05-17T13:01:55+02:00
tags = ["uni", "security-ds"]
draft = false
+++

## Attacks on End Systems {#attacks-on-end-systems}

Attacks on end systems via

-   computer viruses
-   computer worms
-   trojan horses
-   exploits
-   cracking systems

might focus on

-   unsecured computer systems
-   exploiting programming errors
-   bad security measures
-   weak passwords

Computer Virus

-   based on biological model
-   infects resources of the host system to replicate itself
-   malicious functions
    -   load generation
    -   data corruption
    -   spying
-   various types
    -   boot sector viruses
    -   file viruses
    -   macro viruses
    -   script viruses
    -   composites
-   self-defense mechanisms of viruses:
    -   stealth
    -   modification
    -   cryptographic methods
    -   polymorphism
    -   retroviruses (against anti-virus programs)
-   passive distribution: by embedding into other programs and execution by the host system

Computer Worm

-   based on biological model
-   uses resources of the host system and of the network to spread over to other systems _automatically_ in order to execute its malicious function there
-   malicious functions
    -   load generation
    -   data corruption
    -   spying
    -   spamming
    -   DDoS
-   various types
    -   email worms (social worms, file attachment, active content)
    -   interactive worms (ask the user "please press OK" to use exploits)
    -   instant messaging worm (sending of malicious software / links to all chat partners)
    -   IRC worms (usage of scripting in IRC programs)
    -   P2P worms (at file-sharing sites: tempting names &rarr; download)
    -   cell phone worms (distribution via Bluetooth, MMS, etc)
-   often in combination with other forms of malware, eg viruses droppers, backdoors, trojans

Dropper (virus dropper, DDoS dropper)

-   executable program that acts as a carrier program for malware
-   is usually terminated after the virurs has been installed

Injector

-   similar to dropper, but the malware will only be "installed" (injected) in memory

Backdoor

-   part of a program that allows users to gain acces to the machine / system bypassing the normal access security
-   variants: default passwords (BIOS); specially equipped passwords / routines / servers that allow access (sometimes subsequently installed programs)
-   closely linked to trojans and droppers

Trojan (trojan horse)

-   similar to the well-known story..
-   program that executes a potentially harmful function without user's knowledge
-   attention: often mixed up in the context of rootkits and backdoors

Rootkit (administrator toolbox)

-   collection of software tools for concealment and stealth intrusions of malicious software
-   examples: hiding backdoors by hiding processes, logs, log-ins

Exploit

-   a program (including scripts & macros) that exploits the weaknesses or failures of a system or another application to obtain privileges or to use it for DoS attacks

**Malware** as generic term refers to malicious or unwanted software or programs.

Buffer Overflow

-   application reserves a buffer to store some input values
-   the length of the input is larger than the buffer but the whole input still gets processed
-   memory space outside the buffer gets overwritten/accessed


## Attacks on Infrastructures {#attacks-on-infrastructures}

Attacks on infrastructures via

-   attacks on signaling mechanisms
-   distributed denial of service (DDoS)
-   attacks on WLAN hotspots and routers
-   break-ins (password theft, bugs, exploits)

might focus on

-   unsecured intermediate system
-   overload situations
-   unsecure data storage
-   weak passwords

Attacks on signaling mechanisms

-   ICMP: fake control messages
-   RSVP: fake resource allocation

Attacks on router

-   attacks on routing protocols
-   distribution of false routes
-   WLAN, Bluetooth etc

Attacks on Hardware, eg virtual server

-   usb-attacks

Denial of Service Attack

-   the targeted weak spot is the overload of the network component
    -   may result in loss of service or entire computer systems
-   attack possibilities
    -   basic principle: large amount of requests sent to the target service or target system
    -   requests must be designed in a way that they lead to an overload situation (more efficient use of exploits)
-   examples:
    -   ping of death = fake "echo request" information leads to a crash
    -   smurf = broadcasting of an ICMP "echo request" with false return address (address of the victim)
-   special forms
    -   **Distributed** DoS = coordinated attack with a large number of computers
        -   closely linked with trojan / droppers infected systems that can be used as a remote-controlled attack network (BotNets)
        -   BotNets - Malware starts its DDoS attacks after being distributed via a dropper

WLAN Attacks

-   the targeted weakspot is the transmission medium as well as utilizing encryption techniques
-   attack scenario
    -   capture data packets of a protected WIFI network
    -   "attack" on encryption &rarr; search for a key
    -   use the found key for further attacks in the protected network
-   examples: wepcrack, weplab etc.

Break-in

-   the targeted weakspots are routers, proxys, computers and services in a network as well as weak passwords, poor and faulty security mechanisms
-   attack scenarios
    1.  _host scanning_ &rarr; which computer / router / proxy exist in close proximity of the target (broadcasts, routing list, traffic, sniffing, DNSpredict/Google)? &rarr; list of target systems
    2.  _scanning the target system_ &rarr; type of systems (by means of fingerprints, traffic analysis, Google, whois, etc.)  which services (IP/TCP/UDP) are available or vulnerable (portscanning & ICMP etc)
    3.  _attack_ &rarr; exploiting bugs, backdoors, exploits, password scanners/lists, dropper, GoogleHackingDB
    4.  _successfull breach_ &rarr; read password lists, install droppers, backdoors, keyloggers, proxy monitor, rootkit, etc
        -   start attacks from the compromised system
        -   remove traces
-   examples:
    -   GHDB &rarr; default SSID and passwords of WIFI routers
    -   NBTEnum &rarr; search for other Windows systems
    -   Network Monitors &rarr; traffic analysis (eg TTL field observations) with respect to transparent bridges or dangers arising from IDS (not to attract attention)
-   break-in via exploits for example toolkits, known exploits, zero day exploits


## Attacks on Data / Protocols {#attacks-on-data-protocols}

Attacks on data / protocols via

-   communication interception
-   information manipulation
-   attacks on protocols and core mechanism

Focus on

-   protocol weaknesses
-   (lack of) communication weaknesses
-   focus on manipulating algorithms and protocols (eg via "contributions" to open source projects)

Examples:<br />


#### Address Resolution Protocol {#address-resolution-protocol}

-   **weak spot** of the ARP is that it is a stateless protocol and therefore it is possible to send ARP-Replies without any requests
-   **ARP-Spoofing** (ARP Request Poisoning, ARP Poison Routing)
    -   sniffing = collecting network information
    -   poisoning = targeted sending of wrong ARP packets (ARP-Reply with MAC adress for a foreign IP adress) to caches
    -   data packets will now be sent to attacker (address in the cache) which manipulates/spies on the data packets before they are sent to their real destination &rarr; this faked association enables Man-in-the-Middle attacks
-   there are various tools to simplify attacks eg [ARP Video](https://www.youtube.com/watch?v=RTXAUJ2yqCg)


#### Internet Protocol {#internet-protocol}

-   **weak spot** of the IP is that IP-packets are not protected
-   **attack possibilities**
    -   reading IP-packets is simple
    -   checksums for integrity checking are not safe
    -   no protection of IP-PCI (IP Header) &rarr; manipulation of the protocol header is simple
    -   liability is unsafe because authenticity of addresses is not provable
-   **attack scenario**
    -   target system is protected by IP-sender adresses (meaning that only systems with registered IP addresses are alllowed to use the target system)
    -   sniffing: spying of systems that exchange data with the target system (can also be encrypted)
    -   connecting to the target system using spied out IP addresses


#### Transmission Control Protocol (TCP) {#transmission-control-protocol--tcp}

-   **weak spot** of TCP is that a large number of ACK messages leads to high load on the firewall control
    -   ACK = acknowledgement; TCP is an acknowledgement-based protocol; when computers communicate via TCP, received packets are acknowledged by sending back a packet with ACK bit set
    -   some firewalls check incoming home network internet traffic insufficiently
    -   verification only for SYN messages, ACK messages are all let through
        -   SYN =  synchronize message via which a client requests a connection from the server
        -   part of the TCP three-way handshake (SYN &rarr; SYN-ACK &rarr; ACK)
-   **attack possibilities**
    -   incorrect ACKS are used to implement exploits (rather unproblematic)
    -   ACK-Tunneling = ACK is used for data transport &rarr; Trojan/Dropper acts as an ACK server and reads fata from the ACK (problematic)
    -   [SYN flood](https://en.wikipedia.org/wiki/SYN%5Fflood)
-   **attack scenario**
    -   intrusion into the target system and installation of an ACK server, which acts as a remote shell, or dropper, etc
    -   target system can now be controlled remotely (until replacement by a better firewall)


### Web-based attacks {#web-based-attacks}


#### SQL Injection {#sql-injection}

-   **weak spot**: web applications that use databases and without properly sanatizing etc
-   **attack possibilities**
    -   transfer of input data to the database (Form, URL) in a way to spy, change, delete data and execute code


#### XSS - Cross Site Scripting {#xss-cross-site-scripting}

-   **weak spot**
    -   possibility of executing script code in the browser
    -   weak user input checks
-   **attack possibilities**
    -   identify weak spots in web applications (eg possible user input via URL) that allow execution of script code &rarr; construct URL with script code
    -   other variants possible: <img>, <iframe>, etc and send those to potential targets (spam)
-   **attack scenario**
    -   URL queries cookies and sends those to a script &rarr; script calls the current application with the stolen cookies and uses the application under false idenity (session hijacking)


#### Cross Site Request Forgery (CSRF) {#cross-site-request-forgery--csrf}

-   exploiting the functionality of a web applications where victims have accounts
-   submit manipulated HTTP requests
    -   embed link or images in e-mails
    -   cross-site scripting
    -   malware


## Attacks by Communication Partner {#attacks-by-communication-partner}

Attacks of the communication partner by

-   faking identities
-   trust abuse
-   attacks on the data
    -   listening to the data (sniffing)
    -   manipulating data
    -   decrypting protected data

Focus on

-   misuse of trust, eg social engineering