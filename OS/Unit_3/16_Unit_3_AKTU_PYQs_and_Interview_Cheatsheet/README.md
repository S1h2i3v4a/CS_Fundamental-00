# Module 16: Unit 3 AKTU PYQs, Numerical Masterclass & Interview Cheatsheet

> **Unit 3: CPU Scheduling & Deadlock** | *B.Tech CS/IT/Allied (AKTU BCS401)*

---

## 1. Top AKTU Previous Years Questions (Solved Repository)

### Q1. What is a deadlock? Discuss the necessary conditions for deadlock with examples. (2018-19, 10 Marks)
- **Answer Structure:**
  1. Definition of deadlock (Permanent blocked state of processes).
  2. The 4 Coffman conditions explained in detail (Mutual Exclusion, Hold and Wait, No Preemption, Circular Wait).
  3. Traffic intersection or dining philosophers practical example.
  4. Conclusion: Deadlock occurs if and only if all 4 conditions hold simultaneously.

### Q2. Write the condition for deadlock. Explain the protocol to break circular wait condition. (2017-18, 10 Marks)
- **Answer Structure:**
  1. Define Circular Wait formal mathematical definition ($P_0 \to P_1 \dots \to P_0$).
  2. **Havender's Protocol:** Assign linear ordering $F : R \to \mathbb{N}$.
  3. Enforce that process can only request resources in strictly ascending order ($F(R_i) < F(R_j)$).
  4. Prove mathematical impossibility ($F(R_0) < F(R_0)$) so cycle cannot form.

### Q3. Differentiate between Deadlock and Starvation in detail. (2018-19, 2 Marks)
- **Answer:** Deadlock me processes aapas me blocked rehte hain aur external intervention ke bina resolve nahi ho sakte. Starvation me high-priority process continuous aane ki wajah se low-priority process indefinitely delay hota hai, par resources continuously active hote hain aur Aging se solve ho sakta hai.

---

## 2. Master Formula Cheatsheet

| Parameter | Mathematical Formula | Key Rules & Tips |
| :--- | :--- | :--- |
| **Turnaround Time (TAT)** | $\text{TAT} = \text{CT} - \text{AT}$ | Total time spent in the system |
| **Waiting Time (WT)** | $\text{WT} = \text{TAT} - \text{BT}$ | Time spent waiting in Ready Queue |
| **Response Time (RT)** | $\text{RT} = T_{\text{first CPU}} - \text{AT}$ | Non-preemptive me $\text{RT} = \text{WT}$ |
| **CPU Efficiency ($\eta$)** | $\frac{T_{\text{useful}}}{T_{\text{useful}} + T_{\text{context\_switch}}} \times 100\%$ | Maximize by sizing quantum appropriately |
| **Next Burst Prediction** | $\tau_{n+1} = \alpha t_n + (1 - \alpha) \tau_n$ | Exponential smoothing formula |
| **Need Matrix (Banker's)** | $\text{Need}[i][j] = \text{Max}[i][j] - \text{Allocation}[i][j]$ | Basic test: $\text{Need}_i \le \text{Available}$ |

---

## 3. Comprehensive Unit 3 Mindmap Diagram

<div class="diagram">
  <img src="diagrams/unit3_scheduling_deadlock_mindmap.svg" alt="Unit 3 Mindmap Diagram" style="max-width: 100%;">
</div>

---

## 4. Top Tech Interview FAQs

1. **How does the Linux CFS (Completely Fair Scheduler) differ from traditional MLFQ?**
   - CFS red-black tree data structure maintain karta hai sorted by virtual runtime (`vruntime`). CFS hamesha leftmost node (least `vruntime`) ko schedule karta hai, eliminating fixed queue slices.
2. **Why does Banker's Algorithm have $O(m \times n^2)$ complexity?**
   - Outer loop finds a candidate process ($n$ iterations), checking each requires comparing $m$ resources ($m \times n$). In worst case, this repeats for all $n$ processes: $O(m \times n^2)$.
