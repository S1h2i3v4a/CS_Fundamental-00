# Module 07: Flow Control Foundations & Stop-and-Wait ARQ Protocol

## 1. Flow Control and Error Control Concepts
Data Link Layer par do major challenges hote hain:
1. **Flow Control:** Fast sender slow receiver ko overwhelm (buffer overflow) na kare.
2. **Error Control:** Noise ke karan damaged ya lost frames ko recover karna.

Jab Flow Control ke sath Error Control (**Timer + Retransmission**) add kiya jata hai, to is mechanism ko **ARQ (Automatic Repeat reQuest)** kehte hain.

```
Flow Control Protocols
 ├── Stop-and-Wait (Sender sends 1 frame, waits for ACK)
 └── Sliding Window Protocols (Pipelined transmission)
      ├── Go-Back-N ARQ
      └── Selective Repeat ARQ
```

---

## 2. Stop-and-Wait ARQ Architecture
Stop-and-Wait ARQ me sender tab tak agla frame nahi bhej sakta jab tak use pichle frame ka Acknowledgment (**ACK**) na mil jaye.

### 2.1 Essential Protocol Components
1. **Timer (Time-out Mechanism):** Sender frame bhejte hi timer start karta hai. Agar frame ya ACK raste me kho jaye, to timer expire hote hi frame retransmit hota hai.
2. **Sequence Numbering (1-Bit: 0 and 1):**
   - Kyun zaroorat hai? Agar ACK lost ho jaye, to sender same frame dubara bhejega. Agar sequence number na ho, to receiver duplicate frame ko naya frame samajh kar accept kar lega!
   - 1-bit sequence number frame ko alternating `0` aur `1` tags deta hai.
3. **Acknowledgment Numbering:**
   - In modern ARQ, ACK number hamesha **Next Expected Frame Number** represent karta hai. E.g., `ACK 1` ka matlab hai: *"Frame 0 successfully mil gaya, ab Frame 1 bhejo"*.
4. **Piggybacking:**
   - Agar bidirectional communication ho, to ACK ko alag se na bhej kar outgoing data frame ke header me include kar diya jata hai, jisse bandwidth bachti hai.

---

## 3. Mathematical Efficiency Derivation ($\eta$)

### 3.1 Cycle Time Components
Ek single frame cycle me lagne wala total time:
$$T_{total} = T_t + T_p + T_{proc} + T_{ack} + T_p$$

Standard derivations me:
- Receiver processing delay $T_{proc} pprox 0$
- ACK frame size bohot chhota hota hai (few bytes), isliye $T_{ack} pprox 0$
$$T_{total} pprox T_t + 2 \cdot T_p$$

Jahan:
- $T_t = rac{	ext{Frame Length } L}{	ext{Bandwidth } B}$ (Transmission Delay)
- $T_p = rac{	ext{Distance } d}{	ext{Propagation Speed } v}$ (Propagation Delay)
- $2 \cdot T_p = 	ext{Round Trip Propagation Time (RTT)}$

### 3.2 Efficiency / Channel Utilization ($\eta$)
$$\eta = rac{	ext{Useful Time}}{	ext{Total Time}} = rac{T_t}{T_t + 2 \cdot T_p}$$

Numerator aur denominator ko $T_t$ se divide karne par:
$$\eta = rac{1}{1 + 2 \left(rac{T_p}{T_t}ight)}$$

Let $a = rac{T_p}{T_t}$ (Ratio of Propagation Delay to Transmission Delay):
$$\mathbf{\eta = rac{1}{1 + 2a}}$$

### 3.3 Throughput (Effective Bit Rate)
$$	ext{Throughput } U = \eta 	imes 	ext{Bandwidth} = rac{L}{T_t + 2 \cdot T_p}$$

---

## 4. Physical Significance of Parameter '$a$'
Parameter $a = rac{T_p}{T_t}$ communication link ke characteristics ko decide karta hai:

1. **Case 1: $a \ll 1$ ($T_p \ll T_t$, e.g., Local Area Networks):**
   - Short distance link par propagation delay negligible hota hai.
   - Efficiency $\eta pprox rac{1}{1 + 0} pprox 100\%$. Stop-and-Wait LANs ke liye fine hai.
2. **Case 2: $a \gg 1$ ($T_p \gg T_t$, e.g., Satellite Communication / Long Distance WAN):**
   - Satellite $36,000	ext{ km}$ door geostationary orbit me hota hai, isliye $T_p pprox 250	ext{ ms}$.
   - Denominator $1 + 2a$ bohot bada ho jata hai, jisse efficiency drop hokar $< 1\%$ ho jati hai!
   - Sender transmission time khatam hone ke baad 99% time bilkul idle betha rehta hai ACK ke intezar me.

---

## 5. AKTU Core Solved Numericals

### Numerical 1: Satellite Link Efficiency Calculation (AKTU 10 Marks)
> **Problem Statement:**  
> A 1000-bit frame is transmitted over a 1 Mbps satellite channel with a one-way propagation delay of 250 ms. Calculate:  
> 1. Transmission delay ($T_t$).  
> 2. The parameter $a$.  
> 3. Link efficiency ($\eta$) of Stop-and-Wait protocol.  
> 4. Actual throughput achieved.

#### Solution:
**Step 1: Transmission Delay ($T_t$):**
$$T_t = rac{L}{B} = rac{1000\ 	ext{bits}}{1 	imes 10^6\ 	ext{bps}} = 10^{-3}\ 	ext{s} = 1\ 	ext{ms}$$

**Step 2: Propagation to Transmission Ratio ($a$):**
$$a = rac{T_p}{T_t} = rac{250\ 	ext{ms}}{1\ 	ext{ms}} = 250$$

**Step 3: Link Efficiency ($\eta$):**
$$\eta = rac{1}{1 + 2a} = rac{1}{1 + 2(250)} = rac{1}{501} pprox 0.001996 \implies \mathbf{0.1996\%}$$

**Step 4: Throughput ($U$):**
$$	ext{Throughput} = \eta 	imes B = 0.001996 	imes 1\ 	ext{Mbps} pprox \mathbf{1.996\ 	ext{kbps}}$$

---

### Numerical 2: Minimum Frame Size for Given Efficiency
> **Problem Statement (AKTU BCS603):**  
> A point-to-point link of length 2000 km has a transmission speed of $2 	imes 10^8\ 	ext{m/s}$ and bandwidth 2 Mbps. Determine the minimum frame size required to achieve at least 50% efficiency using Stop-and-Wait ARQ.

#### Solution:
**Step 1: Propagation Delay ($T_p$):**
$$T_p = rac{	ext{Distance}}{	ext{Speed}} = rac{2000 	imes 10^3\ 	ext{m}}{2 	imes 10^8\ 	ext{m/s}} = 0.01\ 	ext{s} = 10\ 	ext{ms}$$

**Step 2: Condition for $\eta \ge 50\%$:**
$$\eta = rac{1}{1 + 2a} \ge 0.5 \implies 1 + 2a \le 2 \implies 2a \le 1 \implies a \le 0.5$$

Kyunki $a = rac{T_p}{T_t} \le 0.5$:
$$T_t \ge 2 \cdot T_p = 2 	imes 10\ 	ext{ms} = 20\ 	ext{ms} = 0.02\ 	ext{s}$$

**Step 3: Minimum Frame Size ($L_{min}$):**
$$T_t = rac{L}{B} \implies L_{min} = T_t 	imes B = 0.02\ 	ext{s} 	imes 2 	imes 10^6\ 	ext{bps} = 40,000\ 	ext{bits} = \mathbf{5,000\ 	ext{Bytes}}$$
