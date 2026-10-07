# Module 10: Network Performance Metrics & Latency Analysis

## 1. Network Performance Metrics: Bandwidth, Throughput & Goodput

| Metric | Definition | Measurement Unit | Practical Reality |
| :--- | :--- | :--- | :--- |
| **Bandwidth (Hertz)** | Range of frequencies passing through channel. | Hertz (Hz, kHz, MHz) | Physical transmission capacity |
| **Bandwidth (bps)** | Maximum potential bit transmission rate. | bps, Mbps, Gbps | Link hardware specification (e.g., 1 Gbps NIC) |
| **Throughput** | Actual measured rate at which data is successfully transmitted. | Mbps, Gbps | Hamesha Bandwidth se kam hota hai (Bottlenecks, congestion) |
| **Goodput** | Rate of actual useful application payload delivered (excluding protocol headers and retransmissions). | Mbps, Gbps | $	ext{Goodput} < 	ext{Throughput} < 	ext{Bandwidth}$ |

---

## 2. 4 Components of Network Latency (Total Delay)
Jab koi packet source se destination tak travel karta hai, to total delay ($T$) char components ka sum hota hai:

$$T_{	ext{total}} = T_t + T_p + T_q + T_{	ext{proc}}$$

### 2.1 Transmission Delay ($T_t$)
- Packet ke sabhi bits ko transmitter dwara wire/medium par inject karne me laga samay.
- Formula:
  $$T_t = rac{	ext{Packet Length } (L)}{	ext{Bandwidth } (B)}$$
  - Jahan $L$ bits me aur $B$ bits/sec (bps) me hota hai.
  - *Key Feature:* Iska transmission distance ($d$) se koi lena-dena nahi hota!

### 2.2 Propagation Delay ($T_p$)
- Ek single bit ko cable ke ek end se doosre end tak physical distance travel karne me laga samay.
- Formula:
  $$T_p = rac{	ext{Distance } (d)}{	ext{Propagation Speed } (v)}$$
  - Medium me light/signal ki speed $v pprox 2 	imes 10^8 	ext{ m/s}$ (twisted pair / optical fiber me) ya $3 	imes 10^8 	ext{ m/s}$ (vacuum / wireless me).
  - *Key Feature:* Iska packet size ($L$) ya network bandwidth ($B$) se koi lena-dena nahi hota!

### 2.3 Queuing Delay ($T_q$)
- Intermediate routers ke buffer memory me packet ko line (queue) me khade rehne ka samay.
- Traffic congestion par depend karta hai. Agar queue full ho jaye to packet drop ho jata hai.

### 2.4 Processing Delay ($T_{	ext{proc}}$)
- Router CPU dwara header inspect karne, CRC error check karne, aur routing table lookup karke output port decide karne ka samay (Microseconds me hota hai).

---

## 3. Bandwidth-Delay Product (BDP)
Network link ko ek pipe ki tarah imagine karein:
- Pipe ka cross-sectional area = Bandwidth ($B$)
- Pipe ki length = Propagation delay ($T_p$)
- Pipe ka total volume = **Bandwidth-Delay Product (BDP)**

$$	ext{BDP} = B 	imes T_p 	ext{ bits}$$

**Significance:** BDP yeh batata hai ki kisi bhi given instant par cable/wire me kitne maximum bits "in flight" (yatra me) ho sakte hain bina acknowledge huye. Yeh TCP Sliding Window Protocol ke window size ko tune karne ke liye critical hota hai ($W \ge 2 	imes 	ext{BDP}$).

---

## 4. AKTU Solved Numerical
**Question:** Do computers ke beech distance $d = 2000	ext{ km}$ hai aur link bandwidth $B = 10	ext{ Mbps}$ hai. Propagation speed $v = 2 	imes 10^8	ext{ m/s}$ hai. Ek $1000	ext{ bytes}$ ke packet ke liye:
1. Transmission delay ($T_t$) nikalein.
2. Propagation delay ($T_p$) nikalein.
3. Bandwidth-Delay Product (BDP) nikalein.

**Solution:**
1. **Transmission Delay ($T_t$):**
   - $L = 1000 	ext{ bytes} = 8000 	ext{ bits}$.
   - $B = 10 	ext{ Mbps} = 10^7 	ext{ bps}$.
   - $T_t = rac{8000}{10^7} = 0.0008 	ext{ s} = 0.8 	ext{ ms}$.
2. **Propagation Delay ($T_p$):**
   - $d = 2000 	ext{ km} = 2 	imes 10^6 	ext{ m}$.
   - $v = 2 	imes 10^8 	ext{ m/s}$.
   - $T_p = rac{2 	imes 10^6}{2 	imes 10^8} = 0.01 	ext{ s} = 10 	ext{ ms}$.
3. **BDP:**
   - $	ext{BDP} = B 	imes T_p = 10^7 	ext{ bps} 	imes 0.01 	ext{ s} = 100,000 	ext{ bits} = 12,500 	ext{ bytes}$.
