# 00: Unit 3 Ultra High-Yield Quick Revision Notes (Exact 3 Pages)

> **Unit 3: CPU Scheduling & Deadlock** | *B.Tech CS/IT/Allied (AKTU BCS401)*

---

## ⚡ Overview
Ye document pure Unit 3 syllabus ka **exact 3-page ultra high-yield revision summary** hai. Semester exams (AKTU) se 1 ghante pehle ya technical interviews se pehle poora unit recall karne ke liye design kiya gaya hai.

---

## 📄 Page Breakdown & Content Summary

### 📄 Page 1: Processes, Address Space, Schedulers & Metrics
- **Program vs Process & Memory Segments:** Text, Data (.data & .bss), Heap (grows up), Stack (grows down).
- **Process State Models:** 5-state standard transitions and 7-state suspended model (MTS swapping).
- **PCB Structure:** PID, State, PC, Registers, Memory limits, Open files (`task_struct`).
- **Schedulers Comparison:** Long-Term (LTS), Short-Term (STS), Medium-Term (MTS). Dispatcher latency & CPU efficiency formula.
- **Threads & Multithreading:** User-level vs Kernel-level threads, Models ($M:1$, $1:1$, $M:N$).
- **Scheduling Performance Criteria:** TAT, WT, RT, Throughput, CPU Utilization golden formulas.

### 📄 Page 2: CPU Scheduling Algorithms Masterclass
- **FCFS & Convoy Effect:** FIFO mechanics, Convoy effect numerical proof ($17.0\text{ ms} \to 3.0\text{ ms}$).
- **SJF & SRTF:** Optimal average waiting time proof, Exponential smoothing burst prediction formula ($\tau_{n+1} = \alpha t_n + (1-\alpha)\tau_n$), SRTF preemption mechanism.
- **Priority Scheduling & Aging:** Integer conventions, Preemptive trace, Starvation mitigation via Aging.
- **Round Robin (RR) & Quantum Dynamics:** Circular FIFO queue, $q \to \infty$ vs $q \to 0$, 80% rule of thumb.
- **Comprehensive Comparison Table:** Preemption, optimality, starvation risk, and best use-cases.
- **Multilevel Queues & Multiprocessor:** MLQ vs MLFQ dynamic priority feedback, SMP, Cache warmth & Processor Affinity.

### 📄 Page 3: Deadlock Comprehensive Masterclass
- **Deadlock Definition & 4 Coffman Conditions:** Mutual Exclusion, Hold & Wait, No Preemption, Circular Wait.
- **Resource Allocation Graph (RAG):** Request vs Assignment edges, Cycle rules in Single-instance (guaranteed deadlock) vs Multi-instance (may/may not).
- **Deadlock Handling Strategies:** Ignorance (Ostrich), Prevention, Avoidance, Detection & Recovery.
- **Deadlock Prevention:** Havender's linear resource ordering protocol ($F(R_i) < F(R_j)$) and mathematical cycle impossibility proof.
- **Deadlock Avoidance & Banker's Algorithm:** Safe vs Unsafe state, Need matrix ($Need = Max - Allocation$), Safety algorithm ($O(m \times n^2)$), Resource request verification.
- **Deadlock Detection & Recovery:** Wait-For Graph (WFG) cycle detection, Process abort, Resource preemption, Checkpoint rollback, and Starvation control.

---

## 📥 Direct PDF Downloads
- 📄 [Unit_3_Quick_Revision_3_Page_Notes.pdf](Unit_3_Quick_Revision_3_Page_Notes.pdf) (Exact 3-Page Printable PDF)
- 🌐 [Unit_3_Quick_Revision_3_Page_Notes.html](Unit_3_Quick_Revision_3_Page_Notes.html) (Interactive HTML)
