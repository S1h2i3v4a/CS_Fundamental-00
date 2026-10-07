# Module 13: Switching Techniques: Circuit, Message & Packet

## 1. Switching ka Parichay
Bade networks me har ek device ke beech direct dedicated wire lagana impossible hota hai ($N(N-1)/2$). Isliye network me intermediate nodes lagaye jate hain jinhe **Switches** kehte hain. Switch incoming data ko correct destination port par redirect karta hai.
Switching techniques ko teen broad categories me classify kiya jata hai:
1. **Circuit Switching**
2. **Message Switching**
3. **Packet Switching** (Datagram approach vs Virtual Circuit approach)

---

## 2. The 3 Switching Paradigms Compared

| Evaluation Parameter | Circuit Switching | Message Switching | Packet Switching |
| :--- | :--- | :--- | :--- |
| **Dedicated Physical Path** | **YES**, dedicated copper/time path | **NO**, dynamic store-and-forward | **NO**, dynamic store-and-forward |
| **Transmission Phases** | 3 Phases: Setup $	o$ Data $	o$ Teardown | 1 Phase: Direct message dispatch | Datagram: 1 Phase; Virtual Circuit: 3 Phases |
| **Bandwidth Utilization** | Low (Wasted if user is silent) | High | **Maximum** (Statistical multiplexing) |
| **Buffer Requirement at Switches** | Zero buffer needed | **Massive Hard Disk storage** | Small RAM buffers |
| **Store-and-Forward Delay** | Zero store-and-forward delay | Extremely High (entire message) | Low (pipelined small packets) |
| **Traffic Congestion Danger** | At call setup time (busy signal) | In switch queues | In switch queues (packet drop) |
| **Real-time Voice/Video Support** | Excellent (zero jitter) | Completely unsuitable | Good (with QoS / buffering) |
| **Historical / Modern Example** | Traditional PSTN Landline phone | Telegraph, Telex, UUCP mail | **The Global Internet (IP)** |

---

## 3. Packet Switching: Datagram vs Virtual Circuit

Modern computer networking Packet Switching par operate karti hai. Isme large files ko chhote fixed/variable size pieces me divide kiya jata hai jinhe **Packets** kehte hain.

### 3.1 Datagram Approach (Connectionless - IP Network Standard)
- Har packet ko ek independent entity maana jata hai (**Datagram**).
- Har packet ke header me **Full Source IP aur Destination IP Address** hota hai.
- Intermediate routers har packet ko independent route se forward kar sakte hain (agar link crash ho jaye to agla packet doosre raste se nikal jata hai).
- Packets destination par **out-of-order** (ulta-pulta sequence) deliver ho sakte hain. Destination par transport layer (TCP) sequence numbers ke zariye unhe reassemble karti hai.
- *Advantage:* Highly robust, flexible, zero connection setup overhead.

### 3.2 Virtual Circuit Approach (Connection-Oriented - ATM / X.25 / Frame Relay)
- Data transmit karne se pehle source aur destination ke beech ek logical pre-planned route setup kiya jata hai (**Virtual Circuit**).
- Sabhi packets usi fixed path se travel karte hain aur strictly in-order deliver hote hain.
- Packet ke header me bada IP address nahi balki ek chhota **VCI (Virtual Circuit Identifier)** ya Label hota hai.
- Types:
  - **SVC (Switched Virtual Circuit):** Dynamically create hota hai session ke liye aur end hone par teardown ho jata hai.
  - **PVC (Permanent Virtual Circuit):** Network admin dwara statically configure kiya gaya dedicated permanent tunnel.
- *Disadvantage:* Agar beech ka koi router crash ho jaye to pura virtual circuit break ho jata hai aur fir se call setup karna padta hai.
