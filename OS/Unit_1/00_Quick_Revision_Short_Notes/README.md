# ⚡ Unit 1: Ultra High-Yield 3-Page Quick Revision Short Notes

> **Exam & Interview Rapid Recall Guide:** Yeh short notes document Unit 1 ke sabhi 19 subtopics ko **sirf 3 pages** mein condense karta hai. Last-minute exam revision ya tech interview se 10 minute pehle pure unit ko recall karne ke liye design kiya gaya hai.

---

## 📑 Page 1: Introduction, System Architecture, Dual-Mode & Booting

### 1.1 Core OS Definitions
- **Operating System:** System software jo bare hardware aur user application software ke beech abstraction bridge aur **Resource Manager** ka kaam karta hai.
- **3 System Entities:**
  1. *Hardware:* Bare physical components (CPU, Registers, RAM, I/O devices).
  2. *System Software:* OS kernel, device drivers, translators (Assembler, Compiler, Interpreter).
  3. *Application Software:* User-facing tools (Browsers, IDEs, Databases, Video players).
- **Translators Quick Recall:**
  - *Assembler:* Low-level Assembly (`MOV`, `ADD`) $\rightarrow$ Binary Machine Code ($0$s & $1$s).
  - *Compiler:* High-Level Language (C/C++) poora code ek saath parse karke Object Code banata hai.
  - *Interpreter:* Code ko line-by-line interpret aur execute karta hai (Python, JavaScript).

### 1.2 Dual Perspectives: User View vs System View
- **User View (Goal = Convenience):** Simple GUI/CLI, interactive responsiveness, intuitive UX.
- **System View (Goal = Resource Efficiency):** CPU cycle scheduling, fair memory partitioning, preventing deadlocks, conflict resolution.
- **Execution Trace ($a = b + c$):**
  - High-level C statement $\rightarrow$ Compiler generates `MOV EAX, [b]`, `ADD EAX, [c]`, `MOV [a], EAX` $\rightarrow$ CPU ALU compute $\rightarrow$ MMU updates RAM bytes.

### 1.3 Computer System Organization & Bus Architecture
- **Common System Bus:** CPU, Memory Controller, aur Device Controllers aapas mein High-Speed Bus ke through interconnected rehte hain.
- **Controller & Buffer:** Har I/O device controller ke paas apna local hardware buffer registers hota hai. Controller local buffer bharne par CPU ko hardware interrupt bhejta hai.

### 1.4 Dual-Mode Operation (Hardware Security Foundation)
- **Problem Solved:** Buggy user code direct hardware registers ya doosre processes ke memory ko corrupt na kar sake.
- **Hardware Mode Bit:**
  - **User Mode (`Mode Bit = 1`, Ring 3):** Unprivileged instructions. Direct disk access, disable interrupts, ya I/O instructions execute karna FORBIDDEN hai.
  - **Kernel Mode (`Mode Bit = 0`, Ring 0 / Supervisor Mode):** All privileged hardware instructions allowed.
- **Transition Mechanism (System Call / Trap):**
  - User app executes `printf("Hello");` $\rightarrow$ Library wrapper $\rightarrow$ Software Trap / `syscall` instruction $\rightarrow$ Hardware Mode Bit flips $1 \to 0$ $\rightarrow$ Kernel executes device routine $\rightarrow$ Mode Bit flips $0 \to 1$ $\rightarrow$ Returns to user app.

### 1.5 Bootstrapping & Booting Modes
- **Booting Steps:** Power ON $\rightarrow$ Power Good signal $\rightarrow$ CPU Program Counter (PC) loads fixed ROM address $\rightarrow$ **POST (Power-On Self-Test)** verifies hardware integrity $\rightarrow$ BIOS/UEFI reads Master Boot Record (MBR / GPT) from Disk $\rightarrow$ Bootloader loads OS Kernel into RAM $\rightarrow$ System daemons initialize.
- **Cold Booting (Hard Boot):** Power completely OFF (0V) se power button press karke start hona. Full POST diagnostic test execute hota hai.
- **Warm Booting (Soft Boot / Reboot):** System running state se restart command (`Ctrl+Alt+Del`, `sudo reboot`) se restart hota hai. Hardware diagnostic (POST) **bypass** ho jata hai, jisse boot time drastically decrease hota hai.

---

## 📑 Page 2: OS Classifications, Scheduling Models & Mathematical Thought Process

### 2.1 OS Classification Matrix

