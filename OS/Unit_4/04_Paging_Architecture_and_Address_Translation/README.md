# Module 04: Paging Architecture and Address Translation

> **Unit 4: Memory Management** | *B.Tech CS/IT/Allied (AKTU BCS401)*

---

## 1. Non-Contiguous Allocation: Paging Concept

Paging ek non-contiguous memory allocation scheme hai jo physical memory ko bina kisi contiguous restriction ke allocate karne ki suvidha deti hai. Iska sabse bada fayda ye hai ki ye **External Fragmentation ko 100% eliminate** kar deti hai.

### 1.1 Fundamental Rules:
1. **Physical Memory (RAM)** ko fixed-size blocks me baanta jata hai jinhe **Frames** kehte hain.
2. **Logical Memory (Process Address Space)** ko bilkul usi size ke blocks me baanta jata hai jinhe **Pages** kehte hain.
3. **Core Invariant:**
   $$	ext{Page Size} = 	ext{Frame Size} = 2^n 	ext{ bytes (Power of 2)}$$
4. Process ka koi bhi page RAM ke kisi bhi free frame me rakha ja sakta hai (Non-contiguous mapping).

---

## 2. Address Translation Scheme: $(p, d) 	o (f, d)$

CPU dwara generate kiya gaya Logical Address 2 hisso me split hota hai:
1. **Page Number ($p$):** Page Table ke index ke roop me use hota hai, jisme us page ka physical frame base address store hota hai.
2. **Page Offset ($d$):** Page ke andar exact byte location. Offset size frame me bilkul unchanged rehta hai.

$$	ext{Logical Address Bits } (m) = p 	ext{ bits} + d 	ext{ bits}$$
$$	ext{If Page Size} = 2^n 	ext{ bytes} \implies d = n 	ext{ bits}, \quad p = m - n 	ext{ bits}$$
$$	ext{Total Number of Pages} = 2^p = 2^{m-n}$$

### Physical Address Generation:
Page table se Frame Number $f$ dhoondhne ke baad:
$$	ext{Physical Address} = (f 	imes 	ext{Frame Size}) + d$$
$$	ext{Ya bit level par: Physical Address} = [f 	ext{ bits}] \,||\, [d 	ext{ bits}]$$

---

## 3. Page Table & Hardware Registers

### 3.1 Page Table Base Register (PTBR)
- Har process ka apna alag Page Table hota hai jo RAM me store hota hai.
- Process switch hone par CPU ka **PTBR (Page Table Base Register)** naye process ke page table ke starting physical address ko point karta hai.
- **PTLR (Page Table Length Register):** Table ka size store karta hai taaki process apne address space ke bahar access na kar sake.

### 3.2 Fragmentation in Paging
- **External Fragmentation:** **ZERO (Completely Eliminated)** kyunki koi bhi free frame kisi bhi page ko assign ho sakta hai.
- **Internal Fragmentation:** Sirf process ke **aakhiri page (last page)** par occur ho sakti hai:
  - Best Case: $0$ bytes (process exactly page size ka multiple ho).
  - Worst Case: $	ext{Page Size} - 1$ bytes (aakhiri page me sirf 1 byte use ho).
  - Average Case: $rac{	ext{Page Size}}{2}$ bytes per process.

---

## 4. Architectural Diagram

![Paging Hardware Address Translation](diagrams/paging_address_translation.svg)

---

## 5. Solved Address Translation Numericals (AKTU Pattern)

### Problem 1 (Bit Breakdown & Translation):
Ek system me:
- Logical Address Space = 32 bits ($m = 32$).
- Page Size = 4 KB ($4096	ext{ bytes} = 2^{12}	ext{ bytes}$).
- Physical RAM Size = 512 MB ($2^{29}	ext{ bytes}$).

Calculate kijiye:
1. Number of bits for Page Offset ($d$).
2. Number of bits for Page Number ($p$).
3. Total number of pages per process.
4. Number of frames in physical memory.
5. Number of bits in Physical Address.
6. Agar Page Table me Page 5 maps to Frame 12, to Logical Address `20500` (decimal) ka physical address kya hoga?

---

### Step-by-Step Solution & Thought Process:

1. **Page Offset Bits ($d$):**
   $$	ext{Page Size} = 4	ext{ KB} = 4 	imes 1024	ext{ bytes} = 4096	ext{ bytes} = 2^{12}	ext{ bytes}$$
   $$\implies d = 12	ext{ bits}$$

2. **Page Number Bits ($p$):**
   $$p = m - d = 32 - 12 = 20	ext{ bits}$$

3. **Total Pages per Process:**
   $$	ext{Total Pages} = 2^p = 2^{20} = 1,048,576 	ext{ pages (1 Mega Pages)}$$

4. **Physical RAM Frames:**
   $$	ext{Physical RAM Size} = 512	ext{ MB} = 2^{29}	ext{ bytes}$$
   $$	ext{Number of Frames} = rac{	ext{Physical Memory Size}}{	ext{Frame Size}} = rac{2^{29}}{2^{12}} = 2^{17} = 131,072 	ext{ frames}$$
   $$\implies f = 17	ext{ bits}$$

5. **Physical Address Bits:**
   $$	ext{Physical Address} = f + d = 17 + 12 = 29	ext{ bits}$$

6. **Decimal Address Translation (`20500`):**
   - Page Number $p = \lfloor 20500 / 4096 floor = 5$
   - Offset $d = 20500 \pmod{4096} = 20500 - (5 	imes 4096) = 20500 - 20480 = 20$
   - Given: Page $5$ maps to Frame $12$.
   - Physical Address $= (f 	imes 	ext{Frame Size}) + d = (12 	imes 4096) + 20 = 49152 + 20 = 49172$.
   - **Answer:** Physical Address = `49172` (decimal).
