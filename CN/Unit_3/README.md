# Computer Networks — Unit 3: Network Layer (Core Routing & Addressing)

> **Course:** Computer Networks (AKTU BCS-603 / GATE CS / IT)  
> **Source Material:** Gateway Classes AKTU Notes by Dr. Nidhi Parashar Ma'am (197 Slides Comprehensive Coverage)  
> **Author & Repository:** [Shivam Keshari / CS_Fundamental-00](https://github.com/S1h2i3v4a/CS_Fundamental-00)

---

## Master Documents & High-Yield Revision
- **[Unit_3_Master_Notes.pdf](Unit_3_Master_Notes.pdf)** — Consolidated master textbook notes compiling all 15 modules with interactive Table of Contents.
- **[Unit_3_Quick_Revision_3_Page_Notes.pdf](Unit_3_Quick_Revision_3_Page_Notes.pdf)** — Ultra high-density 3-page verified exam revision cheat sheet.

---

## Complete 15-Module Architectural Index

| Module | Chapter Title | Key Topics Covered | Artifacts & PDF |
| :--- | :--- | :--- | :--- |
| **00** | [Quick Revision Short Notes](00_Quick_Revision_Short_Notes/) | Strict 3-page high-yield cheat sheet covering all 14 modules | [PDF](00_Quick_Revision_Short_Notes/00_Quick_Revision_Short_Notes.pdf) |
| **01** | [Network Layer Foundations & Switching](01_Network_Layer_Foundations_and_Virtual_Circuits/) | End-to-end host delivery, Store-and-forward, Datagram vs Virtual Circuit, Control Plane vs Data Plane | [SVG](01_Network_Layer_Foundations_and_Virtual_Circuits/diagrams/network_layer_services_and_switching.svg) • [PDF](01_Network_Layer_Foundations_and_Virtual_Circuits/01_Network_Layer_Foundations_and_Virtual_Circuits.pdf) |
| **02** | [IPv4 Header Format & Protocol Design](02_IPv4_Header_Format_and_Protocol_Design/) | 20-60B Header anatomy, VER, HLEN, ToS, Total Length, TTL, Protocol multiplexing, 16-bit Checksum | [SVG](02_IPv4_Header_Format_and_Protocol_Design/diagrams/ipv4_datagram_header_architecture.svg) • [PDF](02_IPv4_Header_Format_and_Protocol_Design/02_IPv4_Header_Format_and_Protocol_Design.pdf) |
| **03** | [IPv4 Fragmentation & MTU Numericals](03_IPv4_Fragmentation_and_MTU_Numericals/) | MTU limits, Identification, Flags (DF, MF), Fragment Offset calculation (`Offset = byte/8`), Solved numericals | [SVG](03_IPv4_Fragmentation_and_MTU_Numericals/diagrams/ipv4_fragmentation_process.svg) • [PDF](03_IPv4_Fragmentation_and_MTU_Numericals/03_IPv4_Fragmentation_and_MTU_Numericals.pdf) |
| **04** | [IPv4 Classful Addressing Architecture](04_IPv4_Classful_Addressing_and_Special_Blocks/) | Classes A, B, C, D, E, NetID vs HostID, Default masks, RFC 1918 Private IPs, Loopback, Broadcasts | [SVG](04_IPv4_Classful_Addressing_and_Special_Blocks/diagrams/ipv4_classful_addressing_architecture.svg) • [PDF](04_IPv4_Classful_Addressing_and_Special_Blocks/04_IPv4_Classful_Addressing_and_Special_Blocks.pdf) |
| **05** | [Subnetting Mechanics & Classful Design](05_Subnetting_Mechanics_and_Classful_Subnet_Design/) | Host bit borrowing ($s$ bits), $N_s = 2^s$, $N_h = 2^h - 2$, Block size formula, Bitwise AND routing extraction | [SVG](05_Subnetting_Mechanics_and_Classful_Subnet_Design/diagrams/subnetting_bit_borrowing_architecture.svg) • [PDF](05_Subnetting_Mechanics_and_Classful_Subnet_Design/05_Subnetting_Mechanics_and_Classful_Subnet_Design.pdf) |
| **06** | [Classless Addressing (CIDR) & Supernetting](06_Classless_Addressing_CIDR_and_Supernetting/) | Prefix length `/n`, 3 mandatory block rules, Supernetting / Route Aggregation, Longest Prefix Match (LPM) | [SVG](06_Classless_Addressing_CIDR_and_Supernetting/diagrams/cidr_slash_notation_and_supernetting.svg) • [PDF](06_Classless_Addressing_CIDR_and_Supernetting/06_Classless_Addressing_CIDR_and_Supernetting.pdf) |
| **07** | [Network Address Translation (NAT) & IPv6](07_Network_Address_Translation_NAT_and_PAT/) | Static, Dynamic, PAT (NAT Overload) with L4 ports, IPv6 128-bit format, 40B fixed header, Dual Stack, Tunneling | [SVG](07_Network_Address_Translation_NAT_and_PAT/diagrams/nat_pat_translation_table_mechanics.svg) • [PDF](07_Network_Address_Translation_NAT_and_PAT/07_Network_Address_Translation_NAT_and_PAT.pdf) |
| **08** | [Address Resolution Protocol (ARP) & RARP](08_Address_Resolution_Protocol_ARP_and_RARP/) | L3 to L2 address mapping, Request broadcast vs Reply unicast, 28B packet, ARP Cache, Gratuitous ARP, RARP | [SVG](08_Address_Resolution_Protocol_ARP_and_RARP/diagrams/arp_packet_format_and_broadcast_request.svg) • [PDF](08_Address_Resolution_Protocol_ARP_and_RARP/08_Address_Resolution_Protocol_ARP_and_RARP.pdf) |
| **09** | [Dynamic Host Configuration Protocol (DHCP)](09_Dynamic_Host_Configuration_Protocol_DHCP/) | Dynamic IP allocation, DORA 4-step handshake, UDP 67/68, Relay Agent across subnets, Lease renewal ($T_1, T_2$) | [SVG](09_Dynamic_Host_Configuration_Protocol_DHCP/diagrams/dhcp_dora_handshake_architecture.svg) • [PDF](09_Dynamic_Host_Configuration_Protocol_DHCP/09_Dynamic_Host_Configuration_Protocol_DHCP.pdf) |
| **10** | [Internet Control Message Protocol (ICMP)](10_Internet_Control_Message_Protocol_ICMP/) | Error reporting (Type 3, 11, 12, 5), Query messages (Type 8/0 Ping), Traceroute TTL hop-by-hop discovery | [SVG](10_Internet_Control_Message_Protocol_ICMP/diagrams/icmp_messages_and_traceroute_ttl.svg) • [PDF](10_Internet_Control_Message_Protocol_ICMP/10_Internet_Control_Message_Protocol_ICMP.pdf) |
| **11** | [Distance Vector Routing & Count-to-Infinity](11_Distance_Vector_Routing_and_Count_to_Infinity/) | Bellman-Ford algorithm, RIP periodic updates, Count-to-Infinity problem, Split Horizon, Poison Reverse | [SVG](11_Distance_Vector_Routing_and_Count_to_Infinity/diagrams/distance_vector_count_to_infinity.svg) • [PDF](11_Distance_Vector_Routing_and_Count_to_Infinity/11_Distance_Vector_Routing_and_Count_to_Infinity.pdf) |
| **12** | [Link State Routing & Dijkstra Algorithm](12_Link_State_Routing_and_Dijkstra_Algorithm/) | OSPF / IS-IS, 5 phases, LSP reliable flooding, Dijkstra Shortest Path Tree computation, DVR vs LSR | [SVG](12_Link_State_Routing_and_Dijkstra_Algorithm/diagrams/link_state_routing_and_dijkstra.svg) • [PDF](12_Link_State_Routing_and_Dijkstra_Algorithm/12_Link_State_Routing_and_Dijkstra_Algorithm.pdf) |
| **13** | [Path Vector, Hierarchical Routing & BGP](13_Path_Vector_Hierarchical_Routing_and_BGP/) | Inter-domain AS routing, BGP-4, AS-PATH attribute, Loop discard rule, Kamoun-Klein Hierarchical Clustering | [SVG](13_Path_Vector_Hierarchical_Routing_and_BGP/diagrams/path_vector_and_bgp_architecture.svg) • [PDF](13_Path_Vector_Hierarchical_Routing_and_BGP/13_Path_Vector_Hierarchical_Routing_and_BGP.pdf) |
| **14** | [Congestion Control, QoS & AKTU PYQs](14_Congestion_Control_QoS_and_Unit_3_AKTU_PYQs/) | Open vs Closed-loop, Leaky Bucket constant rate vs Token Bucket burst formula ($T = C/(M-R)$), AKTU PYQs | [SVG](14_Congestion_Control_QoS_and_Unit_3_AKTU_PYQs/diagrams/congestion_control_and_leaky_bucket.svg) • [PDF](14_Congestion_Control_QoS_and_Unit_3_AKTU_PYQs/14_Congestion_Control_QoS_and_Unit_3_AKTU_PYQs.pdf) |

---

## Pedagogical Design Highlights
1. **100% Handcrafted XML Vector SVGs:** Every single diagram is an error-free, responsive SVG rendered cleanly across web and print.
2. **Bilingual Hinglish Explanations:** Core intuition explained in lucid Hinglish, supplemented by strict English technical definitions for exams.
3. **Solved Numericals with Derivations:** Step-by-step mathematical procedures for Fragmentation, Subnetting, CIDR, Dijkstra, and Token Bucket.
4. **Verified 3-Page Cheat Sheet:** Compact summary engineered to fit on exactly 3 A4 pages for last-minute exam recall.
