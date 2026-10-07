# Module 00: Ultra Quick Revision Short Notes (Exact 3-Page Cheat Sheet)

> **Unit 3: Network Layer (Core Routing & Addressing)**  
> **Course:** Computer Networks (BCS-603 / GATE CS / IT)  
> **Target:** AKTU Semester Exams, GATE CS, Technical Interviews  
> **Format:** Strict 3-Page High-Density Formula & Concept Cheat Sheet

---

## Download Cheat Sheet PDF
- **Direct PDF:** [00_Quick_Revision_Short_Notes.pdf](00_Quick_Revision_Short_Notes.pdf)
- **Unit 3 Root Copy:** [Unit_3_Quick_Revision_3_Page_Notes.pdf](../Unit_3_Quick_Revision_3_Page_Notes.pdf)

---

## 3-Page Architecture Overview

### Page 1: Foundations, IPv4 Header, Fragmentation & Classful Addressing
- **Network Layer Foundations:** Host-to-Host delivery, Store-and-forward, Routing (Control Plane) vs Forwarding (Data Plane).
- **Datagram vs Virtual Circuit:** Stateless vs Stateful, full IP header vs 16-bit VCI tag, dynamic rerouting vs circuit termination.
- **IPv4 Datagram Header:** 20-60 Bytes, VER (4b), HLEN (4b words), ToS, Total Length, TTL, Protocol numbers (1=ICMP, 6=TCP, 17=UDP), 16-bit Checksum.
- **IPv4 Fragmentation Math:** MTU limit, Identification, Flags (DF, MF), Fragment Offset formula (`Offset = Byte_Offset / 8`), 8-byte boundary rule.
- **Classful Addressing:** Classes A, B, C, D, E ranges, default masks, RFC 1918 Private IPs, Loopback 127.0.0.1, Limited & Directed Broadcasts.

### Page 2: Subnetting Math, CIDR, Supernetting, NAT/PAT, IPv6 & ARP
- **Subnetting Mechanics:** Host bit borrowing ($s$ bits), $N_{	ext{subnets}} = 2^s$, $N_{	ext{hosts}} = 2^h - 2$, Jump size $= 256 - 	ext{Mask Octet}$, Bitwise AND Subnet ID extraction.
- **Classless Addressing (CIDR):** Prefix length `/n`, 3 mandatory block rules (Contiguous, Power of 2, Divisible by block size).
- **Supernetting & LPM:** Route aggregation, prefix shrinking, Longest Prefix Match routing forwarding decision.
- **NAT & PAT Overload:** RFC 1631, Private to Public IP mapping, Port Address Translation (PAT) multiplexing via L4 transport ports.
- **IPv6 Architecture:** 128-bit hex colon representation, zero compression (`::`), fixed 40-byte base header, transition strategies (Dual Stack, Tunneling, NAT-PT).
- **ARP & RARP:** Logical IP to Physical MAC binding, Request broadcast vs Reply unicast, 28-byte packet format, ARP Cache, Gratuitous ARP.

### Page 3: DHCP DORA, ICMP, Unicast Routing Algorithms, Congestion Control & PYQs
- **DHCP DORA:** Discover (Broadcast), Offer, Request (Broadcast), ACK, UDP 67/68, Relay Agent across subnets, Lease renewal ($T_1, T_2$).
- **ICMP:** Error reporting (Type 3, 11, 12, 5), Query messages (Type 8/0 for Ping), Traceroute TTL hop-by-hop discovery.
- **Distance Vector Routing:** Bellman-Ford recurrence, RIP periodic updates, Count-to-Infinity failure, Split Horizon & Poison Reverse.
- **Link State Routing:** OSPF / IS-IS, 5 phases, LSP reliable flooding, Dijkstra Shortest Path Tree computation.
- **Path Vector & BGP:** Inter-domain AS routing, AS-PATH attribute, Loop discard rule, Kamoun-Klein Hierarchical Clustering ($k = \ln N$).
- **Congestion Control:** Open-loop vs Closed-loop, Leaky Bucket constant rate vs Token Bucket burst formula ($T = C / (M - R)$).
- **Top AKTU PYQs:** 5 high-frequency 10-marks semester exam questions with structured model answer guidelines.
