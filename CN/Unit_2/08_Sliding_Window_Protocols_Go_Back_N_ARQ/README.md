# Module 08: Sliding Window Protocols: Go-Back-N ARQ Architecture

## 1. The Pipelining Concept
Stop-and-Wait ARQ me sender har frame ke baad transmission rok kar ACK ka intezar karta tha, jisse channel capacity waste hoti thi ($a = T_p/T_t$ badhne par $\eta 	o 0$).

**Pipelining** is limitation ko solve karta hai:
- Sender bina pichle ACK ka intezar kiye, back-to-back multiple frames transmit kar sakta hai.
- Outstanding unacknowledged frames ki maximum limit ko **Window Size ($W_S$)** kehte hain.

```
Pipelining Comparison:
Stop-and-Wait:   [Frame 0] ----------------------------> [ACK 1] ===> [Frame 1]
Go-Back-N:       [Frame 0][Frame 1][Frame 2][Frame 3] -> Continuous Stream!
```

---

## 2. Go-Back-N (GBN) ARQ Protocol Mechanics

### 2.1 Window Configurations
- **Sender Window Size ($W_S$):** $W_S = 2^m - 1$ (jahan $m$ sequence number bits hain).
- **Receiver Window Size ($W_R$):** $W_R = 1$ (Receiver sirf strictly agla ordered frame accept karta hai).

### 2.2 Sender Window Pointers
Sender teen variables maintain karta hai:
1. $S_f$ (Sequence First): Sabse pehla (oldest) unacknowledged frame.
2. $S_n$ (Sequence Next): Agla frame jo transmit hone ke liye ready hai.
3. $S_{size}$ (Window Size): Maximum unacknowledged frames allow ($W_S \le 2^m - 1$).

Sender condition check karta hai:
$$S_n - S_f < S_{size}$$

### 2.3 Cumulative Acknowledgments
GBN me ACKs individual nahi balki **Cumulative** hote hain:
- Agar receiver `ACK 4` bhejta hai, iska matlab hai: *"Frames 0, 1, 2, aur 3 safely receive ho gaye hain, ab mujhe Frame 4 chahiye"*.
- **Advantage:** Agar `ACK 2` raste me loose bhi ho jaye, lekin baad me `ACK 3` pahunch jaye, to Frame 2 automatically acknowledged ho jata hai!

### 2.4 Single Timer Rule
Sender sirf **sabse oldest unacknowledged frame ($S_f$)** ke liye ek single timer run karta hai. Jab bhi naya valid ACK aata hai, $S_f$ aage slide hota hai aur timer reset ho jata hai.

---

## 3. Mathematical Proof: Why $W_S \le 2^m - 1$ and NOT $2^m$?

Yeh AKTU BCS603 exam ka favorite conceptual derivation question hai:

> **Theorem:** In Go-Back-N ARQ with $m$-bit sequence numbers, the maximum sender window size must be $2^m - 1$. If $W_S = 2^m$, the protocol fails completely.

### Proof by Contradiction:
Maan lijiye $m = 2$ bits hain.
Possible sequence numbers: $0, 1, 2, 3$ (Total = $2^2 = 4$).

**Suppose we set $W_S = 2^m = 4$:**
1. Sender frames $0, 1, 2, 3$ transmit karta hai.
2. Receiver sabhi 4 frames ($0, 1, 2, 3$) safely receive kar leta hai.
3. Receiver window aage slide hoti hai aur ab wo next round ke frames ka intezar karta hai: Next expected frame is `Frame 0` (sequence wraps around modulo $2^2$).
4. Receiver `ACK 0` (or ACK for all) send karta hai.
5. **Catastrophe:** Maan lijiye link par saare ACKs **LOST** ho jate hain!
6. Sender ka timer expire ho jata hai. Sender unacknowledged frames $0, 1, 2, 3$ ko dubara retransmit karta hai.
7. Receiver ko `Frame 0` milta hai.
8. **The Ambiguity Dilemma:**  
   Receiver ko pata hi nahi chal sakta ki:
   - Kya yeh **Naya Frame 0** hai (previous ACKs sender tak pahunch gaye the)?
   - Ya yeh **Purana Duplicate Frame 0** hai (ACKs raste me destroy ho gaye the)?
9. Receiver ise duplicate detect karne me fail ho jata hai aur purane frame ko duplicate copy ki tarah file me save kar leta hai!

