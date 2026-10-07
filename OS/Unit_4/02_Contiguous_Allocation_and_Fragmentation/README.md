# Module 02: Contiguous Allocation and Fragmentation

> **Unit 4: Memory Management** | *B.Tech CS/IT/Allied (AKTU BCS401)*

---

## 1. Contiguous Memory Allocation Concept

Contiguous Memory Allocation me har process ko execution ke liye physical RAM me ek **single continuous block of memory addresses** assign kiya jata hai. Process ka koi bhi hissa scattered nahi ho sakta.

### 1.1 Single-Contiguous Allocation (Single User Systems)
- Early systems me poori RAM ko do hisso me baanta jata tha:
  1. Operating System (usually low memory me).
  2. Exactly ek User Process (high memory me).
- Jab process complete hota tha, agla process poori available memory occupy karta tha.
- Degree of Multiprogramming = 1. Resource utilization kafi poor tha.

---

## 2. Fixed Partition Allocation (MFT: Multiprogramming with Fixed Tasks)

### 2.1 Working Principle
- System boot time par OS physical memory ko $N$ fixed partitions me pehle se divide kar deta hai.
- Partitions ka size equal bhi ho sakta hai ya unequal bhi.
- Har partition me strictly ek samay par **sirf ek process** reh sakta hai.
- Degree of Multiprogramming strictly fixed rehti hai (maximum $N$ processes).

### 2.2 Internal Fragmentation (Fixed Partitions ki sabse badi samasya)
- **Definition:** Jab kisi process ko allocate kiya gaya partition size process ke actual required size se bada hota hai, to partition ke andar bachi hui unused memory waste ho jaati hai. Is unused block ko **Internal Fragmentation** kehte hain.
- Yeh memory partition ke *andar* hoti hai, isliye kisi doosre process ko allocate nahi ki ja sakti.
$$	ext{Internal Fragmentation} = 	ext{Allocated Partition Size} - 	ext{Process Size}$$

---

## 3. Variable Partition Allocation (MVT: Multiprogramming with Variable Tasks)

### 3.1 Working Principle
- Memory ko pehle se statically divide nahi kiya jata.
- Jab koi naya process arrive hota hai, OS uski exact requirement ke barabar memory block allocate karta hai.
- Shuru me memory continuous rehti hai, lekin jaise-jaise processes execute hokar terminate hote hain, memory me alag-alag jagah free blocks (**Holes**) create ho jate hain.

### 3.2 External Fragmentation (Variable Partitions ki samasya)
- **Definition:** Jab system me overall total free memory available hoti hai jo incoming process ki requirement ko satisfy kar sakti hai, lekin free memory continuous na hokar chhote-chhote fragmented blocks me scattered hoti hai, to request satisfy nahi ho paati. Ise **External Fragmentation** kehte hain.
- **50-Percent Rule (Knuth's Rule):** Agar first-fit ya best-fit allocation strategy use ki jaye, to statistically $N$ allocated blocks ke sath lagbhag $0.5 N$ free blocks external fragmentation ki wajah se waste ho jate hain (Lagbhag $1/3$ memory unusable rehti hai).

---

## 4. Hardware Protection: Base & Limit Registers

Contiguous memory allocation me doosre processes aur OS ko unauthorized access se bachane ke liye MMU me do special hardware registers hote hain:

1. **Base Register (Relocation Register):** Holds the smallest physical memory address jaha se process start hota hai.
2. **Limit Register:** Holds the length / range of the process logical address space.

### Hardware Validation Flow:
$$	ext{CPU generates Logical Address } L$$
$$	ext{IF } (L < 	ext{Limit Register}) \implies 	ext{Physical Address} = L + 	ext{Base Register}$$
$$	ext{ELSE } \implies 	ext{TRAP to OS: Memory Access Violation / Segfault}$$

---

## 5. Architectural Diagram

![Contiguous Allocation & Fragmentation](diagrams/contiguous_and_fragmentation.svg)

---

## 6. Numerical Example: Internal vs External Fragmentation

### Problem Statement:
Ek 1000 KB RAM me 200 KB OS ke liye reserved hai. Bachi hui 800 KB memory me:
- Scheme A: Fixed Partitions of 200 KB each (total 4 partitions).
- Processes arrive hote hain: $P_1 = 120	ext{ KB}$, $P_2 = 180	ext{ KB}$, $P_3 = 100	ext{ KB}$.
- Scheme B: Variable partitions me $P_1(120), P_2(180), P_3(100)$ allocate hone ke baad $P_2$ terminate ho jata hai, aur bachi hui memory ke end me 400 KB hole hai. Ek naya process $P_4 = 450	ext{ KB}$ arrive hota hai.

### Step-by-Step Thought Process:
1. **Scheme A (Fixed Partitions):**
   - Partition 1 (200 KB) $	o$ $P_1(120	ext{ KB}) \implies 	ext{Internal Frag} = 200 - 120 = 80	ext{ KB}$.
   - Partition 2 (200 KB) $	o$ $P_2(180	ext{ KB}) \implies 	ext{Internal Frag} = 200 - 180 = 20	ext{ KB}$.
   - Partition 3 (200 KB) $	o$ $P_3(100	ext{ KB}) \implies 	ext{Internal Frag} = 200 - 100 = 100	ext{ KB}$.
   - Total Internal Fragmentation = $80 + 20 + 100 = 200	ext{ KB}$.
   - Partition 4 (200 KB) bilkul free hai, lekin $P_4(250	ext{ KB})$ nahi aa sakta kyunki max partition size 200 KB hi hai!

2. **Scheme B (Variable Partitions):**
   - $P_2$ terminate hua $\implies$ 180 KB free hole create hua.
   - Memory end me free hole = 400 KB.
   - Total available free space = $180	ext{ KB} + 400	ext{ KB} = 580	ext{ KB}$.
   - Incoming $P_4$ ki requirement = $450	ext{ KB}$.
   - Check: $580	ext{ KB} > 450	ext{ KB}$ (Free space kafi hai).
   - Lekin largest contiguous hole sirf 400 KB ka hai!
   - Result: $P_4$ allocate nahi ho sakta $\implies$ **External Fragmentation = 580 KB waste**.