| OS Architecture | Core Working Mechanism | Primary Advantage | Major Limitation / Trade-off | Real-World Example |
| :--- | :--- | :--- | :--- | :--- |
| **Batch OS** | Similar jobs punch cards ke through operator group karke batches ($B_1, B_2$) mein feed karta hai. | Zero manual setup time between similar jobs. | No interactivity; CPU idle during I/O wait. | Early IBM Mainframes |
| **Multiprogrammed OS** | Multiple active jobs simultaneously RAM mein resident rehte hain. | High CPU utilization; switches to Ready job on I/O. | Complex memory protection & scheduling needed. | Modern Linux/Windows |
| **Time-Sharing OS** | Round Robin CPU allocation with fixed Time Quantum ($q$). Preemptive timer interrupts. | Minimum response time; interactive user feel. | Context switch CPU overhead ($q$ vs $\delta$). | Unix, macOS, Linux |
| **Hard Real-Time** | Strict deterministic deadlines ($WCET \le D$). Miss deadline = Total System Failure. | Zero jitter; absolute timing guarantee. | Paging/Virtual Memory disabled; minimal UI. | Pacemaker, Airbags |
| **Soft Real-Time** | Deadlines are prioritized but flexible. Miss deadline = Graceful QoS degradation. | Rich multimedia support with priority boost. | Cannot be used for life-critical missions. | YouTube, CS:GO Gaming |
| **Multiprocessor (SMP)** | Multiple peer CPUs share common Bus, Clock, and RAM. Peer load balancing. | High throughput; graceful degradation (fault-soft). | Bus & cache coherency contention. | Multi-core Intel/AMD |
| **Multiprocessor (ASMP)**| Master-Slave: Master CPU runs OS Kernel; Slave CPUs execute user tasks. | Simple OS architecture. | Master CPU becomes single point bottleneck. | Embedded Master chips |

### 2.2 Spooling vs Buffering
- **Buffering:** Temporary small RAM area jo single device aur CPU ke beech short-term speed mismatch ko smooth karta hai.
- **Spooling (*Simultaneous Peripheral Operation On-Line*):** Secondary storage disk par dedicated FIFO queue buffer jo multiple processes ke I/O jobs (e.g., Print jobs) ko queue karta hai. CPU I/O wait kiye bina directly disk buffer mein dump karke aage badh jata hai.

### 2.3 Mathematical Thought Process & High-Yield Formulas
1. **CPU Utilization with Degree of Multiprogramming ($n$):**
   $$\text{CPU Utilization} = 1 - p^n$$
   *(where $p$ = fraction of time a process waits for I/O, $n$ = degree of multiprogramming)*
   - *Thought Process:* Agar $p = 70\%$, to Uniprogramming ($n=1$) par $\text{Util} = 30\%$. Lekin Multiprogramming ($n=4$) par $\text{Util} = 1 - (0.7)^4 = \mathbf{76\%}$!

2. **Amdahl's Law (Speedup with $N$ Cores):**
   $$\text{Speedup } S = \frac{1}{(1 - P) + \frac{P}{N}}$$
   *(where $P$ = parallel portion, $(1 - P)$ = serial portion)*
   - *Insight:* Agar program ka $20\%$ code serial hai, to infinite cores ($N \to \infty$) lagane par bhi max speedup $\frac{1}{0.20} = \mathbf{5\times}$ se upar nahi ja sakta!

3. **Time-Sharing Context Switch Overhead:**
   $$\text{Overhead} = \frac{\delta}{q + \delta}$$
   *(where $\delta$ = context switch latency, $q$ = time quantum)*
   - *Rule of Thumb:* $80\%$ CPU bursts time quantum $q$ se chhote hone chahiye taaki context switch overhead $< 1\%$ rahe.

4. **Average Memory Access Time (AMAT):**
   $$\text{AMAT} = T_{\text{hit}} + (\text{Miss Rate} \times \text{Miss Penalty})$$

---

## 📑 Page 3: OS Structures, Reentrancy, System Calls & Core Services

### 3.1 Operating System Structures: The Architectural Duel

```
[Monolithic Architecture]                  [Microkernel Architecture]
+-------------------------------+          +-------------------------------+
| User Applications (Ring 3)    |          | User Apps | File Srv | Net Srv|
+-------------------------------+          +-------------------------------+
| === Syscall (Trap) ========= |          | === IPC Message Passing ===== |
| Kernel Space (Ring 0):        |          | Microkernel (Ring 0):         |
| [Scheduler] [VMM] [File Sys]  |          | [IPC] [Scheduling] [Low Mem]  |
| [Device Drivers] [Network]    |          +-------------------------------+
+-------------------------------+          | Computer Hardware             |
| Computer Hardware             |          +-------------------------------+
+-------------------------------+
```

