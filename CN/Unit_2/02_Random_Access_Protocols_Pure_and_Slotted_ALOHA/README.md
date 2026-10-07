# Module 02: Random Access Protocols: Pure & Slotted ALOHA

## 1. Random Access (Contention) Protocols
Jab multiple stations ek common shared channel ko access karti hain, to koi centralized controller nahi hota jo yeh decide kare ki agla turn kiska hai. Stations medium ko access karne ke liye aapas me compete karti hain (**Contention Method**).
- Agar do ya do se adhik stations ek sath transmit karein, to access conflict (**Collision**) hota hai aur frames destroy ho jate hain.
- **ALOHA** protocol ko Norman Abramson ne 1970 me University of Hawaii me design kiya tha radio broadcasting ke through islands ko connect karne ke liye.

---

## 2. Pure ALOHA vs Slotted ALOHA

### 2.1 Pure ALOHA (Continuous Time)
- **Rule:** Har station jab chahe tab transmit kar sakti hai.
- **Vulnerable Time ($V_t$):** Pure ALOHA me ek frame $T_{fr}$ duration tak transmit hota hai. Agar koi doosri station frame transmit hone se theek pehle ($t - T_{fr}$) ya frame transmit hone ke dauran ($t + T_{fr}$) transmit kar de, to collision ho jayega:
  $$V_t = 2 	imes T_{fr}$$
- **Throughput Formula ($S$):**
  $$S = G \cdot e^{-2G}$$
  - Jahan $G$ total generated traffic load hai (frames per frame time).
  - Maximum Throughput tab milta hai jab $rac{dS}{dG} = 0 \implies G = rac{1}{2} = 0.5$:
    $$S_{	ext{max}} = 0.5 \cdot e^{-1} = rac{1}{2e} pprox 0.184 \quad (18.4\%)$$
  - Pure ALOHA me channel bandwidth ka maximum 18.4% hi successful transmission me use hota hai; baaki 81.6% collisions me waste hota hai!

### 2.2 Slotted ALOHA (Discrete Time)
- **Rule:** Channel time ko discrete synchronized slots me divide kiya jata hai (har slot ka time $= T_{fr}$). Station sirf aur sirf **agle slot ke shuruat par** hi transmit kar sakti hai.
- **Vulnerable Time ($V_t$):** Agar do stations same slot me transmit karti hain to collision hota hai, par adjacent slots me collision nahi ho sakta:
  $$V_t = 1 	imes T_{fr}$$
- **Throughput Formula ($S$):**
  $$S = G \cdot e^{-G}$$
  - Maximum Throughput tab milta hai jab $G = 1.0$:
    $$S_{	ext{max}} = 1.0 \cdot e^{-1} = rac{1}{e} pprox 0.368 \quad (36.8\%)$$
  - Slotted ALOHA Pure ALOHA ki capacity ko **exact double ($2	imes$)** kar deta hai!

---

## 3. Comparison Matrix

| Evaluation Parameter | Pure ALOHA | Slotted ALOHA |
| :--- | :--- | :--- |
| **Synchronization Required** | **None** (Continuous time, uncoordinated) | **Mandatory** (Global clock synchronizes slot boundaries) |
| **Transmission Start Time** | Any arbitrary instant | Strictly at the start of a time slot |
| **Vulnerable Time Window** | $2 	imes T_{fr}$ | $1 	imes T_{fr}$ |
| **Throughput Formula** | $S = G \cdot e^{-2G}$ | $S = G \cdot e^{-G}$ |
| **Maximum Efficiency ($S_{	ext{max}}$)** | **18.4%** at $G = 0.5$ | **36.8%** at $G = 1.0$ |
| **Collision Probability** | Very High | Half of Pure ALOHA |
| **Hardware Complexity** | Extremely Simple | Requires master clock synchronization |

---

## 4. AKTU Solved Numerical Problems

### Problem 1 (AKTU Exam):
*Ek Slotted ALOHA channel me measurement se pata chala ki 10% slots idle hain. Find karein:*
1. Channel load ($G$)
2. Throughput ($S$)
3. Channel underloaded hai ya overloaded?

**Solution:**
Poisson distribution me $k = 0$ frames generate hone ki probability (idle slot):
$$P(0) = e^{-G}$$
Given: $10\% 	ext{ idle} \implies P(0) = 0.10$
1. **Channel Load ($G$):**
   $$e^{-G} = 0.10 \implies -G = \ln(0.10) = -2.302 \implies G pprox 2.3$$
2. **Throughput ($S$):**
   $$S = G \cdot e^{-G} = 2.3 	imes 0.10 = 0.23 \quad (23\%)$$
3. **Channel Status:**
   Slotted ALOHA maximum throughput $G = 1.0$ par achieve karta hai. Yahan $G = 2.3 > 1.0$, isliye channel **Overloaded** hai (too many collision retransmissions).

---

### Problem 2 (AKTU Exam):
*Ek Slotted ALOHA shared channel ki bandwidth $400	ext{ kbps}$ hai aur frame size $400	ext{ bits}$ hai. Throughput calculate karein agar system:*
*(a) 1000 frames/sec (b) 500 frames/sec (c) 250 frames/sec produce kare.*

**Solution:**
Frame transmission time: $T_{fr} = rac{400	ext{ bits}}{400	ext{ kbps}} = rac{400}{400,000} = 1	ext{ ms} = 0.001	ext{ s}$.
Channel capacity in frames/sec $= rac{1}{T_{fr}} = 1000	ext{ frames/sec}$.

- **(a) For 1000 frames/sec:**
  $$G = rac{1000}{1000} = 1.0 \implies S = G e^{-G} = 1.0 	imes e^{-1} = 0.368$$
  Throughput $= 0.368 	imes 1000 = \mathbf{368	ext{ frames/sec}} \quad (147.2	ext{ kbps})$.
- **(b) For 500 frames/sec:**
  $$G = rac{500}{1000} = 0.5 \implies S = 0.5 	imes e^{-0.5} = 0.5 	imes 0.6065 = 0.303$$
  Throughput $= 0.303 	imes 1000 = \mathbf{303	ext{ frames/sec}} \quad (121.2	ext{ kbps})$.
- **(c) For 250 frames/sec:**
  $$G = rac{250}{1000} = 0.25 \implies S = 0.25 	imes e^{-0.25} = 0.25 	imes 0.7788 = 0.195$$
  Throughput $= 0.195 	imes 1000 = \mathbf{195	ext{ frames/sec}} \quad (78	ext{ kbps})$.
