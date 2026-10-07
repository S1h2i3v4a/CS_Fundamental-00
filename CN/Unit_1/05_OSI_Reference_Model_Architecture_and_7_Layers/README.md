# Module 05: OSI Reference Model Architecture & 7 Layers

## 1. Introduction to the OSI Model
OSI (**Open Systems Interconnection**) model ko **ISO** (International Organization for Standardization) ne 1984 me develop kiya tha (ISO standard 7498).
- Yeh ek **Theoretical Reference Model** hai jo yeh describe karta hai ki kisi network me alag-alag systems ke beech application programs aapas me kaise communicate karenge.
- Isme **7 distinct layers** hoti hain. Har layer ek specific well-defined task perform karti hai aur apne adjacent layers ko services deti hai.
- **Mnemonic to memorize 7 layers:**
  - *Bottom to Top (1 to 7):* **P**lease **D**o **N**ot **T**ouch **S**teve's **P**et **A**lligators (Physical, Data Link, Network, Transport, Session, Presentation, Application).
  - *Top to Bottom (7 to 1):* **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing.

---

## 2. 7 Layers ka Deep Dive & Primary Functions

### Layer 1: Physical Layer
- **Responsibility:** Transmission medium ke upar individual raw bits (`0` aur `1`) ka transmission.
- **Key Functions:**
  1. *Physical characteristics of interfaces and medium:* Cable type, connector pin configuration (RJ-45).
  2. *Representation of bits:* Bits ko electrical signals (voltage), optical pulses (light), ya electromagnetic waves me convert karna (Line coding / Modulation).
  3. *Data rate (Transmission rate):* Number of bits sent per second (bps).
  4. *Synchronization of bits:* Sender aur receiver clock synchronization.
  5. *Line configuration:* Point-to-point ya multipoint link.
  6. *Physical topology:* Mesh, Star, Bus, Ring.
  7. *Transmission mode:* Simplex, Half-duplex, ya Full-duplex.
- **PDU:** Bits.
- **Devices:** Repeaters, Hubs, Cables, Modems.

### Layer 2: Data Link Layer (DLL)
- **Responsibility:** Unreliable physical link ko ek completely error-free link me transform karna; **Hop-to-Hop (Node-to-Node)** frame delivery.
- **Sub-layers:** LLC (Logical Link Control - 802.2) aur MAC (Medium Access Control - 802.3/802.11).
- **Key Functions:**
  1. *Framing:* Network layer ke packets ko manageable data units (Frames) me divide karna (Flag bytes, Bit/Byte stuffing).
  2. *Physical Addressing (MAC):* 48-bit hardware MAC address add karna (Sender MAC aur Receiver MAC).
  3. *Flow Control:* Fast sender ko slow receiver ko overwhelm karne se rokna (Stop-and-Wait, Sliding Window).
  4. *Error Control:* Damaged ya lost frames detect/retransmit karna (CRC, Checksum, ARQ).
  5. *Access Control:* Shared multipoint channel par kis device ka right to transmit hai yeh decide karna (CSMA/CD, Token Passing).
- **PDU:** Frame.
- **Devices:** Bridge, Layer-2 Switch, NIC.

### Layer 3: Network Layer
- **Responsibility:** **Source-to-Destination (Host-to-Host)** packet delivery across multiple independent networks (Internetworking).
- **Key Functions:**
  1. *Logical Addressing:* Universal globally unique IP address add karna (IPv4 / IPv6 header).
  2. *Routing:* Source se destination tak packet pahunchane ke liye best physical route select karna (Dijkstra, Bellman-Ford, OSPF, BGP).
  3. *Packetizing & Fragmentation:* MTU limits exceed hone par packets ko divide karna.
- **PDU:** Packet / Datagram.
- **Devices:** Router, Layer-3 Switch.

### Layer 4: Transport Layer ("The Heart of OSI")
- **Responsibility:** **End-to-End (Process-to-Process)** message delivery between running application programs.
- **Key Functions:**
  1. *Port Addressing (Service Point Addressing):* Specific application process identify karna (Port numbers 0 to 65535).
  2. *Segmentation & Reassembly:* Message ko smaller segments me todna aur destination par sequence number se assemble karna.
  3. *Connection Control:* Connection-Oriented (TCP - 3-way handshake) ya Connectionless (UDP).
  4. *End-to-End Flow Control:* Sliding window buffer matching across the entire network path.
  5. *End-to-End Error Control:* Lossless delivery guarantee.
- **PDU:** Segment (TCP) / User Datagram (UDP).

### Layer 5: Session Layer
- **Responsibility:** Communication devices ke beech session (dialogue) establish, maintain aur synchronize karna.
- **Key Functions:**
  1. *Dialog Controller:* Half-duplex ya full-duplex mode me conversation allow karna.
  2. *Synchronization & Checkpointing:* Lambe file transfers me checkpoints insert karna. (Agar 1000 pages transfer ho rahe hain aur page 520 par crash ho jaye, to retransmission sirf page 501 se start hoga).

### Layer 6: Presentation Layer ("Syntax / Translation Layer")
- **Responsibility:** Transmit ho rahe data ke syntax aur semantics ko handle karna.
- **Key Functions:**
  1. *Translation / Encoding:* Heterogeneous systems ke character codes match karna (e.g., EBCDIC to ASCII).
  2. *Encryption & Decryption:* Security/Privacy maintain karna (Cipher text conversion: SSL/TLS, AES, RSA).
  3. *Compression:* Bits count reduce karna taaki bandwidth optimize ho sake (Lossless vs Lossy: JPEG, MP3, GZIP).

### Layer 7: Application Layer
- **Responsibility:** End-user applications aur operating system services ko direct network access provide karna.
- **Key Functions:**
  1. *Network Virtual Terminal (NVT):* Remote host login (TELNET, SSH).
  2. *File Transfer, Access, and Management (FTAM / FTP).*
  3. *Mail Services:* Email forwarding aur storage (SMTP, POP3, IMAP).
  4. *Directory Services:* Distributed database access (DNS, LDAP).
- **PDU:** Data / Message.

---

## 3. Encapsulation & Decapsulation Process

```
[Application Layer]       Data
                               ↓
[Presentation Layer]     H6 + Data
                               ↓
[Session Layer]          H5 + H6 + Data
                               ↓
[Transport Layer]        H4 + H5 + H6 + Data                     ==> SEGMENT (Port Added)
                               ↓
[Network Layer]          H3 + [Segment]                          ==> PACKET (IP Added)
                               ↓
[Data Link Layer]        H2 + [Packet] + T2 (CRC)                ==> FRAME (MAC Added)
                               ↓
[Physical Layer]         1 0 1 0 0 1 1 0 1 1 0 1                 ==> BITS (On Medium)
```

- **Note on Trailer ($T_2$):** Data link layer akeli aisi layer hai jo **Header ($H_2$)** ke sath **Trailer ($T_2$)** bhi append karti hai. Trailer me CRC (Cyclic Redundancy Check) checksum hota hai jo hardware level par bit errors detect karta hai.
