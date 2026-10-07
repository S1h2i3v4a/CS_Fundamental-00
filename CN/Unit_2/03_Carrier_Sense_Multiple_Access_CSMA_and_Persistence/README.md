# Module 03: Carrier Sense Multiple Access (CSMA) & Persistence

## 1. CSMA ka Fundamental Principle: "Listen Before Talk"
ALOHA me stations bina soche-samjhe transmit kar deti thi, jisse high collision hota tha. CSMA (**Carrier Sense Multiple Access**) is problem ko solve karta hai ek simple human intuition se:
> *"Pehle suno ki koi bol to nahi raha; agar koi bol raha hai to chup raho; agar shanti hai tabhi bolo!"*

- Transmit karne se pehle har station transmission medium (carrier) ko **sense** karti hai.
- **Vulnerable Time:** CSMA me vulnerable time ALOHA ke muqable dramatically reduce hokar sirf **Propagation Delay ($T_p$)** ke barabar ho jata hai!
  $$V_t = T_p$$

---

## 2. The 3 Persistence Strategies
Jab station ke paas transmit karne ke liye frame ready ho:
- Agar medium **Busy** hai to kya kare?
- Agar medium **Idle** hai to kya kare?

In sawalon ke jawab ke liye teen strategies develop ki gayi hain:

| Persistence Strategy | Action if Channel is IDLE | Action if Channel is BUSY | Collision Probability | Channel Idle Delay | Practical Application |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **1-Persistent CSMA** | Transmit immediately with probability $P = 1$. | Line ko continuously monitor karta rehta hai; jaise hi idle hoti hai turant transmit karta hai. | **Highest** (Agar busy period me multiple stations wait kar rahi thi to wo sab ek sath transmit karengi). | **Zero** (Line free hote hi turant data transmit). | Traditional **IEEE 802.3 Ethernet**. |
| **Non-Persistent CSMA** | Transmit immediately. | Line ko continuously sense **NAHI** karta. Ek random time interval wait (back off) karta hai, phir dubara sense karta hai. | **Lowest** (Random wait times alag hone ke karan stations simultaneously transmit nahi karti). | **High** (Channel khali hone ke bawjood stations backoff me baithi rehti hain). | Low-traffic, high-delay networks. |
| **p-Persistent CSMA** | Transmits with probability $p$; waits for next time slot with probability $(1-p)$. | Continuously monitors line until idle, then applies probabilistic test. | **Tunable / Low** (Setting $p = 1/N$ yields near-zero collisions). | **Moderate** | Slotted channels, **IEEE 802.11 (Wi-Fi)**. |

---

## 3. Why Collisions Still Occur in CSMA?
Agar stations transmit karne se pehle sense karti hain, to collision kyun hota hai?

### Root Cause: Finite Propagation Delay ($T_p = d/v$)
1. Maan lijiye Host A aur Host B cable ke do opposite ends par hain. Propagation delay $T_p = 5\ \mu	ext{s}$.
2. Time $t = 0$ par Host A ne line sense ki. Channel bilkul idle mila. A ne transmit shuru kiya.
3. Signal ko cable me chal kar Host B tak pahunchne me $5\ \mu	ext{s}$ lagenge.
4. Time $t = 4\ \mu	ext{s}$ par Host B ko bhi data bhejna hai. B ne line sense ki. Kyunki A ka signal abhi tak B tak nahi pahuncha hai, B ko channel **IDLE** dikha!
5. Host B ne bhi transmit kar diya.
6. A aur B ke electrical signals cable ke beech me takrayenge aur corrupt ho jayenge (**COLLISION**).
7. Hence, **CSMA reduces collisions drastically, but CANNOT eliminate them entirely!**
