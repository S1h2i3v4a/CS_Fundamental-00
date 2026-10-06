# 5. Hardware Synchronization: Test-and-Set & Swap

> **Unit 2 Module 5 Reference:** Gateway Classes Slides 40–59. Software Lock variable ka flaw, Hardware Atomic Instructions (`Test_and_Set` / TSL, `Swap`), Spinlocks, Busy Waiting aur unka evaluation.

---

## 5.1 Simple Software Lock Variable ka Flaw (Why Software Lock Fails?)
Aksar beginners sochte hain ki ek simple integer `lock` variable le kar critical section ko protect kiya ja sakta hai:

```c
// Flawed Software Lock Approach
while (lock == 1); // 1. Test the lock
// <--- PREEMPTION / CONTEXT SWITCH POINT! --->
lock = 1;          // 2. Set the lock
/* Critical Section */
lock = 0;          // 3. Release lock
```

### The Bug Trace:
1. Maan lo `lock = 0` (CS khali hai).
2. Process $P_1$ while loop check karta hai: `lock == 1` is **false**. $P_1$ loop se bahar nikalta hai.
3. **Lekin `lock = 1` execute karne se theek pehle CPU timer interrupt aa jata hai aur context switch ho jata hai!**
4. Ab Process $P_2$ CPU pata hai. Woh bhi check karta hai: `lock == 1` is **false**.
5. $P_2$ turant `lock = 1` set karke **Critical Section mein chala jata hai**.
6. Agli baari mein jab $P_1$ dobara CPU pata hai, toh woh line number 2 (`lock = 1`) execute karke **woh bhi Critical Section mein chala jata hai!**
7. **Disaster:** $P_1$ aur $P_2$ dono ek saath Critical Section mein aa gaye! **Mutual Exclusion violated!**

> **Root Cause:** "Testing the lock" aur "Setting the lock" do alag-alag instructions the. Unke beech mein process preempt ho sakta tha. Solution hai ki Test aur Set ko **ek single un-interruptible (Atomic) instruction** banaya jaye!

---

## 5.2 Test-and-Set Instruction (TSL - Test and Set Lock)
- **Atomic Instruction:** Hardware level (CPU instruction set) par implement ki gayi aisi instruction jise execute hone se koi interrupt beech mein rok nahi sakta. CPU memory bus ko lock kar deta hai jab tak yeh execute nahi ho jati.
- **C Definition (Semantics):**
```c
boolean Test_and_Set(boolean *target) {
    boolean r = *target; // Purani value read ki
    *target = true;      // Target ko 1 (locked) set kiya
    return r;            // Purani value return ki
}
```

### Critical Section Code using Test_and_Set:
```c
boolean lock = false; // Initial shared lock state

do {
    // 1. Entry Section
    while (Test_and_Set(&lock)); // Busy wait if lock was already true!

    // 2. Critical Section
    /* Access shared data */

    // 3. Exit Section
    lock = false; // Release the lock

    // 4. Remainder Section
    /* Independent code */
} while (true);
```

### Step-by-Step Execution Trace:
- **Case 1 (CS is free, `lock = false`):**
  - $P_1$ calls `Test_and_Set(&lock)`.
  - Target memory par `lock = true` set ho jata hai, aur purani value `false` return hoti hai.
  - While loop condition `while (false)` ban jati hai $ightarrow$ Loop break! $P_1$ enters CS!
- **Case 2 (CS is occupied, $P_2$ tries to enter):**
  - $P_2$ calls `Test_and_Set(&lock)`.
  - `lock` pehle se `true` tha, toh return value `true` aati hai aur `lock` true hi rehta hai.
  - While loop condition `while (true)` ban jati hai $ightarrow$ $P_2$ continuous spin karta rehta hai (**Busy Waiting**).
- **Case 3 ($P_1$ exits):**
  - $P_1$ executes `lock = false`.
  - $P_2$ ke agle `Test_and_Set` call par return value `false` aayegi aur $P_2$ enter ho jayega.

---

## 5.3 Swap / Exchange Instruction
Hardware vendor kuch CPUs mein Test-and-Set ke bajaye **Swap (XCHG in x86)** instruction dete hain:

```c
void Swap(boolean *a, boolean *b) {
    boolean temp = *a;
    *a = *b;
    *b = temp;
}
```

### Usage with Local Variable `key`:
```c
boolean lock = false; // Shared

do {
    // 1. Entry Section
    boolean key = true; // Local to each process
    while (key == true) {
        Swap(&lock, &key); // Atomically swap local key and shared lock
    }

    // 2. Critical Section
    /* Shared data access */

    // 3. Exit Section
    lock = false; // Release lock

    // 4. Remainder Section
    /* Local code */
} while (true);
```

---

## 5.4 Spinlocks & Busy Waiting (Analysis)
- **Busy Waiting:** Jab koi process lock pane ke liye CPU cycle waste karte hue continuous `while` loop condition check karta rehta hai, toh isse **Busy Waiting** kehte hain.
- **Spinlock:** Aisa lock jo busy waiting mechanism ka use karta hai use Spinlock kehte hain.
- **Advantages:**
  - Fast for short delays: Process ko sleep state mein daalne aur context switch karne ka overhead (jo ki ~1000 CPU cycles le sakta hai) bach jata hai.
- **Disadvantages:**
  - Wastes CPU time: Agar CS lamba hai, toh waiting process CPU ko 100% load par useless spinning mein busy rakhta hai.
  - Priority Inversion Problem: Agar low-priority process CS mein hai aur high-priority process spin kar raha hai, toh single core par dead-lock jaisi sthiti ban sakti hai.

---

## 5.5 Hardware Solutions ka Criteria Evaluation
1. **Mutual Exclusion:** **✓ SATISFIED.** Hardware atomicity guarantee karti hai ki ek samay par sirf ek process ko return value `false` milegi.
2. **Progress:** **✓ SATISFIED.** CS khali hote hi jo process pehle Test-and-Set karega woh enter kar jayega.
3. **Bounded Waiting:** **✗ NOT GUARANTEED!** Agar multiple processes ($P_1, P_2, P_3$) spin kar rahe hain, toh CPU scheduler random selection ke karan kisi ek bechare process ko baar-baar ignore kar sakta hai, leading to **Starvation**.
