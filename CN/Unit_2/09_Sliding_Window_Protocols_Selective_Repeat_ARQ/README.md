# Module 09: Sliding Window Protocols: Selective Repeat ARQ Architecture

## 1. Motivation: Overcoming Go-Back-N Inefficiency
Go-Back-N (GBN) me jab koi single frame loss hota hai, to receiver out-of-order buffer na hone ki wajah se baad ke saare correctly received frames ko discard kar deta hai. Isse sender ko pura window dobara retransmit karna padta hai (**Go-Back penalty**).

**Selective Repeat (SR) ARQ** is problem ko completely solve karta hai:
- Receiver ke paas ek **Out-of-Order Buffer ($W_R > 1$)** hota hai.
- Agar Frame 2 lost hota hai aur Frames 3, 4 pahunchte hain, to receiver unhe discard karne ki jagah apne buffer me store kar leta hai.
- Sender sirf aur sirf **damaged ya lost frame (Frame 2)** ko retransmit karta hai. Baaki frames retransmit nahi hote!

---

## 2. Protocol Architecture & Mechanics

### 2.1 Window Configurations
- **Sender Window Size ($W_S$):** $W_S = 2^{m-1}$
- **Receiver Window Size ($W_R$):** $W_R = W_S = 2^{m-1}$ (Out-of-order frames ko store karne ke liye receiver window sender window ke barabar hoti hai).

### 2.2 Independent Timers
GBN me sabhi frames ke liye ek single timer tha. Selective Repeat me sender **har outstanding unacknowledged frame ke liye ek independent individual timer** maintain karta hai.

### 2.3 Negative Acknowledgment (NAK / Selective Reject)
Jab receiver koi missing frame detect karta hai (jaise Frame 1 ke baad direct Frame 3 aa gaya), to timer expire hone ka wait karne ki jagah wo turant sender ko ek **NAK (Negative Acknowledgment)** bhej deta hai: `NAK 2`.
- Sender NAK 2 milte hi bina timer expire huye turant Frame 2 ko retransmit kar deta hai, jisse latency drastically decrease ho jati hai.

---

## 3. Mathematical Proof: Why $W_S = W_R \le 2^{m-1}$? (AKTU Core Derivation)

> **Theorem (AKTU Semester Exam 10 Marks):**  
> In a Selective Repeat ARQ protocol using $m$-bit sequence numbers, prove that the maximum window size of sender and receiver must satisfy $W_S = W_R \le 2^{m-1}$. Show the ambiguity that arises if $W_S > 2^{m-1}$.

### Formal Proof:
Total available sequence numbers modulo $2^m$ are:
$$N = 2^m \quad (\text{Numbers: } 0, 1, 2, \dots, 2^m - 1)$$

Ek protocol cycle me:
1. Sender window purane unacknowledged frames ko cover kar rahi hoti hai (Old window).
2. Receiver window naye incoming expected frames ko cover kar rahi hoti hai (New window).

Agar link par saare ACKs lost ho jayein aur sender purana frame retransmit kare, to Receiver ki window me aur Sender ki retransmitted frames me koi overlap nahi hona chahiye:
$$\text{Window}_{Sender} + \text{Window}_{Receiver} \le \text{Total Sequence Space}$$
$$W_S + W_R \le 2^m$$

Since receiver must have sufficient buffer space to accept all frames sender could possibly send:
$$W_S = W_R$$
$$2 \cdot W_S \le 2^m \implies \mathbf{W_S \le 2^{m-1}} \quad \text{and} \quad \mathbf{W_R \le 2^{m-1}}$$

---

### Proof by Counter-Example (If $W_S > 2^{m-1}$):
Let $m = 2$ bits.
Total sequences = $2^2 = 4$ ($\{0, 1, 2, 3\}$).
Formula gives $W_S = 2^{2-1} = 2$.

**Suppose we choose $W_S = W_R = 3$ ($3 > 2$):**
1. **Initial State:**
   - Sender window: $\{0, 1, 2\}$
   - Receiver window: $\{0, 1, 2\}$
