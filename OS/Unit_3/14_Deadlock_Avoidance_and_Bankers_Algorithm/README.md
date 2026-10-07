# Module 14: Deadlock Avoidance, Safe State & Banker's Algorithm

> **Unit 3: CPU Scheduling & Deadlock** | *B.Tech CS/IT/Allied (AKTU BCS401)*

---

## 1. Deadlock Avoidance Concept

### 1.1 Safe State vs Unsafe State vs Deadlock
- **Safe State:** Ek aisi state jisme system ke paas kam se kam ek aisi execution sequence (**Safe Sequence**) available hoti hai jisse sabhi processes bina deadlock me fase successfully execute hokar finish ho sakte hain.
- **Unsafe State:** Aisi state jisme koi safe sequence exist nahi karti. **NOTE:** Unsafe state ka matlab turant Deadlock nahi hota, balki Unsafe state me deadlock hone ki *possibility* hoti hai agar processes ne maximum resources ek saath maang liye!
- **Deadlock Avoidance Goal:** Har allocation se pehle test karna aur system ko kabhi bhi Unsafe state me enter hone na dena!

---

## 2. Banker's Algorithm Architecture

Banker's algorithm Dijkstra ne bank credit systems ke analogy par develop kiya tha (Jaise bank kabhi saara cash ek customer ko nahi deta taaki kisi ka check bounce na ho).

### 2.1 Core Data Structures ($n$ processes, $m$ resource types)
1. **`Available[m]`:** Har resource type ke kitne instances currently free hain.
2. **`Max[n][m]`:** Har process ko execution ke dauran maximum kitne resources ki zaroorat pad sakti hai.
3. **`Allocation[n][m]`:** Process ko currently kitne instances allocated hain.
4. **`Need[n][m]`:** Process ko finish hone ke liye aur kitne instances chahiye:
   $$\text{Need}[i][j] = \text{Max}[i][j] - \text{Allocation}[i][j]$$

### 2.2 Safety Algorithm ($O(m \times n^2)$)
1. Initialize `Work = Available`, aur sabhi $i$ ke liye `Finish[i] = False`.
2. Find an index $i$ such that:
   $$\text{Finish}[i] == \text{False} \quad \text{AND} \quad \text{Need}_i \le \text{Work}$$
   Agar aisa koi $i$ nahi milta &rarr; Go to Step 4.
3. $\text{Work} = \text{Work} + \text{Allocation}_i$, $\text{Finish}[i] = \text{True}$. Go back to Step 2.
4. Agar sabhi $i$ ke liye $\text{Finish}[i] == \text{True}$, to system **SAFE STATE** me hai!

### 2.3 Resource-Request Algorithm
Jab process $P_i$ resource request $Request_i$ generate karta hai:
1. If $Request_i \le \text{Need}_i$ (warna error: exceeded maximum claim).
2. If $Request_i \le \text{Available}$ (warna process $P_i$ must wait).
3. Pretend allocate:
   - $\text{Available} = \text{Available} - Request_i$
   - $\text{Allocation}_i = \text{Allocation}_i + Request_i$
   - $\text{Need}_i = \text{Need}_i - Request_i$
4. Run Safety Algorithm. Agar state **Safe** aati hai &rarr; Request grant karo! Agar **Unsafe** aati hai &rarr; Allocation rollback karo aur $P_i$ ko wait karao!

---

## 3. Comprehensive Solved AKTU Numerical Problem (Gateway Slide 240-250)

Consider 5 processes ($P_1, P_2, P_3, P_4, P_5$) and 3 resources ($A, B, C$ with total instances 10, 5, 7):

### 3.1 Initial State Matrix
| Process | Allocation (A B C) | Max (A B C) | Need = Max - Allocation (A B C) |
| :---: | :---: | :---: | :---: |
| **P1** | 0 1 0 | 7 5 3 | **7 4 3** |
| **P2** | 2 0 0 | 3 2 2 | **1 2 2** |
| **P3** | 3 0 2 | 9 0 2 | **6 0 0** |
| **P4** | 2 1 1 | 2 2 2 | **0 1 1** |
| **P5** | 0 0 2 | 4 3 3 | **4 3 1** |

- Total Allocated: $A = 7, B = 2, C = 5$.
- **`Available` = Total - Total Allocated = `[3, 3, 2]`**.

### 3.2 Step-by-Step Safety Algorithm Execution Trace
1. **Initial Work = `[3, 3, 2]`**
2. **Check P1:** Need `[7, 4, 3]` $\le$ `[3, 3, 2]`? **False** ($7 > 3$). Cannot satisfy.
3. **Check P2:** Need `[1, 2, 2]` $\le$ `[3, 3, 2]`? **True!**
   - $P_2$ finishes. Releases `[2, 0, 0]`.
   - New Work = `[3, 3, 2] + [2, 0, 0] = [5, 3, 2]`. Finish[P2] = True.
4. **Check P4:** Need `[0, 1, 1]` $\le$ `[5, 3, 2]`? **True!**
   - $P_4$ finishes. Releases `[2, 1, 1]`.
   - New Work = `[5, 3, 2] + [2, 1, 1] = [7, 4, 3]`. Finish[P4] = True.
5. **Check P5:** Need `[4, 3, 1]` $\le$ `[7, 4, 3]`? **True!**
   - $P_5$ finishes. Releases `[0, 0, 2]`.
   - New Work = `[7, 4, 3] + [0, 0, 2] = [7, 4, 5]`. Finish[P5] = True.
6. **Check P1:** Need `[7, 4, 3]` $\le$ `[7, 4, 5]`? **True!**
   - $P_1$ finishes. Releases `[0, 1, 0]`.
   - New Work = `[7, 4, 5] + [0, 1, 0] = [7, 5, 5]`. Finish[P1] = True.
7. **Check P3:** Need `[6, 0, 0]` $\le$ `[7, 5, 5]`? **True!**
   - $P_3$ finishes. Releases `[3, 0, 2]`.
   - New Work = `[7, 5, 5] + [3, 0, 2] = [10, 5, 7]`. Finish[P3] = True.

### 3.3 Conclusion:
System is in a **SAFE STATE** with Safe Sequence:
$$\langle P_2, P_4, P_5, P_1, P_3 \rangle$$

---

## 4. Architectural Diagram

<div class="diagram">
  <img src="diagrams/deadlock_avoidance_bankers.svg" alt="Deadlock Avoidance Banker's Diagram" style="max-width: 100%;">
</div>

---

## 5. AKTU Exam & Interview Highlights

> **AKTU PYQ (10 Marks):**
> *"State and explain Banker's algorithm for deadlock avoidance. Given Allocation, Max, and Available matrices, determine whether the system is in safe state or not."*
>
> **Top Tech Interview Insight:**
> *"What is the primary practical drawback of Banker's Algorithm in real-world operating systems?"*
> **Answer:** It requires processes to declare their **maximum resource requirement in advance** before execution, which is virtually impossible for modern dynamic applications (web browsers, databases).
