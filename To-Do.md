# 🔐 NETWORK & NETWORK SECURITY – COMPLETE ROADMAP

*(Beginner → Internship-Ready → Strong Candidate)*

---

## 🧱 PHASE 0: Prerequisites (Before Networking)

### Programming Basics (Required)

* C / C++ basics
* Python basics
* Socket programming basics (later deep dive)

### OS Basics

* Process vs Thread
* User space vs Kernel space
* File descriptors
* Interrupts
* System calls

📘 Reference:

* **Operating System Concepts**

---

## 🧠 PHASE 1: Core Networking Fundamentals (FOUNDATION)

![Image](https://cdn2.hubspot.net/hubfs/2954816/The%207%20Layers%20of%20OSI.png)

![Image](https://afteracademy.com/images/what-is-the-tcp-ip-model-and-how-it-works-tcp-ip-model-five-layers-195bdaa7116cd850.jpg)

![Image](https://www.computernetworkingnotes.com/wp-content/uploads/ccna-study-guide/images/csg25-02-osi-encapsulation.png)

![Image](https://www.techtarget.com/rms/onlineimages/encapsulation_decapsulation-f_mobile.png)

### 1.1 Network Models

* OSI model (all 7 layers in detail)
* TCP/IP model
* Mapping OSI ↔ TCP/IP
* Role of each layer
* Encapsulation & decapsulation

### 1.2 Data Transmission

* Bit, Frame, Packet, Segment
* MTU
* Fragmentation
* Latency, Bandwidth, Throughput, Jitter

---

## 🌐 PHASE 2: IP Addressing & Subnetting (CRITICAL)

![Image](https://media.geeksforgeeks.org/wp-content/cdn-uploads/IP_addressing_3.jpg)

![Image](https://ipcisco.com/wp-content/uploads/subnetting-example-ipcisco.jpg)

![Image](https://www.ipxo.com/app/uploads/2021/09/Private-vs-Public_2-1024x455.png)

![Image](https://www.avast.com/hs-fs/hubfs/New_Avast_Academy/Public%20vs.%20local%20IP%20addresses%20%28Academy%29/Public-vs-Private-IP-Addresses-01-EN.png?name=Public-vs-Private-IP-Addresses-01-EN.png\&width=1111)

### 2.1 IPv4

* Classes (A, B, C, D, E)
* Network ID vs Host ID
* Private vs Public IP
* Loopback & APIPA

### 2.2 Subnetting (MUST MASTER)

* CIDR notation
* Subnet masks
* Borrowed bits
* Hosts per subnet
* VLSM
* Supernetting

### 2.3 IPv6

* Address format
* Types (Global, Link-local, Multicast)
* IPv6 vs IPv4

---

## 🔁 PHASE 3: Core Network Protocols

![Image](https://afteracademy.com/images/what-is-a-tcp-3-way-handshake-process-three-way-handshaking-establishing-connection-6a724e77ba96e241.jpg)

![Image](https://www.imperva.com/learn/wp-content/uploads/sites/13/2019/01/UDP-packet.jpg)

![Image](https://www.researchgate.net/publication/342003872/figure/fig2/AS%3A900085244248066%401591608453435/Domain-name-resolution-process-with-DNS.ppm)

![Image](https://www.indusface.com/wp-content/uploads/2024/10/DNS-lookup-process-.png)

### 3.1 Transport Layer

#### TCP

* 3-way handshake
* Sequence & ACK numbers
* Flow control
* Congestion control
* TCP teardown
* TCP flags

#### UDP

* Connectionless model
* Use cases (VoIP, DNS, streaming)
* Why UDP is faster

### 3.2 Network & Application Protocols

* IP
* ICMP (ping, traceroute)
* ARP
* DNS
* DHCP
* HTTP vs HTTPS
* FTP vs SFTP
* SMTP, POP3, IMAP

---

## 🛣️ PHASE 4: Routing & Switching

![Image](https://www.cs.emory.edu/~cheung/Courses/558/Syllabus/13-Routing/FIGS/graph4.gif)

![Image](https://www.baeldung.com/wp-content/uploads/sites/4/2022/11/RoutingDifferences-2.jpg)

![Image](https://i.adroitacademy.com/blog/69240134.jpg)

![Image](https://media.geeksforgeeks.org/wp-content/uploads/20230327175419/Unicast-routing-1.png)

### 4.1 Switching

* MAC address
* CAM table
* Broadcast, Unicast, Multicast
* VLANs
* Trunking

### 4.2 Routing

* Routing table
* Static routing
* Dynamic routing (conceptual)

  * RIP
  * OSPF
  * BGP (high level)

---

## 🐧 PHASE 5: Linux Networking (VERY IMPORTANT)

![Image](https://phoenixnap.com/kb/wp-content/uploads/2023/09/linux-networking-commands-cheat-sheet-pdf-preview.png)

![Image](https://media.geeksforgeeks.org/wp-content/uploads/20200521231351/capture-packets-tcpdump.png)

![Image](https://opensource.com/sites/default/files/uploads/iptables1.jpg)

### 5.1 Linux Commands

```bash
ip a
ip route
ss -tulnp
netstat
ping
traceroute
nmcli
```

### 5.2 Network Tools

* tcpdump
* Wireshark
* nmap
* netcat

### 5.3 Firewall & NAT

* iptables
* ufw
* SNAT / DNAT
* Port forwarding

---

## 🔐 PHASE 6: Network Security Fundamentals

![Image](https://miro.medium.com/0%2AZE2dgfCfy4tU4GpJ.jpg)

![Image](https://ipwithease.com/wp-content/uploads/2020/05/IDS-VS-IPS.jpg.webp)

![Image](https://www.paloaltonetworks.com/content/dam/pan/en_US/images/cyberpedia/types-of-firewalls/types-of-firewalls.png?imwidth=480)

![Image](https://media.geeksforgeeks.org/wp-content/uploads/20240423131026/Firewall.webp)

### 6.1 Security Basics

* CIA Triad
* Threat vs Vulnerability vs Risk
* Authentication vs Authorization
* AAA model
* Security policies

### 6.2 Security Devices

* Firewalls
* IDS / IPS
* Proxy servers
* VPNs
* Load balancers

---

## ⚔️ PHASE 7: Network Attacks (MUST KNOW)

![Image](https://www.imperva.com/learn/wp-content/uploads/sites/13/2017/09/man-in-the-middle-mitm-attack.png)

![Image](https://upload.wikimedia.org/wikipedia/commons/3/33/ARP_Spoofing.svg)

![Image](https://www.imperva.com/learn/wp-content/uploads/sites/13/2019/01/DNS-spoofing.jpg)

![Image](https://www.keycdn.com/img/support/dns-spoofing.png)

### 7.1 Attacks

* MITM
* ARP spoofing
* DNS poisoning
* Replay attack
* Session hijacking
* Port scanning
* Brute force
* DoS / DDoS

### 7.2 Detection & Mitigation

* Packet inspection
* Rate limiting
* Secure ARP
* DNSSEC
* Firewall rules

---

## 🔑 PHASE 8: Cryptography for Network Security

![Image](https://assets.bytebytego.com/diagrams/0349-symmetric-encryption-vs-asymmetric-encryption.png)

![Image](https://cf-assets.www.cloudflare.com/slt3lc6tev37/5aYOr5erfyNBq20X5djTco/3c859532c91f25d961b2884bf521c1eb/tls-ssl-handshake.png)

![Image](https://www.thesslstore.com/blog/wp-content/uploads/2021/12/2-tier-ca-pki-architecture-diagram.png)

### 8.1 Cryptography Basics

* Symmetric encryption (AES)
* Asymmetric encryption (RSA, ECC)
* Hash functions (SHA-256)
* MAC vs Hash
* Digital signatures

### 8.2 PKI & TLS

* Certificates
* CA chain
* TLS handshake
* HTTPS working
* Perfect Forward Secrecy

📘 Reference:

* **Cryptography and Network Security**

---

## 🧪 PHASE 9: Hands-On Labs (NON-NEGOTIABLE)

![Image](https://user-content.gitlab-static.net/d1f2cbdbc064b2cfa0acc4fe483cd8fd4fac931c/687474703a2f2f746370697067756964652e636f6d2f667265652f6469616772616d732f7463706f70656e337761792e706e67)

![Image](https://nmap.org/book/images/zenmap-fig-tab-nmap-output.png)

![Image](https://upload.wikimedia.org/wikipedia/commons/3/33/ARP_Spoofing.svg)

### Labs to perform

* Capture TCP handshake
* Analyze DNS queries
* Inspect HTTPS traffic
* Scan local network with nmap
* ARP spoofing (lab only)
* Detect spoofing

Platforms:

* TryHackMe
* Hack The Box (starter tiers)

---

## 🛠️ PHASE 10: Projects (RESUME GOLD)

### Must-Do Projects

1. Packet Sniffer (Python + Scapy)
2. Network Scanner (custom nmap)
3. Secure Chat App (TLS + sockets)
4. ARP Spoof Detector
5. Firewall Rule Analyzer

---

## 🎯 PHASE 11: Interview Readiness

### Questions you MUST answer

* What happens when you open google.com?
* Explain TCP handshake
* TCP vs UDP
* How HTTPS works
* What is NAT?
* What is a firewall?
* Explain MITM

---

## 📅 10-Week Timeline

| Week | Focus               |
| ---- | ------------------- |
| 1    | OS + OSI + TCP/IP   |
| 2    | IP & Subnetting     |
| 3    | TCP/UDP + DNS       |
| 4    | Routing & Switching |
| 5    | Linux Networking    |
| 6    | Network Security    |
| 7    | Cryptography        |
| 8    | Wireshark + nmap    |
| 9    | Project             |
| 10   | Resume + Interviews |

---

## 🚀 Final Advice

If you can:

* Explain packet flow
* Read Wireshark captures
* Write basic scanners
* Understand TLS

👉 **You’re intern-ready.**

---

If you want next:

* ✅ **Daily study checklist**
* 📄 **Intern-level resume**
* 🧠 **Mock interview**
* 🛠️ **Project code walkthrough**

Just tell me what you want next.
