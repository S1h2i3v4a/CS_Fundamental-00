# Module 12: IEEE 802 LAN Standards & Ethernet (IEEE 802.3)

## 1. The IEEE 802 LAN Architectural Model
IEEE ne OSI Data Link Layer ko do distinct sublayers me divide kiya:
1. **Logical Link Control (LLC - IEEE 802.2):**
   - Upper sublayer jo Network Layer ko uniform interface provide karta hai.
   - Flow control, error control, aur SAP (Service Access Point) multiplexing handle karta hai. Yeh underlying physical medium se independent hota hai.
2. **Medium Access Control (MAC - IEEE 802.3, 802.4, 802.5, 802.11):**
   - Lower sublayer jo actual physical transmission medium ke contention, framing, MAC addressing, aur CSMA/CD ko manage karta hai.

```
+-------------------------------------------------------+
| Network Layer (IP Protocol)                           |
+-------------------------------------------------------+
| Data Link Layer:                                      |
|   1. Logical Link Control (LLC - IEEE 802.2)          |
|   -------------------------------------------------   |
|   2. Medium Access Control (MAC Sublayer)             |
|      (802.3 Ethernet | 802.4 Token Bus | 802.5 Token) |
+-------------------------------------------------------+
| Physical Layer (Twisted Pair, Coaxial, Optical Fiber) |
+-------------------------------------------------------+
```

---

## 2. Standard Ethernet (IEEE 802.3) Frame Format
Ethernet frame me minimum 64 bytes aur maximum 1518 bytes hote hain (excluding Preamble aur SFD):

```
+----------+-----+----------+----------+----------+--------------------+---------+
| Preamble | SFD | Dest MAC | Src MAC  | Length/  | Data Payload       | FCS     |
| 7 Bytes  | 1 B | 6 Bytes  | 6 Bytes  | Type (2B)| (46 to 1500 Bytes) | (CRC 4B)|
+----------+-----+----------+----------+----------+--------------------+---------+
|<-- 8B Physical Layer Sync -->|<--------- 64 to 1518 Bytes MAC Frame ---------->|
```

### Field-by-Field Breakdown:
1. **Preamble (7 Bytes = 56 bits):** Alternating bit pattern `10101010...` jo receiver clock ko sender clock ke sath synchronize karne ke liye use hota hai.
2. **Start Frame Delimiter (SFD - 1 Byte = 8 bits):** Bit pattern `10101011`. Aakhiri do bits `11` indicate karti hain ki synchronization complete ho chuka hai aur agla byte Destination Address hai!
3. **Destination MAC Address (6 Bytes = 48 bits):** Receiving network interface card (NIC) ka hardware physical address.
4. **Source MAC Address (6 Bytes = 48 bits):** Sending NIC ka physical address.
5. **Length / EtherType (2 Bytes):**
   - If $\le 1500$: Length field (IEEE 802.3 standard), payload length batata hai.
   - If $\ge 1536$ ($0x0600$): Type field (Ethernet II standard), upper network protocol identify karta hai (e.g., `0x0800` for IPv4, `0x0806` for ARP).
6. **Data Payload (46 to 1500 Bytes):** Upper layer ka actual data.
   - **Padding:** Agar data 46 bytes se kam ho, to minimum 64-byte frame condition fulfill karne ke liye extra zero bits (`PAD`) add ki jati hain.
7. **Frame Check Sequence (FCS - 4 Bytes = 32 bits):** CRC-32 checksum error detection ke liye.

---

## 3. Mathematical Derivation: Why Exactly 64 Bytes Minimum Frame Size? (AKTU Core)

Yeh AKTU BCS603 semester exam ka 10-marks classic derivation question hai:

> **Derivation:** Prove why standard 10 Mbps Ethernet enforces a minimum frame size of 64 bytes (512 bits).

### Derivation Steps:
1. **CSMA/CD Fundamental Requirement:**  
   Sender collision detect tabhi kar sakta hai jab wo collision signal aane tak **khud wire par transmit kar raha ho**.
   $$\mathbf{T_t \ge 2 \cdot T_p} \implies \text{Transmission Time} \ge \text{Round Trip Time (Slot Time)}$$

