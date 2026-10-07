# Module 05: Translation Lookaside Buffer (TLB) and EMAT

> **Unit 4: Memory Management** | *B.Tech CS/IT/Allied (AKTU BCS401)*

---

## 1. Pure Paging ki Double Memory Access Samasya

Pure paging architecture me CPU ko kisi bhi memory address ko access karne ke liye RAM ko **do baar access** karna padta hai:
1. **Access 1:** Page Table se Frame Number $f$ dhoondhne ke liye (RAM access).
2. **Access 2:** Actual data ya instruction ko read/write karne ke liye (RAM access).

Iska matlab memory access time sidha **double (100% slow down)** ho jata hai! Agar RAM access time $100	ext{ ns}$ hai, to har reference me $200	ext{ ns}$ lagte hain.

---

## 2. TLB (Translation Lookaside Buffer) Architecture

Is samasya ko solve karne ke liye CPU chip me ek ultra-fast associative hardware cache integrate kiya jata hai jise **TLB (Translation Lookaside Buffer)** kehte hain.

### 2.1 TLB Key Characteristics:
- **Speed:** $1 - 10	ext{ ns}$ (SRAM cells par bana hota hai).
- **Search Type:** Fully associative hardware search; saari entries ko ek hi clock cycle me simultaneously compare kiya jata hai.
- **Capacity:** Chhota size (typically 32 se 1024 entries).
- **Entries:** $\langle 	ext{Page Number } (p), 	ext{Frame Number } (f) angle$.

### 2.2 Translation Flow:
1. CPU logical address generate karta hai: $(p, d)$.
2. Hardware simultaneously TLB me Page $p$ search karta hai.
3. **TLB Hit (Probability $h$):**
   - Frame $f$ turant mil jata hai.
   - Physical address banta hai aur direct RAM se data access hota hai.
   - Total Time = $t_{	ext{TLB}} + t_{	ext{RAM}}$.
4. **TLB Miss (Probability $1 - h$):**
   - Page $p$ TLB me nahi hai.
   - CPU ko RAM ke Page Table me jana padta hai (1st RAM access).
   - Frame $f$ milne ke baad TLB ko naye $\langle p, f angle$ pair se update kiya jata hai (taaki future me hit ho).
   - Finally actual data access hota hai (2nd RAM access).
   - Total Time = $t_{	ext{TLB}} + 2 	imes t_{	ext{RAM}}$.

---

## 3. Effective Memory Access Time (EMAT / EAT) Formula

$$	ext{EMAT} = h 	imes (t_{	ext{TLB}} + t_{	ext{RAM}}) + (1 - h) 	imes (t_{	ext{TLB}} + 2 	imes t_{	ext{RAM}})$$

Simplifying:
$$	ext{EMAT} = t_{	ext{TLB}} + t_{	ext{RAM}} + (1 - h) 	imes t_{	ext{RAM}} = t_{	ext{TLB}} + (2 - h) 	imes t_{	ext{RAM}}$$

> **Note on Notation:** Agar question me explicitly diya ho ki TLB search aur Page table search parallel hote hain ya TLB search time ignore kiya gaya hai, to formula adjust hota hai. Standard AKTU questions me upar diya gaya formula use hota hai.

---

## 4. Page Protection & Valid-Invalid Bits

Page table me frame number ke alawa protection aur status bits bhi hote hain:
1. **Valid / Invalid Bit ($V/I$):**
   - `Valid (1):` Page process ke valid logical address space ka hissa hai aur legal hai.
   - `Invalid (0):` Page process ke address space me nahi hai (Trap: Illegal memory access).
2. **Access Rights Bits:**
   - Read-only (`r--`), Read-Write (`rw-`), Execute-only (`--x`).
   - Operating system kernel code ya shared library code ko accidental overwrite se bachata hai.

---

## 5. Architectural Diagram

![TLB Hardware Lookup & EMAT](diagrams/tlb_emat_pipeline.svg)

---

## 6. Solved Numerical Masterclass (AKTU Frequent 10-Marker)

### Problem 1:
Ek system me:
- Main Memory (RAM) access time = $100	ext{ ns}$.
- TLB lookup time = $20	ext{ ns}$.
- TLB Hit Ratio ($h$) = $80\% = 0.8$.

Calculate kijiye:
1. Effective Memory Access Time (EMAT).
2. Agar Hit ratio badhkar $98\% = 0.98$ ho jaye, to EMAT kitna improve hoga?

---

### Step-by-Step Solution & Thought Process:

1. **Case 1 ($h = 0.8$):**
   - $	ext{Time on Hit} = t_{	ext{TLB}} + t_{	ext{RAM}} = 20 + 100 = 120	ext{ ns}$.
   - $	ext{Time on Miss} = t_{	ext{TLB}} + 2 	imes t_{	ext{RAM}} = 20 + 200 = 220	ext{ ns}$.
   $$	ext{EMAT} = 0.8 	imes 120 + (1 - 0.8) 	imes 220$$
   $$	ext{EMAT} = 96 + 0.2 	imes 220 = 96 + 44 = 140	ext{ ns}$$
   - Without TLB access time kitna hota? Pure paging me $200	ext{ ns}$ lagte. TLB ne time $140	ext{ ns}$ kar diya!

2. **Case 2 ($h = 0.98$):**
   $$	ext{EMAT} = 0.98 	imes 120 + 0.02 	imes 220$$
   $$	ext{EMAT} = 117.6 + 4.4 = 122	ext{ ns}$$
   - **Conclusion:** $98\%$ hit ratio par average access time $122	ext{ ns}$ ho gaya, jo ideal $100	ext{ ns}$ RAM speed ke kafi kareeb hai (Sirf 22% overhead)!
