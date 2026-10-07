# Module 03: IPv4 Fragmentation, Reassembly & Solved MTU Numericals

## 1. Why is Fragmentation Required?
Internetwork par different physical layer technologies ka Maximum Transmission Unit (**MTU**) alag-alag hota hai:
- **Ethernet 802.3 MTU:** $1500	ext{ Bytes}$
- **FDDI MTU:** $4352	ext{ Bytes}$
- **Point-to-Point Protocol (PPP) MTU:** $576	ext{ Bytes}$ or $1500	ext{ Bytes}$

Jab koi router bade MTU wale network se packet receive karke use chhote MTU wale link par forward karta hai, to pura packet physical frame me fit nahi ho sakta. Router us datagram ko multiple smaller units me divide karta hai jise **Fragmentation** kehte hain.

---

## 2. Core Fields Controlling Fragmentation

1. **Identification (16 Bits):**
   - Source host original datagram ko ek unique number assign karta hai (e.g., `14285`).
   - Jab packet fragment hota hai, to **saare fragments me exact same Identification number copy hota hai**. Destination host isi ID se fragments ko identify aur regroup karta hai.
2. **Flags (3 Bits):**
   - **DF (Don't Fragment):** Agar $	ext{DF} = 1$, to fragmentation prohibited hai. Packet drop ho jayega.
   - **MF (More Fragments):**
     - $	ext{MF} = 1 \implies$ Yeh packet ke aage aur fragments aane baaki hain.
     - $	ext{MF} = 0 \implies$ Yeh **aakhiri (last) fragment** hai.
3. **Fragment Offset (13 Bits):**
   - Batata hai ki yeh fragment original data stream me kis byte number se shuru hota hai.
   - **The Multiple of 8 Rule:** Offset field 13 bits ki hai jabki datagram 65,535 bytes tak ho sakta hai. Isliye offset ko **8-byte units** me measure kiya jata hai:
     $$\mathbf{	ext{Fragment Offset} = rac{	ext{Byte Offset}}{8}}$$
   - **Golden Rule:** Har intermediate fragment ki payload length **strictly 8 ki multiple** honi chahiye! (Last fragment exception hai).

---

## 3. Reassembly Architecture
Internet Protocol me fragmentation intermediate routers karte hain, lekin **Reassembly hamesha aur hamesha Final Destination Host par hoti hai**:
- Routers intermediate reassembly karke apni CPU aur buffer memory waste nahi karte.
- Fragments alag-alag paths se travel kar sakte hain, isliye ho sakta hai ki saare fragments same router se guzrein hi na!
- **Drawback:** Agar 10 fragments me se ek bhi fragment raste me lost ho jaye, to receiver ka reassembly timer expire ho jata hai aur **pura datagram discard ho jata hai**!

---

## 4. AKTU Solved Numerical: 4000-Byte Datagram Fragmentation

> **Problem Statement (AKTU Semester Exam 10 Marks):**  
> An IPv4 datagram of Total Length 4000 bytes (with a 20-byte standard header) arrives at a router. The router needs to forward it over a link with MTU = 1500 bytes.  
> 1. Determine how many fragments will be generated.  
> 2. For each fragment, calculate:  
>    - Total Length  
>    - Data Length and Byte Range  
>    - More Fragments (MF) Flag  
>    - Fragment Offset value.

### Step-by-Step Solution:

#### Step 1: Data to be fragmented:
$$	ext{Header Length} = 20\ 	ext{Bytes}$$
$$	ext{Total Data Payload} = 4000 - 20 = \mathbf{3980\ 	ext{Bytes}}\quad (	ext{Bytes } 0 	ext{ to } 3979)$$

#### Step 2: Maximum Data per Fragment for MTU = 1500:
$$	ext{Available Space for Data} = 	ext{MTU} - 	ext{Header} = 1500 - 20 = 1480\ 	ext{Bytes}$$
Let's check if 1480 is divisible by 8:
$$rac{1480}{8} = 185 \implies \mathbf{	ext{Exact Integer! Divisible by 8.}}$$
So, maximum data per fragment = **1480 Bytes**.

#### Step 3: Fragment Computations:

**Fragment 1:**
- **Data Carried:** 1480 Bytes ($	ext{Bytes } 0 	ext{ to } 1479$).
- **Total Length:** $1480 + 20 = \mathbf{1500\ 	ext{Bytes}}$.
- **MF Flag:** $\mathbf{1}$ (More data remains).
- **Fragment Offset:**
  $$	ext{Offset} = rac{	ext{Starting Byte}}{8} = rac{0}{8} = \mathbf{0}$$

**Fragment 2:**
- **Data Carried:** 1480 Bytes ($	ext{Bytes } 1480 	ext{ to } 2959$).
- **Total Length:** $1480 + 20 = \mathbf{1500\ 	ext{Bytes}}$.
- **MF Flag:** $\mathbf{1}$ (More data remains).
- **Fragment Offset:**
  $$	ext{Offset} = rac{	ext{Starting Byte}}{8} = rac{1480}{8} = \mathbf{185}$$

**Fragment 3 (Last Fragment):**
- **Remaining Data:** $3980 - (1480 + 1480) = 3980 - 2960 = \mathbf{1020\ 	ext{Bytes}}\quad (	ext{Bytes } 2960 	ext{ to } 3979)$.
- **Total Length:** $1020 + 20 = \mathbf{1040\ 	ext{Bytes}} \le 1500$ (Fits easily!).
- **MF Flag:** $\mathbf{0}$ (This is the **LAST** fragment!).
- **Fragment Offset:**
  $$	ext{Offset} = rac{	ext{Starting Byte}}{8} = rac{2960}{8} = \mathbf{370}$$

### Summary Verification Table:

| Fragment | Total Length | Header | Data Payload | Byte Range | MF Flag | Fragment Offset |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Fragment 1** | 1500 Bytes | 20 B | 1480 Bytes | $0 - 1479$ | `1` | `0` |
| **Fragment 2** | 1500 Bytes | 20 B | 1480 Bytes | $1480 - 2959$ | `1` | `185` |
| **Fragment 3** | 1040 Bytes | 20 B | 1020 Bytes | $2960 - 3979$ | `0` | `370` |

---

## 5. Second-Level Fragmentation (Heterogeneous Hop)
Agar Fragment 2 (Total Length 1500B) aage chal kar ek aise link par pahunchta hai jiska **MTU = 500 Bytes** ho:
- Available data space = $500 - 20 = 480	ext{ Bytes}$ ($rac{480}{8} = 60$, divisible by 8).
- Fragment 2 khud 4 sub-fragments me divide ho jayega!
- Sub-fragment 1 starts at byte 1480 $\implies 	ext{Offset} = rac{1480}{8} = 185$.
- Sub-fragment 2 starts at byte $1480 + 480 = 1960 \implies 	ext{Offset} = rac{1960}{8} = 245$.
- Sub-fragments will all retain original Identification `14285`!
