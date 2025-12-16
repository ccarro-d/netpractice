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

### Submission (what should be inside this repo)

* The repository root should contain **10 exported configuration files** (**1 per level**). 
* During the defense, only what exists inside the repository is evaluated, so filenames and location should be kept clean and double-checked. 
* The login should be entered in the training interface before exporting each config file. 

### Defense note

During the defense, three random levels are expected to be solved within a limited time. External tools are not allowed; at most, a simple calculator such as `bc` is tolerated. 

## Resources

### Networking concepts studied (what they are in practice)

* **TCP/IP addressing (IPv4)**: the system used to identify interfaces and move packets between networks. In NetPractice, every link works only if both sides are addressed consistently. 
* **Subnet mask / CIDR**: the rule that splits an IP into *network part* and *host part*. This is what allows calculating the network address, broadcast, host range, and deciding whether two interfaces are on the same subnet (e.g., `/25`, `/28`, `/30`). 
* **Default gateway**: the “exit” used by a host to reach destinations outside its local subnet; it must be directly reachable from that host (i.e., inside the same subnet). 
* **Routers and routing tables**: routers forward packets between different subnets. A routing table is essentially a set of rules of the form “destination network → next hop”, used when the destination is not directly connected. 
* **Switches**: devices that forward traffic inside a LAN (layer-2 behavior). In NetPractice logs, it is normal to see the switch “trying” multiple links and endpoints discarding packets that aren’t for them. 
* **OSI layers (high level)**: a mental model to separate “switching/L2” problems (same subnet, MAC-level forwarding) from “routing/L3” problems (subnets, gateways, routes). 

### References (what each one helped with)

* **[Official subject PDF (42)](./en.subject.pdf)**: defines the rules, deliverable format (10 config files), how the interface works, and what must be explained during the defense.
* **[tblaase / Net_Practice](https://github.com/tblaase/Net_Practice/tree/main)**: community notes and level-by-level hints that help build intuition for CIDR splits and routing patterns.
* **[caroldaniel / 42sp-cursus-netpractice](https://github.com/caroldaniel/42sp-cursus-netpractice)**: condensed explanations of common pitfalls (wrong gateway, wrong network, missing return route).
* **[lpaube / NetPractice (README.es.md)](https://github.com/lpaube/NetPractice/blob/main/README.es.md)**: Spanish explanations and subnetting reminders, useful as a quick refresher.
* **[42 GitBook guide](https://42-cursus.gitbook.io/guide/4-rank-04/netpractice)**: a broader 42-oriented summary of what NetPractice expects and how to approach it efficiently.
* **[NetPractice: An Intro to IP Addresses and Subnets](https://www.youtube.com/watch?v=HQUw0CfQWAM)**: introduction to IP addressing and subnetting basics.
* **[Netpractice 42 - IPs, Routers, Tablas de Rutas y Trazas](https://www.youtube.com/watch?v=pwjAyiscts8)**: overview of IPs, routers, routing tables, and how to read traces/logs in NetPractice.
* **[Netpractice 42 - Resolución de ejercicios con errores](https://www.youtube.com/watch?v=6yAnT4YzmvQ)**: practical walkthroughs solving common NetPractice mistakes and debugging patterns.

### AI usage (how it was used and for what)

AI was used as a learning assistant to:

* sanity-check subnetting calculations (network/broadcast/range) and validate that chosen masks fit the diagram constraints,
* interpret NetPractice logs (forward vs reverse paths, gateway reachability, missing routes) and propose debugging checklists,
* draft and iterate this README to match the subject’s required structure.

All configurations were tested in the NetPractice interface, and the routing choices can be explained during the defense.
