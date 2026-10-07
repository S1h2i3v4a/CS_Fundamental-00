# Module 14: Bridges, Switches, Spanning Tree Protocol (STP) & Unit 2 AKTU PYQs

## 1. Connecting Devices at Data Link Layer
Network devices unke operating OSI layer ke according classify hote hain:
- **Repeater / Hub (Layer 1 - Physical):** Sirf electrical signals regenerate karte hain. Collision domain ko split nahi karte.
- **Bridge / Switch (Layer 2 - Data Link):** MAC addresses examine karte hain. Har port ka apna dedicated **Collision Domain** hota hai, jisse network performance dramatically increase hoti hai!
- **Router (Layer 3 - Network):** IP addresses examine karte hain aur **Broadcast Domains** ko split karte hain.

```
Device Hierarchy Comparison:
+-------------------+---------------+-------------------+--------------------+
| Device            | OSI Layer     | Collision Domains | Broadcast Domains  |
+-------------------+---------------+-------------------+--------------------+
| Hub / Repeater    | Layer 1       | 1 (Shared by all) | 1 (Shared by all)  |
| Bridge / Switch   | Layer 2       | 1 per port (Split)| 1 (Shared by all)  |
| Router            | Layer 3       | 1 per port (Split)| 1 per port (Split) |
+-------------------+---------------+-------------------+--------------------+
```

---

## 2. Transparent Learning Bridges
Ek bridge transparent tab kehlata hai jab stations ko uski existence ke baare me kuch pata na ho (plug-and-play).

### 2.1 Forwarding Database (MAC Table) Learning Algorithm:
Jab bhi Bridge ke port $X$ par koi frame aata hai:
1. **LEARN (Source MAC Analysis):**
   - Bridge incoming frame ke **Source MAC Address** aur arrival port $X$ ko apni table me record kar leta hai (or refreshes its aging timer).
2. **FORWARD / FILTER (Destination MAC Analysis):**
   - **Case A (Known on another port):** Destination MAC address table me maujood hai aur port $Y$ ($Y \ne X$) par mapped hai $\implies$ Bridge frame ko **strictly port $Y$ par forward** karta hai.
   - **Case B (Known on same port):** Destination MAC address table me maujood hai aur usi port $X$ par hai $\implies$ Bridge frame ko **FILTER (Drop)** kar deta hai kyunki recipient usi segment me hai aur usne frame directly sun liya hai!
   - **Case C (Unknown MAC or Broadcast):** Destination MAC table me nahi hai $\implies$ Bridge frame ko arrival port $X$ ko chhodkar **baaki sabhi ports par FLOOD** kar deta hai!

---

## 3. Bridging Loops and Broadcast Storms
Redundancy aur reliability ke liye network administrators aksar switches ke beech multiple parallel cables connect kar dete hain. Lekin loops ke karan teen dangerous problems paida hoti hain:
1. **Broadcast Storm:** Jab koi host broadcast packet bhejta hai (e.g., ARP request), to switches use infinite loop me flood karte rehte hain. Network traffic 100% saturate ho jata hai aur switch crash ho jata hai.
2. **Multiple Frame Copies:** Destination host ko ek hi frame ki hazaron duplicate copies milti hain.
3. **MAC Table Instability:** Frame loop me ghoomne ke karan switch ki MAC table me station ki port mapping har millisecond flip-flop hoti rehti hai.

---

## 4. Spanning Tree Protocol (STP - IEEE 802.1D)
Radia Perlman dwara design kiya gaya **Spanning Tree Protocol (STP)** graph theory ka use karke physically redundant loopy network ko logically **Loop-Free Tree** me convert kar deta hai.

### 4.1 The 4-Step STP Algorithm:

#### Step 1: Root Bridge Election
- Pure network me sabse lowest **Bridge ID (BID)** wale switch ko **Root Bridge** elect kiya jata hai.
  $$\text{Bridge ID (BID)} = \text{Priority (2 Bytes, default 32768)} + \text{MAC Address (6 Bytes)}$$
- Sabse low MAC address wala switch Root Bridge ban jata hai.

#### Step 2: Root Port (RP) Selection on Non-Root Bridges
- Har non-root switch par exactly **1 Root Port** select hota hai.
- Root Port wo port hota hai jiska Root Bridge tak **Cumulative Path Cost sabse kam** ho.

#### Step 3: Designated Port (DP) Selection on Each Segment
- Har network segment/link par exactly **1 Designated Port** select hota hai.
- Link ke dono switches me se jiska Root Bridge tak cost kam ho, uska port DP banta hai. Root Bridge ke saare active ports hamesha DP hote hain!

