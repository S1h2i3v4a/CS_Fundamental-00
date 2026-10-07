# Module 00: Ultra Quick Revision Short Notes (Exact 3-Page Cheat Sheet)

## Overview
Yeh 3-page ultra-dense verified formula aur concept sheet hai jo **Computer Networks Unit 2: Data Link Layer & Medium Access Sublayer (AKTU BCS603 / GATE CS)** ke pure syllabus ko exact 3 pages me summarize karti hai:

- **Page 1: Data Link Layer Foundations, Framing & Random Access Protocols**
  - DLL 5 Services, LLC 802.2 vs MAC decomposition
  - Framing: Character count, Byte stuffing (ESC), Bit stuffing (5-ones rule)
  - Pure ALOHA ($S = G e^{-2G}$, Max 18.4%) vs Slotted ALOHA ($S = G e^{-G}$, Max 36.8%)
  - CSMA Persistence: 1-Persistent, Non-Persistent, p-Persistent & Collision window
  - CSMA/CD: "Listen While Talk", Jam signal, Binary Exponential Backoff, $T_t \ge 2T_p$ derivation
  - CSMA/CA (802.11): Hidden/Exposed stations, IFS hierarchy (SIFS, PIFS, DIFS), RTS/CTS and NAV

- **Page 2: Controlled Access, CDMA & Flow Control ARQ Protocols**
  - Controlled Access: Reservation bitmap, Polling (Primary-Secondary), Token Passing (THT)
  - CDMA & Orthogonal Walsh Codes: $W_{2N} = [W_N, W_N; W_N, -W_N]$, data encoding & receiver dot product decoding
  - Stop-and-Wait ARQ: 1-bit sequence numbering, efficiency $\eta = rac{1}{1 + 2a}$ where $a = T_p/T_t$, satellite penalty
  - Go-Back-N ARQ: $W_S = 2^m - 1$, $W_R = 1$, cumulative ACKs, single timer, window sizing proof, optimal window $W_S \ge 1 + 2a$
  - Selective Repeat ARQ: $W_S = W_R = 2^{m-1}$, receiver out-of-order buffers, NAK, independent timers

- **Page 3: Error Detection, Error Correction, LAN Standards & Layer 2 Devices**
  - Error Detection: Simple parity vs 2D parity, Internet checksum (1's complement), Modulo-2 CRC polynomial division
  - Error Correction (FEC): Hamming distance theorems, redundancy inequality $2^r \ge m + r + 1$, Hamming (7, 4) syndrome decoding
  - IEEE 802.3 Ethernet: Complete 64 to 1518 byte frame format, 64-byte minimum frame size derivation, 48-bit MAC anatomy
  - Token Ring (802.5) & FDDI: MSAU star-ring, Active Monitor, FDDI dual counter-rotating self-healing ring, Timed Token Protocol
  - Layer 2 Devices: Transparent learning bridge (Learn, Forward, Filter, Flood), Collision vs Broadcast domains, Spanning Tree Protocol (STP 802.1D)

### PDF Downloads
- [00_Quick_Revision_Short_Notes.pdf](00_Quick_Revision_Short_Notes.pdf)
- [Unit_2_Quick_Revision_3_Page_Notes.pdf](../Unit_2_Quick_Revision_3_Page_Notes.pdf)
