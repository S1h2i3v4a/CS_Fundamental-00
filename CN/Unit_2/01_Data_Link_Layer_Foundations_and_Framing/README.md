# Module 01: Data Link Layer Foundations & Framing Techniques

## 1. Data Link Layer (DLL) ke Core Functions
Data Link Layer OSI model ki Layer 2 hai. Iska primary responsibility raw physical bit-stream ko reliable, error-free **Frames** me convert karna aur adjacent nodes ke beech hop-to-hop delivery guarantee karna hai.

### 1.1 DLL ke do Sublayers (IEEE 802 Standard)
1. **LLC (Logical Link Control - IEEE 802.2):**
   - Upper sublayer jo Network layer (IP) ke sath interface karti hai.
   - Hardware-independent hoti hai (chahe niche Ethernet ho, Wi-Fi ho ya Token Ring).
   - Multiplexing, flow control, aur error notification handle karti hai.
2. **MAC (Medium Access Control):**
   - Lower sublayer jo Physical layer ke sath interact karti hai.
   - Hardware-dependent hoti hai (e.g., IEEE 802.3 for Ethernet, 802.11 for Wi-Fi).
   - 48-bit physical MAC address add karti hai aur shared channel par access control regulate karti hai.

---

## 2. Framing: Concept & Types
Physical layer raw bits ka unformatted continuous stream deti hai. Receiver ko yeh pata hona chahiye ki ek message kahan se shuru hota hai aur kahan khatam hota hai. Is boundary demarcation process ko **Framing** kehte hain.

### 2.1 Fixed-Size Framing vs Variable-Size Framing
- **Fixed-Size Framing:** Har frame ki length strictly fixed hoti hai (e.g., ATM cells with 53 bytes: 5 byte header + 48 byte payload). Isme end boundary demarcate karne ki zaroorat nahi hoti, par internal fragmentation waste hoti hai.
- **Variable-Size Framing:** Frames alag-alag lengths ke ho sakte hain (e.g., Ethernet 64 to 1518 bytes). Isme boundary define karne ke liye delimiter flags use kiye jate hain.

---

## 3. Framing Approaches in Detail

### 3.1 Character Count Method
- Frame ke header me pehla field ek integer hota hai jo frame me total characters ki sankhya batata hai.
- *Problem:* Agar transmission noise ke karan character count ka ek bit bhi corrupt ho jaye (e.g., `5` becomes `7`), to receiver desynchronize ho jata hai aur aage ke sabhi frames corrupt treat hote hain (**Catastrophic Framing Error**).

### 3.2 Byte Stuffing (Character-Oriented Framing)
- Frame ke start aur end par ek special **FLAG byte** lagaya jata hai (e.g., `01111110` ya ASCII `DLE STX` / `DLE ETX`).
- **Transparency Problem:** Agar user ke original data me wahi exact FLAG byte sequence aa jaye, to receiver use prematurely end-of-frame samajh lega!
- **Byte Stuffing Solution:**
  - Sender data stream ko scan karta hai. Jahan bhi FLAG byte ya ESC byte aata hai, sender uske theek pehle ek special **ESC (Escape) byte** insert (stuff) kar deta hai.
  - Receiver jab bhi ESC byte dekhta hai, wo use drop kar deta hai aur uske agle byte ko normal data treat karta hai.

```
Original Data:    [DATA A]  [FLAG]  [DATA B]  [ESC]  [DATA C]
Transmitted:      FLAG [DATA A] [ESC][FLAG] [DATA B] [ESC][ESC] [DATA C] FLAG
```

### 3.3 Bit Stuffing (Bit-Oriented Framing - HDLC / SDLC / PPP)
- Modern networks me frames arbitrary bits ka stream hote hain (byte boundary uri nahi).
- Frame delimiter FLAG pattern hamesha hota hai:
  $$	ext{FLAG} = 01111110 \quad (	ext{Six consecutive 1s flanked by 0s})$$
- **The 5-Consecutive-Ones Rule:**
  - Sender jab bhi data me **five consecutive 1s (`11111`)** dekhta hai, wo bina soche uske theek baad ek **`0` bit** inject (stuff) kar deta hai!
  - Chahe agla bit originally `0` ho ya `1`, sender `0` zaroor daalega taaki data me kabhi bhi 6 consecutive 1s na ban sakein.
  - Receiver side: Receiver data me jab bhi 5 consecutive 1s ke baad `0` dekhta hai, wo us `0` ko discard (destuff) kar deta hai. Agar 5 ones ke baad `1` aur phir `0` aata hai, to wo actual FLAG hota hai!

---

## 4. AKTU Solved Numerical: Bit Stuffing
**Question (AKTU Exam):** Bit sequence `000111111101111101111110` ko bit-stuffing rule se encode karein.

**Solution:**
Original bits: `0 0 0 1 1 1 1 1 1 1 0 1 1 1 1 1 0 1 1 1 1 1 1 0`
1. First group: `0 0 0 1 1 1 1 1` $	o$ 5 ones detected! Insert `0` $\implies$ `0 0 0 1 1 1 1 1 [0] 1 1 0`
2. Second group: `1 1 1 1 1` $	o$ 5 ones detected! Insert `0` $\implies$ `1 1 1 1 1 [0] 0`
3. Third group: `1 1 1 1 1` $	o$ 5 ones detected! Insert `0` $\implies$ `1 1 1 1 1 [0] 1 0`
Stuffed bitstream: `000111110110111110011111010` wrapped inside starting and ending `01111110` flags.
