# Module 14: Network Devices, Components & Unit 1 AKTU PYQs

## 1. Network Devices ka Complete Layer-Wise Classification

| Device | Operating OSI Layer | Addressing Used | Function / Role | Collision Domains | Broadcast Domains |
| :--- | :--- | :--- | :--- | :---: | :---: |
| **Repeater** | Layer 1 (Physical) | None (Raw bits) | Regenerates attenuated electrical/optical signals over long cables. | 1 (Shared) | 1 (Shared) |
| **Hub** | Layer 1 (Physical) | None (Blind broadcast) | Multi-port repeater. Incoming bit stream ko sabhi output ports par blind copy karta hai. | 1 (Shared) | 1 (Shared) |
| **Bridge** | Layer 2 (Data Link) | 48-bit MAC Address | Connects 2 LAN segments. Filters frames using software MAC table. | 2 (1 per port) | 1 (Shared) |
| **Switch** | Layer 2 (Data Link) | 48-bit MAC Address | Multi-port bridge with dedicated hardware (ASIC CAM table). Full-duplex microsegmentation. | **$N$ (1 per port)** | 1 (Shared) |
| **Router** | Layer 3 (Network) | 32-bit / 128-bit IP | Routes packets between different networks using Routing Tables (FIB). | **$N$ (1 per port)** | **$N$ (1 per port)** |
| **Gateway** | Layer 4 - 7 (All Layers) | Application protocol | Translates between completely incompatible protocol architectures (e.g., AppleTalk to TCP/IP). | Separate | Separate |
| **Modem** | Physical Layer | Carrier analog frequencies | **MO**dulator / **DEM**odulator (Digital bits $\leftrightarrow$ Analog voice line). | 1 | 1 |
| **Brouter** | Layer 2 & 3 | MAC & IP | Bridge + Router hybrid. Routes routable protocols (IP) aur bridges non-routable protocols (NetBIOS). | $N$ | $N$ for IP |

---

## 2. Collision Domain vs Broadcast Domain (Concept & Formulas)

### 2.1 Collision Domain
- Network ka wo physical segment jahan agar do devices ek sath transmit karein, to unke electrical signals aapas me takra kar collide (corrupt) ho jayenge.
- **Hub:** Pura hub ek single collision domain hota hai ($1$).
- **Switch:** Har ek port ek independent collision domain hota hai ($N$ ports $\implies N$ collision domains).

### 2.2 Broadcast Domain
- Network ka wo region jahan kisi ek device dwara bheja gaya broadcast frame (`FF:FF:FF:FF:FF:FF`) us region ke sabhi hosts tak deliver hota hai.
- **Hub & Switch:** Broadcast frame ko aage flood kar dete hain $\implies$ Single broadcast domain banate hain.
- **Router:** By default broadcast packets ko aage forward **NAHI** karta (drop kar deta hai). Har router interface ek independent broadcast domain define karta hai!

---

## 3. AKTU Unit 1 Solved Past Year Questions (Comprehensive Bank)

### Question 1 (AKTU 2023-24, 10 Marks):
*Describe all the layers of the OSI model with a well-labeled diagram. Explain the working of Bridge.*

**Answer Summary:**
1. **OSI 7-Layer Architecture:** (Physical $	o$ DLL $	o$ Network $	o$ Transport $	o$ Session $	o$ Presentation $	o$ Application). Draw 7-layer stack with headers $H_7 \dots H_2$ and trailer $T_2$.
2. **Working of Bridge:**
   - Bridge Data Link layer (Layer 2) device hai jo do alag-alag physical LAN segments ko connect karta hai.
   - Yeh ek **MAC Address Table (Forwarding Database)** maintain karta hai jisme `[MAC Address, Port Number]` store hota hai.
   - **Forwarding / Filtering Logic:**
     - Jab frame port 1 par aata hai, bridge source MAC inspect karke apni table me learn karta hai (**Learning**).
     - Phir destination MAC ko table me look up karta hai:
       - Agar destination MAC usi port 1 par hai $\implies$ Frame ko **Filter** (discard) kar deta hai (segment 2 par traffic nahi bhejta).
       - Agar destination MAC port 2 par hai $\implies$ Frame ko **Forward** karta hai.
       - Agar destination MAC table me nahi hai $\implies$ Frame ko sabhi ports par **Flood** kar deta hai.

---

### Question 2 (AKTU 2023-24, 2 Marks):
*Define delivery in Network Layer vs Transport Layer.*

**Answer:**
- **Network Layer Delivery:** **Host-to-Host (Source-to-Destination)** delivery. Yeh packet ko source machine se destination machine tak pahunchata hai using Logical IP addresses.
- **Transport Layer Delivery:** **Process-to-Process (Port-to-Port)** delivery. Yeh packet ko destination machine ke andar running specific software process tak pahunchata hai using 16-bit Port numbers.

---

### Question 3 (AKTU 2022-23, 10 Marks):
*Construct the Polar NRZ-L and NRZ-I schemes for the following Data: 01001110.*

**Answer:**
- Complete verified waveform step-by-step drawn in Module 11 (NRZ-L levels: $+V, -V, +V, +V, -V, -V, -V, +V$; NRZ-I transitions on bit 1).

---

### Question 4 (AKTU 2021-22, 10 Marks):
*Define Datagram in switching. Differentiate between circuit switching and datagram switching.*

**Answer:**
- **Datagram Definition:** Packet switching me har individual independent packet ko Datagram kehte hain, jisme complete destination addressing hoti hai.
- **Differences:** Circuit switching dedicated physical path banata hai jabki datagram switching connectionless independent routing karta hai. Circuit switching zero store-and-forward delay deta hai jabki datagram switching maximum bandwidth utilization provide karta hai.
