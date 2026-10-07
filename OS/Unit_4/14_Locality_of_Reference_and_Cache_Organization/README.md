# Module 14: Locality of Reference and Cache Organization

> **Unit 4: Memory Management** | *B.Tech CS/IT/Allied (AKTU BCS401)*

---

## 1. Principle of Locality (Why Caching & Virtual Memory Work!)

Statistical analysis se pata chalta hai ki ek computer program apne execution time ka **$90\%$ samay sirf $10\%$ code** par bitata hai (**90/10 Rule**). Is predictability ko **Locality of Reference** kehte hain.

### 1.1 Temporal Locality (Locality in Time)
- Jo memory address abhi access hua hai, bahut sambhav hai ki agle kuch cycles me woh **dobara access hoga**.
- **Practical Examples:**
  - Loop body (`for (i=0; i<1000; i++)`)
  - Loop iteration variable `i`
  - Frequently called recursive subroutines
  - Stack top pointer

### 1.2 Spatial Locality (Locality in Space)
- Jo memory address abhi access hua hai, bahut sambhav hai ki uske **padosi (nearby) memory addresses** jaldi access honge.
- **Practical Examples:**
  - Array traversal (`A[0], A[1], A[2]...`)
  - Sequential machine instruction execution (Program Counter $+ 4$)
  - Consecutive struct fields

---

## 2. Cache Memory Mapping Schemes

Cache memory SRAM par bani hoti hai aur CPU core ke andar rehti hai. RAM ke blocks ko cache me map karne ki 3 standard techniques hoti hain:

### 2.1 Direct Mapping
- Har Main Memory block strictly ek predefined cache line me hi ja sakta hai:
  $$	ext{Cache Line Number} = (	ext{Block Number}) \pmod{	ext{Total Cache Lines}}$$
- **Hardware:** Sabse simple aur fast comparator ($O(1)$).
- **Drawback:** Conflict misses bohot zyada hote hain agar do active blocks ek hi line par map ho jayein.

### 2.2 Fully Associative Mapping
- Main Memory ka koi bhi block Cache memory ke **kisi bhi free slot/line me** store ho sakta hai.
- **Advantage:** Zero conflict misses.
- **Drawback:** Lookup karne ke liye saari lines ko ek sath parallel compare karna padta hai (Expensive associative comparators).

### 2.3 $k$-Way Set Associative Mapping (Modern CPU Standard)
- Cache ko Sets me divide kiya jata hai. Har Set ke andar $k$ cache lines hoti hain (e.g., 2-way, 4-way, 8-way).
- Block ka set number fixed hota hai:
  $$	ext{Set Number} = (	ext{Block Number}) \pmod{	ext{Total Number of Sets}}$$
- Lekin us set ke andar wo $k$ lines me se kisi bhi line me ja sakta hai.
- Ye Direct Mapping ki simplicity aur Fully Associative ki low miss rate ko perfect balance karta hai.

---

## 3. Average Memory Access Time (AMAT) Formula

$$	ext{AMAT} = t_{	ext{Cache}} + (1 - h) 	imes t_{	ext{Miss Penalty}}$$
Jaha $h$ cache hit ratio hai, aur $t_{	ext{Miss Penalty}}$ RAM se cache block load karne ka time hai.

---

## 4. Architectural Diagram

![Locality & Cache Memory](diagrams/locality_and_cache.svg)
