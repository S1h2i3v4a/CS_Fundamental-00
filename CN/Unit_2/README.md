# Unit 2: Data Link Layer & Medium Access Sublayer

## 📚 Course & Curriculum Context
- **Subject:** Computer Networks (BCS603)
- **University:** Dr. A.P.J. Abdul Kalam Technical University (AKTU) & GATE CS Curriculum
- **Lectures Reference:** Gateway Classes by Dr. Nidhi Parashar Ma'am (Lectures 1 to 11, 259 Slides)
- **Architecture Standard:** 15 Modular Sequential Subfolders (`00_` to `14_`), Handcrafted XML Vector SVGs, In-depth Bilingual Hinglish Notes, Solved Numericals & AKTU Previous Year Questions.

---

## 📑 Complete Module Index & Direct Links

| Module | Topic Title | Core Focus & AKTU Syllabus Scope | Vector Diagram | PDF Chapter |
| :---: | :--- | :--- | :---: | :---: |
| **00** | [**Quick Revision Short Notes**](00_Quick_Revision_Short_Notes/) | **Exact 3-Page Verified Formula Sheet** for Exam Revision | — | [3-Page PDF](00_Quick_Revision_Short_Notes/00_Quick_Revision_Short_Notes.pdf) |
| **01** | [**DLL Foundations & Framing**](01_Data_Link_Layer_Foundations_and_Framing/) | DLL Services, LLC 802.2 vs MAC, Byte Stuffing (ESC) & Bit Stuffing (5-ones rule) | [framing.svg](01_Data_Link_Layer_Foundations_and_Framing/diagrams/framing_byte_and_bit_stuffing.svg) | [Chapter PDF](01_Data_Link_Layer_Foundations_and_Framing/01_Data_Link_Layer_Foundations_and_Framing.pdf) |
| **02** | [**Random Access: Pure & Slotted ALOHA**](02_Random_Access_Protocols_Pure_and_Slotted_ALOHA/) | Pure ALOHA ($S = Ge^{-2G}$, 18.4%), Slotted ALOHA ($S = Ge^{-G}$, 36.8%), Vulnerable Time | [aloha.svg](02_Random_Access_Protocols_Pure_and_Slotted_ALOHA/diagrams/aloha_pure_vs_slotted.svg) | [Chapter PDF](02_Random_Access_Protocols_Pure_and_Slotted_ALOHA/02_Random_Access_Protocols_Pure_and_Slotted_ALOHA.pdf) |
| **03** | [**CSMA & Persistence Strategies**](03_Carrier_Sense_Multiple_Access_CSMA_and_Persistence/) | 1-Persistent, Non-Persistent, p-Persistent Strategies & Propagation Delay Collision Window | [csma.svg](03_Carrier_Sense_Multiple_Access_CSMA_and_Persistence/diagrams/csma_persistence_methods.svg) | [Chapter PDF](03_Carrier_Sense_Multiple_Access_CSMA_and_Persistence/03_Carrier_Sense_Multiple_Access_CSMA_and_Persistence.pdf) |
| **04** | [**CSMA with Collision Detection (CSMA/CD)**](04_CSMA_with_Collision_Detection_CSMA_CD/) | "Listen While Talk", Jam Signal, Binary Exponential Backoff & $T_t \ge 2T_p$ Derivation | [csma_cd.svg](04_CSMA_with_Collision_Detection_CSMA_CD/diagrams/csma_cd_architecture.svg) | [Chapter PDF](04_CSMA_with_Collision_Detection_CSMA_CD/04_CSMA_with_Collision_Detection_CSMA_CD.pdf) |
| **05** | [**CSMA with Collision Avoidance (CSMA/CA)**](05_CSMA_with_Collision_Avoidance_CSMA_CA/) | Wireless LANs, Hidden/Exposed Stations, IFS (SIFS, PIFS, DIFS), RTS/CTS & NAV Virtual Sensing | [csma_ca.svg](05_CSMA_with_Collision_Avoidance_CSMA_CA/diagrams/csma_ca_and_rts_cts.svg) | [Chapter PDF](05_CSMA_with_Collision_Avoidance_CSMA_CA/05_CSMA_with_Collision_Avoidance_CSMA_CA.pdf) |
| **06** | [**Controlled Access & Channelization**](06_Controlled_Access_and_Channelization_Protocols/) | Reservation, Polling, Token Passing, FDMA, TDMA & CDMA Orthogonal Walsh Codes | [cdma.svg](06_Controlled_Access_and_Channelization_Protocols/diagrams/controlled_access_and_cdma.svg) | [Chapter PDF](06_Controlled_Access_and_Channelization_Protocols/06_Controlled_Access_and_Channelization_Protocols.pdf) |
| **07** | [**Flow Control & Stop-and-Wait ARQ**](07_Flow_Control_Foundations_and_Stop_and_Wait_ARQ/) | Timer Timeouts, 1-Bit Sequence Numbering, Efficiency Derivation $\eta = rac{1}{1+2a}$ | [stop_wait.svg](07_Flow_Control_Foundations_and_Stop_and_Wait_ARQ/diagrams/stop_and_wait_arq_efficiency.svg) | [Chapter PDF](07_Flow_Control_Foundations_and_Stop_and_Wait_ARQ/07_Flow_Control_Foundations_and_Stop_and_Wait_ARQ.pdf) |
| **08** | [**Sliding Window: Go-Back-N ARQ**](08_Sliding_Window_Protocols_Go_Back_N_ARQ/) | Pipelining, $W_S = 2^m - 1$, $W_R = 1$, Cumulative ACKs, Window Sizing Proof & Retransmit-N | [gobackn.svg](08_Sliding_Window_Protocols_Go_Back_N_ARQ/diagrams/gobackn_sliding_window_arq.svg) | [Chapter PDF](08_Sliding_Window_Protocols_Go_Back_N_ARQ/08_Sliding_Window_Protocols_Go_Back_N_ARQ.pdf) |
| **09** | [**Sliding Window: Selective Repeat ARQ**](09_Sliding_Window_Protocols_Selective_Repeat_ARQ/) | Out-of-Order Receiver Buffers, NAK Selective Reject, $W_S = W_R = 2^{m-1}$ Formal Proof | [selective_repeat.svg](09_Sliding_Window_Protocols_Selective_Repeat_ARQ/diagrams/selective_repeat_arq_buffers.svg) | [Chapter PDF](09_Sliding_Window_Protocols_Selective_Repeat_ARQ/09_Sliding_Window_Protocols_Selective_Repeat_ARQ.pdf) |
| **10** | [**Error Detection: Parity, Checksum & CRC**](10_Error_Detection_Parity_Checksum_and_CRC/) | Single/Burst Errors, 2D Parity, 1's Complement Internet Checksum, Modulo-2 CRC Division | [crc.svg](10_Error_Detection_Parity_Checksum_and_CRC/diagrams/crc_polynomial_division_process.svg) | [Chapter PDF](10_Error_Detection_Parity_Checksum_and_CRC/10_Error_Detection_Parity_Checksum_and_CRC.pdf) |
| **11** | [**Error Correction & Hamming Code**](11_Error_Correction_and_Hamming_Code/) | Hamming Distance, Redundancy Inequality $2^r \ge m+r+1$, Hamming (7, 4) Syndrome Decoding | [hamming.svg](11_Error_Correction_and_Hamming_Code/diagrams/hamming_code_syndrome_architecture.svg) | [Chapter PDF](11_Error_Correction_and_Hamming_Code/11_Error_Correction_and_Hamming_Code.pdf) |
| **12** | [**IEEE 802 Standards & Ethernet (802.3)**](12_IEEE_802_LAN_Standards_and_Ethernet_802_3/) | Standard Ethernet Frame, 64-Byte Minimum Frame Size Derivation, 48-Bit MAC Anatomy | [ethernet.svg](12_IEEE_802_LAN_Standards_and_Ethernet_802_3/diagrams/ethernet_frame_format_and_standards.svg) | [Chapter PDF](12_IEEE_802_LAN_Standards_and_Ethernet_802_3/12_IEEE_802_LAN_Standards_and_Ethernet_802_3.pdf) |
| **13** | [**Token Bus, Token Ring & FDDI**](13_Token_Bus_Token_Ring_and_FDDI_Architecture/) | MSAU Wiring, Active Monitor, FDDI Dual Counter-Rotating Ring & Self-Healing Loopback | [token_ring.svg](13_Token_Bus_Token_Ring_and_FDDI_Architecture/diagrams/token_ring_and_fddi_dual_ring.svg) | [Chapter PDF](13_Token_Bus_Token_Ring_and_FDDI_Architecture/13_Token_Bus_Token_Ring_and_FDDI_Architecture.pdf) |
| **14** | [**Bridges, Switches, STP & AKTU PYQs**](14_Bridges_Switches_STP_and_Unit_2_AKTU_PYQs/) | Transparent Learning Bridge, Collision Domains, Spanning Tree Protocol (STP 802.1D) & PYQs | [stp.svg](14_Bridges_Switches_STP_and_Unit_2_AKTU_PYQs/diagrams/transparent_bridge_and_spanning_tree.svg) | [Chapter PDF](14_Bridges_Switches_STP_and_Unit_2_AKTU_PYQs/14_Bridges_Switches_STP_and_Unit_2_AKTU_PYQs.pdf) |

---

## 📦 Consolidated Master Downloads
- 📕 [**Unit_2_Master_Notes.pdf**](Unit_2_Master_Notes.pdf) — Complete consolidated master book containing all 15 chapters with Table of Contents bookmark outlines.
- ⚡ [**Unit_2_Quick_Revision_3_Page_Notes.pdf**](Unit_2_Quick_Revision_3_Page_Notes.pdf) — Exact 3-page verified exam revision cheat sheet.