**Conclusion:**  
Ambiguity avoid karne ke liye, Receiver window ($W_R = 1$) aur Sender window ($W_S$) ka sum available sequence numbers se zyada nahi ho sakta:
$$W_S + W_R \le 2^m$$
Kyunki GBN me $W_R = 1$:
$$W_S + 1 \le 2^m \implies \mathbf{W_S \le 2^m - 1}$$

For $m = 3$ bits: $W_S = 2^3 - 1 = 7$.

---

## 4. The Go-Back-N Penalty & Disadvantage
GBN ka sabse bada drawback yeh hai ki **Receiver out-of-order frames ko store nahi kar sakta ($W_R = 1$)**:
- Agar Frame 2 lost ho jata hai, lekin Frame 3, 4, 5 bilkul sahi salamat receiver par pahunch jate hain, to receiver unhe unconditionally **DISCARD** kar deta hai!
- Jab sender ka Timer 2 expire hota hai, to sender ko piche mudna padta hai (**Go-Back**) aur pura unacknowledged window ($2, 3, 4, 5$) dobara retransmit karna padta hai.
- High error rate channels par yeh massive bandwidth waste karta hai.

---

## 5. Efficiency Formula & Optimal Window Size

### 5.1 Efficiency Equation
Pipelined protocol me jab $W_S$ frames pipeline me hote hain:
$$\mathbf{\eta = rac{W_S \cdot T_t}{T_t + 2 \cdot T_p} = rac{W_S}{1 + 2a}}$$
(Condition: $W_S \le 1 + 2a$)

Agar $W_S \ge 1 + 2a$, to transmission pipe continuously full rehti hai aur sender ko kabhi idle nahi hona padta:
$$\mathbf{\eta_{max} = 100\% = 1.0}$$

### 5.2 Optimal Window Size for 100% Utilization
$$W_S \ge 1 + 2a = 1 + 2 \left(rac{T_p}{T_t}ight)$$

Minimum sequence number bits $m$ required for 100% efficiency:
$$2^m - 1 \ge 1 + 2a \implies 2^m \ge 2 + 2a \implies \mathbf{m \ge \lceil \log_2(2 + 2a) ceil}$$

---

## 6. AKTU Solved Numerical: Optimal Window & Bits Derivation

> **Problem Statement (AKTU Semester Exam):**  
> A 1000 km point-to-point link has a bandwidth of 100 Mbps. Propagation speed is $2 	imes 10^8\ 	ext{m/s}$. Frame size is 1000 Bytes.  
> 1. Find the ratio $a = T_p/T_t$.  
> 2. What is the minimum sender window size $W_S$ required to achieve 100% link utilization?  
> 3. How many bits ($m$) are required in the frame sequence number field for Go-Back-N ARQ?  
> 4. If $m = 4$ bits are used, what will be the actual efficiency?

### Step-by-Step Solution:

#### Step 1: Calculate $T_p$ and $T_t$:
$$T_p = rac{	ext{Distance}}{	ext{Speed}} = rac{1000 	imes 10^3\ 	ext{m}}{2 	imes 10^8\ 	ext{m/s}} = 5 	imes 10^{-3}\ 	ext{s} = 5\ 	ext{ms}$$
$$T_t = rac{	ext{Frame Size}}{	ext{Bandwidth}} = rac{1000 	imes 8\ 	ext{bits}}{100 	imes 10^6\ 	ext{bps}} = rac{8000}{10^8} = 8 	imes 10^{-5}\ 	ext{s} = 0.08\ 	ext{ms}$$

Ratio $a$:
$$a = rac{T_p}{T_t} = rac{5\ 	ext{ms}}{0.08\ 	ext{ms}} = \mathbf{62.5}$$

#### Step 2: Optimal Window Size $W_S$ for 100% Utilization:
$$W_S \ge 1 + 2a = 1 + 2(62.5) = 1 + 125 = \mathbf{126\ 	ext{Frames}}$$

#### Step 3: Minimum Sequence Number Bits $m$:
For Go-Back-N:
$$W_S = 2^m - 1 \ge 126$$
$$2^m \ge 127$$
$$2^7 = 128 \ge 127 \implies \mathbf{m = 7\ 	ext{Bits}}$$
Sequence number field me kam se kam 7 bits hone chahiye.

#### Step 4: Actual Efficiency if $m = 4$ Bits are used:
If $m = 4$:
$$W_S = 2^4 - 1 = 15$$
Efficiency:
$$\eta = rac{W_S}{1 + 2a} = rac{15}{126} pprox \mathbf{0.119\ (11.9\%)}$$
7 bits ki jagah 4 bits use karne par link utilization 100% se gir kar sirf 11.9% reh jayega!
