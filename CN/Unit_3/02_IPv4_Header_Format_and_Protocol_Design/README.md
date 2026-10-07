# Module 02: IPv4 Header Format & Protocol Architecture

## 1. The IPv4 Datagram Architecture
Internet Protocol version 4 (**IPv4**) unreliable, connectionless packet delivery service provide karta hai. Datagram me do parts hote hain: **Header** (20 to 60 Bytes) aur **Payload Data** (up to 65,515 Bytes).

```
+-------------------------------------------------------------------------+
| IPv4 Header: 20 to 60 Bytes (5 to 15 32-bit words)                     |
+-------------------------------------------------------------------------+
| Payload Data: Up to (65,535 - Header Length) Bytes                      |
+-------------------------------------------------------------------------+
```

---

## 2. Field-by-Field Header Breakdown (32-Bit Rows)

### Row 1: Basic Identifiers
1. **Version (VER - 4 Bits):** Protocol version number batata hai. IPv4 ke liye value hamesha binary `0100` ($4$) hoti hai.
2. **Header Length (HLEN - 4 Bits):**
   - Header length ko **4-Byte words (32-bit units)** me measure kiya jata hai.
   - **Formula:**
     $$	ext{Actual Header Length (Bytes)} = 	ext{HLEN} 	imes 4$$
   - **Minimum HLEN:** $5 \implies 5 	imes 4 = 20	ext{ Bytes}$ (Jab koi Options na ho).
   - **Maximum HLEN:** $15 \implies 15 	imes 4 = 60	ext{ Bytes}$ (Maximum 40 bytes of Options).
3. **Type of Service / DSCP (ToS - 8 Bits):** Quality of Service (QoS), delay, throughput, reliability preferences specify karta hai.
4. **Total Length (16 Bits):**
   - Header + Data ka total length in bytes.
   - Maximum theoretical size = $2^{16} - 1 = \mathbf{65,535\ 	ext{Bytes}}$.
   - **Payload Data Size:**
     $$	ext{Data Length} = 	ext{Total Length} - (	ext{HLEN} 	imes 4)$$

---

