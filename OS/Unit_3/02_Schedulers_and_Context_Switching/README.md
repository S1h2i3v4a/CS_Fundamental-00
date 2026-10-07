# Module 02: Schedulers (LTS, STS, MTS), Dispatcher & Context Switching

> **Unit 3: CPU Scheduling & Deadlock** | *B.Tech CS/IT/Allied (AKTU BCS401)*

---

## 1. Operating System Schedulers Hierarchy

Operating System me multi-programming aur resource utilization ko balance karne ke liye 3 distinct types ke Schedulers hote hain:

### 1.1 Long-Term Scheduler (LTS) / Job Scheduler
- **Location & Role:** Hard disk ke Job Pool se programs ko select karke RAM ke Ready Queue me load karta hai.
- **Degree of Multiprogramming:** Ye decide karta hai ki memory me kitne processes concurrently rahenge.
- **Process Mix:** LTS ka sabse important kaam **I/O-bound** (e.g., text editor, web download) aur **CPU-bound** (e.g., mathematical matrix multiplication) processes ka balanced mix create karna hai. Agar saare process CPU-bound honge, to I/O devices idle rahenge; agar saare I/O-bound honge, to CPU idle rahega.
- **Frequency:** Bahut kam baar invoke hota hai (Seconds ya Minutes me).

### 1.2 Short-Term Scheduler (STS) / CPU Scheduler
- **Role:** Ready Queue me already present processes me se kisi ek process ko choose karke CPU assign karta hai.
- **Frequency:** Extremely high frequency (Har 10ms - 100ms me ya context switch par invoke hota hai).
- **Execution Speed:** Ye algorithm ultra-fast hona chahiye kyunki iska execution time pure overhead hai.

### 1.3 Medium-Term Scheduler (MTS) / Swapper
- **Role:** Jab RAM full ho jati hai ya thrashing start hoti hai, to ye partially executed processes ko RAM se swap-out karke disk ke Swap Space (Paging file) me bhej deta hai. Jab memory available hoti hai, to unhe wapas Swap-in kar leta hai.
- **Degree of Multiprogramming:** Ye degree of multiprogramming ko temporarily **reduce** karta hai.

---

## 2. Dispatcher vs Scheduler

Students aksar Scheduler aur Dispatcher me confuse hote hain:
- **Scheduler:** Ye ek **Decision-Maker** algorithm hai (Selects *which* process runs next).
- **Dispatcher:** Ye ek **Execution Module** hai jo actual switching handle karta hai:
  1. Switching context (saving old registers, loading new registers).
  2. Switching to user mode from kernel mode.
  3. Jumping to the appropriate program counter (PC) location to restart the program.
- **Dispatch Latency:** Dispatcher dwara ek process ko stop karke doosre process ko start karne me lagne wale samay ko **Dispatch Latency** kehte hain.

---

## 3. Context Switching Deep Dive

### 3.1 Context Switch Kya Hota Hai?
Jab CPU kisi running process $P_0$ se switch hokar doosre process $P_1$ par jata hai, to current state (Registers, PC, Flags) ko $P_0$ ke PCB me save karna padta hai aur $P_1$ ke PCB se uska saved context CPU registers me load karna padta hai. Is mechanism ko **Context Switching** kehte hain.

### 3.2 Context Switching Overhead & CPU Efficiency
Context switch ke dauran CPU koi bhi actual useful user-code execute nahi karta. Ye purely OS overhead hai:
$$\text{Total Time} = T_{\text{useful}} + T_{\text{overhead}}$$
$$\text{CPU Efficiency } (\eta) = \frac{T_{\text{useful}}}{T_{\text{useful}} + T_{\text{overhead}}} \times 100\%$$

#### Numerical Example (AKTU 2-Marks):
> **Question:** Ek system me quantum $q = 10\text{ ms}$ hai aur har context switch me $2\text{ ms}$ lagte hain. CPU Efficiency calculate kijiye.
> **Solution:**
> - Useful execution time per slice = $10\text{ ms}$
> - Overhead per slice = $2\text{ ms}$
> - Total Time = $10 + 2 = 12\text{ ms}$
> - Efficiency $\eta = \frac{10}{12} \times 100\% = 83.33\%$.
> - Wasted CPU power = $16.67\%$.

---

## 4. Architectural Diagram

<div class="diagram">
  <img src="diagrams/schedulers_and_context_switch.svg" alt="Schedulers and Context Switch Diagram" style="max-width: 100%;">
</div>

---

## 5. AKTU Exam & Interview Highlights

> **AKTU PYQ (7.5 Marks):**
> *"Differentiate between Long-term, Short-term, and Medium-term schedulers. What is dispatch latency?"*
>
> **Top Tech Interview Insight:**
> *"How do hardware features like multiple register sets optimize context switching?"*
> **Answer:** Modern processors (e.g., UltraSPARC) me multiple register sets hote hain. Context switch ke samay register save/restore karne ki jagah processor sirf current register set pointer (CWP) change kar deta hai, reducing context switch latency from microseconds to single clock cycles!
