# Module 12: Counting Algorithms and Clock Replacement

> **Unit 4: Memory Management** | *B.Tech CS/IT/Allied (AKTU BCS401)*

---

## 1. Second Chance (Clock) Replacement Algorithm

Pure LRU ko implement karne me hardware overhead bahut bada hota hai (har access par stack update ya timestamp counter). Isliye modern operating systems LRU ka ek efficient approximation use karte hain jise **Second Chance (Clock) Algorithm** kehte hain.

### 1.1 Working Principle:
- Har page table entry me ek **Reference Bit ($R$)** hota hai (CPU hardware dwara set to `1` on read/write).
- Pages circular queue me arranged hote hain aur ek **Clock Pointer** hota hai.
- **Replacement Logic:**
  1. Pointer current page ko inspect karta hai:
  2. **Agar $R == 0$:** Is page ko replace kar do (Victim found!). Pointer ko agle page par shift karo.
  3. **Agar $R == 1$:** Is page ko **Second Chance** do! Iska bit reset karke $R = 0$ banao, aur pointer ko clockwise aage ghuma kar agle page ko check karo.
  4. Worst case me agar sabhi pages ke bits $1$ hain, to pointer poora circle ghoomkar sabko $0$ karta jayega aur wapas starting page ko replace kar dega (Degenerates into FIFO).

---

## 2. Enhanced Second Chance Algorithm

Clock algorithm ko further optimize karne ke liye Operating System do bits ke pair ko inspect karta hai:
$$\langle 	ext{Reference Bit } (R), 	ext{ Modify Bit } (M) angle$$

Kernel memory ko 4 classes me categorize karta hai:
1. **Class 1 (0, 0):** Neither recently used nor modified $\implies$ **BEST VICTIM!** (Disk write nahi karni padegi, access latency zero).
2. **Class 2 (0, 1):** Not recently used, but modified $\implies$ Replaceable, but requires disk write before eviction.
3. **Class 3 (1, 0):** Recently used, but clean $\implies$ Likely to be used again soon.
4. **Class 4 (1, 1):** Recently used and modified $\implies$ **WORST CANDIDATE!**

**Algorithm:** Clock pointer poori queue ko scan karke lowest non-empty class ke pehle page ko replace karta hai.

---

## 3. Counting-Based Page Replacement

Operating system har page ke references ka ek software counter maintain karta hai:

### 3.1 LFU (Least Frequently Used)
- **Principle:** Us page ko replace karo jiska reference count sabse chhota hai.
- **Intuition:** Heavily used pages ka count bada hoga aur wo RAM me rahenge.
- **Flaw:** Initial phase me bohot use hone wala page (e.g., initialization routine) lifetime memory me atka rehta hai chahe baad me kabhi use na ho (Solution: Counter aging/decay).

### 3.2 MFU (Most Frequently Used)
- **Principle:** Us page ko replace karo jiska reference count sabse bada hai.
- **Intuition:** Aisa page jo abhi-abhi memory me laya gaya hai uska count $0$ ya $1$ hoga, isliye use thoda time execution ke liye milna chahiye.

---

## 4. Architectural Diagram

![Clock and Counting Page Replacement](diagrams/clock_and_counting.svg)
