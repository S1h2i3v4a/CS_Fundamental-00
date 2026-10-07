# Module 05: CSMA with Collision Avoidance (CSMA/CA) & Wireless LANs

## 1. Why CSMA/CD Fails in Wireless Networks
Wired Ethernet me collision detection (**CSMA/CD**) successfully kaam karta hai kyunki cable ke andar transmitted signal aur incoming collision voltage ko aasani se compare kiya ja sakta hai ($V_{channel} > 2 \cdot V_{trans}$). Lekin Wireless LANs (**IEEE 802.11 Wi-Fi**) me CSMA/CD do fundamental reasons ki wajah se fail ho jata hai:

1. **Hardware / Dynamic Range Limitations:**
   - Wireless antenna se transmit hone wali energy receiver antenna par aane wale signal se lakho guna ($10^5$ to $10^8$ times) zyada powerful hoti hai ($P_{tx} \gg P_{rx}$).
   - Jab station transmit kar rahi hoti hai, to uska apna transmitter receiver amplifier ko saturate kar deta hai. Iss dynamic range difference ke karan station transmission ke dauran doosre station ka weak signal detect nahi kar sakti.
2. **Hidden and Exposed Station Problems:**
   - Wireless signals distance ke sath quadratically decay hote hain ($1/r^2$). Isliye channel sabhi stations ko equally visible nahi hota.

---

## 2. The Hidden and Exposed Station Problems

### 2.1 Hidden Station Problem
Maan lijiye teen wireless stations hain: `A`, `B`, aur `C`:
- `A` aur `B` ek doosre ki radio range me hain.
- `B` aur `C` ek doosre ki radio range me hain.
- Lekin `A` aur `C` itni door hain ki unki radio ranges overlap nahi karti (**A cannot hear C**, and **C cannot hear A**).

```
[ Station A ] <----- Radio Range -----> [ Station B ] <----- Radio Range -----> [ Station C ]
   (Sender 1)                             (Access Point)                           (Sender 2)
```

1. Station A ko Station B (AP) ko frame bhejna hai. A channel sense karta hai; channel idle milta hai. A transmission start karta hai.
2. Usi waqt Station C ko bhi B ko frame bhejna hai. C channel sense karta hai. Kyunki C, A ke signals sun nahi sakta, C ko channel "IDLE" dikhta hai!
3. C bhi B ko transmit kar deta hai.
4. **Collision Result:** Station B par dono signals collide ho jate hain aur frame destroy ho jata hai!
5. **Conclusion:** Station A aur C ek doosre ke liye **Hidden Stations** hain.

### 2.2 Exposed Station Problem
Yahan station unnecessary delay face karti hai jabki actual collision hone ki koi possibility nahi hoti.
- Station B, A ko data bhej raha hai.
- Station C, D ko data bhejna chahta hai (jahan D, B ki range se bahar hai).
- C channel sense karta hai aur B ki transmission sun kar ruk jata hai, jabki B ka receiver A tha aur C ka D, dono simultaneous transmissions safe the!

---

## 3. CSMA/CA Architecture & Interframe Spaces (IFS)
Kyunki hum collision detect nahi kar sakte, hume collision ko **pehle se hi prevent (avoid)** karna padta hai. Iske liye IEEE 802.11 teen mechanisms use karta hai:
1. **Interframe Spaces (IFS):** Har transmission ke beech mandatory silence intervals.
2. **Contention Window & Backoff:** Channel idle hone par immediate transmit na karke random slots rukna.
3. **Virtual Carrier Sensing (RTS/CTS with NAV):** Channel reservation packets.

### 3.1 Interframe Space (IFS) Hierarchy
Priority encode karne ke liye IFS timings define ki gayi hain. **Jitna chhota IFS, utni high priority!**

```
+-------------------------------------------------------------------------+
| SIFS (Shortest IFS)   : For ACK, CTS, Polling responses (Top Priority!) |
| PIFS (PCF IFS)        : Used in centralized contention-free polling     |
| DIFS (DCF IFS)        : Used by normal stations for starting Contention |
| EIFS (Extended IFS)   : Used when a corrupted/error frame is received   |
+-------------------------------------------------------------------------+
Priority: SIFS > PIFS > DIFS > EIFS
Duration: SIFS < PIFS < DIFS < EIFS
```

---

## 4. The 4-Way Handshake: RTS / CTS and NAV Virtual Carrier Sensing

Jab frame size bada hota hai, to collision avoidance ke liye **4-Way Handshake** protocol execute hota hai:

### Step 1: Request to Send (RTS)
Sender (Station A) channel idle hone aur DIFS + Backoff complete hone ke baad ek chhota control packet bhejta hai: **RTS (Request to Send)**.
- RTS frame me ek field hoti hai: `Duration`. Yeh batata hai ki upcoming transaction kitne micro-seconds chalega:
  $$	ext{Duration} = 	ext{SIFS} + T_{CTS} + 	ext{SIFS} + T_{DATA} + 	ext{SIFS} + T_{ACK}$$