#### Step 4: Block Alternate Ports
- Saare remaining ports jo na Root Port bane aur na hi Designated Port bane, unhe **BLOCKING / DISCARDING State** me daal diya jata hai.
- Yeh blocked ports data traffic stop kar dete hain, jisse loop break ho jata hai! Agar koi active link tut jaye, to STP blocked port ko automatically unblock karke network restore kar deta hai.

### 4.2 STP Port States:
$$\text{Blocking} \xrightarrow{20\text{s}} \text{Listening} \xrightarrow{15\text{s}} \text{Learning} \xrightarrow{15\text{s}} \text{Forwarding}$$

---

## 5. Comprehensive AKTU BCS603 Unit 2 Previous Year Questions & Model Answers

### Question 1: Framing and Stuffing (AKTU 2022-23, 10 Marks)
> **Problem:** What is framing? Explain Character (Byte) stuffing and Bit stuffing with suitable examples. A bit stream `011111101111110` is transmitted. Show the output after bit stuffing.

**Answer Summary:**
- **Framing:** Physical layer ke continuous raw bit stream ko discrete manageable data units me divide karna.
- **Bit Stuffing (5-Ones Rule):** Whenever sender detects five consecutive `1`s (`11111`) in data, it automatically inserts a `0` bit after them to prevent confusion with FLAG (`01111110`).
- **Input Stream:** `0 1 1 1 1 1 1 0 1 1 1 1 1 1 0`
- **After 5th One:**
  1. First pattern: `011111` $\to$ Stuffs `0` $\to$ `011111 0 10...`
  2. Second pattern: `11111` $\to$ Stuffs `0` $\to$ `...11111 0 10`
- **Output Bit Stream:** `01111101011111010`

---

### Question 2: ALOHA Throughput Derivation (AKTU 2021-22, 2023-24, 10 Marks)
> **Problem:** Derive the throughput expression for Pure ALOHA and Slotted ALOHA. Why is Slotted ALOHA twice as efficient as Pure ALOHA?

**Answer Summary:**
- Let $G$ = Average number of frames generated per frame transmission time $T_{fr}$.
- Pure ALOHA vulnerable window = $2 \cdot T_{fr}$. Probability of zero collisions in $2 \cdot T_{fr}$ under Poisson distribution: $P(0) = e^{-2G}$.
  $$\mathbf{S_{pure} = G \cdot e^{-2G}} \implies S_{max} = \frac{1}{2e} \approx \mathbf{18.4\%} \quad (\text{at } G = 0.5)$$
- Slotted ALOHA vulnerable window is restricted to exactly $1 \cdot T_{fr}$. Probability of zero collisions: $P(0) = e^{-G}$.
  $$\mathbf{S_{slotted} = G \cdot e^{-G}} \implies S_{max} = \frac{1}{e} \approx \mathbf{36.8\%} \quad (\text{at } G = 1.0)$$
- Slotted ALOHA vulnerable window ko half kar deta hai ($2 T_{fr} \to 1 T_{fr}$), isliye throughput exactly **double** ho jata hai!

---

### Question 3: CSMA/CD Minimum Frame Size Derivation (AKTU 2022-23, 10 Marks)
> **Problem:** Explain CSMA/CD protocol. Prove the condition $T_t \ge 2 T_p$ and derive the minimum 64-byte frame size in Ethernet.

**Answer Summary:**
*(See detailed mathematical derivation in Module 04 & Module 12)*:
- Sender worst-case me collision notice karne ke liye transmit kar raha hona chahiye: $T_t \ge 2 T_p$.
- Round trip time in 2500m coax + 4 repeaters = $51.2\ \mu\text{s}$.
- $L_{min} = 51.2\ \mu\text{s} \times 10\ \text{Mbps} = 512\ \text{bits} = \mathbf{64\ \text{Bytes}}$.

---

### Question 4: Sliding Window Window Sizing Proof (AKTU 2020-21, 2022-23, 10 Marks)
> **Problem:** Explain Go-Back-N and Selective Repeat ARQ. Prove that $W_S \le 2^m - 1$ for GBN and $W_S \le 2^{m-1}$ for Selective Repeat.

**Answer Summary:**
*(See formal mathematical proofs and counter-examples in Module 08 and Module 09)*:
- GBN: $W_S + W_R \le 2^m$. Since $W_R = 1 \implies W_S \le 2^m - 1$.
- Selective Repeat: $W_S + W_R \le 2^m$. Since $W_R = W_S \implies 2 W_S \le 2^m \implies W_S \le 2^{m-1}$.