2. **Network Geometry of 10Base5 (Thick Ethernet):**
   - Standard Ethernet specification allow karti hai maximum **5 segments** separated by **4 repeaters** (5-4-3 rule).
   - Maximum cable distance = $2500\text{ meters}$.
   - Propagation speed in copper coax cable $v \approx 2 \times 10^8\text{ m/s}$ ($200\text{ m/\mu s}$).
   - Cable propagation delay for 2500m:
     $$T_p = \frac{2500\text{ m}}{2 \times 10^8\text{ m/s}} = 12.5\ \mu\text{s}$$
   - Round trip propagation delay through cable:
     $$2 \cdot T_p = 25\ \mu\text{s}$$
   - 4 repeaters ka signal regeneration delay + station transceiver delays $\approx 26.2\ \mu\text{s}$.
   - **Worst-case Round Trip Time (Slot Time):**
     $$\text{Slot Time } (2 \cdot T_p) = 51.2\ \mu\text{s}$$

3. **Minimum Frame Size Calculation ($L_{min}$):**
   At 10 Mbps bandwidth ($B = 10 \times 10^6\text{ bps}$):
   $$L_{min} = T_t \times B \ge (2 \cdot T_p) \times B$$
   $$L_{min} = 51.2\ \mu\text{s} \times 10\ \text{Mbps} = (51.2 \times 10^{-6}\text{ s}) \times (10 \times 10^6\text{ bps})$$
   $$\mathbf{L_{min} = 512\ \text{Bits}}$$

   In Bytes:
   $$L_{min} = \frac{512\ \text{Bits}}{8\ \text{Bits/Byte}} = \mathbf{64\ \text{Bytes}}$$

4. **Payload Contribution:**
   Header + Trailer size:
   $$\text{Dest MAC (6) + Src MAC (6) + Type (2) + FCS (4)} = 18\ \text{Bytes}$$
   $$\text{Minimum Payload} = 64\ \text{Bytes} - 18\ \text{Bytes} = \mathbf{46\ \text{Bytes}}$$
   Agar application sirf 1 byte data bhejti hai, to Ethernet 45 bytes of padding add karke frame ko 64 bytes banata hai!

---

## 4. MAC Address Architecture (48-Bit / 6-Byte)
MAC address hexadecimal format me likha jata hai (e.g., `00:1A:2B:3C:4D:5E`):
- **First 24 Bits (OUI - Organizationally Unique Identifier):** IEEE dwara manufacturer (e.g., Intel, Cisco, Realtek) ko globally unique assign kiya jata hai.
- **Last 24 Bits (NIC Identifier):** Manufacturer har physical network card ko unique assign karta hai.
- **Addressing Types:**
  1. **Unicast:** Frame ek specific station ke liye hota hai (Byte 0 ki LSB bit = 0).
  2. **Multicast:** Frame ek group of stations ke liye hota hai (Byte 0 ki LSB bit = 1).
  3. **Broadcast:** Pura LAN receive karta hai (`FF:FF:FF:FF:FF:FF`, all 48 bits are 1s).

---

## 5. Evolution of Ethernet Standards

| Standard | IEEE Spec | Data Rate | Cable Type | Max Segment Length | Medium Access |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **10Base5** | 802.3 | 10 Mbps | Thick Coaxial | 500 meters | Half-Duplex CSMA/CD |
| **10Base2** | 802.3a | 10 Mbps | Thin Coaxial | 185 meters | Half-Duplex CSMA/CD |
| **10Base-T** | 802.3i | 10 Mbps | Cat3 UTP Twisted | 100 meters | Half/Full Duplex |
| **Fast Ethernet** | 802.3u | 100 Mbps | Cat5 UTP (100BaseTX)| 100 meters | Slot time reduced to 5.12 μs |
| **Gigabit Ethernet**| 802.3z/ab| 1000 Mbps | Cat5e/Fiber | 100m UTP / 5km Fiber| Carrier Extension (512B) |
| **10G Ethernet** | 802.3ae | 10 Gbps | Optical Fiber | Up to 40 km | **Full-Duplex ONLY (No CSMA/CD)** |