### Step 2: Clear to Send (CTS)
Receiver (Station B / AP) RTS receive karne ke baad `SIFS` duration rukta hai aur **CTS (Clear to Send)** broadcast karta hai.
- CTS frame me remaining duration copy hoti hai.
- Kyunki CTS Station B (AP) broadcast karta hai, B ke aas-paas ke **sabhi stations** (including Hidden Station C) CTS ko sun lete hain!

### Step 3: Network Allocation Vector (NAV)
Jab Station C (Hidden Station) CTS frame ko sunta hai, to usme maujood `Duration` value ko dekh kar apna ek internal timer start karta hai jise **NAV (Network Allocation Vector)** kehte hain.
- **Virtual Carrier Sensing:** Jab tak NAV timer count down ho kar 0 nahi hota, Station C medium ko "BUSY" manta hai aur RF circuitry ko sleep/silent rakhta hai. Battery bachti hai aur collision completely eliminate ho jata hai!

### Step 4: Data & Acknowledgment (ACK)
- Station A bina kisi fear ke apna large **DATA frame** transmit karta hai.
- Receiver Station B frame successfully receive karke SIFS ke baad ek **ACK frame** bhejta hai.

---

## 5. AKTU Solved Numerical: NAV Duration Calculation

> **Problem Statement (AKTU BCS603 Model Exam):**  
> In an 802.11b wireless network, Station A wishes to send a 1500-byte data frame to Station B at 11 Mbps. Control frames (RTS, CTS, ACK) are 20 bytes each and sent at the base rate of 1 Mbps. Given SIFS = $10\ \mu	ext{s}$ and propagation delay is negligible.  
> 1. Calculate the transmission time of Data, RTS, CTS, and ACK frames.  
> 2. Calculate the Duration value placed inside the RTS frame.  
> 3. Calculate the NAV value set by neighboring stations when they receive the CTS frame.

### Step-by-Step Solution:
**1. Frame Transmission Times:**
$$T_{RTS} = rac{20 	imes 8\ 	ext{bits}}{1 	imes 10^6\ 	ext{bps}} = rac{160}{10^6} = 160\ \mu	ext{s}$$
$$T_{CTS} = rac{20 	imes 8\ 	ext{bits}}{1 	imes 10^6\ 	ext{bps}} = 160\ \mu	ext{s}$$
$$T_{ACK} = rac{20 	imes 8\ 	ext{bits}}{1 	imes 10^6\ 	ext{bps}} = 160\ \mu	ext{s}$$
$$T_{DATA} = rac{1500 	imes 8\ 	ext{bits}}{11 	imes 10^6\ 	ext{bps}} = rac{12000}{11} pprox 1090.9\ \mu	ext{s}$$

**2. RTS Duration Field:**
RTS frame ke baad bache huye pure exchange ka time:
$$	ext{Duration}_{RTS} = 	ext{SIFS} + T_{CTS} + 	ext{SIFS} + T_{DATA} + 	ext{SIFS} + T_{ACK}$$
$$	ext{Duration}_{RTS} = 10 + 160 + 10 + 1090.9 + 10 + 160 = 1440.9\ \mu	ext{s}$$

**3. CTS Duration Field (NAV set by neighbors):**
CTS ke baad bache huye transaction ka time:
$$	ext{Duration}_{CTS} = 	ext{SIFS} + T_{DATA} + 	ext{SIFS} + T_{ACK}$$
$$	ext{NAV} = 10 + 1090.9 + 10 + 160 = 1270.9\ \mu	ext{s}$$

Neighboring stations apna NAV $1270.9\ \mu	ext{s}$ par set kar legi aur iss duration tak channel par bilkul transmit nahi karegi!

---

## 6. Summary Comparison: CSMA/CD vs CSMA/CA

| Feature | CSMA/CD (Wired Ethernet 802.3) | CSMA/CA (Wireless LAN 802.11) |
| :--- | :--- | :--- |
| **Philosophy** | Detect collisions while transmitting | Avoid collisions before transmitting |
| **Transmission Action** | Transmits immediately if channel idle | Waits IFS + Random Backoff even if idle |
| **Collision Handling** | Abort + Send Jam Signal + Backoff | Wait for ACK timeout + Exponential Backoff |
| **Control Handshake** | None | RTS / CTS Handshake with NAV |
| **Channel Sensing** | Electrical / Voltage level sensing | Physical (CCA) + Virtual (NAV timer) |
| **Acknowledgment** | No DLL ACK needed (Collision-free implies OK) | Mandatory DLL ACK frame required |
