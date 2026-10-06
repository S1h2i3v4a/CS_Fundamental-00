# ⚡ Unit 2: Ultra High-Yield 3-Page Quick Revision Short Notes

> **Exam & Interview Rapid Recall Guide:** Yeh short notes document Unit 2 (Concurrent Processes & Synchronization) ke sabhi topics ko **sirf 3 pages** mein condense karta hai. AKTU Semester Exam se 15 minute pehle ya Tech Interview mein revision ke liye design kiya gaya hai.

---

## 📑 Page 1: Process Concurrency, Critical Section, Peterson & Dekker

### 1.1 Process Concurrency & Race Conditions
- **Independent Process:** Does not share state/memory. Strictly deterministic output. Zero synchronization hazard.
- **Cooperating Process:** Shares memory, files, buffer, or variables. Execution sequence non-deterministic.
- **Race Condition:** Jab multiple concurrent processes shared data ko bina synchronization ke read/write karte hain aur final output unke arbitrary execution sequence par depend karta hai.
- **Lost Update Trace:** $P_1$ deposits 500, $P_2$ withdraws 200 on initial 1000 balance. Preemption between register computation and RAM store causes balance to corrupt to either 800 or 1500!

### 1.2 Critical Section Problem & 4 Criteria
- **4 Code Sections:** Entry Section (permission check) $	o$ Critical Section (shared resource access) $	o$ Exit Section (lock release) $	o$ Remainder Section (local work).
- **Primary Criteria (Mandatory):**
  1. *Mutual Exclusion:* Only ONE process in CS at any time.
  2. *Progress:* If CS is empty, only processes NOT in remainder can decide who enters next, and decision cannot be postponed indefinitely (No Deadlock).
- **Secondary Criteria (Desirable):**
  3. *Bounded Waiting:* Bound on the number of times others enter CS after a request is made (Prevents Starvation).
  4. *Architectural Neutrality:* Independent of hardware CPU speeds or clock frequencies.

### 1.3 Software Solutions: Peterson's Algorithm (1981)
- **Variables:** `boolean flag[2] = {false, false}; int turn;`
- **Protocol for $P_i$ ($j = 1 - i$):**
  ```c
  flag[i] = true; turn = j;
  while (flag[j] && turn == j); // Busy wait
  /* CRITICAL SECTION */
  flag[i] = false;
  ```
- **Proof:** `turn` cannot be simultaneously 0 and 1 $\implies$ Mutual Exclusion strictly holds. Progress and Bounded Waiting ($k=1$) fully satisfied.

### 1.4 Software Solutions: Dekker's Algorithm (1965)
- **First correct software solution** for 2-process mutual exclusion.
- **Collision Back-off:** When both `flag[i]` and `flag[j]` are true, process with `turn != i` temporarily sets `flag[i] = false` (polite back-off to prevent Livelock), waits for `turn == i`, and re-asserts intention.

---

## 📑 Page 2: Hardware Sync, Semaphores, Mutex & Producer-Consumer

### 2.1 Hardware Synchronization Primitives
- **Why Software Lock Fails:** Preemption between test (`while(lock==1)`) and set (`lock=1`) allows both processes into CS.
- **Test-and-Set Lock (TSL):** Single atomic clock cycle instruction:
  ```c
  boolean Test_and_Set(boolean *target) {
      boolean r = *target; *target = true; return r;
  }
  // Usage: while (Test_and_Set(&lock)); /* CS */ lock = false;
  ```
- **Swap Instruction:** Atomically swaps `lock` and local `key`.
- **Spinlocks:** Locks utilizing busy-waiting loops. Efficient for short waits on multi-core CPUs; wastes CPU cycles on long waits.

### 2.2 Semaphores (Dijkstra, 1965)
- **Integer variable** accessed only via atomic `wait()` (P / Down) and `signal()` (V / Up).
- **Counting vs Binary:**
  - *Binary Semaphore:* Range [0, 1]. Used for Mutual Exclusion.
  - *Counting Semaphore:* Range [0, N]. Used for managing pools of finite resources.
- **Block & Wakeup Implementation (Avoiding Busy Waiting):**
  - `wait(S)`: `S.value--; if (S.value < 0) { add to S.list; block(); }`
  - `signal(S)`: `S.value++; if (S.value <= 0) { remove from S.list; wakeup(P); }`
  - *Magic Rule:* Absolute value `|S.value|` when negative equals count of blocked processes!

### 2.3 Mutex vs Binary Semaphore
- **Mutex:** Ownership exists (only locking thread can unlock); supports Priority Inheritance Protocol.
- **Binary Semaphore:** No ownership (any thread can signal); purely signaling mechanism.

### 2.4 Producer-Consumer (Bounded Buffer Problem)
- **3 Semaphores:** `mutex = 1` (Buffer lock), `empty = N` (Empty slots count), `full = 0` (Filled slots count).
- **Producer:** `wait(empty) -> wait(mutex) -> write -> signal(mutex) -> signal(full)`
- **Consumer:** `wait(full) -> wait(mutex) -> read -> signal(mutex) -> signal(empty)`
- **⚠️ Deadlock Pitfall:** `wait(mutex)` ko `wait(empty)` se pehle rakhne par Deadlock ho jata hai jab buffer full ho!

---

## 📑 Page 3: Readers-Writers, Dining Philosophers, IPC & Process Lifecycle

### 3.1 Readers-Writers Problem
- **Rules:** Concurrent readers allowed ($\checkmark$); Writers require strict exclusivity.
- **Variables:** `int rc = 0; semaphore mutex = 1; semaphore db = 1;`
- **First-In Last-Out Lock:** First reader locks DB (`if (rc == 1) wait(db);`); Last reader unlocks DB (`if (rc == 0) signal(db);`).
- **Writer Starvation:** Continuous stream of readers keeps `rc > 0`, starving pending writers.

### 3.2 Dining Philosophers & Sleeping Barber
- **Dining Philosophers:** 5 philosophers, 5 chopsticks. All grabbing left chopstick simultaneously $\implies$ Circular Wait $\implies$ Deadlock!
  - *Fix:* Asymmetric pickup (Odd pick left first; Even pick right first).
- **Sleeping Barber:** 1 barber chair, $N$ waiting chairs. Semaphores: `customers = 0`, `barbers = 0`, `mutex = 1`. Customers drop out if waiting chairs full.

### 3.3 Process Generation & The `fork()` Math
- **Return Values:** Child receives `0`; Parent receives child's `PID > 0`; Error returns `-1`.
- **$2^n$ Process Tree Formula:**
  $$	ext{Total Processes} = 2^n \quad \Big| \quad 	ext{Child Processes Created} = 2^n - 1$$
- **Zombie Process (`<defunct>`):** Child terminated, but parent hasn't called `wait()`. Wastes PID in Process Table.
- **Orphan Process:** Parent died before child. Adopted by `init` / `systemd` (PID 1).

### 3.4 Inter-Process Communication (IPC) Models
- **Shared Memory:** Fastest IPC; direct RAM access; zero kernel copy; programmer handles synchronization.
- **Message Passing:** Uses kernel primitives (`send()`, `receive()`); slower syscall overhead; ideal for distributed systems.
- **Buffering:** Zero Capacity (Rendezvous), Bounded Capacity, Unbounded Capacity.

---

## 📥 PDF Download
📄 **[Download Unit 2 Ultra High-Yield 3-Page Notes (PDF)](./Unit_2_Quick_Revision_3_Page_Notes.pdf)**
