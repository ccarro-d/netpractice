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

* **TCP/IP addressing (IPv4)**: the system used to identify interfaces and move packets between networks. In NetPractice, every link works only if both sides are addressed consistently. 
* **Subnet mask / CIDR**: the rule that splits an IP into *network part* and *host part*. This is what allows calculating the network address, broadcast, host range, and deciding whether two interfaces are on the same subnet (e.g., `/25`, `/28`, `/30`). 
* **Default gateway**: the “exit” used by a host to reach destinations outside its local subnet; it must be directly reachable from that host (i.e., inside the same subnet). 
* **Routers and routing tables**: routers forward packets between different subnets. A routing table is essentially a set of rules of the form “destination network → next hop”, used when the destination is not directly connected. 
* **Switches**: devices that forward traffic inside a LAN (layer-2 behavior). In NetPractice logs, it is normal to see the switch “trying” multiple links and endpoints discarding packets that aren’t for them. 
* **OSI layers (high level)**: a mental model to separate “switching/L2” problems (same subnet, MAC-level forwarding) from “routing/L3” problems (subnets, gateways, routes). 

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