2. Sender frames $0, 1, 2$ transmit karta hai.
3. Receiver teeno frames successfully accept kar leta hai. Receiver window slide ho kar 3 slots aage badh jati hai:
   - Receiver new window: $\{3, 0, 1\}$ (expecting Frame 3, Frame 0 of next round, and Frame 1 of next round).
4. Receiver ACKs bhejta hai, lekin **saare ACKs raste me DESTROY** ho jate hain!
5. Sender ka timer expire ho jata hai. Sender purana `Frame 0` retransmit karta hai.
6. Jab `Frame 0` receiver par pahunchta hai:
   - Receiver dekhta hai ki uski current active window $\{3, 0, 1\}$ me `0` maujood hai!
   - Receiver ise **Next Cycle ka brand-new Frame 0** samajh kar accept kar leta hai!
   - Receiver purane duplicate data ko nayi data samajh kar application layer ko pass kar deta hai. Data corruption ho gaya!

**Conclusion:**  
To prevent sequence space wrap-around overlap, window size strictly $2^{m-1}$ se badi nahi ho sakti.

---

## 4. Master Comparison: Stop-and-Wait vs Go-Back-N vs Selective Repeat

| Feature | Stop-and-Wait ARQ | Go-Back-N ARQ | Selective Repeat ARQ |
| :--- | :--- | :--- | :--- |
| **Sender Window ($W_S$)** | $1$ | $2^m - 1$ | $2^{m-1}$ |
| **Receiver Window ($W_R$)** | $1$ | $1$ | $2^{m-1}$ |
| **Out-of-Order Buffering** | No | No (Discarded) | **Yes (Stored in buffer)** |
| **Acknowledgment Type** | Individual | Cumulative | Individual / NAK |
| **Retransmission Scope** | 1 frame on timeout | Entire window ($N$ frames) | **Only the damaged frame** |
| **Number of Timers** | 1 Timer | 1 Timer (for oldest) | **Multiple (1 per frame)** |
| **Bandwidth Efficiency** | Very Low ($\frac{1}{1+2a}$) | Moderate ($\frac{W_S}{1+2a}$) | **Highest** on noisy links |
| **Hardware Complexity** | Minimal | Low | Highest (Buffer + Logic) |

---

## 5. AKTU Solved Numerical: Bandwidth Utilization under Packet Loss

> **Problem Statement (AKTU BCS603):**  
> A 1 Gbps satellite link has a propagation delay of 250 ms. Frame size is 2 KB (16,000 bits).  
> 1. Calculate the transmission delay $T_t$ and parameter $a$.  
> 2. Determine the minimum sequence number bits $m$ for 100% utilization in (a) Go-Back-N, and (b) Selective Repeat.  
> 3. If the frame loss probability is $P = 10^{-2}$ (1%), compare the retransmission overhead of GBN vs Selective Repeat.

### Solution:

#### Step 1: Delays:
$$T_t = \frac{16,000\ \text{bits}}{10^9\ \text{bps}} = 16\ \mu\text{s} = 0.016\ \text{ms}$$
$$a = \frac{T_p}{T_t} = \frac{250\ \text{ms}}{0.016\ \text{ms}} = 15,625$$

Optimal window size for 100% efficiency:
$$W_{opt} \ge 1 + 2a = 1 + 2(15,625) = 31,251\ \text{Frames}$$

#### Step 2: Minimum Sequence Bits $m$:
- **For Go-Back-N ($W_S = 2^m - 1 \ge 31,251$):**
  $$2^m \ge 31,252 \implies 2^{15} = 32,768 \ge 31,252 \implies \mathbf{m = 15\ \text{Bits}}$$
- **For Selective Repeat ($W_S = 2^{m-1} \ge 31,251$):**
  $$2^{m-1} \ge 31,251 \implies m - 1 \ge 15 \implies \mathbf{m = 16\ \text{Bits}}$$

#### Step 3: Retransmission Overhead under 1% Frame Loss:
- In Selective Repeat: Only lost frame retransmitted. For 100 frames, 1 lost frame $\implies$ total transmissions = $101$ frames (Overhead = 1%).
- In Go-Back-N: When 1 frame is lost, all outstanding $N = 31,251$ frames in the window must be retransmitted!
  Retransmission penalty per error = $31,251$ frames! Channel collapses due to massive retransmission storms.
