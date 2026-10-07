# Module 13: Token Bus (802.4), Token Ring (802.5) & FDDI Architecture

## 1. Token-Based Local Area Networks
Deterministic networks me station ko transmit karne ke liye ek logical permission frame ki zaroorat hoti hai jise **Token** kehte hain. Yahan collision probability exactly **zero** hoti hai.

```
Token LANs
 ├── IEEE 802.4 Token Bus (Physical Bus, Logical Ring)
 ├── IEEE 802.5 Token Ring (Physical Star with MSAU, Logical Ring)
 └── FDDI (Fiber Distributed Data Interface - Dual Counter-Rotating Fiber Ring)
```

---

## 2. Token Bus (IEEE 802.4)
- **Topology:** Physically ek single linear bus cable hoti hai, lekin logically stations descending order me arranged hoti hain ($S_{40} \to S_{25} \to S_{10} \to S_{40}$).
- **Operation:** Station data transmit karne ke baad token frame apne immediate logical successor ko bhejti hai.
- **Ring Maintenance:**
  - **Adding a station:** Periodic `SOLICIT_SUCCESSOR` frames broadcast kiye jate hain.
  - **Removing a station:** Station jaate waqt `SET_SUCCESSOR` frame bhejti hai.
  - **Fault Recovery:** Agar successor respond na kare, to station claim token frame bhej kar ring ko reconfigure karti hai.

---

## 3. Token Ring (IEEE 802.5)

### 3.1 Physical vs Logical Topology
- Physical layout ek **Star Topology** hoti hai jo ek centralized hub (**MSAU - Multi-Station Access Unit**) se connected hoti hai.
- MSAU ke andar internally wiring ek continuous **Logical Ring** form karti hai. Agar koi station disconnect hoti hai, to MSAU ke andar internal bypass relay click ho kar use ring se cut kar deta hai, jisse ring break nahi hoti!

### 3.2 Token Passing Mechanism:
1. Ek 3-byte **Free Token** ring me ghoomta rehta hai:
   $$\text{Free Token Format} = \text{Starting Delimiter (SD)} + \text{Access Control (AC)} + \text{Ending Delimiter (ED)}$$
2. Jab station ko transmit karna ho, to wo token aane par uske AC byte me `Token bit` ko $0 \to 1$ flip kar deti hai (making it Start of Frame).
3. Station apna data frame inject karti hai.
4. Frame pure ring me traverse karta hai. Destination station frame copy karti hai aur frame ke end me maujood **Frame Status (FS)** byte me `Address Recognized (A)` aur `Frame Copied (C)` bits ko `1` set kar deti hai.
5. Jab frame wapas sender ke paas aata hai, to sender frame ko ring se drain (remove) karta hai aur naya **Free Token** release karta hai!

### 3.3 Active Monitor Station
Ring me ek station **Active Monitor** banti hai:
- **Lost Token Detection:** Timer maintain karta hai ($T_{no\_token}$). Expire hone par naya token regenerate karta hai.
- **Orphan / Circulating Frame Elimination:** Agar sender crash ho jaye aur apna frame remove na kare, to Active Monitor frame ke AC byte me `Monitor Bit` ko `1` set karta hai. Agar frame dubara Monitor ke paas `1` ke sath aaye, to Monitor use destroy kar deta hai!

### 3.4 Early Token Release (ETR)
Standard Token Ring me sender tab tak token release nahi karta jab tak uska apna frame ghoom kar wapas na aa jaye.  
In **16 Mbps Token Ring (ETR)**, sender apna frame transmit karte hi turant naya Free Token release kar deta hai, jisse multiple frames simultaneously ring me travel kar sakte hain!

---

## 4. FDDI (Fiber Distributed Data Interface - ANSI X3T9.5)

FDDI ek high-speed optical fiber LAN/MAN standard hai (100 Mbps over optical fiber, up to 200 km span, 1000 stations).

### 4.1 Dual Counter-Rotating Ring Architecture
FDDI me do independent optical fiber rings hoti hain:
1. **Primary Ring (CW):** Data transmission clockwise direction me 100 Mbps par carry karti hai.
2. **Secondary Ring (CCW):** Backup ring jo counter-clockwise direction me run hoti hai aur normal operation me idle rehti hai.

### 4.2 Self-Healing Wrap-Around Mechanism
Agar fiber cut ho jaye ya koi station permanently fail ho jaye:
- Fault ke dono sides wali stations (Station B aur Station C) automatically internal optical switches ko activate karti hain aur **Primary ring ko Secondary ring ke sath loop-back (wrap)** kar deti hain!
- Pura network bina kisi downtime ke ek **Single Giant Ring** me reconfigure ho jata hai!

```
Normal Operation:
Primary   :  [A] ------> [B] ------> [C] ------> [D] ------> [A]
Secondary :  [A] <------ [B] <------ [C] <------ [D] <------ [A]

Cable Break between B and C:
Wrap Mode :  [A] ------> [B] (Wrap)
                          |  (Looped into Secondary!)
             [A] <-------+
             (Network continues operating seamlessly!)
```

### 4.3 Timed Token Protocol in FDDI
FDDI do tarah ka traffic support karta hai: **Synchronous** (Real-time voice/video) aur **Asynchronous** (Data files).
- **TTRT (Target Token Rotation Time):** Sabhi stations ring initialization ke waqt negotiate karti hain.
- **TRT (Token Rotation Time):** Pichle token aane se lekar ab tak ka actual elapsed time.
- **THT (Token Holding Time):**
  $$\mathbf{THT = \max(0, \text{TTRT} - \text{TRT})}$$
- **Transmission Rule:**
  - Synchronous traffic hamesha transmit ho sakta hai.
  - Asynchronous traffic tabhi transmit ho sakta hai jab token jaldi aaya ho ($\text{TRT} < \text{TTRT}$).

---

## 5. AKTU Solved Numerical: FDDI Timed Token Efficiency

> **Problem Statement (AKTU Semester Exam):**  
> An FDDI network has a Target Token Rotation Time (TTRT) of 20 ms. In a particular cycle, a station observes that the token arrived after TRT = 14 ms.  
> 1. Calculate the Token Holding Time (THT) available for asynchronous transmission.  
> 2. If the data rate is 100 Mbps, how many bytes of asynchronous data can this station transmit in this cycle?

### Solution:
**Step 1: Token Holding Time (THT):**
$$\text{THT} = \text{TTRT} - \text{TRT} = 20\ \text{ms} - 14\ \text{ms} = \mathbf{6\ \text{ms}} = 0.006\ \text{s}$$

**Step 2: Maximum Data Transmitted:**
$$\text{Bits} = \text{THT} \times \text{Bandwidth} = 0.006\ \text{s} \times 100 \times 10^6\ \text{bps} = 600,000\ \text{bits}$$
$$\text{Bytes} = \frac{600,000}{8} = \mathbf{75,000\ \text{Bytes} = 75\ \text{KB}}$$
