# Module 03: Dynamic Storage Allocation Strategies

> **Unit 4: Memory Management** | *B.Tech CS/IT/Allied (AKTU BCS401)*

---

## 1. The Dynamic Storage Allocation Problem

Variable Partition Allocation (MVT) me jab memory me alag-alag size ke free holes ki list hoti hai, to ek naye process $P$ (size $S$) ko kis hole me allocate kiya jaye?
Is problem ko solve karne ke liye 4 standard strategies use hoti hain:

1. **First Fit**
2. **Best Fit**
3. **Worst Fit**
4. **Next Fit**

---

## 2. Algorithm Details & Comparison

### 2.1 First Fit
- **Algorithm:** Free list ke starting pointer se scan karo. Jo pehla hole mila jiska size $\ge S$, wahi allocate kar do.
- **Performance:** Speed ke hisaab se sabse fast hai kyunki poori list traverse karne ki zaroorat nahi padti.
- **Drawback:** Memory ke shuruati hisse me chhote-chhote leftover fragments jam ho jate hain.

### 2.2 Best Fit
- **Algorithm:** Poori list traverse karke wo hole dhoondho jiska size process size se bada ya barabar ho, par leftover hole **smallest** ho:
  $$\min (	ext{Hole Size} - S) \quad 	ext{such that } 	ext{Hole Size} \ge S$$
- **Advantage:** Badi size ke holes preserve rehte hain future ke large processes ke liye.
- **Drawback:** Ye sabse chhote leftover holes chhodta hai jo itne chhote hote hain ki future me kisi kaam nahi aate (Worst external fragmentation). Poori list scan karne me time lagta hai ($O(n)$).

### 2.3 Worst Fit
- **Algorithm:** Poori list me se **sabse bada available hole** dhoondho aur process ko usme allocate karo.
- **Intuition:** Large hole me se allocate karne ke baad jo leftover block bachega, wo kafi bada hoga taaki future me koi doosra chhota process usme fit ho sake.
- **Drawback:** Large processes ke liye bade blocks jaldi exhaust ho jate hain. Poori list scan karni padti hai ($O(n)$).

### 2.4 Next Fit
- First Fit ka variation. Har baar shuru se scan karne ke bajaye, pichhle allocation ke pointer se scanning start karta hai (Circular search).
- Poori memory me allocations ko evenly distribute karta hai.

---

## 3. Compaction (Defragmentation)

External fragmentation ko solve karne ka contiguous memory me ekmatra tarika **Compaction** hai:
- Saare running processes ko memory ke ek taraf (low addresses) push kiya jata hai, jisse saari scattered free space judkar ek single large continuous free block ban jati hai.
- **Mandatory Requirement:** Compaction tabhi sambhav hai jab system me **Execution Time Dynamic Relocation** supported ho (Base register update karke). Agar compile-time ya load-time binding hai, to compaction impossible hai.
- **Overhead:** Extremely high I/O aur CPU copying overhead.

---

## 4. Architectural Diagram

![Dynamic Storage Allocation Strategies](diagrams/allocation_strategies.svg)

---

## 5. Comprehensive Solved Numerical (Standard AKTU Exam Pattern)

### Problem:
Memory me nimn 5 free holes available hain (order me):
`100 KB, 500 KB, 200 KB, 300 KB, 600 KB`

Sequential order me 4 processes arrive hote hain:
- $P_1 = 212	ext{ KB}$
- $P_2 = 417	ext{ KB}$
- $P_3 = 112	ext{ KB}$
- $P_4 = 426	ext{ KB}$

Calculate kijiye ki First Fit, Best Fit, aur Worst Fit ke tehat kaunsa process kis hole me jayega, aur kya koi process wait karega?

---

### Step-by-Step Solution & Thought Process:

#### Strategy 1: First Fit
- **Initial Holes:** `H1(100), H2(500), H3(200), H4(300), H5(600)`
1. **$P_1 (212	ext{ KB})$:**
   - H1(100) $	o$ Too small.
   - H2(500) $	o$ Fits! Allocated to **H2**.
   - Remaining in H2 = $500 - 212 = 288	ext{ KB}$.
2. **$P_2 (417	ext{ KB})$:**
   - Scan from start: H1(100) $	o$ No; H2(288) $	o$ No; H3(200) $	o$ No; H4(300) $	o$ No; H5(600) $	o$ Fits!
   - Allocated to **H5**.
   - Remaining in H5 = $600 - 417 = 183	ext{ KB}$.
3. **$P_3 (112	ext{ KB})$:**
   - Scan from start: H1(100) $	o$ No; H2(288) $	o$ Fits!
   - Allocated to **H2**.
   - Remaining in H2 = $288 - 112 = 176	ext{ KB}$.
4. **$P_4 (426	ext{ KB})$:**
   - Current holes: H1(100), H2(176), H3(200), H4(300), H5(183).
   - Largest available hole is 300 KB.
   - $P_4(426	ext{ KB})$ **MUST WAIT! (Cannot be allocated)**.

#### Strategy 2: Best Fit
- **Initial Holes:** `H1(100), H2(500), H3(200), H4(300), H5(600)`
1. **$P_1 (212	ext{ KB})$:**
   - Candidates ($\ge 212$): H2(500), H4(300), H5(600).
   - Smallest among candidates is H4(300).
   - Allocated to **H4**. Remaining in H4 = $300 - 212 = 88	ext{ KB}$.
2. **$P_2 (417	ext{ KB})$:**
   - Candidates ($\ge 417$): H2(500), H5(600).
   - Smallest candidate is H2(500).
   - Allocated to **H2**. Remaining in H2 = $500 - 417 = 83	ext{ KB}$.
3. **$P_3 (112	ext{ KB})$:**
   - Candidates ($\ge 112$): H3(200), H5(600).
   - Smallest candidate is H3(200).
   - Allocated to **H3**. Remaining in H3 = $200 - 112 = 88	ext{ KB}$.
4. **$P_4 (426	ext{ KB})$:**
   - Candidates ($\ge 426$): Only H5(600).
   - Allocated to **H5**! Remaining in H5 = $600 - 426 = 174	ext{ KB}$.
- **Result:** **ALL 4 PROCESSES ALLOCATED SUCCESSFULLY!**

#### Strategy 3: Worst Fit
- **Initial Holes:** `H1(100), H2(500), H3(200), H4(300), H5(600)`
1. **$P_1 (212	ext{ KB})$:**
   - Largest hole is H5(600). Allocated to **H5**.
   - Remaining in H5 = $600 - 212 = 388	ext{ KB}$.
2. **$P_2 (417	ext{ KB})$:**
   - Largest hole is H2(500). Allocated to **H2**.
   - Remaining in H2 = $500 - 417 = 83	ext{ KB}$.
3. **$P_3 (112	ext{ KB})$:**
   - Current holes: H1(100), H2(83), H3(200), H4(300), H5(388).
   - Largest hole is H5(388). Allocated to **H5**.
   - Remaining in H5 = $388 - 112 = 276	ext{ KB}$.
4. **$P_4 (426	ext{ KB})$:**
   - Current holes: H1(100), H2(83), H3(200), H4(300), H5(276).
   - Largest available hole is 300 KB.
   - $P_4(426	ext{ KB})$ **MUST WAIT!**

### Conclusion:
Iss specific problem me **Best Fit** ne sabhi 4 processes ko successfully allocate kiya, jabki First Fit aur Worst Fit me $P_4$ block ho gaya.
