*This project has been created as part of the 42 curriculum by **ccarro-d*** 

## Description

NetPractice is a practical networking exercise built around small, non-real network topologies. Each level presents a broken diagram (hosts / routers / switches / “Internet”) and one or more connectivity goals. The objective is to make the network work by editing only the **unshaded** fields (IP addresses, masks/CIDR, gateways and static routes) and validating the result with the built-in checker and logs. 

A total of **10 levels** are solved, and each solution is exported as a configuration file to be submitted in this repository. 

## Instructions

### Running the training interface

* The NetPractice archive attached to the project page should be downloaded and then extracted into any folder.
* From that folder, the training interface should be started by opening `index.html` in a web browser. 
* Practice can be done by entering a 42 login (personal configuration), and the “evaluation” tab can be used to generate random configurations closer to defense conditions. 

### Solving levels and exporting configs

* Each level is solved by adjusting the available configuration until all goals are **OK**.
* **Check again** is used to validate the current setup, and the logs at the bottom are used to understand why something fails (missing gateway, invalid address, no route forward/reverse, etc.). 
* Before moving to the next level, the configuration should be exported using **Get my config**, since that exported file is what gets submitted. 

### Submission

* The repository root should contain **10 exported configuration files** (**1 per level**). 
* During the defense, only what exists inside the repository is evaluated, so filenames and location should be kept clean and double-checked. 
* The login should be entered in the training interface before exporting each config file. 

### Defense note

During the defense, three random levels are expected to be solved within a limited time. External tools are not allowed; at most, a simple calculator such as `bc` is tolerated. 

## Resources

### Networking concepts studied

- **Network**
  > **Definition:** A network is a set of devices connected in a way that allows them to exchange data, following shared rules (protocols).  
  > **In NetPractice:** Every diagram is basically a collection of small networks connected together. The whole game is figuring out which devices are in the same network (same subnet) and how traffic moves between networks (routing).

- **TCP/IP**
  > **Definition:** TCP/IP is a suite of protocols that defines how data is addressed, transported, routed, and delivered across networks. IP handles addressing/routing; TCP adds reliable, ordered delivery on top of IP (UDP is an alternative transport without that reliability).  
  > **In NetPractice:** The project is mostly “IP world” (addresses, subnets, gateways, routes). TCP isn’t configured directly, but it helps to remember the big picture: first the packet must reach the correct network (IP/routing), then transport sits above that.

- **OSI model**
  > **Definition:** The OSI model is a conceptual framework that describes network communication in layers, to separate responsibilities (what happens “locally”, what happens “between networks”, etc.).  
  > **In NetPractice:** No memorization of 7 layers is needed. It’s mainly a mental tool to avoid mixing concepts: local connectivity inside a segment vs routing between segments.

- **IPv4 addressing**
  > **Definition:** IPv4 is one version of IP addressing, using 32-bit addresses written in dotted decimal (e.g., `163.172.250.12`). Another common IP version is IPv6 (not covered here).  
  > **In NetPractice:** Every interface in the diagram needs an IPv4 address that makes sense for its subnet. If the address doesn’t belong to the expected subnet range (given the mask), links won’t behave as intended even if the numbers “look close”.

- **Subnet mask**
  > **Subnet mask — Definition:** A subnet mask is a 32-bit value that splits an IPv4 address into a **network part** and a **host part**, defining the subnet’s size and boundaries.  
  > **CIDR — Definition:** CIDR is a compact way to write the same mask as a *prefix length* (e.g., `/28` means “28 bits are network bits”). The prefix length is the count of `1` bits in the mask, and it determines the subnet size: **number of addresses = 2^(32 − prefix)** (usable hosts are usually that minus network/broadcast).  
  > **In NetPractice:** This is the core skill. The mask/CIDR is what lets you compute the network block, broadcast, and valid host range, and check whether two interfaces are actually on the same subnet.

