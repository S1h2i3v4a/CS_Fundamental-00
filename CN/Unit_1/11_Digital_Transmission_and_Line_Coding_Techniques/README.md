# Module 11: Digital Transmission & Line Coding Techniques

## 1. Line Coding Fundamentals
Line coding digital data (sequence of binary `0`s and `1`s) ko digital signals (discrete voltage levels) me convert karne ka process hai. Transmitter hardware computer memory ke bits ko physical medium par travel karne layak waveform me encode karta hai.

### 1.1 Line Coding ke 5 Crucial Criteria (Exam Theory)
1. **Signal Level vs Data Level ($r$):**
   - $r = rac{	ext{Data elements (bits)}}{	ext{Signal elements}}$.
   - Signal rate (Baud rate) $S = c 	imes N 	imes rac{1}{r}$, jahan $N$ data rate (bps) hai aur $c$ case factor hai ($0 \le c \le 1$).
2. **DC Component (Direct Current):**
   - Agar voltage levels ka average non-zero ho, to signal me DC component create hota hai. DC components transformers aur AC-coupled circuits pass nahi kar sakte. Good line coding me **Zero DC Component** hona chahiye.
3. **Self-Synchronization:**
   - Receiver clock sender clock se drift ho sakti hai. Signal ke andar frequent transitions hone chahiye taaki receiver un transitions se apna clock synchronise kar sake (prevent bit slipping).
4. **Baseline Wandering:**
   - Consecutive identical bits (`0000...` ya `1111...`) aane par receiver ka voltage reference baseline shift ho jata hai, jisse decoding error aate hain.
5. **Noise Immunity & Bandwidth:**
   - Minimum bandwidth consume honi chahiye aur error detection capability honi chahiye.

---

## 2. Line Coding Schemes ka Master Classification

### 2.1 Unipolar Scheme (NRZ - Non-Return to Zero)
- Sirf ek polarity voltage use hoti hai (positive vs zero).
- `1` $\implies$ High Voltage ($+V$), `0` $\implies$ Zero Voltage ($0	ext{ V}$).
- *Problems:* Severe DC component aur long runs of `0`s ya `1`s me zero self-synchronization.

### 2.2 Polar Schemes
Voltage dono sides swing karti hai (positive $+V$ aur negative $-V$). Average DC level kam hota hai.
1. **Polar NRZ-L (NRZ-Level):**
   - Signal ka voltage level bit ki value decide karta hai.
   - Typically: `0` $\implies$ Positive level ($+V$), `1` $\implies$ Negative level ($-V$).
2. **Polar NRZ-I (NRZ-Invert):**
   - Signal level tab change/invert hota hai jab bit `1` encounter hoti hai.
   - `0` $\implies$ No change in signal level (stay same).
   - `1` $\implies$ Inversion at the start of bit interval.
3. **Polar RZ (Return-to-Zero):**
   - Signal mid-interval me `0 V` par return karta hai.
   - Har bit ke beech transition hota hai $\implies$ Good synchronization.
   - *Problem:* Requires 3 voltage levels ($+V, 0, -V$) aur double bandwidth consume karta hai.
4. **Biphase: Manchester Encoding (IEEE 802.3 Ethernet Standard):**
   - Har bit interval ke theek beech me (mid-bit) mandatory transition hota hai:
     - Bit `0` $\implies$ High-to-Low transition (↓).
     - Bit `1` $\implies$ Low-to-High transition (↑).
   - *Benefit:* Guaranteed synchronization for every bit; Zero DC component. Baud rate $= 2 	imes$ Bit rate.
5. **Biphase: Differential Manchester:**
   - Mid-bit transition hamesha synchronization ke liye hota hai.
   - Bit `0` $\implies$ Transition at the BEGINNING of bit interval.
   - Bit `1` $\implies$ NO transition at the beginning of bit interval.

### 2.3 Bipolar Schemes (Multilevel Binary)
Three voltage levels use hote hain: Positive ($+V$), Zero ($0	ext{ V}$), aur Negative ($-V$).
1. **Bipolar AMI (Alternate Mark Inversion):**
   - Bit `0` $\implies$ Strictly Zero voltage ($0	ext{ V}$).
   - Bit `1` $\implies$ Alternating positive ($+V$) aur negative ($-V$) voltages.
   - *Benefit:* Zero DC component, single-bit error detection (agar do consecutive `+V` aa jayein to violation detect ho jata hai).

---

## 3. AKTU Solved Problem: Waveform Drawing
**Question (AKTU 2022-23):** Bit sequence `01001110` ke liye Polar NRZ-L aur Polar NRZ-I schemes construct karein.

**Detailed Step-by-Step Construction:**
- **Bit stream:** `[0, 1, 0, 0, 1, 1, 1, 0]`
- **Polar NRZ-L:**
  - Bit 0: $+V$ (High)
  - Bit 1: $-V$ (Low)
  - Bit 0: $+V$ (High)
  - Bit 0: $+V$ (High)
  - Bit 1: $-V$ (Low)
  - Bit 1: $-V$ (Low)
  - Bit 1: $-V$ (Low)
  - Bit 0: $+V$ (High)
- **Polar NRZ-I (Assuming initial level was $+V$):**
  - Bit 0: No transition $	o$ stays $+V$.
  - Bit 1: Transition at start $	o$ flips to $-V$.
  - Bit 0: No transition $	o$ stays $-V$.
  - Bit 0: No transition $	o$ stays $-V$.
  - Bit 1: Transition at start $	o$ flips to $+V$.
  - Bit 1: Transition at start $	o$ flips to $-V$.
  - Bit 1: Transition at start $	o$ flips to $+V$.
  - Bit 0: No transition $	o$ stays $+V$.