1. **Simple Structure (MS-DOS):** No dual-mode protection; applications can directly overwrite BIOS & disk routines.
2. **Monolithic Kernel (Original UNIX, Linux core):** Saare subsystems (VMM, Scheduler, Drivers, Network) ek hi kernel address space (Ring 0) mein run karte hain.
   - *Pros:* Blazing fast (zero IPC overhead, direct C function calls).
   - *Cons:* Zero fault isolation. Ek third-party driver crash poore OS ko crash (BSOD) kar deta hai.
3. **Layered Approach (Dijkstra's THE System):** OS $N$ layers mein divided: Layer 0 (Hardware) se Layer $N$ (UI). Strict rule: Layer $i$ only calls Layer $i-1$. Modularity high, but slow invocation traversal.
4. **Microkernel Architecture (Mach, QNX):** Minimal primitives (IPC, low scheduling) in Ring 0. Drivers aur File Systems User Space mein independent servers ki tarah run karte hain.
   - *Pros:* Extreme reliability; driver crash hone par sirf user process restart hota hai.
   - *Cons:* IPC context-switching latency ($10\%-20\%$ performance penalty).
5. **Modular LKM (Modern Linux, Solaris):** Core monolithic speed + Dynamic Loadable Kernel Modules (`.ko` files) runtime link/unload via `insmod`/`rmmod` without rebooting.

### 3.2 Reentrant Kernel Architecture
- **Problem in Non-Reentrant:** Multiple processes kernel mode mein shared data structures (Process Table, Inode Table) parallel update nahi kar sakte the without race conditions.
- **Reentrant Solution:** Har process ka apna **independent Kernel Stack** hota hai, aur shared kernel data structures **fine-grained Spinlocks & Mutexes** se protected rehte hain.

### 3.3 6-Stage System Call Execution Lifecycle
1. **User Invocation:** User program standard C library wrapper (`read()`) call karta hai.
2. **Register Setup:** Syscall number CPU register `RAX` mein load hota hai (e.g., `sys_read` has ID `0`), arguments `RDI`, `RSI`, `RDX` mein load hote hain.
3. **Hardware Trap:** CPU assembly instruction (`syscall` / `int 0x80`) execute karta hai. Hardware Mode Bit flips **$1 \to 0$**.
4. **Table Dispatcher:** Kernel `sys_call_table[RAX]` index lookup karta hai aur user buffer pointer ko security check (`access_ok()`) karta hai.
5. **Driver Execution:** Kernel I/O subsystem physical hardware se data read karke user buffer mein copy karta hai (`copy_to_user`).
6. **Return (`sysret`):** Result `RAX` mein load hota hai, Mode Bit flips **$0 \to 1$**, aur control user program ko return hota hai.

### 3.4 Parameter Passing in System Calls
1. **CPU Registers:** Fastest, but limited count ($\le 6$ parameters).
2. **Memory Block / Table:** Parameters memory struct mein pack karke table ka starting pointer CPU register (EBX) mein pass hota hai.
3. **Program Stack:** Parameters user stack par push hote hain aur kernel stack se pop karta hai.

### 3.5 The 8 Core Subsystems of Operating Systems
1. **Process Management:** PCB creation, CPU scheduling, synchronization (Semaphores), deadlocks.
2. **Main Memory Management:** Status tracking, Virtual Memory paging, dynamic allocation.
3. **File Management:** Hierarchical directories, Inodes, file CRUD, disk block mapping.
4. **I/O System Management:** Buffer caching, spooling print queues, uniform driver interface.
5. **Secondary Storage Management:** Free space bitmaps, disk head scheduling (SCAN, SSTF).
6. **Networking & Distributed:** TCP/IP stack, socket abstraction, distributed routing.
7. **Protection & Security:** Dual-mode enforcement, ACL permissions, memory boundaries.
8. **Command Interpreter (Shell):** CLI/GUI parser jo user commands ko system calls mein translate karta hai.

---

## 📥 PDF Download
📄 **[Download Unit 1 Ultra High-Yield 3-Page Notes (PDF)](./Unit_1_Quick_Revision_3_Page_Notes.pdf)**