- **Switch and LAN**
  > **Switch — Definition:** A switch is a device that connects multiple devices within the same local network and forwards traffic based on MAC addresses (local delivery).  
  > **LAN — Definition:** A LAN is a local network (home/office-style) where devices share the same local segment/subnet.  
  > **In NetPractice:** Think of the switch as the practical solution to “I have multiple devices but only one uplink” (the classic “modem/router has limited ports” problem). It lets several devices share the same local segment so they can talk locally and also reach the upstream router.

- **Router**
  > **Definition:** A router is a device that connects different networks (subnets) and forwards IP packets between them based on destination IP addresses.  
  > **In NetPractice:** Routers are the junctions between subnets. Most levels are about making routers aware of remote networks and ensuring traffic can go out *and* come back.

- **Routing table**
  > **Definition:** A routing table is a set of rules mapping **destination networks (prefixes)** to a **next hop** (or outgoing interface). A static route is a manually configured entry in that table.  
  > **In NetPractice:** Always read a route as: **“to reach THIS network → send to THIS neighbor”**. Routes should usually target networks (CIDR), not single host IPs, and the next hop must be directly reachable from that router (on-link).

- **Default gateway**
  > **Definition:** A default gateway is the next-hop router a host uses to reach any destination outside its local subnet (the host’s “exit door”).  
  > **In NetPractice:** Golden rule: the gateway must be in the **same subnet** as the host interface.

### References (what each one helped with)

* **[Official subject PDF (42)](./en.subject.pdf)**: The source of truth for the project: what NetPractice is, what the deliverable looks like (10 exported configs), and what is expected during the defense.

* **[tblaase / Net_Practice](https://github.com/tblaase/Net_Practice/tree/main)**: A structured “mini-handbook” plus **level-by-level walkthroughs**. It’s organized into *Basics* (special IP ranges, masks, switches/routers, routing tables) and then *Levels 1–10*, which is useful to compare patterns between exercises.
* **[caroldaniel / 42sp-cursus-netpractice](https://github.com/caroldaniel/42sp-cursus-netpractice)**: A concept-first guide that explains the foundations (what a network is, TCP/IP addressing, IPv4 + subnet masks, switch/router behavior, routing tables) before connecting those ideas to NetPractice. Good for building intuition when the “why” is missing.

* **[lpaube / NetPractice (README.es.md)](https://github.com/lpaube/NetPractice/blob/main/README.es.md)**: A detailed guide (Spanish version available) with a clear *Important Concepts* section (TCP, IP address, subnet mask, switch, router) and then a Levels section. Helpful as a quick refresher when stuck on routing-table logic.

* **[42 GitBook guide — NetPractice](https://42-cursus.gitbook.io/guide/4-rank-04/netpractice)**: A high-level overview of what NetPractice is and how the training flow works (10 levels, “link all machines”), plus navigation to theory/early levels. Useful as orientation rather than a deep technical reference.

* **[NetPractice: An Intro to IP Addresses and Subnets](https://www.youtube.com/watch?v=HQUw0CfQWAM)**: Concept-focused walkthrough for NetPractice: revisits TCP/IP, LAN basics, what an IP address is, and subnetting fundamentals (with timestamps), useful as a quick reset before solving levels.

* **[Netpractice 42 - IPs, Routers, Tablas de Rutas y Trazas](https://www.youtube.com/watch?v=pwjAyiscts8)**: Spanish video focused on the exact pieces that usually block NetPractice: IPs, routers, routing tables, and reading traces/logs.

* **[Netpractice 42 - Resolución de ejercicios con errores](https://www.youtube.com/watch?v=6yAnT4YzmvQ)**: Spanish “debugging” style video aimed at solving exercises by spotting typical mistakes (gateway reachability, missing return routes, wrong CIDR/network, etc.).

### AI usage

AI was used as a learning assistant to:

* sanity-check subnetting calculations (network/broadcast/range) and validate that chosen masks fit the diagram constraints,
* interpret NetPractice logs (forward vs reverse paths, gateway reachability, missing routes) and propose debugging checklists,
* draft and iterate this README to match the subject’s required structure.

All configurations were tested in the NetPractice interface, and the routing choices can be explained during the defense.
