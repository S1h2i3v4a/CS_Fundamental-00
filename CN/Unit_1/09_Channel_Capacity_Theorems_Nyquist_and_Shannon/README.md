# Module 09: Channel Capacity Theorems: Nyquist & Shannon

## 1. Data Rate Limits ka Parichay
Data rate ka matlab hota hai ki per second kitne bits kisi communication channel par transmit kiye ja sakte hain (bps). Data rate teen parameters par depend karta hai:
1. **Available Bandwidth ($B$ in Hertz)**
2. **Number of Signal Levels ($M$)**
3. **Channel Quality / Noise Level (Signal-to-Noise Ratio: $SNR$)**

Do legendary scientists ne channel data rate ke fundamental mathematical limits diye:
- **Harry Nyquist (1928):** Noiseless (ideal) channel ke liye.
- **Claude Shannon (1948):** Noisy (practical) channel ke liye.

---

## 2. Nyquist Bit Rate Formula (Noiseless Channel)
Agar kisi channel me **zero noise** ho, to maximum theoretical bit rate sirf bandwidth aur discrete signal levels par depend karta hai:

$$C = 2 \cdot B \cdot \log_2(M) 	ext{ bps}$$

- **$B$:** Bandwidth of the channel in Hertz (Hz).
- **$M$:** Number of discrete signal levels (voltage levels) used to represent data.
- **$\log_2(M)$:** Har ek signal element kitne bits carry karta hai.
- **Baud Rate:** Ek noiseless channel me maximum signal rate $S_{	ext{max}} = 2B$ signals/sec (baud) hota hai.

### Critical Insight:
Nyquist formula kehta hai ki agar hum $M$ ko badhate jayein ($M = 2, 4, 8, 16, 64, 256$), to data rate bina kisi limit ke badhta jayega. Par real world me noise hoti hai; agar $M$ bohot zyada ho jaye to do adjacent voltage levels ke beech ka gap itna chhota ho jata hai ki halka sa noise bhi `0` ko `1` bana deta hai!

---

## 3. Shannon Channel Capacity Theorem (Noisy Channel)
Claude Shannon ne prove kiya ki kisi noisy channel (thermal white noise) par bina errors ke transmit karne ka ek absolute physical ceiling hota hai jise **Channel Capacity ($C$)** kehte hain:

$$C = B \cdot \log_2(1 + 	ext{SNR}) 	ext{ bps}$$

- **$B$:** Channel bandwidth in Hertz.
- **$	ext{SNR}$:** Signal-to-Noise Ratio in **Linear Scale** (Power ratio: $rac{P_{	ext{signal}}}{P_{	ext{noise}}}$).
- **Note:** Agar question me SNR Decibels ($	ext{SNR}_{	ext{dB}}$) me diya ho:
  $$	ext{SNR} = 10^{rac{	ext{SNR}_{	ext{dB}}}{10}}$$

### Shannon Theorem ke Key Points:
1. Shannon capacity ek **Upper Bound** hai. Chahe aap 1024 signal levels use karein ya kitna bhi complex modulation karein, aap Shannon capacity se tez error-free data transmit nahi kar sakte.
2. Capacity bandwidth ($B$) aur SNR dono par depend karti hai. Agar noise bohot high hai ($	ext{SNR} 	o 0$), to $C 	o B \log_2(1) = 0$.

---

## 4. Combining Shannon and Nyquist: Finding Signal Levels ($M$)
Practical engineering me hum pehle Shannon formula se theoretical maximum capacity $C$ calculate karte hain. Phir Nyquist formula ko us capacity ke barabar rakhkar hardware ke liye required signal levels $M$ find karte hain:

$$2 \cdot B \cdot \log_2(M) \le B \cdot \log_2(1 + 	ext{SNR})$$
$$\log_2(M) \le rac{1}{2} \log_2(1 + 	ext{SNR})$$
$$M \le \sqrt{1 + 	ext{SNR}}$$

---

## 5. AKTU Past Year Solved Numericals

### Problem 1 (Standard Telephone Line):
Ek telephone subscriber line ki bandwidth $B = 3000	ext{ Hz}$ hai aur uska $	ext{SNR}_{	ext{dB}} = 30	ext{ dB}$ hai. Maximum theoretical channel capacity calculate karein.

**Solution:**
1. Convert $	ext{SNR}_{	ext{dB}}$ to linear scale:
   $$	ext{SNR} = 10^{30 / 10} = 10^3 = 1000$$
2. Apply Shannon Formula:
   $$C = B \cdot \log_2(1 + 	ext{SNR}) = 3000 \cdot \log_2(1 + 1000) = 3000 \cdot \log_2(1001)$$
   $$\log_2(1001) pprox 9.967 	ext{ bits}$$
   $$C = 3000 	imes 9.967 pprox 29,901 	ext{ bps} pprox 30 	ext{ kbps}$$

---

### Problem 2 (Finding Signal Levels $M$):
Ek noiseless channel ki bandwidth $4	ext{ kHz}$ hai. Humein $32	ext{ kbps}$ ka data rate achieve karna hai. Signal me kitne discrete levels ($M$) hone chahiye?

**Solution:**
Nyquist Formula: $C = 2 \cdot B \cdot \log_2(M)$
$$32000 = 2 \cdot 4000 \cdot \log_2(M)$$
$$32000 = 8000 \cdot \log_2(M)$$
$$\log_2(M) = rac{32000}{8000} = 4$$
$$M = 2^4 = 16 	ext{ levels}$$
Har signal element 4 bits carry karega ($16$ distinct voltage levels).
