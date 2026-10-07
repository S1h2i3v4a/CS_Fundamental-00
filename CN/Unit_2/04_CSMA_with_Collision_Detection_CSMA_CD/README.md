# Module 04: CSMA with Collision Detection (CSMA/CD)

## 1. The Need for Collision Detection
CSMA me stations transmit karne se pehle channel sense karti hain, par finite propagation delay ($T_p$) ke karan collisions fir bhi ho sakti hain.
- Pure CSMA me agar collision ho jaye, to stations tab bhi apna pura lamba frame transmit karti rehti hain (chahe data corrupt ho chuka ho), jisse massive channel bandwidth waste hoti hai.
- **CSMA/CD (Collision Detection)** is problem ko solve karta hai: Station transmit karte waqt bhi medium ko continuously monitor karti rehti hai (**"Listen While Talk"**).

---

## 2. Operation of CSMA/CD
1. **Transmit & Monitor:** Station frame transmit karna shuru karti hai aur sath me channel ka voltage measure karti rehti hai.
2. **Collision Detection:**
   - Agar do signals aapas me collide karte hain, to channel par voltage normal level se double ($> 2 V$) spike ho jata hai.
   - Voltage spike detect hote hi transceiver turant samajh jata hai ki Collision ho gaya hai.
3. **Immediate Abort:** Station apna baaki ka frame transmit karna turant cancel kar deti hai.
4. **Jam Signal Broadcast:** Station ek 32-bit ya 48-bit ka **Jam Signal** transmit karti hai taaki cable par juddi baaki sabhi stations ko confirm ho jaye ki collision hua hai aur wo corrupt bits ko discard karein.
5. **Exponential Backoff:** Retransmission attempt karne se pehle station random time wait karti hai.

---

## 3. Mathematical Condition: $T_t \ge 2 \cdot T_p$ (AKTU Core Derivation)

Station ko collision ka pata tabhi chal sakta hai jab wo khud transmit kar rahi ho! Agar frame itna chhota ho ki collision ka signal laut kar aane se pehle hi frame transmission complete ho jaye, to sender samjhega ki frame safely pahunch gaya, jabki receiver par garbage deliver hua hoga!

### Worst-Case Collision Timing:
- Time $t = 0$: Host A transmission shuru karta hai.
- Time $t = T_p - \epsilon$: Signal cable ke doosre end par Host B ke paas pahunchne hi wala hota hai ki B transmit kar deta hai.
- Time $t = T_p$: Collision B ke paas hota hai.
- Time $t = 2 \cdot T_p$: Collision ka electrical noise signal laut kar Host A tak pahunchta hai.

Isliye sender A ko kam se kam $2 \cdot T_p$ (Round Trip Time) tak transmit karte rehna zaroori hai:

$$T_t \ge 2 \cdot T_p$$

### Minimum Frame Size ($L_{	ext{min}}$) Derivation:
$$T_t = rac{L}{B}$$
$$rac{L}{B} \ge 2 \cdot T_p \implies L_{	ext{min}} = 2 \cdot T_p \cdot B 	ext{ bits}$$

- **$L_{	ext{min}}$:** Minimum allowable frame size (bits me).
- **$T_p$:** Propagation delay across maximum network distance ($d/v$).
- **$B$:** Bandwidth of the network (bps me).

---

## 4. Why Ethernet Minimum Frame Size is Exactly 64 Bytes?
Traditional 10 Mbps Ethernet (10Base5):
- Maximum cable distance $d = 2500	ext{ m}$ (with 4 repeaters).
- Propagation speed $v = 2 	imes 10^8	ext{ m/s}$.
- $T_p = rac{2500}{2 	imes 10^8} = 12.5\ \mu	ext{s}$.
- Round-trip time with repeater delays $pprox 51.2\ \mu	ext{s}$ (Slot Time).
- Minimum Frame Size:
  $$L_{	ext{min}} = 2 \cdot T_p \cdot B = 51.2\ \mu	ext{s} 	imes 10	ext{ Mbps} = 512	ext{ bits} = rac{512}{8} = \mathbf{64	ext{ Bytes}}$$
Isliye Ethernet standard me frame minimum 64 bytes ka hona mandatory hai! Agar user data 46 bytes se kam ho, to padding bits add kiye jate hain.

---

## 5. Binary Exponential Backoff (BEB) Algorithm
Collision ke baad stations dobara aapas me na takrayein, iske liye har station random wait time calculate karti hai:

$$	ext{Backoff Wait Time} = R 	imes 	ext{Slot Time}$$
Jahan $R$ ek integer random number hai jo uniformly pick kiya jata hai:
$$0 \le R \le 2^k - 1$$
- $k$: Collision count (Current collision number).
- Collision 1 ($k=1$): $R \in \{0, 1\}$. (Either 0 or 1 slot wait).
- Collision 2 ($k=2$): $R \in \{0, 1, 2, 3\}$.
- Collision 3 ($k=3$): $R \in \{0, 1, 2, \dots, 7\}$.
- Maximum backoff exponent cap: $k = 10 \implies R \in \{0, 1, \dots, 1023\}$.
- Maximum 16 attempts ($k = 16$): Agar 16 collisions ke baad bhi frame transmit na ho, to frame drop ho jata hai aur system error report karta hai.

---

## 6. AKTU Solved Numerical
**Question (AKTU Exam):** Ek 1 km lambi 100 Mbps CSMA/CD network me velocity of propagation $v = 2 	imes 10^8	ext{ m/s}$ hai. Minimum frame size calculate karein.

**Solution:**
1. Distance $d = 1	ext{ km} = 1000	ext{ m}$.
2. Propagation Delay:
   $$T_p = rac{d}{v} = rac{1000}{2 	imes 10^8} = 5 	imes 10^{-6}	ext{ s} = 5\ \mu	ext{s}$$
3. Bandwidth $B = 100	ext{ Mbps} = 10^8	ext{ bps}$.
4. Minimum Frame Size:
   $$L_{	ext{min}} = 2 \cdot T_p \cdot B = 2 	imes (5 	imes 10^{-6}	ext{ s}) 	imes (10^8	ext{ bps}) = 1000	ext{ bits} = 125	ext{ Bytes}$$
