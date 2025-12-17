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
* This README file should also be included at the repository root as part of the submission deliverable.
* During the defense, only what exists inside the repository is evaluated, so filenames and location should be kept clean and double-checked.
* The login should be entered in the training interface before exporting each config file.

### Defense note

During the defense, three random levels are expected to be solved within a limited time. External tools are not allowed; at most, a simple calculator such as `bc` is tolerated.

## Resources

### Networking concepts studied

- **Network**
  > A network is a set of devices connected in a way that allows them to exchange data, following shared rules (protocols).
  > In NetPractice, every diagram is basically a collection of small networks connected together, so the main job is figuring out which devices are in the same network (same subnet) and how traffic moves between networks (routing).

- **TCP/IP**
  > TCP/IP is a suite of protocols that defines how data is addressed, transported, routed, and delivered across networks: IP handles addressing/routing; TCP adds reliable, ordered delivery on top of IP (UDP is an alternative transport without that reliability).
  > In NetPractice, the focus is almost entirely on the IP side (addresses, subnets, gateways, routes), but keeping the “IP first, transport above” mental model helps.

- **OSI model**
  > The OSI model is a conceptual framework that describes network communication in layers, mainly to separate responsibilities (what happens locally vs what happens between networks).
  > In NetPractice, there’s no need to memorize the 7 layers; it’s just a useful way to avoid mixing up local connectivity problems with routing problems.

- **IPv4 addressing**
  > IPv4 is one version of IP addressing, using 32-bit addresses written in dotted decimal (e.g., `163.172.250.12`); another common version is IPv6 (not covered here).
  > In NetPractice, every interface needs an IPv4 address that actually belongs to its subnet—if it’s outside the expected range (given the mask), links won’t behave as intended even if the numbers look “close”.

- **Subnet mask and CIDR notation**
  > A subnet mask is a 32-bit value that splits an IPv4 address into a network part and a host part, defining the subnet’s size and boundaries; CIDR is simply the compact way to write that mask as a prefix length (e.g., `/28` means 28 network bits).
  > In NetPractice, this is the core skill: the mask/CIDR is what lets you compute the network block, broadcast, valid host range, and confirm whether two interfaces are truly on the same subnet.

- **Switch and LAN**
  > A switch is a device that connects multiple devices within the same local network and forwards traffic based on MAC addresses; a LAN is a local network (home/office-style) where devices share the same local segment/subnet.
  > In NetPractice, a switch is basically how multiple hosts can share the same “local side” before going upstream to a router, and the logs can look noisy (`packet not for me`, `loop detected`) because the simulator explores paths—those messages are often informational if the goal ends OK.

- **Router**
  > A router is a device that connects different networks (subnets) and forwards IP packets between them based on destination IP addresses.
  > In NetPractice, routers are the junctions between subnets, and most levels are about making routers aware of remote networks and ensuring traffic can go out *and* come back.

- **Routing table**
  > A routing table is a set of rules mapping destination networks (prefixes) to a next hop (or outgoing interface), and a static route is just a manually configured entry in that table.
  > In NetPractice, it helps to read routes as “to reach THIS network → send to THIS neighbor”, keeping in mind that the next hop must be directly reachable (on-link) and that “almost working” setups usually miss the return route.

- **Default gateway**
  > A default gateway is the next-hop router a host uses to reach any destination outside its local subnet (the host’s “exit door”).
  > In NetPractice, the golden rule is that the gateway must be in the same subnet as the host interface—otherwise the host can’t even reach the gateway to leave its network.

### References

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

* Sanity-check subnetting calculations (network/broadcast/range) and validate that chosen masks fit the diagram constraints,
* Interpret NetPractice logs (forward vs reverse paths, gateway reachability, missing routes) and propose debugging checklists,
* Draft and iterate this README to match the subject’s required structure.

All configurations were tested in the NetPractice interface, and the routing choices can be explained during the defense.