### Row 2: Fragmentation Controls
5. **Identification (16 Bits):** Source host dwara assign kiya gaya unique integer jo original unfragmented datagram ke saare fragments ko identify karta hai.
6. **Flags (3 Bits):**
   - **Bit 0 (Reserved):** Hamesha `0` hona chahiye.
   - **Bit 1 (DF - Don't Fragment):** Agar `DF = 1`, to router ko datagram fragment karne ki permission nahi hai. Agar packet MTU se bada ho, to packet drop ho jata hai aur ICMP *Fragmentation Needed* error return hota hai.
   - **Bit 2 (MF - More Fragments):** Agar `MF = 1`, iska matlab aage aur fragments aane baaki hain. Agar `MF = 0`, iska matlab yeh **aakhiri (last) fragment** hai (ya packet fragment hi nahi hua).
7. **Fragment Offset (13 Bits):**
   - Batata hai ki yeh fragment original datagram ke data stream me kis byte position se shuru hota hai.
   - **Scale Factor 8:** Kyunki offset field sirf 13 bits ($2^{13} = 8192$) ki hai jabki Total Length 65,535 bytes ho sakti hai, isliye offset ko **8-byte units** me measure kiya jata hai:
     $$\mathbf{	ext{Fragment Offset Value} = rac{	ext{Byte Offset}}{8}}$$

---

### Row 3: Routing Controls & Integrity
8. **Time to Live (TTL - 8 Bits):**
   - Infinite looping packets ko network me survive hone se rokata hai.
   - Har intermediate router jab packet ko forward karta hai, to TTL ko **1 se decrement** karta hai:
     $$	ext{TTL}_{new} = 	ext{TTL}_{old} - 1$$
   - Agar $	ext{TTL} == 0$ ho jaye, to router packet ko discard kar deta hai aur source ko **ICMP Time Exceeded (Type 11)** message bhej deta hai (`traceroute` isi TTL expiry mechanism ka use karta hai!).
9. **Protocol (8 Bits):** Upper Transport Layer protocol identify karta hai jisko payload deliver karna hai:
   - `1` $\implies$ **ICMP**
   - `2` $\implies$ **IGMP**
   - `6` $\implies$ **TCP**
   - `17` $\implies$ **UDP**
   - `89` $\implies$ **OSPF**
10. **Header Checksum (16 Bits):**
    - 16-bit 1's complement checksum jo **sirf header fields** ki transmission integrity protect karta hai (data payload transport layer TCP/UDP checksum dwara protect hota hai).
    - **Hop-by-Hop Recalculation:** Kyunki har router par TTL decrement hota hai, isliye **har intermediate router par Checksum recalculate karna mandatory hota hai**!

---

### Rows 4 & 5: Universal Addressing
11. **Source IP Address (32 Bits / 4 Bytes):** Original sending host ka universal logical address.
12. **Destination IP Address (32 Bits / 4 Bytes):** Ultimate receiving host ka universal logical address.

---

### Row 6: Options & Padding (0 to 40 Bytes)
13. **Options (Variable, up to 40 Bytes):** Network testing, debugging, aur security ke liye:
    - *Record Route:* Packet jis-jis router se guzra, unke IP addresses note karna.
    - *Strict Source Routing:* Sender exactly har intermediate router ka path specify karta hai.
    - *Loose Source Routing:* Packet specified routers se hokar zaroor guzrega, chahe beech me doosre routers bhi aa jayein.
    - *Timestamp:* Har router arrival time record karta hai.
14. **Padding:** Agar options ki length 32 bits (4 bytes) ki multiple na ho, to zeros add kiye jaate hain taaki total header length exactly 4-byte boundary par align ho.

---

## 3. AKTU Solved Numerical: Header Analysis & Data Extraction

> **Problem Statement (AKTU Semester Exam 10 Marks):**  
> An IPv4 packet arrives at a router with the first 8 bytes in hexadecimal representation given as:  
> `45 00 00 54 1A 2B 40 00`  
> 1. What is the version of IPv4?  
> 2. What is the header length in bytes? Are there any options present?  
> 3. What is the total length of the packet, and what is the payload data length?  
> 4. Can this packet be fragmented? Is this packet a fragment?

### Step-by-Step Solution:

#### Step 1: Byte 0 analysis (`0x45`):
- First nibble (`4`) = **Version** $\implies$ **IPv4**.
- Second nibble (`5`) = **HLEN** $\implies 5$.
- Header Length:
  $$	ext{Header Length} = 	ext{HLEN} 	imes 4 = 5 	imes 4 = \mathbf{20\ 	ext{Bytes}}$$
- Kyunki header length 20 bytes hai, **Options are NOT present** (Zero options).

#### Step 2: Bytes 2 & 3 analysis (`0x0054`):
- Total Length field = `0x0054` in hex.
- Converting to decimal:
  $$	ext{Total Length} = (5 	imes 16^1) + (4 	imes 16^0) = 80 + 4 = \mathbf{84\ 	ext{Bytes}}$$
- Payload Data Length:
  $$	ext{Data Length} = 	ext{Total Length} - 	ext{Header Length} = 84 - 20 = \mathbf{64\ 	ext{Bytes}}$$

#### Step 3: Bytes 6 & 7 analysis (`0x4000`):
- In binary: `0x4000` = `0100 0000 0000 0000`
- First 3 bits are **Flags**:
  - Bit 0 = `0` (Reserved)
  - Bit 1 = `1` (**DF Flag = 1**) $\implies$ **Don't Fragment!** Packet CANNOT be fragmented.
  - Bit 2 = `0` (**MF Flag = 0**) $\implies$ No more fragments.
- Remaining 13 bits are **Fragment Offset**:
  - Offset = `0000000000000` = `0`.
- **Conclusion:** Yeh packet fragment nahi hai, original whole unfragmented packet hai, aur router ise fragment nahi kar sakta.
