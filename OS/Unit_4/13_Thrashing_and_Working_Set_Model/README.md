# Module 13: Thrashing and Working-Set Model

> **Unit 4: Memory Management** | *B.Tech CS/IT/Allied (AKTU BCS401)*

---

## 1. Thrashing: Definition & Vicious Cycle

### 1.1 What is Thrashing?
Jab koi computer system instructions execute karne ki tulna me **pages ko swap-in aur swap-out karne me zyada samay bitane lagta hai**, to is condition ko **Thrashing** kehte hain.
- System ki CPU utilization gir kar almost zero ho jaati hai.
- Disk queue 100% busy ho jaati hai (Disk thrashing).
- System completely hang / unresponsive pratit hota hai.

### 1.2 The Vicious Cycle of Thrashing:
1. System me processes ki sankhya (Degree of Multiprogramming) badhai jati hai.
2. Har process ko milne wale physical RAM frames kam pad jate hain (Below process locality needs).
3. Processes continuously Page Faults trigger karte hain.
4. Processes I/O wait queue me chale jate hain taaki disk se page load ho sake.
5. CPU idle ho jata hai kyunki Ready queue khali ho jati hai.
6. **OS ka galat anumaan:** CPU scheduler dekhta hai ki CPU utilization kam hai, isliye wo degree of multiprogramming aur badha deta hai!
7. Naye processes aur zyada frames demand karte hain, situation aur kharab ho jaati hai, aur system crash/freeze ho jata hai.

---

## 2. The Working-Set Model (Peter Denning)

Working-Set Model **Locality of Reference** ke concept par aadharit hai.

### 2.1 Working-Set Window ($\Delta$)
- Parameter $\Delta$ ek fixed number of recent page references ko represent karta hai (Working-set window).
- **Working-Set Size ($WSS_i$):** Pichhle $\Delta$ page references me process $P_i$ dwara access kiye gaye distinct pages ka set.
- **Total Frame Demand ($D$):**
  $$D = \sum_{i=1}^{n} WSS_i$$
- Agar total physical memory frames $M$ hain:
  - **Case 1 ($D \le M$):** Har process ko sufficient frames mile hue hain $\implies$ No Thrashing!
  - **Case 2 ($D > M$):** Total demand physical memory se badh gayi hai $\implies$ **Thrashing will occur!**
- **OS Action:** Jaise hi $D > M$ hota hai, OS medium-term scheduler ko bula kar kisi ek process ko poora disk par swap-out kar deta hai taaki bache hue processes smoothly run kar sakein.

---

## 3. Page-Fault Frequency (PFF) Strategy

Working set model me $\Delta$ ko continuously monitor karna high hardware overhead lata hai. Iska alternate aur practical solution **Page-Fault Frequency (PFF)** hai.

### 3.1 Upper and Lower Bounds:
OS har process ke page fault frequency ka moving average count karta hai aur do thresholds rakhta hai:
1. **Upper Threshold:** Agar process ka page fault rate upper threshold se badh jaye $\implies$ Is process ke paas frames kam hain. OS is process ko **additional frames allocate** karta hai.
2. **Lower Threshold:** Agar page fault rate lower threshold se kam ho jaye $\implies$ Process ke paas zarurat se zyada frames hain. OS isse **extra frames wapas le leta hai**.
3. Agar kisi process ka fault rate upper threshold cross kar jaye aur RAM me koi free frame na ho, to process ko swap-out kar diya jata hai.

---

## 4. Architectural Diagram

![Thrashing & Working Set Model](diagrams/thrashing_and_working_set.svg)
