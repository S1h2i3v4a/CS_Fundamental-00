# Module 08: Round Robin (RR) Scheduling & Time Quantum Trade-off

> **Unit 3: CPU Scheduling & Deadlock** | *B.Tech CS/IT/Allied (AKTU BCS401)*

---

## 1. Round Robin (RR) Algorithm Principle

### 1.1 Core Architecture
- Round Robin time-sharing systems ke liye specially design kiya gaya standard preemptive CPU scheduling algorithm hai.
- **Time Quantum ($q$):** Har process ko execution ke liye ek chhota time slice ($q$) allocate hota hai (e.g. 10ms to 100ms).
- **Circular Queue:** Ready Queue ko circular FIFO queue ki tarah treat kiya jata hai.
- **Execution Flow:**
  1. Scheduler queue ke head se pehla process pick karta hai.
  2. Timer set kiya jata hai $q$ time units ke liye.
  3. Process run karta hai:
     - Agar burst time $\le q$ ho: Process voluntarily complete hokar terminate hota hai.
     - Agar burst time $> q$ ho: Timer interrupt trigger hota hai, OS context switch execute karta hai, aur process ko Ready Queue ke **tail par re-insert** kar deta hai.

---

## 2. Time Quantum ($q$) Ka Critical Impact

### 2.1 Very Large Time Quantum ($q \to \infty$)
- Jab $q$ itna bada ho ki koi bhi process bina interrupt ke complete ho sake, to Round Robin **FCFS (First-Come First-Served)** me convert ho jata hai.
- Convoy effect wapas aa jata hai aur interactive response time khrab ho jata hai.

### 2.2 Very Small Time Quantum ($q \to 0$)
- Theoretical perspective se ise **Processor Sharing** kehte hain (N processes appear to run simultaneously on a CPU with $1/N^{\text{th}}$ speed).
- Lekin practically, har quantum switch par **Context Switching Overhead** add hota hai. Agar context switch time quantum ke barabar ya bada ho gaya, to CPU ka majority samay sirf switching me waste hoga!

### 2.3 The 80% Rule of Thumb
- Engineering standard kehta hai ki time quantum aisa choose karna chahiye jisse **at least 80% of CPU bursts time quantum se chhote hon**. Isse majority interactive jobs ek single slice me finish ho jati hain aur overhead minimal rehta hai.

---

## 3. Step-by-Step Solved Numerical (Quantum $q = 2\text{ ms}$)

Consider 3 processes at arrival time $t=0$:
- $P_1$ Burst Time = $5\text{ ms}$
- $P_2$ Burst Time = $3\text{ ms}$
- $P_3$ Burst Time = $6\text{ ms}$

### Gantt Chart Trace:
`[P1: 0-2] [P2: 2-4] [P3: 4-6] [P1: 6-8] [P2: 8-9] [P3: 9-11] [P1: 11-12] [P3: 12-14]`

| Process | AT | BT | CT | TAT (CT-AT) | WT (TAT-BT) | RT (First CPU - AT) |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **P1** | 0 | 5 | 12 | 12 | 12 - 5 = 7 | 0 - 0 = 0 |
| **P2** | 0 | 3 | 9 | 9 | 9 - 3 = 6 | 2 - 0 = 2 |
| **P3** | 0 | 6 | 14 | 14 | 14 - 6 = 8 | 4 - 0 = 4 |

- **Average Turnaround Time:** $\frac{12 + 9 + 14}{3} = \frac{35}{3} = 11.67\text{ ms}$
- **Average Waiting Time:** $\frac{7 + 6 + 8}{3} = \frac{21}{3} = 7.0\text{ ms}$
- **Average Response Time:** $\frac{0 + 2 + 4}{3} = 2.0\text{ ms}$ (Extremely responsive!)

---

## 4. Architectural Diagram

<div class="diagram">
  <img src="diagrams/round_robin_quantum.svg" alt="Round Robin Scheduling Diagram" style="max-width: 100%;">
</div>

---

## 5. AKTU Exam & Interview Highlights

> **AKTU PYQ (10 Marks):**
> *"Explain Round Robin CPU scheduling algorithm. Discuss how performance is influenced by the size of time quantum."*
>
> **Top Tech Interview Insight:**
> *"Why does Round Robin guarantee that no process starves?"*
> **Answer:** Ready queue circular FIFO hone ki wajah se har process ko at most $(n-1)q$ time units ke andar CPU allocation guaranteed milta hai. Isiliye maximum wait time bounded hota hai aur starvation impossible hai.
